---
title: Endringer
category: Parameter
---

Etter et initielt uttak er gjort kan man polle for endringer/slettinger.

## Nye/oppdaterte objekter

For å finne nye/oppdaterte objekter kan du bruke områdefilter på samme måte som ved objektsøk.

**NB! Egenskapsfilteret støttes ikke.**

### Ekstra parametere

Selv om ingen av to tidsparameterene er obligatoriske må brukeren inkludere <emph>minst én</emph> av dem for å gjøre et gyldig søk.

| Felt | Format | Beskrivelse |
| --- | --- | --- |
| antall | nummer | Angir hvor mange objekter som skal returneres. Se [bruk](#/retningslinjer#Pagination) for hvordan paginering virker. |
| etter | [Tidsformat](#/tid) | Denne parameteren brukes til å definere siden <emph>når</emph> man vil finne endringer. Obligatorisk |
| kun_objekt | true/false | Dersom brukeren er interessert i å finne endringer kun blant egenskaper og assosiasjoner settes denne parameteren til true. Default: false |


### Eksempel

```
GET /vegobjekter/45/endringer
```

```json
{
    "endringer": [
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 12312354,
            "type": "NY"
        },
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 12312355,
            "type": "NY"
        },
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 12312358,
            "type": "SATT_HISTORISK"//Hersermanaltsåatobjekterharblittgjorthistorisk
        }
    ]
}
```

## Slettede objekter

Slettede objekter vil være fullstendig vasket vekk fra NVDB og ingen informasjon beholdes utenom hva id-en var før den ble slettet. **Dette betyr at verken område- eller egenskapsfilteret er støttet her.** Det går an å liste opp slettede objekter på følgende vis:

### Ekstra parametere

| Felt | Format |Beskrivelse | 
| --- | --- | --- |
| antall | nummer | Angir hvor mange objekter som skal returneres. Se [bruk](#/retningslinjer#Pagination) for hvordan paginering virker. |
| etter | [Tidsformat](#/tid) | Sett tidsbegrensing på søket. Obligatorisk |

### Eksempel

`GET /vegobjekter/45/slettinger?etter="2014-03-27"`

```
{
    "slettinger": [
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 12312354,
            "type": "SLETTING"
        },
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 24123564,
            "type": "SLETTING"
        },
        {
            "tidspunkt": "2015-05-27T05:00:00+02:00",
            "task_id": 124153355,
            "vegobjekt": 23155122,
            "type": "SLETTING"
        }
    ]
}
```
