# Nasjonal vegdatabank API

Statens vegvesen tilbyr et REST-basert API som kan benyttes for å få tilgang til informasjonen som befinner seg i Nasjonal vegdatabank (NVDB).

## Tips for å komme raskt igang

1.  Besøk [Vegkart](https://www.vegvesen.no/vegkart/vegkart) for å få innblikk i hvilke data som er tilgjengelig.
2.  Les [Om Nasjonal vegdatabank](om_nvdb) for å bli kjent med NVDBs datastruktur.
3.  Utforsk endepunktene i APIet gjennom nettleseren, og bli motivert til å fortsette.
4.  Les [Bruk av NVDB API](retningslinjer) for å lære hvordan APIet er ment å brukes.
5.  Om du skriver i Java, kan du bruke bruke [NVDB API Client](https://github.com/nvdb-vegdata/nvdb-api-client) som er skrevet som åpen kildekode.

## NVDB API versjon 2

**Versjon 2** er gjeldende versjon av NVDB API, og er dokumentert på dette nettstedet.

NVDB API v2 er tilgjengelig på følgende adresse:

>    [https://www.vegvesen.no/nvdb/api/v2](https://www.vegvesen.no/nvdb/api/v2)


Denne API dokumentasjonen inneholder oversikt over:

- [Endepunkt](endepunkt)
- [Parametre](parameter)
- [Verdier](verdi)


## NVDB API versjon 1

**Versjon 1** er forrige versjon av APIet. Versjonen er fortsatt tilgjengelig, men vil på sikt utfases.

Det legges ikke til ny funksjonalitet i versjon 1 av APIet, og brukere oppfordres til å gå over til versjon 2 så snart som mulig.

NVDB API v1 er tilgjengelig på følgende adresse:

>    [https://www.vegvesen.no/nvdb/api](https://www.vegvesen.no/nvdb/api)


*   [Dokumentasjon for NVDB API v1](/nvdb/apidokumentasjon/v1)


## Endringslogg

### 2016-06-24

Versjon 2 av NVDB API lanseres. Dette er det viktigste endringene sammenlignet med versjon 1:

*   Endepunktet **/sok** fjernes, og erstattes av **/vegobjekter**.
*   **/vegobjekter** har fått støtte for område- og egenskapsfilter som tidligere var tilgjengelig for **/sok**.
*   Område- og egenskapsfilter er nå tilgjengelige som query-parametere, i stedet for at det angis _et_ sammensatt json-objekt som inneholder alle søkekriterier.
*   **/datakatalog** erstattes av **/vegobjekttyper**.
*   **/vegreferanse** erstattes av **/posisjon** og **/veg**.
*   Endepunktet **/endringer** fjernes, og endringer gjøres tilgjengelig som en undertjeneste til hver vegobjekttype.
*   Det tilbys bedre muligheter for paginering, så en stor respons kan hentes ved å gjennomføre flere spørringer mot APIet.
*   **/vegobjekter** har støtte for segmentering.
*   Responsen for **/vegobjekter** kan leveres ut i form av vegsegmenter, der stedfesting, geometri og vegreferanse er koblet sammen.
*   **/vegnett** leverer veglenker som også inneholder informasjon om vegreferanse.
*   For **/vegobjekter** finnes det et helt nytt overlappfilter, som kan brukes til å søke frem vegobjekter som befinner seg på samme sted på vegnettet som andre angitte vegobjekttyper.
