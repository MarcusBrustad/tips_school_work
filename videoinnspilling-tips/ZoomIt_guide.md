## 🔍 ZoomIt for highlighting

ZoomIt er et kraftig verktøy fra Microsoft for å zoome inn og markere deler av skjermen under presentasjoner og opptak.

### Installasjon
Last ned ZoomIt fra [Microsoft Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/zoomit)

- Last ned `ZoomIt.zip`
- Pakk ut filen til en mappe (f.eks. `C:\Tools\ZoomIt\`)
- Kjør `ZoomIt.exe` (ingen installasjon nødvendig)
- Ved første oppstart: Kryss av for "Run ZoomIt when Windows starts" hvis du vil ha den tilgjengelig alltid

### Tre hovedmoduser

#### 1. Zoom-modus (`Ctrl + 1`)
- **Aktivere zoom:** Trykk `Ctrl + 1`
- **Zoome inn/ut:** Hold museknappen inne og beveg musen opp/ned, eller bruk scrollhjulet
- **Flytte zoomområdet:** Beveg musen
- **Avslutt:** Trykk `Esc` eller høyreklikk

#### 2. Draw-modus (Tegne/markere) (`Ctrl + 2`)
**Aktivere:** Trykk `Ctrl + 2`

**Tegneverktøy:**
- **Frihåndstegning:** Venstreklikk og dra
- **Rett linje:** Hold `Shift` mens du drar
- **Pil:** Hold `Ctrl` mens du drar (lager pil som peker mot sluttpunktet)
- **Rektangel:** Hold `Ctrl + Shift` mens du dra (tegner rektangel/firkant)
- **Ellipse/Sirkel:** Hold `Tab` mens du drar
- **Understrek:** Trykk `u` for å aktivere, deretter dra musen (lager en pil som understreker)

**Farger og viskelær:**
- **Bytt farge:** Høyreklikk (veksler mellom fargene du har definert)
- **Gul farge:** Trykk `y` (yellow)
- **Oransje farge:** Trykk `o` (orange)
- **Rød farge:** Trykk `r` (red)
- **Grønn farge:** Trykk `g` (green)
- **Blå farge:** Trykk `b` (blue)
- **Rosa farge:** Trykk `p` (pink)
- **Viskelær:** Trykk `e` (eraser), deretter klikk og dra over det du vil fjerne
- **Slett alt:** Trykk `Esc` eller trykk `Ctrl + Z` for undo

**Tekstverktøy:**
- **Skriv tekst:** Trykk `t`, deretter skriv teksten din
- **Skriv tekst (hvit bakgrunn):** Trykk `Shift + t` for tekst med hvit boks rundt

**Zoom mens du tegner:**
- Trykk `Ctrl + 1` for å zoome inn mens du er i draw-modus
- Trykk `Esc` eller høyreklikk for å gå tilbake til draw-modus

**Avslutt draw-modus:** Trykk `Esc`

#### 3. Break Timer (`Ctrl + 3`)
- En pauseskjerm med nedtelling
- Nyttig for å ta pauser, men mindre relevant for opptak av arbeidskrav

### Tilpasse innstillinger

Høyreklikk på ZoomIt-ikonet i systemstatusfeltet (system tray) og velg "Options":

**Zoom-fanen:**
- Endre hurtigtast for zoom (standard: `Ctrl + 1`)
- Juster zoom-faktor
- Aktiver/deaktiver animasjon

**Draw-fanen:**
- Endre hurtigtast for draw-modus (standard: `Ctrl + 2`)
- Velg standard pennfarge
- Juster penntykkelse (width)
- Legg til flere farger i rotasjonen

**Type-fanen:**
- Innstillinger for tekstverktøyet
- Endre font og størrelse

### Praktisk arbeidsflyt under opptak

1. **Start OBS-opptak**
2. **Når du skal forklare noe detaljert:**
   - Trykk `Ctrl + 2` for draw-modus
   - Bruk pil (`Ctrl + dra`) for å peke på viktige deler
   - Bruk rektangel (`Ctrl + Shift + dra`) for å ramme inn kodeblokker
   - Bruk understrek (`u` + dra) for å understreke viktige linjer
3. **Trykk `Esc` for å fortsette som normalt**
4. **Ved behov for zoom:**
   - Trykk `Ctrl + 1` og zoom inn på detaljer
   - Trykk `Esc` for å gå tilbake

### Tips for effektiv bruk

- **Øv før opptak:** Bli kjent med hurtigtastene først
- **Bruk konsekvent farge:** Velg én eller to farger og hold deg til dem
- **Ikke overdriv:** For mange markeringer kan bli distraherende
- **Fjern markeringer:** Trykk `Esc` etter hvert punkt for en ryddig presentasjon
- **Kombiner med zoom:** Zoom inn først, deretter marker detaljer

### Vanlige problemer

**ZoomIt reagerer ikke:**
- Sjekk at programmet kjører (se i systemstatusfeltet)
- Restart ZoomIt
- Sjekk at hurtigtastene ikke er i konflikt med andre programmer

**Tegningen er usynlig:**
- Bytt farge med høyreklikk
- Sjekk penntykkelse i innstillinger
- Noen farger kan være vanskelige å se mot visse bakgrunner

**Zoom er for sensitiv:**
- Juster zoom-faktor i innstillinger
- Bruk scrollhjul i stedet for musebevegelse for mer presis kontroll