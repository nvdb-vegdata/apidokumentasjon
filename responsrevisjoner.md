---
title: Responsrevisjoner
order: 4
---

# Oppdatert API-dokumentasjon for versjon 3
Bruk heller dokumentasjon for versjon 3 av NVDB api [https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon](https://nvdbapiles-v3.atlas.vegvesen.no/dokumentasjon)

De sidene du besøker akkurat kan fungere godt for å få et overblikk over NVDB datamodell, men er utdatert på en del tekniske detaljer.

## Gammel dokumentasjon

Tilgjengelige responsrevisjoner

## Revisjon 0
* Geometri har tre koordinater, men har ikke `Z`, `LINESTRING (1 2 3)`. 

## Revisjon 1
* Geometri med tre koordinater har `Z`, `LINESTRING Z (1 2 3)`.
* Tekst for om et attributt er påkrevd endret fra `PÅKREVD` til `PÅKREVD_IKKE_ABSOLUTT`.
* `metadata.antall` fjernes fordi den ikke er pålitelig.

## Revisjon 2
* Format for `objekt.metadata.lastmodified` endres fra `yyyy-MM-dd HH:mm:ss` til `yyyy-MM-ddTHH:mm:ss`
* 3D-geometri hvor z-koordinat mangler bruker `-999999` som z-koordinat.
