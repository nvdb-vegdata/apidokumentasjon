---
title: Geometri
---

Vegobjekter i NVDB har en geografisk stedfesting, som beskrives på en standardisert måte.

## Geometri i respons

Koordinater returneres som en del av responsen til vegobjekter i et eget geometri-objekt.

```json
{
    "geometri": {
        "wkt": "POINT (-9990.051804799827 6567043.160294403)",
        "srid": 32633,
        "egengeometri": true,
        "kvalitet": {
            "målemetode": 22,
            "nøyaktighet": 200,
            "synbarhet": null,
            "målemetodeHøyde": null,
            "nøyaktighetHøyde": -1,
            "datafangstdato": "1998-05-26"
        }
    }
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
<td>wkt</td>
<td>Geometri strukturert på <abbr title="Well-known text">WKT</abbr>-format.
Se: <a href="https://en.wikipedia.org/wiki/Well-known_text">Well Known Text</a>
</td>
</tr>
<tr>
<td>srid</td>
<td>Angir koordiantenes geografiske referansesystem.</td>
</tr>
<tr>
<td>egengeometri</td>
<td>Angir om geometrien er vegobjektets egengeometri, eller om geometrien er utledet fra vegnettes geometri.</td>
</tr>
<tr>
<td>kvalitet</td>
<td>Metadata om geometrien, i henhold til <a href="http://kartverket.no/geodataarbeid/Standarder/SOSI/"> SOSI-standarden</a>.</td>
</tr>
</tbody>
</table>

## Angivelse av geografisk referansesystem

Parameteren `srid` benyttes for å angi hvilket geografisk referansesystem returnerte koordianter skal være stedfestet i. Parameteren har følgende mulige verdier:

<table>
<thead>
<tr>
<th>Verdi</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>6173</td> 
<td>Tilsvarer koordinatsystemet UTM sone 33N med datum WGS 84 (EUREF1989UTM33) og høydereferanse NN1954.  
Mer informasjon: <a href="https://github.com/nvdb-vegdata/utviklerkonferanse-2018/blob/master/doc/epsg6173.md">EPSG:6163</a>
</td>
</tr>
<tr>
<td>4326</td>
<td>Tilsvarer koordinatsystemet WGS 84.  
Mer informasjon: <a href="http://spatialreference.org/ref/epsg/wgs-84/">EPSG:4326</a></td>
</tr>
<tr>
<td>utm33</td>
<td>Et alias for 6173.</td>
</tr>
<tr>
<td>wgs84</td>
<td>Et alias for 4326.</td>
</tr>
</tbody>
</table>

Koordinater lagres i UTM33 I NVDB-databasen, og er derfor standardvalg i APIet.

## Angivelse av kartutsnitt

Det er mulig å hente vegobjekter og vegnett innenfor et spesifikt kartutsnitt, ofte kalt _bounding box_.

Legg merke til at `srid`-parameteren både gjelder kartutsnitt og returnert geometri. Det er ikke mulig å angi kartutsnitt med et annet referansesystem enn det geometrien skal returneres i.

### Eksempel: UTM33

```
  ?kartutsnitt={Xmin, Ymin, Xmax, Ymax}&srid=32633
  ?kartutsnitt=-43991.2,6715654.7,-26539.2,6726862.5&srid=32633
```

### Eksempel: WGS84

```
    ?kartutsnitt={longitudeMin, latitudeMin, longitudeMax, latitudeMax}&srid=4326
    ?kartutsnitt=5.159,60.211,5.441,60.333&srid=4326
```

## Tredimensjonale koordinater

Geometrien som returneres _kan_ inneholde høydeverdi. Høydedatum for disse er **NN54**
3D Geometrier prefikses med Z ihht WKT spesifikasjonen, for eksempel 'POINT Z(...), 'MULTILINESTRING Z(...)'
