---
layout: page
title: GET /posisjon
---

Tjeneste for å finne nærmeste veg til en gitt koordinat.

## Finn posisjon

```
GET https://www.vegvesen.no/nvdb/api/v2/posisjon
```

### Parametere

<table>
<thead>
<tr>
<th>Navn</th>
<th>Verdi</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>nord</td>
<td><flyttall></td>
<td>Østlig koordinat</td>
</tr>
<tr>
<td>ost</td>
<td><flyttall></td>
<td>Nordlig koordinat</td>
</tr>
<tr>
<td>lat</td>
<td><flyttall></td>
<td>Breddegrad</td>
</tr>
<tr>
<td>lon</td>
<td><flyttall></td>
<td>Lengdegrad</td>
</tr>
<tr>
<td>maks_avstand</td>
<td><heltall></td>
<td>Angir søkeavstand i meter.  
<span class="default">Default: 30</span></td>
</tr>
<tr>
<td>maks_antall</td>
<td><heltall></td>
<td>Angir hvor mange resultater som maksimum skal returneres.  
<span class="default">Default: 1</span></td>
</tr>
<tr>
<td>konnekteringslenker</td>
<td>true  
false</td>
<td>Angir om det skal returneres treff på konnekteringslenker.  
<span class="default">Default: false</span></td>
</tr>
<tr>
<td>detaljerte_lenker</td>
<td>true  
false</td>
<td>Angir om det skal returneres treff på detaljerte vegnettsnivå.  
<span class="default">Default: false</span></td>
</tr>
<tr>
<td>vegreferanse</td>
<td>[vegreferanse](#/verdi/vegreferanse)</td>
<td>Angi om det kun skal søkes innenfor spesifikke vegreferanser</td>
</tr>
<tr>
<td>srid</td>
<td>[srid](#/verdi/geometri)</td>
<td>Angir hvilket geografisk referansesystem geometrien skal returneres i.  
<span class="default">Default: 32633</span></td>
</tr>
</tbody>
</table>

Parameterne `nord`+`ost` eller `lat`+`lon` er obligatoriske.

Feltet `avstand` i responsen angir hvor mange meter det er mellom innsendt punkt og de returnerte posisjonene. Resultatene sorteres etter korteste avstand, så når `maks_antall` settes til 1 (default), er det alltid det nærmeste punktet på vegnettet som returneres.

### Eksempel

```
GET https://www.vegvesen.no/nvdb/api/v2/posisjon.json?nord=7038165&ost=269815
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
            "kortform": "1600 Rv706 hp52 m344"
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
GET https://www.vegvesen.no/nvdb/api/v2/posisjon.json?nord=7038165&ost=269815&konnekteringslenker=true
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
            "kortform": "1600 Rg706 hp52 m303"
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
GET https://www.vegvesen.no/nvdb/api/v2/posisjon?lat=63.415855&lon=10.395287&maks_avstand=100&maks_antall=10
```

```json
[
    {
        "vegreferanse": {
            "fylke": 16,
            "kommune": 1601,
            "kategori": "K",
            "status": "V",
            "nummer": 1001,
            "hp": 2,
            "meter": 104,
            "kortform": "1601 Kv1001 hp2 m104"
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
            "kommune": 1601,
            "kategori": "K",
            "status": "G",
            "nummer": 9136,
            "hp": 1,
            "meter": 466,
            "kortform": "1601 Kg9136 hp1 m466"
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
            "kommune": 1601,
            "kategori": "K",
            "status": "G",
            "nummer": 7800,
            "hp": 1,
            "meter": 312,
            "kortform": "1601 Kg7800 hp1 m312"
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
