# Guide: Videoinnspilling av arbeidskrav

En praktisk guide for å spille inn, redigere og levere videobaserte arbeidskrav.

## 📋 Før du starter: Planlegging

**Lag en plan før du begynner å filme!**

- Skriv ned hovedpunktene du skal dekke
- Lag en enkel disposisjon eller manus
- Del innholdet opp i logiske deler (f.eks. introduksjon, hoveddeler, konklusjon)
- Tenk gjennom hva du skal demonstrere og i hvilken rekkefølge

**Tips:** Det er mye lettere å filme flere kortere klipp og redigere dem sammen, enn å filme alt i én sitting!

### Fordeler med å filme i deler:
- Mindre stress – du kan ta pauser
- Enklere å rette opp feil uten å måtte starte helt på nytt
- Bedre kvalitet – du er mer fokusert i kortere økter
- Fleksibilitet – du kan omorganisere rekkefølgen i redigeringen

## 🎥 Innspilling med OBS Studio

### Installasjon
Last ned OBS Studio fra [obsproject.com](https://obsproject.com/)

### Grunnleggende oppsett

1. **Opprett en Scene**
   - Åpne OBS Studio
   - Klikk på `+` under "Scenes" for å lage en ny scene
   - Gi den et beskrivende navn (f.eks. "Desktop Capture")

2. **Legg til Desktop Capture**
   - Klikk på `+` under "Sources"
   - Velg "Display Capture" (for hele skjermen) eller "Window Capture" (for ett vindu)
   - Navngi kilden og klikk OK
   - Velg hvilken skjerm/vindu du vil filme

3. **Legg til mikrofon**
   - Sjekk at mikrofonen din er valgt under "Settings" → "Audio"
   - Du ser lydnivået nederst i OBS-vinduet

4. **Videoinnstillinger**
   - Gå til "Settings" → "Video"
   - Anbefalt oppløsning: 1920x1080 (Full HD)
   - FPS: 30 (mer enn nok for arbeidskrav)

5. **Opptak-innstillinger**
   - Gå til "Settings" → "Output"
   - Recording Format: `mp4` (universelt og enkelt å dele)
   - Encoder: Bruk standard (ofte `x264`)

### Starte og stoppe opptak

- **Start opptak:** Klikk "Start Recording" eller trykk på hurtigtasten (standard: `Ctrl+Shift+F11`)
- **Stopp opptak:** Klikk "Stop Recording" eller samme hurtigtast
- **Finn opptakene:** Gå til "Settings" → "Output" → "Recording Path" for å se hvor filene lagres

## 🔍 ZoomIt for highlighting

ZoomIt er et nyttig verktøy for å zoome inn og markere deler av skjermen mens du filmer.

### Installasjon
Last ned ZoomIt fra [Microsoft Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/zoomit)

### Bruk
- **Zoom inn:** Trykk `Ctrl + 1` (hold inne og scroll for å justere zoom-nivå)
- **Tegne/markere:** Trykk `Ctrl + 2` (venstreklikk for å tegne, høyreklikk for å endre farge)
- **Avslutt:** Trykk `Esc` for å gå tilbake til normal visning

**Tips:** Bruk ZoomIt når du skal forklare kode eller spesifikke detaljer på skjermen!

## ✂️ Redigering med Shotcut

### Installasjon
Last ned Shotcut fra [shotcut.org](https://shotcut.org/)

### Grunnleggende redigering

1. **Import videoklipp**
   - Åpne Shotcut
   - Dra og slipp videofilene dine inn i "Playlist"-panelet

2. **Legg klipp på tidslinjen**
   - Dra klippene fra Playlist ned til tidslinjen nederst
   - Legg dem i ønsket rekkefølge

3. **Kutt og trim**
   - Klikk på et klipp i tidslinjen
   - Bruk `S` for å kutte/splitte klippet ved avspillerens posisjon
   - Høyreklikk og velg "Remove" for å fjerne unødvendige deler

4. **Overganger (valgfritt)**
   - Gå til "Filters" → "Video" → "Fade In Video" / "Fade Out Video"
   - Eller dra klipp litt over hverandre for automatisk overgang

5. **Eksporter ferdig video**
   - Klikk på "Export" øverst
   - Velg "YouTube" eller "H.264 High Profile" for god kvalitet
   - Klikk "Export File" og velg hvor du vil lagre

### Nyttige hurtigtaster i Shotcut
- `Space` – Play/Pause
- `S` – Split (kutt klipp)
- `I` – Set start point
- `O` – Set end point
- `Ctrl + Z` – Undo

## 🎬 Alternative redigeringsverktøy

- **DaVinci Resolve** (gratis, kraftig, men mer avansert)
- **OpenShot** (enklere enn Shotcut)
- **Kdenlive** (Linux-vennlig alternativ)

## ✅ Sjekkliste før innlevering

- [ ] Har du dekket alle kravene i oppgaven?
- [ ] Er lyden god nok? (test med hodetelefoner)
- [ ] Er skjermen leselig? (ikke for liten tekst)
- [ ] Er videoen eksportert i riktig format? (vanligvis MP4)
- [ ] Har du testet avspilling av den endelige videoen?
- [ ] Er filstørrelsen innenfor eventuelle begrensninger?

## 💡 Gode tips

1. **Test utstyret først** – gjør et kort testopptak før du starter for alvor
2. **Fjern distraksjoner** – lukk unødvendige programmer og varsler
3. **Snakk tydelig** – husk at mikrofonen kan være mindre følsom enn du tror
4. **Ta pauser** – spesielt hvis du filmer i flere deler
5. **Ha vann tilgjengelig** – stemmen blir fort tørr når man snakker mye
6. **Øv på vanskelige deler** – øvelseskjør før du starter opptaket
7. **Hold det enkelt** – ikke bruk for avanserte effekter med mindre det er nødvendig

## 🆘 Vanlige problemer

**Ingen lyd i opptaket:**
- Sjekk at riktig mikrofon er valgt i OBS under Settings → Audio

**Lav kvalitet/stor filstørrelse:**
- Juster bitrate under Settings → Output i OBS

**Hakkete opptak:**
- Lukk andre programmer som bruker mye ressurser
- Reduser oppløsning fra 1080p til 720p

**Kan ikke eksportere fra Shotcut:**
- Sjekk at du har nok diskplass
- Prøv et enklere eksportformat (f.eks. "YouTube")

---

**Lykke til med innspillingen! 🎥**
