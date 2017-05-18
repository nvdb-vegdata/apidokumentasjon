---
layout: page
title: GET /vegnett
---

Tjeneste for å hente det topologiske vegnettverket fra NVDB.

## Hent vegnett

Vegnettet i NVDB består av en lenke-node-struktur. I APIet er det kun veglenker som kan hentes gjennom et eget endepunkt.

Det er likevel mulig å bygge opp et topologisk vegnettverk, ved å bruke lenkenes `startnode` og `sluttnode`.

```
GET https://www.vegvesen.no/nvdb/api/v2/vegnett
```


### Respons

```json
[
    {
        "navn": "Veglenker",
        "href": "https://www.vegvesen.no/nvdb/api/v2/vegnett/lenker"
    }
]
```


## Hent veglenker

```
GET https://www.vegvesen.no/nvdb/api/v2/vegnett/lenker
```


```
{
    "objekter": [
        {
            "id": 1000,
            "href": "https://www.vegvesen.no/nvdb/api/v2/vegnett/lenker/1000",
            "metadata": {
                "startdato": "1950-01-01"
            },
            "fra_posisjon": 0,
            "til_posisjon": 1,
            "startnode": "34674-1",
            "sluttnode": "1272325-1",
            "felt": "1#2",
            "medium": "T",
            "temakode": 7001,
            "konnekteringslenke": false,
            "topologinivå": 0,
            "topologinivå_tekst": "Vegtrasé",
            "vegsegment": {
                "geometri": {
                    "wkt": "LINESTRING (147939.8 6514243.8 27.1, 147944.1 6514241.5 27.5, 147948 6514240.6 27.7, 147952.1 6514240.1 27.7, 147956.1 6514239.6 27.6, 147960 6514238.1 27.5, 147963.9 6514236.9 27.2, 147967.6 6514235.4 26.9, 147971.2 6514233.3 26.7)",
                    "srid": 32633,
                    "kvalitet": {
                        "metode": 95,
                        "nøyaktighet": 200,
                        "høydenøyaktighet": -1,
                        "toleranse": -1,
                        "synlighet": 99,
                        "datafangstdato": "2001-06-07"
                    }
                },
                "kommune": 914,
                "fylke": 9,
                "region": 2,
                "vegavdeling": 9,
                "vegreferanse": {
                    "fylke": 9,
                    "kommune": 914,
                    "kategori": "P",
                    "status": "V",
                    "nummer": 1031,
                    "hp": 1,
                    "fra_meter": 0,
                    "til_meter": 33,
                    "kortform": "0914 Pv1031 hp1 m0-33"
                },
                "strekningslengde": 33
            }
        }
    ],
    "metadata": {
        "antall": 1,
        "returnert": 1,
        "neste": {
            "start": "QW9FL0ZHeGpmREV3TURBd2ZERTVOVEF3TVRBeGZEQXdNREF3TURBd01EQXdNREF3TURCOE0yWm1NREF3TURBd01EQXdNREF3TUE9PQ==",
            "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegnett/lenker?antall=1&start=QW9FL0ZHeGpmREV3TURBd2ZERTVOVEF3TVRBeGZEQXdNREF3TURBd01EQXdNREF3TURCOE0yWm1NREF3TURBd01EQXdNREF3TUE9PQ%3D%3D"
        }
    }
}
```


Det er ikke alltid et 1-til-1-forhold mellom veglenkene som finnes i NVDB-databasen, og veglenkene som eksponeres gjennom dette endepunktet.

Veglenkene som eksponeres gjennom APIet er segmentert etter vegreferanse, slik at hvert objekt har én vegreferanse. Det vil derfor finnes flere veglenker som har samme id, og startposisjon og sluttposisjon vil kunne avvike fra henholdsvis 0 og 1.

### Responsbeskrivelse

<table>
<thead>
<tr>
<th>Felt</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>id</td>
<td>Id til veglenke.</td>
</tr>
<tr>
<td>fra_posisjon</td>
<td>Relativ startposisjon på veglenke.</td>
</tr>
<tr>
<td>til_posisjon</td>
<td>Relativ sluttposisjon på veglenke.</td>
</tr>
<tr>
<td>startnode</td>
<td>Lenkens startnode.</td>
</tr>
<tr>
<td>sluttnode</td>
<td>Lenkens sluttnode.</td>
</tr>
<tr>
<td>felt</td>
<td>Angir hvilke kjørefelt veglenken har.</td>
</tr>
<tr>
<td>medium</td>
<td>Verdier i henhold til SOSI
<ul>
<li><b>T</b> - På terrenget/på bakkenivå
<li><b>B</b> - I bygning/bygningsmessig anlegg
<li><b>L</b> - I luft
<li><b>U</b> - Under terrenget
<li><b>S</b> - På sjøbunnen
<li><b>O</b> - På vannoverflaten
<li><b>V</b> - Alltid i vann
<li><b>D</b> - Tidvis under vann
<li><b>I</b> - På isbre
<li><b>W</b> - Under sjøbunnen
<li><b>J</b> - Under isbre
<li><b>X</b> - Ukjent
</dl>
</td>
</tr>
<tr>
<td>temakode</td>
<td>Verdier i henhold til SOSI
<ul>
<li><b>7001</b> - Vegsenterlinje
<li><b>7004</b> - Svingekonnekteringslenke
<li><b>7012</b> - Vegtrase
<li><b>7011</b> - Kjørebane
<li><b>7010</b> - Kjørefelt
<li><b>7201</b> - Bilferjestrekning
<li><b>7042</b> - Gang Sykkelveg Senterlinje
<li><b>7043</b> - Sykkelveg Senterlinje
<li><b>7046</b> - Fortau
<li><b>6304</b> - Frittstående trapp
</dl>
</td>
</tr>
<tr>
<td>konnekteringslenke</td>
<td>Angir om veglenken er en konnekteringslenke</td>
</tr>
<tr>
<td>topologinivå  
topologinivå_tekst</td>
<td>Angir veglenkens detaljnivå
<ul>
<li><b>0</b> - Vegtrasé
<li><b>1</b> - Kjørebane
<li><b>2</b> - Kjørefelt
</dl>
</td>
</tr>
</tbody>
</table>

### Avgrens søkeresultatet

For å avgrense søkeresultatet, støttes følgende parametere:

<table>
<thead>
<tr>
<th>Søkeparameter</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>[Områdefilter](#/parameter/lokasjonsfilter)</td>
<td>Angir hvilke områder og vegnett søket skal gjennomføres innenfor.</td>
</tr>
<tr>
<td>[Paginering](#/parameter/paginering)</td>
<td>Angir hvor mange vegobjekter som skal returneres i hver spørring mot APIet.</td>
</tr>
</tbody>
</table>
