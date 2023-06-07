---
title: Vegobjekttyper
category: endepunkt
---
# Oppdatert API-dokumentasjon for versjon 3
Bruk heller dokumentasjon for versjon 3 av NVDB api [https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon](https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon)

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

Tjeneste for å vise innholdet i NVDBs metadatakatalog, Datakatalogen.

## Hent liste med vegobjekttyper

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper
```


### Parametere

|Navn|Verdi|Beskrivelse|
|:-|:-|:-|
|inkluder|egenskapstyper<br>relasjonstyper<br>styringsparametere<br>alle|Angir hvilke informasjonsfelter som skal inkluderes i tillegg til vegobjekttypenes metadata.|
|kategori|kommaseparerte kategori-id'er|Hent ut vegobjekttyper med de gitte kategoriene. (https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/kategorier) Se: [Hent liste av kategorier](#hent-liste-over-kategorier)|

### Respons

```json
[
    {
        "id": 3,
        "navn": "Skjerm",
        "beskrivelse": "En frittstående konstruksjon som skal være et hinder for f.eks støyutbredelse",
        "stedfesting": "LINJE",
        "objektliste_dato": "2012-05-08",
        "veiledning": "",
        "sosinavn": "Skjerm",
        "sosinvdbnavn": "Skjerm_3",
        "sorteringsnummer": 4760
    },
    {
        "id": 5,
        "navn": "Rekkverk",
        "beskrivelse": "En anordning som skal hindre at kjøretøy forlater vegen (Håndbok N101 (231))",
        "stedfesting": "LINJE",
        "objektliste_dato": "2012-05-08",
        "veiledning": "Der rekkverk følger vegens kurvatur er start og slutt rekkverkets begynnelse/slutt. Dette defineres ved start / støtpute, evt fra der rekkverk blir synlig/usynlig. Rekkverk der vi har avvik fra mellom referanse og målt lengde , skal",
        "sosinavn": "Rekkverk",
        "sosinvdbnavn": "Rekkverk_5",
        "sorteringsnummer": 3600
    },
    {
        "id": 7,
        "navn": "Gjerde",
        "beskrivelse": "Gjerde er frittstående hinder som skal stenge/lede ferdsel av folk eller dyr",
        "stedfesting": "LINJE",
        "objektliste_dato": "2012-05-08",
        "veiledning": "",
        "sosinavn": "Gjerde",
        "sosinvdbnavn": "Gjerde_7",
        "sorteringsnummer": 4800
    },
    ...
]
```


|Felt|Beskrivelse|
|:-|:-|
|id|Angir vegobjekttypens unike id.|
|navn|Angir vegobjekttypens offisielle navn.|
|beskrivelse|Tekstlig beskrivelse av hva vegobjekttypen er.|
|veiledning|Supplerende informasjon til beskrivelsen, for eksempel en registreringsveiledning|
|stedfesting|Angir hvordan vegobjekttypen skal stedfestes på vegnettet:<br><br>**PUNKT** - Er stedfestet i ett punkt på vegnettet<br>**LINJE** - Er stedfestet på en strekning mellom to punkter på vegnettet<br>**FLEREPUNKT** - Er stedfestet i flere punkter på vegnettet<br>**SVING** - Er stedfestet i en node og i flere punkter på vegnettet<br>**INGEN** - Ingen stedfesting til vegnettet<br>|
|sosinvdbnavn|Navn som brukes i dataleveranser.|
|sosinavn|Navn på tilsvarende objekttype i SOSI-standarden|
|objektliste_dato|Dato for når vegobjekttypen ble en del av objektlista. Om feltet ikke har noen verdi, er ikke vegobjekttypen en del av objektlista|
|sorteringsnummer|For bruk i sortering av objektlista|


## Hent vegobjekttype

For å begrense datatrafikk, er det mulig å hente detaljert informasjon om en spesifikk vegobjekttype.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/<vegobjekttype.id>
```


### Parametere

|Navn|Verdi|Beskrivelse|
|:-|:-|:-|
|inkluder|egenskapstyper<br>relasjonstyper<br>styringsparametere<br>alle|Angir hvilke informasjonsfelter som skal inkluderes i tillegg til vegobjekttypenes metadata.|

### Eksempel: Hent fartsgrense (105)

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/105
```


```json
{
    "id": 105,
    "navn": "Fartsgrense",
    "beskrivelse": "Høyeste tillatte hastighet på en vegstrekning.",
    "stedfesting": "LINJE",
    "veiledning": "",
    "sosinavn": "Fartsgrense",
    "sosinvdbnavn": "Fartsgrense_105",
    "sorteringsnummer": 0,
    "kategorier": [ ... ], 
    "egenskapstyper": [ ... ],
    "relasjonstyper": [ ... ],
    "styringsparametere": { ... }
}
```

Dersom ingen `inkluder`-parameter er definert vil all informasjon returneres. Dette tilsvarer `inkluder=alle`.
Egenskapstyper, relasjonstyper og styringsparametere er nærmere beskrevet i avsnittene som følger.

## Beskrivelse av egenskapstyper

Ved angivelse av `inkluder=egenskaper` eller `inkluder=alle`, blir følgende objekt en del av responsen for hver vegobjekttype.

```json
{
    ...
    "egenskapstyper": [
        {
            "id": 2021,
            "navn": "Fartsgrense",
            "beskrivelse": "Fartsgrense",
            "datatype": 31,
            "datatype_tekst": "Flerverdiattributt, Tall",
            "liste": false,
            "sensitivitet": 0,
            "sorteringsnummer": 1,
            "veiledning": "Høyeste tillatte hastighet på en vegstrekning.",
            "viktighet": 1,
            "viktighet_tekst": "PÅKREVD_ABSOLUTT",
            "sosinavn": "Fartsgrense",
            "sosinvdbnavn": "Fartsgrense_2021",
            "tillatte_verdier": [
                {
                    "id": 2738,
                    "kortnavn": "80",
                    "navn": "80",
                    "sorteringsnummer": 35
                },
                {
                    "id": 2741,
                    "kortnavn": "90",
                    "navn": "90",
                    "sorteringsnummer": 36
                },
                {
                    "id": 2726,
                    "kortnavn": "30",
                    "navn": "30",
                    "sorteringsnummer": 30
                },
                ...
            ],
            "feltlengde": 3,
            "enhet": {
                "id": 7,
                "navn": "Kilometer/time",
                "kortnavn": "km/h"
            },
            "styringsparametere": {
                "avledet": false,
                "obligatorisk_verdi": true
            }
        },
        {
            "id": 1891,
            "navn": "Vedtaksnummer",
            "beskrivelse": "Angir vedtaksnummer",
            "datatype": 1,
            "datatype_tekst": "Tekst",
            "liste": false,
            "sensitivitet": 0,
            "sorteringsnummer": 8,
            "veiledning": "Påkrevd der ny fartsgrense avviker fra standardgrensene 50 i tettbygd strøk og 80 i spredtbygd.",
            "viktighet": 3,
            "viktighet_tekst": "BETINGET",
            "sosinavn": "Vedtaksnummer",
            "sosinvdbnavn": "Vedtaksnummer_1891",
            "feltlengde": 30,
            "styringsparametere": {
                "avledet": false,
                "obligatorisk_verdi": false
            }
        },
        ...
    ],
    ...
}
```


|Felt|Beskrivelse|
|:-|:-|
|id|Angir egenskapstypens unike id.|
|navn|Angir egenskapstypens offisielle navn.|
|beskrivelse|Tekstlig beskrivelse av egenskapstypen.|
|veiledning|Supplerende informasjon til beskrivelsen.|
|datatype<br>datatype_tekst|Angir egenskapstypens datatype.|
|sosinvdbnavn|Navn som brukes i dataleveranser.|
|sosinavn|Navn på tilsvarende objekttype i SOSI-standarden.|
|objektliste_dato|Dato for når egenskapstypen ble en del av objektlista. Om feltet ikke har noen verdi, er ikke egenskapstypen en del av objektlista.|
|sorteringsnummer|Sorteringsnummer for egenskapstypen.|
|feltlengde|Angir hvor mange tegn verdien kan ha. Inkluderer antall desimaler og desimaltegn, men inkluderer ikke fortegn.|
|desimaler|Angir hvor mange desimaler verdien kan ha. Relevant for tallverdier.|
|feltmønster|Angir om verdien må følge et bestemt mønster.|
|standardverdi|Angir om egenskapstypen skal få en standardverdi, om verdien ikke angis.|
|min_anbefalt|Anbefalt minimumsverdi. Relevant for tallverdier.|
|maks_anbefalt|Anbefalt minimumsverdi. Relevant for tallverdier.|
|min|Absolutt minimumsverdi. Relevant for tallverdier.|
|maks|Absolutt maksimumsverdi. Relevant for tallverdier.|
|sensitivitet|Angir om egenskapstypen har verdier av sensitiv art:<br>0 - Verdier av denne egenskapstypen er tilgjengelig<br>1 - Verdier av denne egenskapstypen er **ikke** tilgjengelig for allmennheten|
|viktighet<br>viktighet_tekst|Angir om det er krav til regisrering av egenskapstypen:<br>1 - PÅKREVD_ABSOLUTT. Et vegobjekt kan ikke lagres i NVDB uten at denne egenskapstypen har verdi<br>2 - PÅKREVD. Egenskapstypen skal registreres, men vegobjekter som mangler verdi skal ikke avvises<br>3 - BETINGET. Egenskapstypens skal registreres, dersom det er relevant eller om gitte kriterier er oppfylt<br>4 - OPSJONELL. Det er frivillig å registrere egenskapstypen<br>7 - SPESIALINFORMAJSON. Det er frivillig å registrere egenskapstypen<br>9 - HISTORISK. Egenskapstypen skal ikke registreres|
|betingelse_type|Angir om egenskapstypens verdi skal beregnes ut ifra verdien til en annen egenskapstype. Relevant for egenskapstyper med viktighet lik 3, betinget.|
|betingelse_verdi|Angir id til egenskapstype denne egenskapstypens verdi skal beregnes ut ifra.|


### Tillatte verdier

Beskrivelse av feltene knyttet til egenskapstypenes tillatte verdier

|Felt|Beskrivelse|
|id|Angir verdiens unike id.|
|navn|Angir verdiens navn.|
|kortnavn|Angir verdiens forkortelse.|
|beskrivelse|Tekstlig beskrivelse av verdien.|
|objektliste_dato|Dato for når verdien ble en del av objektlista. Om feltet ikke har noen verdi, er ikke verdien en del av objektlista.|
|sorteringsnummer|Sorteringsnummer for verdien|
|standardverdi|Angir om verdien er standardverdi for denne egenskapstypen.|

### Styringsparametere for egenskapstyper

Beskrivelse av feltene knyttet egenskapstypeness styringsparametere.

|Felt|Beskrivelse|
|:-|:-|
|avledet|Angir om egenskapstypen er avledet, og beregnes automatisk:<br>`true` - Avledet<br>`false` - Er ikke avledet|
|tillatte_verdier_kortnavn_offisiell|Angir om kortnavnet for egenskapstypens tillatte verdier er de offisielle navnene:<br>`true` - Ja<br>`false` - Nei|
|tillatte_verdier_kortnavn_offisiell_makslengde|Angir maksimal antall tegn for kortnavnene til egenskapstypens tillatte verdier.|
|ajourhold_snu|Angir om verdier tilknyttet egenskapstypen er avhengig av vegens metreringsretning:<br>`true` - Ja<br>`false` - Nei|
|fortegnsendring_snu|Angir om verdier tilknyttet egenskapstypen skal endre fortegn ved snuing av metreringsetning:<br>`true` - Ja<br>`false` - Nei|
|lengdeavhengig_snu|Angir om egenskapstypens verdi er avhengig av vegobjektets utstrekning eller ikke:<br>`true` - Verdi blir ugyldig ved endring av vegobjektets utstrekning<br>false - Verdi er upåvirket av vegobjektets utstrekning|
|verdi_beregnes_av_geometri|Angir om egenskapstypens verdi skal beregnes basert på tilgjengelig egengeometri:<br>`true` - Ja<br>`false` - Nei|


## Beskrivelse av relasjoner

Ved angivelse av `inkluder=relasjonstyper` eller `inkluder=alle`, blir følgende objekt en del av responsen for hver vegobjekttype.

```json
{
    ...
    "relasjonstyper": {
        "foreldre": [

        ],
        "barn": [
            {
                "relasjonstype": "KOMPOSISJON",
                "id": 1829,
                "type": {
                    "id": 446,
                    "navn": "Dokumentasjon"
                }
            },
            {
                "innenfor_mor": "JA",
                "relasjonstype": "KOMPOSISJON",
                "id": 272,
                "type": {
                    "id": 297,
                    "navn": "Kommentar"
                }
            }
        ]
    },
    ...
}
```


|Felt|Beskrivelse|
|:-|:-|
|foreldre|Tillatte foreldre-relasjoner til vegobjekttypen.|
|barn|Tillatte barn-relasjoner til vegobjekttypen.|
|id|Angir relasjonens unike id|
|relasjonstype|Angir relasjonstype:<br>`KOMPOSISJON`<br>`AGGREGERING`<br>`ASSOSIASJON`|
|type|Angir id og navn til vegobjekttypen det kan finnes en relasjon til|
|beskrivelse|Tekstlig beskrivelse.|
|veiledning|Supplerende informasjon til beskrivelsen.|
|min|Angir et minste antall for hvor mange relasjoner av denne typen det må finnes.|
|maks|Angir et maksimalt antall for hvor mange relasjoner av denne typen det kan finnes.|
|objektliste_dato|Dato for når relasjonstypen ble en del av objektlista. Om feltet ikke har noen verdi, er ikke relasjonstypen en del av objektlista|
|innenfor_mor|Angir hvordan datterobjektet må stedfestes:<br>`NEI` - Stedfestingen til datterobjektet behøver ikke å være innenfor morobjektet<br>`JA` - Stedfestingen til datterobjektet må være innenfor morobjektet<br>`MED_AVVIK` - Stedfestingen til datterobjektet må være innenfor morobjektet, men feltangivelse/sideposisjon kan avvike|

## Beskrivelse av styringsparametere for vegobjekttyper

Ved angivelse av `inkluder=styringsparametere` eller `inkluder=alle`, blir følgende objekt en del av responsen for hver vegobjekttype.

```json
{
    ...
    "styringsparametere": {
        "tidsrom_relevant": true,
        "avledet": false,
        "må_ha_mor": false,
        "overlapp": false,
        "kjørefelt_relevant": "KAN",
        "sideposisjon_relevant": "NEI",
        "ajourhold_i": "OVERLEVER",
        "ajourhold_splitt": "KAN_SPLITTES",
        "dekningsgrad": "x"
    },
    ...
}
```


|Felt|Beskrivelse|
|:-|:-|
|må_ha_mor|Angir hvorvidt vegobjektene må være tilknyttet et morobjekt for å kunne eksistere:<br>`true` - Må være tilknyttet morobjekt<br>`false` - Behøver ikke å være tilknyttet morobjekt|
|sideposisjon_relevant|Angir om sideposisjon skal kunne være en del av vegobjektenes vegnettstilknytning:<br>`NEI` - Sideposisjon skal ikke registreres<br>`KAN` - Sideposisjon kan registreres<br>`MÅ` - Sideposisjon må registreres|
|kjørefelt_relevant|Angir om kjørefelt skal kunne være en del av vegobjektenes vegnettstilknytning:<br>`NEI` - Kjørefelt skal ikke registreres<br>`KAN` - Kjørefelt kan registreres<br>`MÅ` - Kjørefelt må registreres|
|tidsrom_relevant|Angir om vegobjektene normalt har en gyldighetsperiode på operativt vegnett:<br>`true` - Tidsromrelevant<br>`false` - Ikke tidsromrelevant|
|overlapp|Angir om det kan være to eller flere forekomster av vegobjekttypen med overlappende vegnettstilknytning, inkludert sideposisjon og felt:<br>`true` - Overlapp tillatt<br>`false` - Overlapp ikke tillatt|
|avledet|Angir om vegobjekttypen i sin helhet er avledet, og genereres automatisk:<br>`true` - Avledet<br>`false` - Er ikke avledet|
|dekningsgrad|Angir om eksisterende objekter skal bli automatisk splittet når de overlapper med nye objekter:<br>`true` - Skal splittes<br>`false` - Skal ikke splittes|
|ajourhold_i|Knyttet til vegnettsopdateringer. Angir om vegobjektene skal overleve ved et fysisk tiltak på vegen som gir I-status:<br>`OVERLEVER_IKKE` - Overlever ikke<br>`OVERLEVER` - Overlever<br>`IKKE_TATT_STILLING` - Ikke tatt stilling|
|ajourhold_splitt|Knyttet til vegnettsoppdatering. Angir om vegobjektene kan splittes uten at det får konsekvenser for egenskapsverdiene:<br>`KAN_IKKE_SPLITTES` - Kan ikke splittes<br>`KAN_SPLITTES` - Kan splittes|

## Hent egenskapstype

Det er mulig å hente detaljert informasjon om en spesifikk egenskapstype.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/<vegobjekttype.id>/<egenskapstype.id>
```


Det vil bli returnert et komplett egenskapstypeobjekt.

### Eksempel

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/105/2021;
```


## Hent liste over enheter

På dette endepunktet listes alle enhetene fra Datakatalogen.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/enheter
```


```json
[
    {
        "id": 1,
        "navn": "Meter",
        "kortnavn": "m"
    },
    {
        "id": 2,
        "navn": "Desimeter",
        "kortnavn": "dm"
    },
    {
        "id": 3,
        "navn": "Centimeter",
        "kortnavn": "cm"
    },
    ...
]
```


|Felt|Beskrivelse|
|:-|:-|
|id|Angir enhetens unike id.|
|navn|Angir enhetens navn.|
|kortnavn|Angir enhetens forkortelse.|


## Hent liste over datatyper

På dette endepunktet listes alle mulige datatyper egenskapstypene kan ha.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/datatyper
```


```json
[
    {
        "id": 1,
        "navn": "Tekst",
        "kortnavn": "T",
        "beskrivelse": "DatatypebenyttesforETsomskalinneholdetekst.Måangifeltlengde.Kanangimaskeogdefaultverdi.NVDB: Nf_StringAttributeType"
    },
    {
        "id": 2,
        "navn": "Tall",
        "kortnavn": "N",
        "beskrivelse": "DatatypebenyttesforETsomskalinneholdetall.Benyttesbådeomheltallogdesimaltall.Detmåangisfeltlengdeogantalldesimaler.Bådesifferforanogbakkommasamtselvekommaetinngårifeltlengde.Kanangimaksverdi,minverdi,defaultverdiogmaske."
    },
    {
        "id": 8,
        "navn": "Dato",
        "kortnavn": "D",
        "beskrivelse": "DatatypebenyttesforETsomskalinneholdeÅr/Måned/Dag.Skalhafeltlengde=8\.Måoppgimaske.Kanoppgimaksverdi,
        minverdiogdefaultverdi."
    },
    ...
]
```


|Felt|Beskrivelse|
|:-|:-|
|id|Datatypens id|
|datatype|Datatypens navn:<br>`Tekst` - Eksempel: _Strindheimtunnelen_<br>`Tall` - Eksempel: _86_<br>`Flyttall` - Eksempel: _86.0_<br>`Kortdato` - Eksempel: Måned-dag, _01-01_<br>`Dato` - Eksempel: År-Måned-dag, _2015-01-01_<br>`Klokkeslett` - Eksempel: _13:37_<br>`Geometri` - Geometrirepresentasjon<br>`Struktur` - Verdi sammensatt av flere verdier<br>`Binærobjekt` - Eksempel: Et dokument eller et bilde<br>`Boolean` - _True_ eller _false_<br>`Liste` - En liste av objekter|
|kortnavn|Forkortet navn|
|beskrivelse|Tekstlig beskrivelse|

## Hent liste over kategorier

På dette endepunktet listes alle kategoriene en vegobjekttype kan være i.

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegobjekttyper/kategorier
```

```json
[
    {
        "id" : 38,
        "navn" : "Alle",
        "kortnavn" : "alle",
        "sorteringsnummer" : 1,
        "beskrivelse" : "Inneholder ale vegobjekttyper",
        "startdato" : "2012-05-22"
    }, {
        "id" : 43,
        "navn" : "Vegreferansesystem",
        "sorteringsnummer" : 3,
        "beskrivelse" : "Inneholder vegobjekttyper som har med vegreferansesystemet å gjøre",
        "startdato" : "2012-05-22"
    }, {
        "id" : 1,
        "navn" : "Vegsystem",
        "kortnavn" : "vgsy",
        "sorteringsnummer" : 5,
        "beskrivelse" : "Inneholder vegobjekttyper som har med selve vegsystemet å gjøre, eksempel  kan være kryss, vegstrekning, plasser, avkjørsler etc.",
        "startdato" : "2012-05-22"
    },
    ...
]
```

|Felt|Beskrivelse|
|:-|:-|
|id|Kategoriens id|
|navn|Kategoriens navn|
|kortnavn|Forkortet navn|
|sorteringsnummer|Sorteringsnummer fra datakatalogen|
|beskrivelse|Tekstlig beskrivelse|
|startdato|Når gjelder kategorien fra|
