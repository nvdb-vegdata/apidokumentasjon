---
title: Veg
category: endepunkt
---

# Oppdatert API-dokumentasjon for versjon 3

Bruk heller dokumentasjon for versjon 3 av NVDB api https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

Denne tjenesten kan brukes til å gjøre et oppslag på veglenkeposisjon eller vegreferanse, og få returnert det tilhørende punktet på vegnettet med både koordinat, vegreferanse og veglenkeposisjon.

## Finn punkt på vegnettet

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/veg
```


### Parametere

| Navn | Verdi | Beskrivelse |
|:--------|:-------:|--------:|
vegreferanse | [vegreferanse](../verdi/vegreferanse.md) | Angir vegreferanse som punkt på vegnettet. |
veglenke | [veglenke](../verdi/veglenke.md) | Angir veglenke som punkt på vegnettet. |
srid |  [srid](../verdi/geometri.md) | Angir hvilket geografisk referansesystem geometrien skal returneres i.  **Default: 32633** |

`Vegreferanse` eller `veglenke` må oppgis.

### Send inn vegreferanse

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/veg?vegreferanse=5000Ev6hp12m1000
```


```json
{
    "vegreferanse": {
        "fylke": 16,
        "kommune": 0,
        "kategori": "E",
        "status": "V",
        "nummer": 6,
        "hp": 12,
        "meter": 1000,
        "kortform": "5000 Ev6 hp12 m1000"
    },
    "veglenke": {
        "id": 72811,
        "posisjon": 0.21279372589190693,
        "kortform": "0.21279373@72811"
    },
    "geometri": {
        "wkt": "POINT (270765 7038663)",
        "srid": 32633
    }
}
```


### Send inn veglenke

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/veg?veglenke=0.0123456789@1234
```


```json
{
    "vegreferanse": {
        "fylke": 9,
        "kommune": 906,
        "kategori": "K",
        "status": "V",
        "nummer": 55030,
        "hp": 1,
        "meter": 3,
        "kortform": "0906 Kv55030 hp1 m3"
    },
    "veglenke": {
        "id": 1234,
        "posisjon": 0.0123456789,
        "kortform": "0.01234568@1234"
    },
    "geometri": {
        "wkt": "POINT (136089 6496851)",
        "srid": 32633
    }
}
```
### Respons ved ingen treff
Dersom det ikke er noen treff for vegreferansen eller veglenken er statuskoden `204 No content`, og det returneres ikke noe innhold.

## Masseuthenting

Det tilbys et eget batch-endepunkt for å hente flere posisjoner i samme spørring. Det kan sendes inn inntil 1000 posisjoner per spørring. Dersom punktet ikke finnes på vegnettet, returneres `null`.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/veg/batch
```


### Parametere

| Navn | Verdi | Beskrivelse |
|:--------|:-------:|--------:|
vegreferanser | [vegreferanse](../verdi/vegreferanse.md) | Angi en kommaseparert liste med vegreferanser på vegnettet. |  
veglenker | [veglenke](../verdi/veglenke.md) | Angi en kommaseparert liste med veglenker på vegnettet. |  
srid |  [srid](../verdi/geometri.md) | Angir hvilket geografisk referansesystem geometrien skal returneres i. **Default: 32633** |

`Vegreferanser` eller `veglenker` må oppgis. De to parameterene kan ikke kombineres.

### Eksempel

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/veg/batch?veglenker=0.0123456789@1234,0.1243412@5123,0.0123456789@1234245
```


```json
{
    "0.0123456789@1234": {
        "vegreferanse": {
            "fylke": 9,
            "kommune": 906,
            "kategori": "K",
            "status": "V",
            "nummer": 55030,
            "hp": 1,
            "meter": 3,
            "kortform": "0906 Kv55030 hp1 m3"
        },
        "veglenke": {
            "id": 1234,
            "posisjon": 0.0123456789,
            "kortform": "0.01234568@1234"
        },
        "geometri": {
            "wkt": "POINT (136089 6496851)",
            "srid": 32633
        }
    },
    "0.1243412@5123": {
        "vegreferanse": {
            "fylke": 9,
            "kommune": 904,
            "kategori": "P",
            "status": "V",
            "nummer": 99253,
            "hp": 1,
            "meter": 11,
            "kortform": "0904 Pv99253 hp1 m11"
        },
        "veglenke": {
            "id": 5123,
            "posisjon": 0.1243412,
            "kortform": "0.1243412@5123"
        },
        "geometri": {
            "wkt": "POINT (126912 6491405)",
            "srid": 32633
        }
    },
    "0.0123456789@1234245": null
}
```
