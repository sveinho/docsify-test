# Introduksjon til systemarkitektur

<span class="badge spor-arkitekt">Arkitekt</span> <span class="badge spor-utvikler">Utvikler</span>

Dette dokumentet gir en overordnet teknisk oversikt over systemets oppbygning, kjernekomponenter og dataflyt. Det fungerer som utgangspunkt for videre dypdykk i sikkerhet og infrastruktur.

## Overordnet Systemskisse

Systemet er bygget etter en moderne, distribuert mikrotjeneste-arkitektur for å sikre høy tilgjengelighet og uavhengig skalering.

```text
[ Klient / Webapp ] ──( HTTPS )──> [ API Gateway ]
                                       │
            ┌──────────────────────────┼──────────────────────────┐
            ▼                          ▼                          ▼
   [ Autentisering ]            [ Ordretjeneste ]          [ Produkttjeneste ]
            │                          │                          │
            ▼                          ▼                          ▼
     ( PostgreSQL )               ( MongoDB )                ( Redis Cache )
```

---

## Integrasjonsmønster per læringsløp

Avhengig av hvilket spor du følger, vil ditt grensesnitt mot arkitekturen variere. Velg fanen under for å se hvordan din rolle samhandler med systemet:

<!-- tabs:start -->

#### **Introduksjon (Sluttbruker)**
Som generell bruker forholder du deg kun til **Klient/Webapp**-laget. 
* All trafikk rutes automatisk og kryptert via HTTPS.
* Du trenger ikke tenke på underliggende databaser eller mikrotjenester.

#### **Utvikler**
Som utvikler bygger og vedlikeholder du de enkelte **mikrotjenestene** (Ordre, Produkt, etc.).
* Du må forholde deg til API-kontrakter (OpenAPI/Swagger).
* Lokalt kjører du hele denne arkitekturen opp via Docker Compose for isolert testing.
* Kommunikasjon mellom tjenestene foregår asynkront via en meldingskø (RabbitMQ).

#### **Arkitekt**
Som arkitekt har du ansvaret for **API Gateway** og **Infrastrukturlaget**.
* Du må konfigurere rate-limiting og lastbalansering i gatewayen.
* Du har eierskap til datastatestrategien (f.eks. replikering av PostgreSQL og sharding av MongoDB).
* Du overvåker systemhelsen via distribuerte sporingsverktøy (OpenTelemetry).
<!-- tabs:end -->

---

## Tekniske Kjernekrav

Her er minstekravene som gjelder for alle komponenter i landskapet:

*   **Sikkerhet:** All kommunikasjon internt og eksternt skal skje over TLS 1.3.
*   **Identitet:** Tokens utstedes som JWT (JSON Web Tokens) signert med RS256.
*   **Oppetid:** Infrastrukturen skal designes for en tilgjengelighet på 99.9% (Multi-AZ).

---

## Neste skritt
Gå videre i sidebaren for å lese mer om:
1. [Kapittel 1: Systemlandskap](/spor-arkitekt/systemlandskap.md)
2. [Kapittel 2: Sikkerhet og GDPR](/spor-arkitekt/sikkerhet.md)

