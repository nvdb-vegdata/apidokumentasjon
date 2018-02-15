---
title: Retningslinjer
order: 3
---

Retningslinjer for bruk av APIet.

## Bruk av data

Informasjon fra Nasjonal vegdatabank tilgjengeliggjøres under [Norsk lisens for offentlige data](http://data.norge.no/nlod/no/1.0).

Informasjonen kan, med de begrensningene som følger av lisensen, brukes til ethvert formål og i en enhver sammenheng. Informasjonen kan inneholde feil og utelatelser, og Statens vegvesen gir ingen garantier for informasjonens innhold eller aktualitet.

Ved bruk av informasjon fra Nasjonal vegdatabank, skal det refereres til Statens vegvesen. Følgende tekst kan for eksempel benyttes:

«Inneholder data under norsk lisens for offentlige data (NLOD) tilgjengeliggjort av Statens vegvesen.»

## Autentisering

Det er ikke nødvendig å registrere en bruker for å bruke APIet til å lese data fra NVDB. Det anbefales imidlertidig at kontaktperson og applikasjonsnavn angis gjennom HTTP-headere.


```
	"X-Client": "NVDB Rapporter"
  "X-Kontaktperson": "ola@nordmann.no"
```

## Responsformater

Valg av respons angis ved hjelp av HTTP-headeren `Accept`. På alle endepunkt er `JSON` og `XML` tilgjengelige formater. `JSON` benyttes som standard.

Standardmediatypene `application/json` og `application/xml` vil til enhver tid være <emph>alias</emph> for nyeste responsrevisjon. **For å unngå at klienter brekker er det anbefalt å bruke Accept-headeren, og angi responsrevisjon eksplisitt.**

```
Accept: application/vnd.vegvesen.nvdb-v2+json
Accept: application/vnd.vegvesen.nvdb-v2+xml
```

For å gjøre det lettere å bla gjennom APIet ved hjelp av en nettleser, er det mulig å angi format direkte som en del av URI. Eksempel:

```
GET /vegobjekttyper.json
GET /vegobjekttyper.xml
```

## Hent oppdaterte data

Vi oppfordrer våre brukere til å hente data i sanntid, fremfor å laste ned store datasett i bulk, med jevne mellomrom.

For dette tilbys endepunktet [/vegobjekter/{id}/endringer](endepunkt/vegobjekter#hent-endringer)

## Cross Origin Resource Sharing

The API supports Cross Origin Resource Sharing (CORS) for AJAX requests from any origin.

## Pretty print

Dersom brukeren av ønsker formatterte svar fra APIet kan parameteren `pretty=true` brukes. Dette påvirker både XML- og JSON-formatene.

## Feilsituasjoner

APIet har som mål å feile så raskt som mulig for å assistere brukeren. I den grad det er mulig vil alle kall til endepunkter returnere en liste med beskrivende feilobjekter. Dette vil supplere HTTP-statuskoden.

### JSON-eksempel

```json
[
    {
        "code": 4013,
        "message": "Ukjent parameter: vegvdeling",
        "help_url": "https://www.vegvesen.no/nvdb/api/dokumentasjon/api/page/3"
    }
]
```
### Feilkoder

<table>
    <thead>
    <tr>
        <th>HTTP Status</th>
        <th>Feilkode</th>
        <th>Beskrivelse</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>404</td>
        <td>4012</td>
        <td>Objekt ble ikke funnet.</td>
    </tr>
    <tr>
        <td>415</td>
        <td>4001</td>
        <td>Denne mediatypen er ikke støttet.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4000</td>
        <td>Noe er galt med brukerens input.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4002</td>
        <td>Feil i spesifisering av heltallsverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4003</td>
        <td>Feil i spesifisering av heltallslisteverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4004</td>
        <td>Manglende obligatorisk felt.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4005</td>
        <td>Feil i spesifisering av tekstverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4006</td>
        <td>Feil i spesifisering av tekstlisteverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4007</td>
        <td>Feil i spesifisering av datoverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4008</td>
        <td>Feil i spesifisering av boolsk verdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4009</td>
        <td>Konflikterende feltverdier spesifisert.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4010</td>
        <td>Feil i spesifisering av flyttallsverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4011</td>
        <td>Feil i spesifisering av flyttallistesverdi.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4013</td>
        <td>Ukjent felt spesifisert.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>4014</td>
        <td>Dette feltet kan kun forekomme én gang.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>5000</td>
        <td>Uventet feil har oppstått.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>5001</td>
        <td>Feil med kommunikasjon med databaser.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>5002</td>
        <td>Typeregisteret mangler.</td>
    </tr>
    </tbody>
</table>

I tillegg vil feilresponser ha header `X-REQUEST-ID` som du kan bruke om du kontakter oss om feilen, slik at det er lettere å hjelpe deg.

## Evolusjonsstrategi

Kort fortalt vil det fungere på følgende måte:

*   API-versjon berører utformingen av endepunktene og formatet på forespørslene.
*   Responsrevisjon berører da formatet på responsen man får. Så lenge en API-versjon lever støttes alle responsrevisjoner forbundet med denne.

Det er viktig å forstå forskjellen på **brekkende** og **ikke-brekkende** endringer for å forholde seg til hvordan NVDB-APIet endrer seg.

### Brekkende endringer

En brekkende endring vil være et endepunkt som forsvinner eller en parameter som forsvinner eller får ny betydning. Dermed tvinges brukeren til å endre sin klient.

### Ikke-brekkende endringer

Hvis en API-versjon får et nytt endepunkt eller en ny parameter anses dette som en utvidelse. I dette tilfeller tvinges ingen klienter til å endre seg.

### Responsrevisjon

I tillegg til API-versjon er responsene versjonert. I mellom disse revisjonene kan brekkende endringer forekomme. Alle forespørsler til APIet bør indikere korrekt **responsrevisjon**.

### Endringer i datakatalogen

NVDB API forholder seg til den oppdaterte Datakatalogen til enhver tid. Dersom et datafelt blir endret, f.eks. fra heltall til flyttall, vil samtlige responsrevisjoner endre seg.
