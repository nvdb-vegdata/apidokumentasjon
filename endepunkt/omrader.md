---
title: Områder
category: endepunkt
---

# Oppdatert API-dokumentasjon for versjon 3

Bruk heller dokumentasjon for versjon 3 av NVDB api https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

I NVDB er vegobjekter og vegnett stedfestet til flere typer områder, som kan brukes til å avgrense søk. For å gjøre det enklere å bygge opp dynamiske spørringer mot APIet, tilbys det her en tjeneste for å hente ut en liste over alle områder, for hver områdetype.

## Hent områder

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader
```

```json
[
    {
        "navn": "Regioner",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/regioner"
    },
    {
        "navn": "Fylker",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/fylker"
    },
    {
        "navn": "Vegavdelinger",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/vegavdelinger"
    },
    {
        "navn": "Kommuner",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/kommuner"
    },
    {
        "navn": "Riksvegruter",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/riksvegruter"
    },
    {
        "navn": "Kontraktsområder",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/omrader/kontraktsomrader"
    }
]
```

### Parametere

Alle endepunkt støtter følgende parametere.

| Navn | Verdi | Beskrivelse |
|:--------|:-------:|--------:|
inkluder | kartutsnitt, senterpunkt, vegobjekt, alle | En kommaseparert liste over informasjonselementer man vil hente ut for objektet. Det er ikke mulig å velge kartutsnitt eller senterpunkt for riksvegrute, kontraktsområde eller vegavdeling. |
srid | [srid](../verdi/geometri.md) | Angir hvilket geografisk referansesystem geometrien skal returneres i. **Default: 32633** |

## Hent regioner

Regioner er en områdetype som benyttes internt i Statens vegvesen, for å organisere vegavdelingene i større organistoriske enheter.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/regioner
```

```json
[
    {
        "navn": "Øst",
        "nummer": 1
    },
    {
        "navn": "Sør",
        "nummer": 2
    },
    {
        "navn": "Vest",
        "nummer": 3
    },
    {
        "navn": "Midt",
        "nummer": 4
    },
    {
        "navn": "Nord",
        "nummer": 5
    }
]
```

## Hent fylker

Fylkene tilsvarer Norges 19 fylker. Feltet `region` er lagt til for å gjøre koblingen mellom region og fylke enklere.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/fylker
```

```json
[
    {
        "navn": "Østfold",
        "nummer": 1,
        "region": 1
    },
    {
        "navn": "Akershus",
        "nummer": 2,
        "region": 1
    },
    {
        "navn": "Oslo",
        "nummer": 3,
        "region": 1
    },

    ...
]
```

### Eksempel: Hent flere informasjonselementer

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/fylker?inkluder=kartutsnitt,vegobjekt
```

```json
[
    {
        "navn": "Østfold",
        "nummer": 1,
        "region": 1,
        "kartutsnitt": {
            "wkt": "POLYGON ((245176.76 6521820.68, 245176.76 6632089.96, 328157.64 6632089.96, 328157.64 6521820.68, 245176.76 6521820.68))",
            "srid": 32633
        },
        "vegobjekt": {
            "id": 2,
            "type": 535,
            "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/535/2"
        }
    },
    {
        "navn": "Akershus",
        "nummer": 2,
        "region": 1,
        "kartutsnitt": {
            "wkt": "POLYGON ((238585.71 6600381.23, 238585.71 6725181.25, 327553.01 6725181.25, 327553.01 6600381.23, 238585.71 6600381.23))",
            "srid": 32633
        },
        "vegobjekt": {
            "id": 3,
            "type": 535,
            "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/535/3"
        }
    },
    {
        "navn": "Oslo",
        "nummer": 3,
        "region": 1,
        "kartutsnitt": {
            "wkt": "POLYGON ((248657.16 6637446.74, 248657.16 6674536.63, 273925.61 6674536.63, 273925.61 6637446.74, 248657.16 6637446.74))",
            "srid": 32633
        },
        "vegobjekt": {
            "id": 4,
            "type": 535,
            "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/535/4"
        }
    },
    ...
]
```

## Hent vegavdelinger

Vegavdelingene tilsvarer Norges fylker, bortsett fra ett unntak: Nordland og Troms er delt inn i treavdelinger, hvor den ene befinner seg både i Nordland fylke og Troms fylke.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/vegavdelinger
```

```json
[
    ...

    {
        "navn": "Nordland vegavdeling",
        "nummer": 18,
        "region": 5
    },
    {
        "navn": "Troms vegavdeling",
        "nummer": 19,
        "region": 5
    },
    {
        "navn": "Finnmark",
        "nummer": 20,
        "region": 5
    },
    {
        "navn": "Midtre Hålogaland vegavdeling",
        "nummer": 21,
        "region": 5
    }
]
```

## Hent kommuner

Kommunene tilsvarer Norges kommuner.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/kommuner
```

```
[
    {
        "navn": "Halden",
        "nummer": 101,
        "region": 1,
        "fylke": 1,
        "vegavdeling": 1
    },
    {
        "navn": "Moss",
        "nummer": 104,
        "region": 1,
        "fylke": 1,
        "vegavdeling": 1
    },
    {
        "navn": "Sarpsborg",
        "nummer": 105,
        "region": 1,
        "fylke": 1,
        "vegavdeling": 1
    },
    ...
]
```

## Hent kontraktsområder

Et kontraktsområde er en samling av veger hvor en gitt entreprenør har ansvar for drift/vedlikehold.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/kontraktsomrader
```

```json
[
    ...
    {
        "navn": "2042 Nordkyn 2015-2020",
        "nummer": 2042,
        "type": "Driftskontrakt"
    },
    {
        "navn": "5001 Helgeland 2014-2019",
        "nummer": 5001,
        "type": "Elektrokontrakt"
    },
    {
        "navn": "5002 Salten 2014-2019",
        "nummer": 5002,
        "type": "Elektrokontrakt"
    },
    ...
]
```

## Hent riksvegruter

En riksvegrute er en strekning som benyttes i forbindelse med Nasjonal Transportplan.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/omrader/riksvegruter
```

```json
[
    {
        "navn": "RUTE1",
        "nummer": "1",
        "beskrivelse": "E6 Riksgrensen/Svinesund - Oslo",
        "periode": "2014-2023"
    },
    {
        "navn": "RUTE10",
        "nummer": "10",
        "beskrivelse": "Ev39 Ålesund - Trondheim",
        "periode": "2006-2009"
    },
    {
        "navn": "RUTE11",
        "nummer": "11",
        "beskrivelse": "Ev134 Drammen - Haugesund",
        "periode": "2006-2009"
    },
    ...
]
```
