## Vegnett

Tjeneste for å hente det topologiske vegnettverket fra NVDB.

## Hent vegnett

Vegnettet i NVDB består av en lenke-node-struktur. I APIet er det kun veglenker som kan hentes gjennom et eget endepunkt.

Det er likevel mulig å bygge opp et topologisk vegnettverk, ved å bruke lenkenes `startnode` og `sluttnode`.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegnett
```


### Respons

```json
[
    {
        "navn": "Veglenker",
        "href": "https://nvdbapiles-v2.atlas.vegvesen.no/vegnett/lenker"
    }
]
```


## Hent veglenker

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegnett/lenker
```


```
{
    "objekter": [
        {
        "href" : "https://nvdbapiles-v2.atlas.vegvesen.no/vegnett/lenker/1000",
        "metadata" : {
            "startdato" : "2015-08-10"
        },
        "veglenkeid" : 1000,
        "startposisjon" : 0.0,
        "sluttposisjon" : 0.32765825,
        "kortform" : "0.0-0.32765825@1000",
        "felt" : "1#2",
        "medium" : "T",
        "temakode" : 7001,
        "konnekteringslenke" : false,
        "startnode" : "32041",
        "sluttnode" : "32067",
        "geometri" : {
            "wkt" : "LINESTRING Z (136942.82 6494978.51 13.53, 136946.8 6494980.6 14.3, 136954.1 6494983.3 14.1, 136962.8 6494987.7 12.2, 136965.1 6494989.8 12.1, 136971.9 6494999.7 12.1, 136980.9 6495014.4 11.3, 136983.6 6495017.4 10.6, 136987.2 6495020.1 10.5, 136994.1 6495023.5 10.4, 137000.8 6495024.2 10.4)",
            "srid" : 32633,
            "kvalitet" : {
                "metode" : 22,
                "nøyaktighet" : 200,
                "høydenøyaktighet" : -1,
                "toleranse" : -1,
                "synlighet" : 99,
                "datafangstdato" : "1999-05-18"
            }
        },
        "region" : 2,
        "fylke" : 9,
        "vegavdeling" : 9,
        "kommune" : 906,
        "vegreferanse" : {
            "fylke" : 9,
            "kommune" : 906,
            "kategori" : "K",
            "status" : "V",
            "nummer" : 31007,
            "hp" : 1,
            "fra_meter" : 0,
            "til_meter" : 79,
            "kortform" : "0906 Kv31007 hp1 m0-79"
        },
        "strekningslengde" : 78,
        "typeVeg" : "enkelBilveg"
    }
    ],
    "metadata": {
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
                <li><b>T</b> - På terrenget/på bakkenivå</li>
                <li><b>B</b> - I bygning/bygningsmessig anlegg</li>
                <li><b>L</b> - I luft</li>
                <li><b>U</b> - Under terrenget</li>
                <li><b>S</b> - På sjøbunnen</li>
                <li><b>O</b> - På vannoverflaten</li>
                <li><b>V</b> - Alltid i vann</li>
                <li><b>D</b> - Tidvis under vann</li>
                <li><b>I</b> - På isbre</li>
                <li><b>W</b> - Under sjøbunnen</li>
                <li><b>J</b> - Under isbre</li>
                <li><b>X</b> - Ukjent</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>temakode</td>
        <td>Verdier i henhold til SOSI
            <ul>
                <li><b>7001</b> - Vegsenterlinje</li>
                <li><b>7004</b> - Svingekonnekteringslenke</li>
                <li><b>7012</b> - Vegtrase</li>
                <li><b>7011</b> - Kjørebane</li>
                <li><b>7010</b> - Kjørefelt</li>
                <li><b>7201</b> - Bilferjestrekning</li>
                <li><b>7042</b> - Gang Sykkelveg Senterlinje</li>
                <li><b>7043</b> - Sykkelveg Senterlinje</li>
                <li><b>7046</b> - Fortau</li>
                <li><b>6304</b> - Frittstående trapp</li>
            </ul>
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
                <li><b>0</b> - Vegtrasé</li>
                <li><b>1</b> - Kjørebane</li>
                <li><b>2</b> - Kjørefelt</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>superid</td>
        <td>Referanse til foreldrelenke i topologinivå over om lenken er kjørebane eller kjørefelt.</td>
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
        <td><a href="/parameter/lokasjonsfilter">Områdefilter</a></td>
        <td>Angir hvilke områder og vegnett søket skal gjennomføres innenfor.</td>
    </tr>
    <tr>
        <td><a href="/parameter/paginering">Paginering</a></td>
        <td>Angir hvor mange vegobjekter som skal returneres i hver spørring mot APIet.</td>
    </tr>
    </tbody>
</table>
