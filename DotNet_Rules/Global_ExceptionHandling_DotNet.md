# Global Exception Handling in .NET 9 – Complete Guide  
*(without FluentValidation – plain C#)*

> A single copy-paste reference for building a clean, structured `GlobalExceptionHandler` in a controller-based .NET 9 API (works in .NET 8 as well).

---

## 1. Goals / Best-practice checklist

| Requirement                                           | Why                                  |
| ----------------------------------------------------- | ------------------------------------ |
| Always return **RFC 7807 Problem Details**            | Easy for JavaScript, BFF, Swagger    |
| Never leak stack-traces in production                 | Security                             |
| Log **once** with the same **correlation id**         | Fast troubleshooting                 |
| Distinguish **4xx** (client) vs **5xx** (server)      | Stop 3 AM pages for wrong passwords  |
| One **central place** – no `try/catch` in controllers | Less code, fewer bugs                |
| Support **async**                                     | Scale                                |
| **Unit-testable**                                     | Inject `ILogger`, `IHostEnvironment` |
| Work **without** FluentValidation                     | Zero extra deps                      |

---

## 2. Folder layout (suggestion)
```
src/
├── Domain/
│   └── Exceptions/
│       ├── BadRequestException.cs
│       ├── UnauthorizedException.cs
│       ├── ForbiddenException.cs
│       ├── NotFoundException.cs
│       ├── ConflictException.cs
│       ├── GoneException.cs
│       ├── UnprocessableEntityException.cs
│       ├── TooManyRequestsException.cs
│       ├── InternalServerException.cs
│       └── ValidationException.cs   ← plain C# version
├── Infrastructure/
│   └── Exceptions/
│       ├── GlobalExceptionHandler.cs
│       └── ProblemDetailsWithTrace.cs
├── Features/
│   └── Todo/
│       ├── TodoController.cs
│       └── ...
└── Program.cs
```


---

## 3. Domain exceptions (plain C#)

Create one file per class (StyleCop-friendly) or use the primary-constructor style – but keep **one type per file**.

```csharp
// BadRequestException.cs
namespace Domain.Exceptions;

public sealed class BadRequestException : Exception
{
    public BadRequestException(string message) : base(message) { }
}

// UnauthorizedException.cs
public sealed class UnauthorizedException : Exception
{
    public UnauthorizedException(string message = "Unauthorized") : base(message) { }
}

// ForbiddenException.cs
public sealed class ForbiddenException : Exception
{
    public ForbiddenException(string message = "Forbidden") : base(message) { }
}

// NotFoundException.cs
public sealed class NotFoundException : Exception
{
    public NotFoundException(string entity, object key)
        : base($"'{entity}' ({key}) was not found.") { }
}

// ConflictException.cs   (409)
public sealed class ConflictException : Exception
{
    public ConflictException(string message) : base(message) { }
}

// GoneException.cs   (410)
public sealed class GoneException : Exception
{
    public GoneException(string message) : base(message) { }
}

// UnprocessableEntityException.cs   (422)
public sealed class UnprocessableEntityException : Exception
{
    public UnprocessableEntityException(string message) : base(message) { }
}

// TooManyRequestsException.cs   (429)
public sealed class TooManyRequestsException : Exception
{
    public TimeSpan? RetryAfter { get; }
    public TooManyRequestsException(string message, TimeSpan? retryAfter = null)
        : base(message) => RetryAfter = retryAfter;
}

// InternalServerException.cs   (500)
public sealed class InternalServerException : Exception
{
    public InternalServerException(string message) : base(message) { }
    public InternalServerException(string message, Exception inner)
        : base(message, inner) { }
}
```

---

## 4. Validation without FluentValidation

**Tiny error DTO:**

```csharp
// ValidationError.cs
namespace Domain.Exceptions;

public readonly record struct ValidationError(string PropertyName, string ErrorMessage);
```

**The exception:**

```csharp
// ValidationException.cs
namespace Domain.Exceptions;

public sealed class ValidationException : Exception
{
    public Dictionary<string, string[]> Errors { get; }

    // A) list of single errors
    public ValidationException(IEnumerable<ValidationError> errors)
        : base("One or more validation errors occurred.")
    {
        Errors = errors
            .GroupBy(e => e.PropertyName, e => e.ErrorMessage)
            .ToDictionary(g => g.Key, g => g.ToArray());
    }

    // B) already-built dictionary
    public ValidationException(Dictionary<string, string[]> errors)
        : base("One or more validation errors occurred.") => Errors = errors;
}
```

---

## 5. Infrastructure helpers

```csharp
// ProblemDetailsWithTrace.cs
using Microsoft.AspNetCore.Mvc;

namespace Infrastructure.Exceptions;

public sealed class ProblemDetailsWithTrace : ProblemDetails
{
    public string? TraceId { get; init; }
    public Dictionary<string, string[]>? Errors { get; init; }
}
```

---

## 6. GlobalExceptionHandler (IExceptionHandler) example

```csharp
// GlobalExceptionHandler.cs
using System.Diagnostics;
using System.Net;
using System.Net.Mime;
using System.Text.Json;
using Domain.Exceptions;
using Microsoft.AspNetCore.Diagnostics;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Options;

namespace Infrastructure.Exceptions;

public sealed class GlobalExceptionHandler : IExceptionHandler
{
    private readonly ILogger<GlobalExceptionHandler> _logger;
    private readonly IHostEnvironment _env;
    private readonly ProblemDetailsFactory _factory;

    public GlobalExceptionHandler(
        ILogger<GlobalExceptionHandler> logger,
        IHostEnvironment env,
        ProblemDetailsFactory factory)
    {
        _logger = logger;
        _env = env;
        _factory = factory;
    }

    public async ValueTask<bool> TryHandleAsync(
        HttpContext httpContext,
        Exception exception,
        CancellationToken cancellationToken)
    {
        var traceId = Activity.Current?.Id ?? httpContext.TraceIdentifier;

        _logger.LogError(exception,
            "Unhandled exception. TraceId={TraceId}", traceId);

        var (statusCode, title) = MapException(exception);

        // Optional: 429 Retry-After header
        if (exception is TooManyRequestsException tooMany && tooMany.RetryAfter is { } ra)
            httpContext.Response.Headers.RetryAfter = ra.TotalSeconds.ToString("0");

        var problem = new ProblemDetailsWithTrace
        {
            Title = title,
            Status = (int)statusCode,
            Detail = _env.IsDevelopment() ? exception.ToString() : null,
            Instance = httpContext.Request.Path,
            TraceId = traceId,
            Errors = exception is ValidationException ve ? ve.Errors : null
        };

        httpContext.Response.StatusCode = (int)statusCode;
        httpContext.Response.ContentType = MediaTypeNames.Application.Json;

        await httpContext.Response.WriteAsync(
            JsonSerializer.Serialize(problem), cancellationToken);

        return true; // handled
    }

    private static (HttpStatusCode code, string title) MapException(Exception ex) =>
        ex switch
        {
            BadRequestException => (HttpStatusCode.BadRequest, "Bad request"),
            UnauthorizedException => (HttpStatusCode.Unauthorized, "Unauthorized"),
            ForbiddenException => (HttpStatusCode.Forbidden, "Forbidden"),
            NotFoundException => (HttpStatusCode.NotFound, "Resource not found"),
            ConflictException => (HttpStatusCode.Conflict, "Conflict"),
            GoneException => (HttpStatusCode.Gone, "Resource gone"),
            UnprocessableEntityException => (HttpStatusCode.UnprocessableEntity, "Validation error"),
            TooManyRequestsException => (HttpStatusCode.TooManyRequests, "Too many requests"),
            ValidationException => (HttpStatusCode.BadRequest, "Validation error"),
            InternalServerException => (HttpStatusCode.InternalServerError, "Server error"),
            _ => (HttpStatusCode.InternalServerError, "An error occurred")
        };
}
```

---

## 7. Bootstrap in Program.cs

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// 1. Register our handler
builder.Services.AddExceptionHandler<GlobalExceptionHandler>();

// 2. Enable ProblemDetails as default
builder.Services.AddProblemDetails(opts =>
{
    opts.CustomizeProblemDetails = ctx =>
        ctx.ProblemDetails.Extensions["traceId"] =
            ctx.HttpContext.TraceIdentifier;
});

var app = builder.Build();

// 3. Pipeline order matters
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
app.UseHttpsRedirection();
app.UseAuthorization();

app.UseExceptionHandler(); // ← global handler
app.MapControllers();

app.Run();
```

## 8. Controller example – zero try/catch

```csharp
[ApiController]
[Route("api/[controller]")]
public class TodoController : ControllerBase
{
    private readonly ITodoService _service;
    public TodoController(ITodoService service) => _service = service;

    [HttpGet("{id:int}")]
    public async Task<ActionResult<TodoDto>> Get(int id, CancellationToken ct)
    {
        var todo = await _service.GetAsync(id, ct)
            ?? throw new NotFoundException(nameof(Todo), id);
        return todo;
    }

    [HttpPost]
    public async Task<ActionResult<TodoDto>> Create(CreateTodoRequest dto,
                                                    CancellationToken ct)
    {
        // Manual validation (no FluentValidation)
        var failures = new List<ValidationError>();

        if (string.IsNullOrWhiteSpace(dto.Title))
            failures.Add(new(nameof(dto.Title), "Title is required."));

        if (dto.DueDate < DateOnly.FromDateTime(DateTime.UtcNow))
            failures.Add(new(nameof(dto.DueDate), "DueDate cannot be in the past."));

        if (failures.Count > 0)
            throw new ValidationException(failures);

        var created = await _service.CreateAsync(dto, ct);
        return CreatedAtAction(nameof(Get), new { id = created.Id }, created);
    }
}
```

## 9. Testing the handler (unit-test sample)

```csharp 
[Fact]
public async Task Returns_404_ProblemDetails_when_NotFoundException()
{
    // Arrange
    var ctx = new DefaultHttpContext();
    ctx.Request.Path = "/api/todo/99";
    var ex = new NotFoundException("Todo", 99);
    var handler = new GlobalExceptionHandler(
        NullLogger<GlobalExceptionHandler>.Instance,
        new HostingEnvironment { EnvironmentName = Environments.Development },
        new ProblemDetailsFactory());

    // Act
    var handled = await handler.TryHandleAsync(ctx, ex, default);

    // Assert
    handled.Should().BeTrue();
    ctx.Response.StatusCode.Should().Be(404);
    ctx.Response.Body.Position = 0;
    var json = await new StreamReader(ctx.Response.Body).ReadToEndAsync();
    json.Should().Contain("Resource not found");
}
```

---

## 10. Quick cheat-sheet – what to throw

| HTTP  | Throw                                          |
| :---: | :--------------------------------------------- |
|  400  | `BadRequestException` or `ValidationException` |
|  401  | `UnauthorizedException`                        |
|  403  | `ForbiddenException`                           |
|  404  | `NotFoundException`                            |
|  409  | `ConflictException`                            |
|  410  | `GoneException`                                |
|  422  | `UnprocessableEntityException`                 |
|  429  | `TooManyRequestsException`                     |
|  500  | `InternalServerException` (or `unhandled`)     |

 

