---
title: Status
---

# Oppdatert API-dokumentasjon for versjon 3

Bruk heller dokumentasjon for versjon 3 av NVDB api https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

Tjeneste for å hente ulike statusparametere om APIet.

## Hent status

```
GET https://nvdbapiles-v2.atlas.vegvesen.no/status
```

```json
{
    "datagrunnlag": {
        "sist_oppdatert": "2015-01-14T12:52:18+01:00"
    },
    "datakatalog": {
        "id": 706,
        "dato": "2014-11-28",
        "versjon": "2.01"
    }
}
```

| Felt | beskrivelse |
|:--------|:-------:|
datagrunnlag.sist_oppdatert | Angir når datagrunnlaget sist ble hentet fra NVDB-databasen. |
datakatalog.id | Angir id til aktiv datakatalog-versjon. |
datakatalog.versjon | Angir versjonsnummer til aktiv datakatalog-versjon. |
datakatalog.dato | Angir når den aktive versjonen av datakatalogen ble gyldig. |
