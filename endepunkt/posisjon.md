---
title: Posisjon
category: endepunkt
---
# Oppdatert API-dokumentasjon for versjon 3

Bruk heller dokumentasjon for versjon 3 av NVDB api https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon


Tjeneste for å finne nærmeste veg til en gitt koordinat.

## Finn posisjon

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/posisjon
```

### Parametere

| Navn | Verdi | Beskrivelse |
|:--------|:-------|:--------|
|nord | flyttall | Østlig koordinat |
|ost |  flyttall | Nordlig koordinat |
|lat | flyttall |  Breddegrad |
|lon | flyttall | Lengdegrad |
|maks_avstand | heltall | Angir søkeavstand i meter. **Default: 30**|  
|maks_antall | heltall | Angir hvor mange resultater som maksimum skal returneres. **Default: 1** |
|konnekteringslenker | boolsk | Angir om det skal returneres treff på konnekteringslenker. **Default: false** |
|detaljerte_lenker | boolsk | Angir om det skal returneres treff på detaljerte vegnettsnivå. **Default: false** |
|vegreferanse | [vegreferanse](../verdi/vegreferanse.md) | Angi om det kun skal søkes innenfor spesifikke vegreferanser |
|srid | [srid](../verdi/geometri.md) | Angir hvilket geografisk referansesystem geometrien skal returneres i. **Default: 32633** |

Parameterne `nord`+`ost` eller `lat`+`lon` er obligatoriske.

Feltet `avstand` i responsen angir hvor mange meter det er mellom innsendt punkt og de returnerte posisjonene. Resultatene sorteres etter korteste avstand, så når `maks_antall` settes til 1 (default), er det alltid det nærmeste punktet på vegnettet som returneres.

### Eksempel

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/posisjon?nord=7038165&ost=269815
```

```json
[
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 0,
            "kategori": "R",
            "status": "V",
            "nummer": 706,
            "hp": 52,
            "meter": 344,
            "kortform": "5000 Rv706 hp52 m344"
        },
        "veglenke": {
            "id": 72863,
            "posisjon": 0.86618,
            "kortform": "0.86618@72863"
        },
        "geometri": {
            "wkt": "POINT (269812 7038167)",
            "srid": 32633
        },
        "avstand": 3
    }
]
```

### Eksempel: Inkluder konnekteringslenker

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/posisjon?nord=7038165&ost=269815&konnekteringslenker=true
```

```json
[
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 0,
            "kategori": "R",
            "status": "G",
            "nummer": 706,
            "hp": 52,
            "meter": 303,
            "kortform": "5000 Rg706 hp52 m303"
        },
        "veglenke": {
            "id": 2479536,
            "posisjon": 0.09971,
            "kortform": "0.09971@2479536"
        },
        "geometri": {
            "wkt": "POINT (269816 7038166)",
            "srid": 32633
        },
        "avstand": 2
    }
]
```

### Eksempel: Angivelse av maks antall og maks avstand

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/posisjon?lat=63.415855&lon=10.395287&maks_avstand=100&maks_antall=10
```

```json
[
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 5001,
            "kategori": "K",
            "status": "V",
            "nummer": 1001,
            "hp": 2,
            "meter": 104,
            "kortform": "5001 Kv1001 hp2 m104"
        },
        "veglenke": {
            "id": 41254,
            "posisjon": 0.47954,
            "kortform": "0.47954@41254"
        },
        "geometri": {
            "wkt": "POINT (270227 7040211)",
            "srid": 32633
        },
        "avstand": 25
    },
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 5001,
            "kategori": "K",
            "status": "G",
            "nummer": 9136,
            "hp": 1,
            "meter": 466,
            "kortform": "5001 Kg9136 hp1 m466"
        },
        "veglenke": {
            "id": 71939,
            "posisjon": 0.96635,
            "kortform": "0.96635@71939"
        },
        "geometri": {
            "wkt": "POINT (270268 7040210)",
            "srid": 32633
        },
        "avstand": 43
    },
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 5001,
            "kategori": "K",
            "status": "G",
            "nummer": 7800,
            "hp": 1,
            "meter": 312,
            "kortform": "5001 Kg7800 hp1 m312"
        },
        "veglenke": {
            "id": 2234647,
            "posisjon": 1,
            "kortform": "1.0@2234647"
        },
        "geometri": {
            "wkt": "POINT (270263 7040224)",
            "srid": 32633
        },
        "avstand": 48
    },
    ...
]
```
