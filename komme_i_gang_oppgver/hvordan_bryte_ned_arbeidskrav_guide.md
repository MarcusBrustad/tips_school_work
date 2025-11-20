# Hvordan Bryte Ned Et Arbeidskrav: En Strukturert Tilnærming

**Mål:** Lær deg å SELV planlegge og strukturere et arbeidskrav  
**Fokus:** Metode og tankeprosess, ikke ferdig løsning

---

## 🧠 Grunnleggende Tankesett

> "Jeg leser ikke oppgaven for å finne løsningen. Jeg leser den for å forstå PROBLEMET."

### De tre spørsmålene:
1. **Hva skal jeg levere?** (output)
2. **Hva trenger jeg for å lage det?** (verktøy/kunnskap)
3. **I hvilken rekkefølge må ting gjøres?** (avhengigheter)

---

## 📖 FASE 1: Les og Forstå (IKKE kod enda!)

### Steg 1: Skann oppgaven raskt (2 min)
**Se etter:**
- [ ] Hvor mange oppgaver er det?
- [ ] Hva er vektingen? (hvor mye tid skal jeg bruke på hver?)
- [ ] Hva skal leveres inn? (filer, format)
- [ ] Er det noen tegninger/diagrammer/tabeller?

**Output:** En mental oversikt - "Dette er en 4-delt oppgave om databaser"

---

### Steg 2: Identifiser hva som skal leveres (5 min)
**Skriv ned:**
```
Fil 1: [navn] - [type] - [formål]
Fil 2: [navn] - [type] - [formål]
...
```

**Spørsmål til deg selv:**
- Hvilke filer avhenger av hverandre?
- Kan noen lages parallelt?
- Hvilke må lages først?

**Tips:** Tegn piler mellom filer som avhenger av hverandre!

---

### Steg 3: Les hver oppgave grundig (10 min)
**For hver oppgave, identifiser:**

#### Type oppgave:
- [ ] Opprettelse/Kreering (lage noe nytt)
- [ ] Forklaring/Dokumentasjon (skrive om noe)
- [ ] Datahåndtering (INSERT, UPDATE, DELETE)
- [ ] Spørring/Analyse (SELECT, JOIN, COUNT)
- [ ] Programmering (funksjoner, logikk)

#### Vanskelighetsgrad (etter DIN vurdering):
- 🟢 Lett - har gjort dette før
- 🟡 Middels - trenger å tenke, men vet hvordan
- 🔴 Vanskelig - må google/spørre/lære nytt

#### Estimert tid:
- "Dette tar meg ca X minutter"

---

## 🗺️ FASE 2: Lag En Plan

### Steg 4: Identifiser avhengigheter

**For database-oppgaver:**
```
Spørsmål å stille:
- Hvilke tabeller refererer til andre tabeller?
- Hva er primærnøkler?
- Hva er fremmednøkler?
- Hva må eksistere FØRST før jeg kan lage noe annet?
```

**Metode: Tegn et avhengighetsdiagram**
```
[Tabell A] ← [Tabell B] ← [Tabell C]
     ↑
[Tabell D]
```

**Regel:** Pilen peker fra "trenger" til "må eksistere først"

---

### Steg 5: Prioriter oppgavene

**Strategier:**

#### Strategi 1: "Bottom-up" (fundamentet først)
```
1. Lag grunnmuren (database, tabeller)
2. Fyll med data
3. Test at det fungerer
4. Bygg videre (queries, funksjoner)
```

#### Strategi 2: "Etter vanskelighet"
```
1. Start med det du kan (🟢)
2. Bygg selvtillit
3. Takle middels (🟡)
4. Ta de vanskelige til slutt (🔴)
```

#### Strategi 3: "Etter vekting"
```
1. Start med oppgaver som teller mest
2. Sikre at du får poeng selv om du ikke rekker alt
```

**Hvilken passer for DETTE arbeidskravet?**

---

### Steg 6: Lag en TODO-liste

**Format:**
```markdown
## Oppgave 1: [Navn] (XX%)
- [ ] Deloppgave A - [estimat: XX min] - [🟢/🟡/🔴]
- [ ] Deloppgave B - [estimat: XX min] - [🟢/🟡/🔴]

## Oppgave 2: [Navn] (XX%)
- [ ] ...

TOTALT ESTIMAT: X timer
```

**Tips:** Legg på 30% ekstra tid for debugging og testing!

---

## 🔍 FASE 3: Analyser Datastrukturer

### For Database-oppgaver:

#### Steg 7: Forstå relasjonene
**Tegn/skriv opp:**
```
Tabell: [navn]
├─ Kolonner: [liste]
├─ Primærnøkkel: [hvilken?]
├─ Fremmednøkler: [hvilke? peker hvor?]
└─ Spesielle krav: [auto-increment? constraints?]
```

**Gjør dette for ALLE tabeller først!**

#### Steg 8: Identifiser "tricky parts"
**Spørsmål:**
- Er det sammensatte nøkler? (flere kolonner som primærnøkkel)
- Er det flere fremmednøkler i samme tabell?
- Er det spesielle datatyper? (DATE, BOOLEAN, ENUM)
- Er det constraints jeg må huske? (NOT NULL, UNIQUE, CHECK)

**Marker disse med ⚠️ i planen din!**

---

## 🔨 FASE 4: Velg Verktøy og Metode

### Steg 9: Hva trenger jeg?

**For SQL:**
- [ ] Hvor skal jeg skrive SQL? (Workbench? VS Code? Terminal?)
- [ ] Hvor skal jeg teste? (samme sted?)
- [ ] Hvordan sjekker jeg at det fungerer?

**For Python:**
- [ ] Hvilke biblioteker trenger jeg? (`import ???`)
- [ ] Må jeg installere noe? (`pip install ???`)
- [ ] Hvordan tester jeg funksjoner?

**For dokumentasjon:**
- [ ] Markdown-editor med preview?
- [ ] Trenger jeg å lage diagrammer? (draw.io?)

---

### Steg 10: Test-strategi

**Tenk på:**
```
Hvordan vet jeg at Oppgave 1 fungerer?
→ [konkret test]

Hvordan vet jeg at Oppgave 2 fungerer?
→ [konkret test]

...
```

**Eksempel:**
- "Database fungerer → kan kjøre SELECT * på alle tabeller"
- "Query fungerer → får forventet antall rader tilbake"
- "Python-funksjon fungerer → printer riktig output"

---

## 📝 FASE 5: Dokumenter Planen (IKKE koden!)

### Steg 11: Lag en README for PLANLEGGING

**Template:**
```markdown
# Plan: Arbeidskrav [nummer]

## Oversikt
- Hva skal gjøres: [kort beskrivelse]
- Estimert tid: [X timer]
- Verktøy: [liste]

## Oppgavedeling
1. [Oppgave 1] - [XX%] - [estimat]
   - Hva skal gjøres: [beskrivelse]
   - Avhenger av: [liste eller "ingen"]
   - Vanskelighet: [🟢/🟡/🔴]
   - Ting å huske: [spesielle krav]

2. [Oppgave 2] - [XX%] - [estimat]
   ...

## Avhengighetsrekkefølge
```
[diagram eller liste]
```

## Usikre punkter / Må google
- [ ] [Ting jeg ikke kan enda]
- [ ] [Ting jeg må lære]

## Testing
- [ ] Test 1: [beskrivelse]
- [ ] Test 2: [beskrivelse]
```

---

## ⚡ FASE 6: Kjør Planen!

### Steg 12: Følg planen, men vær fleksibel

**Mens du koder:**
- ✅ Kryss av oppgaver underveis (motiverende!)
- 📝 Skriv ned problemer du møter
- ⏱️ Juster estimater hvis nødvendig
- 💡 Skriv ned ting du lærer

**Hvis du kjører fast:**
1. Gå tilbake til planen
2. Bryt oppgaven ned i MINDRE deler
3. Test hver liten del
4. Bygg oppover igjen

---

## 🎯 Oppsummering: Tankeprosessen

### Fra oppgave til plan:

```
1. LES → Forstå HVA som skal gjøres
         ↓
2. ANALYSER → Forstå AVHENGIGHETER
         ↓
3. PRIORITER → Bestem REKKEFØLGE
         ↓
4. SPESIFISER → Lag KONKRETE steg
         ↓
5. ESTIMER → Hvor lang TID?
         ↓
6. KJØR → Følg planen!
```

---

## 💡 Vanlige Tankefeil å Unngå

### ❌ "Jeg må bare starte å kode!"
**Hvorfor galt:** Uten plan koder du deg inn i hjørner
**Løsning:** Bruk 20-30 min på planlegging først

### ❌ "Jeg gjør alt i hodet"
**Hvorfor galt:** Du glemmer ting, mister oversikt
**Løsning:** Skriv planen ned, selv om den er kort

### ❌ "Jeg begynner med det vanskeligste"
**Hvorfor galt:** Demotiverende hvis du kjører fast tidlig
**Løsning:** Start med noe du KAN, bygg momentum

### ❌ "Jeg leser oppgaven én gang og kjører på"
**Hvorfor galt:** Misforstår krav, må gjøre om ting
**Løsning:** Les MINST to ganger, gjerne tre

### ❌ "Testing gjør jeg til slutt"
**Hvorfor galt:** Finner feil for sent, vanskelig å debugge
**Løsning:** Test hver del underveis

---

## 🔧 Praktisk Eksempel: "Hvordan ville JEG tenkt?"

### Gitt: En database-oppgave

**Min tankeprosess (høyt tenkt):**

```
1. "Okay, jeg skal lage en database. La meg se... 4 tabeller."

2. "Hvilke tabeller har fremmednøkler? 
   → Fremmednøkler betyr avhengigheter"

3. "Tabell X peker til Tabell Y, så Y må lages først"

4. "Jeg tegner dette opp:
   Y → X → Z
   og W (uavhengig)"

5. "Rekkefølge blir: Y, W (parallelt mulig), X, Z"

6. "Hva er tricky her? 
   → Sammensatt nøkkel i Tabell X
   → AUTO_INCREMENT må være riktig
   → Datoformat må være YYYY-MM-DD"

7. "Jeg lager en sjekkliste:
   [ ] Opprett Y
   [ ] Opprett W
   [ ] Test SELECT * på Y og W
   [ ] Opprett X (husk foreign key!)
   [ ] Test at foreign key fungerer
   [ ] Opprett Z
   [ ] Insert data (rekkefølge: Y, W, X, Z)
   [ ] Test at alt data er inn
   [ ] Kjør en enkel JOIN for å teste relasjoner"

8. "Jeg estimerer: ca 30 min hvis alt går smooth, 
   1 time hvis jeg møter problemer"

9. "GO!"
```

**Se forskjellen?**
- Ikke "Jeg lager Tabell 1" → klikker i gang
- Men "Jeg PLANLEGGER Tabell 1" → DERETTER koder

---

## 📋 Øvingsoppgave: Test Metoden

### Ta et tidligere arbeidskrav du har gjort

**Gjør dette:**
1. ✅ Gå gjennom Fase 1-5 UTEN å se på koden din
2. ✅ Lag en plan basert på metoden over
3. ✅ Sammenlign med hvordan du faktisk gjorde det
4. ✅ Hva ville vært annerledes med en plan?

**Spørsmål:**
- Hadde du spart tid med en plan?
- Hadde du unngått noen feil?
- Hva lærte du om din egen tankeprosess?

---

## 🎓 Spilleregler for God Planlegging

### Regel 1: "Planlegging er ikke bortkastet tid"
20 min planlegging kan spare deg for 2 timer debugging

### Regel 2: "Skriv det ned"
Det du ikke skriver ned, glemmer du

### Regel 3: "Avhengigheter kommer først"
Alltid start med det som ingenting avhenger av

### Regel 4: "Test tidlig og ofte"
Test hver byggeblokk før du bygger videre

### Regel 5: "Planen kan endres"
Men uten plan har du ingenting å endre

### Regel 6: "Spør før du kjører fast"
10 min hjelp > 2 timer googleing i feil retning

---

## 🚀 Neste Steg: Anvendelse

### For dette arbeidskravet:

**Din oppgave nå:**
1. Ta 30 minutter BARE på planlegging
2. Gå gjennom Fase 1-5 (ingen koding!)
3. Lag en konkret plan i Markdown
4. Del planen med en medstudent eller veileder
5. Få tilbakemelding: "Virker dette fornuftig?"
6. **DERETTER**: Start å kode

**Husk:**
> "En time planlegging kan spare deg for 10 timer frustrasjon"

---

## 💬 Refleksjonsspørsmål

Etter du er ferdig med arbeidskravet:

1. Fulgte jeg planen? Hvorfor/hvorfor ikke?
2. Var estimatene mine realistiske?
3. Hvilke problemer møtte jeg som jeg IKKE hadde planlagt for?
4. Hva ville jeg gjort annerledes neste gang?
5. Hva fungerte bra i planleggingen min?

**Skriv ned svarene!** Dette bygger din erfaring.

---

## 📚 Ressurser for Videre Læring

**Om planlegging:**
- "How to Solve It" av George Pólya (klassiker om problemløsning)
- "Atomic Habits" av James Clear (om små steg)

**Om programmering:**
- "Think Like a Programmer" av V. Anton Spraul
- "The Pragmatic Programmer" av Hunt & Thomas

**Om databaser:**
- "SQL Queries for Mere Mortals" av Hernandez & Viescas
- "Database Design for Mere Mortals" av Hernandez

---

**Lykke til! Du klarer dette! 🎯**

*Husk: Det handler ikke om å være perfekt. Det handler om å være STRUKTURERT.*
