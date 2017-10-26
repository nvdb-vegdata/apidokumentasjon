---
title: Responsrevisjoner
order: 4
---

Tilgjengelige responsrevisjoner

## Revisjon 0
* Geometri har tre koordinater, men har ikke `Z`, `LINESTRING (1 2 3)`. 

## Revisjon 1
* Geometri med tre koordinater har `Z`, `LINESTRING Z (1 2 3)`.
* Tekst for om et attributt er påkrevd endret fra `PÅKREVD` til `PÅKREVD_IKKE_ABSOLUTT`.
* `metadata.antall` fjernes fordi den ikke er pålitelig.

## Revisjon 2
* Format for `objekt.metadata.lastmodified` endres fra `yyyy-MM-dd HH:mm:ss` til `yyyy-MM-ddTHH:mm:ss`
