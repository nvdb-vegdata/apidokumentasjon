
Ved hjelp av et overlappfilter er det mulig å søke frem vegobjekter som befinner seg på samme sted på vegnettet som andre angitte vegobjekttyper.

## Angivelse av filter

Parameteren `overlapp` kan benyttes ved søk etter vegobjekter. Filteret angis ved å oppgi id til den vegobjekttypen det skal overlappes med.

```
?overlapp=<objekttypeid>
```


### Eksempel: Trafikkulykker på samme sted som tunnelløp

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/570?overlapp=67
```


## Overlapp med egenskapsfilter

Overlappfilter kan kombineres med egenskapsfilter. Både for vegobjekttypen det spørres etter, og vegobjekttypen det overlappes med.

Egenskapsfilter til vegobjekttypen det skal overlappes med, angis innenfor en parentes, rett etter vegobjektypeid.

```
?overlapp=<objekttypeid>(<egenskapsfilter>)
```


### Eksempel: Trafikkulykker på samme sted som fartsgrense lik 80 km/t

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/570?overlapp=105(2021=2738)
```


### Eksempel: Trafikkulykker med alvorlig skaffe personer på samme sted som fartsgrense lik 80 km/t

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/570?egenskap="5074=6429"&overlapp=105(2021=2738)
```


## Kombinasjon av flere overlappfiltre

Overlappsfiltre kan kombineres ved å oppgi flere `overlapp`-parametere i samme spørring.

Overlappfiltre kombineres alltid med `AND`.

### Eksempel: Trafikkulykker med alvorlig skaffe personer på samme sted som et tunnelløp og fartsgrense lik 80 km/t

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/570?egenskap="5074=6429"&overlapp=105(2021=2738)&overlapp=67
```
