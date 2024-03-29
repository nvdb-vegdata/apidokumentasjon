---
title: Paginering
category: Parameter
---

# Oppdatert API-dokumentasjon for versjon 3
Bruk heller dokumentasjon for versjon 3 av NVDB api [https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon](https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon)

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

Spørringer mot NVDB API kan potensielt returnere et stort antall objekter. For å begrense belastningen på APIet, og samtidig unngå store responser, legges det opp til at brukere benytter paginering til å laste ned store resultatsett.

## Parametere

| Navn | Verdi | Beskrivelse |
| --- | --- | --- |
| antall | heltall | Angir hvor mange objekter som skal returneres. | 
| start | tekst | Angir markør for hvilke objekter som skal returneres. |


Øvre grense for `antall` er avhengig av størrelse på respons, og vil kunne variere fra endepunkt til endepunkt. Dersom det angis en verdi for antall som overskrider maksimum, vil maksimumsverdien benyttes.

`start`-markøren produseres automatisk av APIet, og kan ikke utledes.

## Eksempel

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/vegnett/lenker?antall=5
```

```json
{
    "objekter": [
        ...
    ],
    "metadata": {
        "returnert": 5,
        "neste": {
            "start": "AoEpMTAwMTk1Nnw3",
            "href": "https://nvdbapiles-v2.atlas.vegvesen.no/vegnett/lenker?antall=5&start=AoEpMTAwMTk1Nnw3"
        }
    }
}
```

Spørringer etter vegobjekter og vegnett vil inneholde en metadata-konvolutt, som forteller hvor mange objekter som er hentet, og gir startmarkør og URL for neste side av resultatsettet.

På grunn av tekniske begrensninger er det nå kun mulig å bevege seg fremover med lenkene. Dersom en klient vil traversere bakover må den huske URLene den har traversert.
