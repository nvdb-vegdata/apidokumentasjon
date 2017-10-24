---
title: Vegobjekter
category: endepunkt
---


Tjeneste for å søke etter vegobjekter i Nasjonal vegdatabank.

## Hent vegobjekter

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter
```


```json
[
    {
        "navn": "Skjerm",
        "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/3"
    },
    {
        "navn": "Rekkverk",
        "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/5"
    },
    {
        "navn": "Gjerde",
        "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/7"
    },
    ...
]
```


## Hent vegobjekter av en gitt vegobjekttype

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/<vegobjekttype.id>/
```


Et kall mot tjenesten returnerer en liste av vegobjekter. `vegobjekttype.id` tilsvarer vegobjekttypens unike id i datakatalogen.

Det er kun mulig å spørre etter vegobjekter av én type i samme spørring.

### Velg respons

Bruk parametere til å angi hvilke informasjonselementer responsen skal inneholde.

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
        <td>inkluder</td>
        <td>
            <ul>
                <li>metadata</li>
                <li>egenskaper</li>
                <li>relasjoner</li>
                <li>lokasjon</li>
                <li>vegsegmenter</li>
                <li>geometri</li>
                <li>alle</li>
            </ul>
        </td>
        <td>En kommaseparert liste over hvilke informasjonselementer som skal returneres i tillegg til vegobjektenes id.</td>
    </tr>
    <tr>
        <td>srid</td>
        <td><a href="/verdi/geometri">srid</a></td>
        <td>Angir hvilket geografisk referansesystem geometrien skal returneres i.
            <span class="default">Default: 32633</span>
        </td>
    </tr>
    <tr>
        <td>geometritoleranse</td>
        <td>
            <ul>
                <li>10</li>
                <li>20</li>
                <li>30</li>
            </ul>
        </td>
        <td>Angir om det skal returneres en forenklet geometri. Dersom parameteren utelates, returneres full geometri for vegobjektene. Nummeret angir distansetoleranse for generering av forenklet geometri. <span class="default">Default: full geometri</span> <em>Vær oppmerksom på at standardverdiene kan erstattes av mer egnede verdier uten at denne dokumentasjonen er helt oppdatert.</em></td>
    </tr>
    <tr>
        <td>segmentering</td>
        <td>
            <ul>
                <li>true</li>
                <li>false</li>
            </ul>
        </td>
        <td>Angir om strekningsobjekter skal segmenteres etter søkeområdet.
            <span>Advarsel: versjon 1 av APIet gav utelukkende ut <em>usegmenterte</em> objekter.</span> <span class="default">Default: true</span>
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
        <td><a href="/parameter/lokasjonsfilter">Områdefilter</a></td>
        <td>Angir hvilke områder og vegnett søket skal gjennomføres innenfor.</td>
    </tr>
    <tr>
        <td><a href="/parameter/egenskapsfilter">Egenskapsfilter</a></td>
        <td>Angir at resultatsettet kun skal inneholde vegobjekter med spesifiserte egenskapsverdier.</td>
    </tr>
    <tr>
        <td><a href="/parameter/overlappfilter">Overlappfilter</a></td>
        <td>Angir at vegobjektene skal overlappe med spesifiserte vegobjekttyper.</td>
    </tr>
    <tr>
        <td><a href="/parameter/paginering">Paginering</a></td>
        <td>Angir hvor mange vegobjekter som skal returneres i hver spørring mot APIet.</td>
    </tr>
    </tbody>
</table>

### Eksempel: Hent bomstasjoner

Som standard returneres en liste av vegobjekter. Vegobjektene er innkapslet i en konvolutt, som også inneholder metadata om spørringen. I de andre responseksemplene er konvolutten utelatt.

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/45?antall=10
```


```json
{
    "vegobjekter": [
        {
            "id": 89204552,
            "href": "https://www.vegvesen.no/nvdb/api/v2/45/89204552"
        },
        {
            "id": 291045342,
            "href": "https://www.vegvesen.no/nvdb/api/v2/45/291045342"
        },
        ...
    ],
    "metadata": {
        "returnert": 10,
        "neste": {
            "start": "Nzk4MTM3Nzc=",
            "href": "https://www.vegvesen.no/nvdb/api/v2/vegobjekter/45?antall=10&start=Nzk4MTM3Nzc="
        }
    }
}
```


Det er satt en grense for hvor mange vegobjekter som kan hentes i samme spørring. Les om [paginering](#/parameter/paginering) for å se hvordan alle vegobjekter hentes ved å bruke flere spørringer.

### Eksempel: Hent bomstasjoner med metadata og egenskaper

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/45?inkluder=metadata,egenskaper
```


```json
{
    "objekter": [
        {
            "id": 79632559,
            "href": "https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/45/79632559",
            "metadata": {
                "type": {
                    "id": 45,
                    "navn": "Bomstasjon"
                },
                "versjon": 6,
                "startdato": "2015-11-19",
                "sist_modifisert": "2016-01-09 01:05:50"
            },
            "egenskaper": [
                {
                    "id": 9409,
                    "navn": "Tidsdifferensiert takst",
                    "datatype": 30,
                    "datatype_tekst": "FlerverdiAttributt, Tekst",
                    "verdi": "Nei",
                    "enum_id": 13256
                },
                {
                    "id": 9412,
                    "navn": "Timesregel",
                    "datatype": 30,
                    "datatype_tekst": "FlerverdiAttributt, Tekst",
                    "verdi": "Ja",
                    "enum_id": 13257
                },
                {
                    "id": 9413,
                    "navn": "Vedtatt til år",
                    "datatype": 2,
                    "datatype_tekst": "Tall",
                    "verdi": 2030
                },
                ...
            ]
        },
        ...
    ],
    "metadata": {

    }
}
```


### Eksempel: Be om segmenterte data

Et vegobjekt kan strekke seg over over flere veger og områder. Som standard returneres segmenterte/avgrensede vegobjekter. Dette medfører at et søk etter fartsgrenser i Trondheim kommune, inneholder utelukkende deler av fartsgrensen som befinner seg i denne kommunen.

Dersom parameteren `segmentering` settes til `false`, returneres alle delene av vegobjektene. Inkludert deler som f.eks. strekker seg utenfor kommunen. Dette er den gamle oppførselen til API v1.

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/67?kommune=1421&segmentering=false&inkluder=lokasjon
```


APIet støtter segmentering på følgende felter:

*   Region
*   Vegavdeling
*   Fylke
*   Kommune
*   Vegkategori
*   Vegstatus
*   Hovedparsell
*   Kontraksområde
*   Riksvegreute

## Hent statistikk

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/<vegobjekttype_id>/statistikk/
```


Ved hjelp av de samme filterene som for selve søket får man statistikk angående resultatet ved en egen forespørsel.

Segmentering støttes også her og _default_ oppførsel er påslått.

Følgende parametere støttes ikke på et statistikkall:

*   antall
*   start
*   inkluder
*   geometritoleranse
*   projeksjon
*   dybde

### Eksempel: Antall og lengde for tunnelløp

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/67/statistikk/
```


```json
{
    "antall": 1371,
    "strekningslengde": 1247690
}
```


<table>
<thead>
<tr>
<th>Felt</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>antall</td>
<td>Angir hvor mange vegobjekter søket resulterte i.</td>
</tr>
<tr>
<td>strekningslengde</td>
<td>Angir den totalt strekningslengden basert på disse objektenes stedfesting.</td>
</tr>
</tbody>
</table>

## Hent et spesifikt vegobjekt

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/<vegobjekttype.id>/<vegobjekt.id>
```


Dersom du ikke vet hvilken vegobjekttype et vegobjekt er, kan du bruke hjelperesurssen nedenfor, som videresender deg til korrekt URL.

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekt?id=<vegobjektid>
```


### Velg respons

Et kall mot tjenesten returnerer det ønskede objektet med alle informasjonsfelter. Hvilke informasjonselementer som inkluderes for objektet kan begrenses og responsen kan også inneholde en liste objekter dersom dybdeparameteren brukes.

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
        <td>dybde</td>
        <td>
            <ul>
                <li>1</li>
                <li>2</li>
                <li>...</li>
                <li>n</li>
                <li><em>full</em></li>
            </ul>
        </td>
        <td>
            Parameteren brukes til å spesifisere antall slektsledd døtre man vil hente ut. <em>Når denne parameteren angis vil responsen alltid inneholde en liste.</em>
            <ul>
                <li><em>full</em> Hent hele hierarkiet for dette objektet.</li>
                <li><em>1</em> Hent kun dette objektet.</li>
                <li><em>n > 1</em> Henter <em>n</em> nivåer inntil bunnen av treet treffes.</li>
            </ul>
            <span class="default">Default: 1</span>
        </td>
    </tr>
    <tr>
        <td>inkluder</td>
        <td>
            <ul>
                <li>metadata</li>
                <li>egenskaper</li>
                <li>relasjoner</li>
                <li>lokasjon</li>
                <li>vegsegmenter</li>
                <li>geometri</li>
                <li>alle</li>    
            </ul>
            
        </td>
        <td>En kommaseparert liste over hvilke informasjonselementer som skal returneres i tillegg til vegobjektets id.
            <span class="default">Default: alle, bortsett fra vegsegmenter</span>
        </td>
    </tr>
    </tbody>
</table>

### Eksempel: Hent et spesifikt tunnelløp

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/67/89204552
```


```json
{
    "id": 89204552,
    "href": "https://www.vegvesen.no/nvdb/api/v2/vegobjekter/67/89204552",
    "metadata": {
        "type": {
            "id": 67,
            "navn": "Tunnelløp"
        },
        "versjon": 3,
        "startdato": "2014-01-17",
        "sist_modifisert": "2015-06-26 10:40:41"
    },
    "egenskaper": [
        {
            "id": 8356,
            "navn": "Åpningsår",
            "datatype": 2,
            "datatype_tekst": "Tall",
            "verdi": 1965
        },
        {
            "id": 1317,
            "navn": "Lengde",
            "datatype": 2,
            "datatype_tekst": "Tall",
            "verdi": 33,
            "enhet": {
                "id": 1,
                "navn": "Meter",
                "kortnavn": "m"
            }
        },
        {
            "id": 1130,
            "navn": "Type tunnelløp",
            "datatype": 30,
            "datatype_tekst": "FlerverdiAttributt, Tekst",
            "verdi": "Berg",
            "enum_id": 3386
        },
        ...
    ],
    "geometri": {
        "wkt": "LINESTRING (528704.0498 7478545.60938 20.23, 528697 7478542.09375 21.9, 528692.7002 7478540.29688 22, 528688.7002 7478538.5 22.1, 528684.90039 7478536.90625 22.1, 528681.2002 7478535.19922 22.2, 528674 7478532.28125 21)",
        "srid": 32633,
        "egengeometri": false
    },
    "lokasjon": {
        "kommuner": [
            1845
        ],
        "fylker": [
            18
        ],
        "regioner": [
            5
        ],
        "vegavdelinger": [
            18
        ],
        "kontraktsområder": [
            {
                "nummer": 5002,
                "navn": "5002 Salten 2014-2019"
            },
            {
                "nummer": 1806,
                "navn": "1806 BODØ 2015-2020"
            }
        ],
        "riksvegruter": [
            {
                "nummer": "8A",
                "navn": "RUTE8A",
                "periode": "2010-2019"
            },
            {
                "nummer": "8A",
                "navn": "RUTE8A",
                "periode": "2014-2023"
            }
        ],
        "vegreferanser": [
            {
                "fylke": 18,
                "kommune": 0,
                "kategori": "E",
                "status": "V",
                "nummer": 6,
                "hp": 23,
                "fra_meter": 17084,
                "til_meter": 17117,
                "kortform": "1800 Ev6 hp23 m17084-17117"
            }
        ],
        "stedfestinger": [
            {
                "veglenkeid": 885141,
                "fra_posisjon": 0.519944958676788,
                "til_posisjon": 0.523005143295034,
                "kortform": "0.519944958676788-0.523005143295034@885141",
                "retning": "MED"
            }
        ],
        "geometri": {
            "wkt": "LINESTRING (528704.0498 7478545.60938 20.23, 528697 7478542.09375 21.9, 528692.7002 7478540.29688 22, 528688.7002 7478538.5 22.1, 528684.90039 7478536.90625 22.1, 528681.2002 7478535.19922 22.2, 528674 7478532.28125 21)",
            "srid": 32633
        },
        "strekningslengde": 33
    },
    "relasjoner": {
        "foreldre": [
            {
                "type": {
                    "id": 581,
                    "navn": "Tunnel"
                },
                "vegobjekter": [
                    89204551
                ]
            }
        ],
        "barn": [
            {
                "type": {
                    "id": 89,
                    "navn": "Signalanlegg"
                },
                "vegobjekter": [
                    481662525
                ]
            },
            {
                "type": {
                    "id": 69,
                    "navn": "Tunnelportal"
                },
                "vegobjekter": [
                    272110916,
                    272110918
                ]
            },
            ...
        ]
    }
}
```


## Hent egenskaper

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581/79608124/egenskaper
```


```json
[
    {
        "id": 8945,
        "navn": "Lengde, skiltet",
        "datatype": 2,
        "datatype_tekst": "Tall",
        "verdi": 120,
        "enhet": {
            "id": 1,
            "navn": "Meter",
            "kortnavn": "m"
        }
    },
    {
        "id": 8150,
        "navn": "Sum lengde alle løp",
        "datatype": 2,
        "datatype_tekst": "Tall",
        "verdi": 120,
        "enhet": {
            "id": 1,
            "navn": "Meter",
            "kortnavn": "m"
        }
    },
    {
        "id": 5225,
        "navn": "Navn",
        "datatype": 1,
        "datatype_tekst": "Tekst",
        "verdi": "Vikatunnelen"
    },
    ...
]
```


## Hent en spesifikk egenskap

Det er også mulig å slå opp spesifikk egenskap direkte.

```
GET https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581/79608124/egenskaper/3947
```


```json
{
    "id": 3947,
    "navn": "Antall parallelle hovedløp",
    "datatype": 31,
    "datatype_tekst": "Flerverdiattributt, Tall",
    "verdi": 1,
    "enum_id": 5011,
    "enhet": {
        "id": 12,
        "navn": "Stykker",
        "kortnavn": "stk"
    }
}
```


## Hent endringer

Det er mulig å hente ut en liste over vegobjekter som er endret etter en gitt dato.

```
GET https://www.vegvesen.no/nvdb/api/v2//vegobjekter/<vegobjekttype.id>/endringer
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
<td>type</td>
<td>endret  
slettet</td>
<td>Ved å sette type kan du få enten en liste over endrede objekter (denne vil inkludere objektet i sin nyeste form) eller en liste med slettede objekter. I det siste tilfellet vil kun objektets id være tilgjengelig.  
<span class="obligatorisk">Obligatorisk</span></td>
</tr>
<tr>
<td>etter</td>
<td>Tid</td>
<td>Her kan du styre tidsterskelen.  
<span class="obligatorisk">Obligatorisk</span></td>
</tr>
</tbody>
</table>

Vær oppmerksom på at også dette endepunktet benytter [paginering](#/parameter/paginering). I responsksemplene er konvolutten med metadata utelatt.

Områdefilter og egenskapsfilter er _ikke_ støttet for dette endepunktet.

### Eksempel for ?type=endret&etter="2014-01-01"

```json
[
    {
        'type': "ENDRET",
        'vegobjekt': {
            ...
        }
    }
]
```


### Eksempel for ?type=slettet&etter="2014-01-01 15:30"

```json
[
    {
        'type': "SLETTET",
        'vegobjekt': 1235415
    }
]
```


### Angivelse av tid

Tidsparameteren kan angis på flere måter:

<table>
<tbody>
<tr>
<td>"2015-05-27T05:00:00+02:00"</td>
<td>ISO 8601-streng</td>
</tr>
<tr>
<td>"2015-05-27 05:00:00"</td>
<td>Alias for "2015-05-27T05:00:00+02:00"</td>
</tr>
<tr>
<td>"2015-05-27 05:00"</td>
<td>Alias for "2015-05-27T05:00:00+02:00"</td>
</tr>
<tr>
<td>"2015-05-27"</td>
<td>Alias for "2015-05-27T00:00:00+02:00"</td>
</tr>
</tbody>
</table>
