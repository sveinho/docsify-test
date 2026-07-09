# Miljø og lokalt oppsett

<span class="badge spor-utvikler">Utvikler</span> <span class="badge spor-arkitekt">Arkitekt</span>

Velkommen til utviklerløpet! Denne modulen tar deg gjennom stegene som kreves for å hente ned kildekoden, sette opp utviklingsmiljøet lokalt på din maskin, og kjøre din første mikrotjeneste.

---

## 🛠️ Forhåndskrav

Før du starter, må du sørge for at du har følgende verktøy installert på maskinen din:

*   **Git** (v2.30 eller nyere)
*   **Docker Desktop** (med Docker Compose inkludert)
*   **Node.js** (v18.x LTS eller nyere)
*   **VS Code** (anbefalt redigeringsverktøy)

---

## 🚀 Kom i gang (Steg-for-steg)

Følg disse tre enkle stegene for å kjøre opp prosjektet lokalt:

### Steg 1: Klon arkivet
Åpne terminalen din og kjør følgende kommando for å laste ned kodebasen:
```bash
git clone https://github.com
cd kjerne-api
```

### Steg 2: Konfigurer miljøvariabler
Kopier eksempelfilen for miljøvariabler for å opprette din lokale konfigurasjon:
```bash
cp .env.example .env
```

### Steg 3: Start infrastrukturen med Docker
Vi bruker Docker for å kjøre opp databasene og meldingskøene lokalt. Start disse i bakgrunnen:
```bash
docker-compose up -d
```

---

## 🖥️ Utviklingsmodus vs. Produksjon

Avhengig av hva du skal gjøre med koden, er det viktig å forstå forskjellen på hvordan miljøet kjører. Velg fanen som passer for din nåværende oppgave:

<!-- tabs:start -->

#### **Lokal utvikling**
Når du skriver kode, kjører du tjenestene direkte i terminalen med automatisk omstart (hot-reload):
```bash
npm run dev
```
*   **API-en kjører på:** `http://localhost:3000`
*   **Database-port:** `5432` (PostgreSQL)

#### **Lokal Docker-test**
Hvis du vil teste systemet nøyaktig slik det vil kjøre i testmiljøet (QA), kan du bygge og kjøre alle mikrotjenestene i Docker-containere:
```bash
docker-compose -f docker-compose.prod.yml up --build
```

#### **Arkitektur / CI-CD**
Når koden skyves til GitHub, trigges en automatisk pipeline i GitHub Actions. 
*   Pipelinen kjører lintere, sikkerhetsskanninger (Snyk) og enhetstester.
*   *For arkitekter:* Se detaljer om utrullingsarkitekturen i [Introduksjon til arkitekturen](/spor-arkitekt/arkitektur.md).
<!-- tabs:end -->

---

## 🔍 Verifisering av oppsettet

For å bekrefte at alt kjører som det skal, kan du åpne nettleseren din og navigere til helsesjekk-endepunktet:
👉 `http://localhost:3000/health`

Du skal få tilbake følgende JSON-respons:
```json
{
  "status": "UP",
  "database": "connected",
  "version": "1.0.0"
}
```

---

## Neste skritt
Nå som miljøet ditt er oppe og kjører, kan du gå videre til neste modul i sidebaren:
👉 [Kapittel 1: Skrive kode](/spor-utvikler/skrive-kode.md)

