# Relasjonsfilter

Ved hjelp av et relasjonsfilter er det mulig å søke frem vegobjekter som har relasjon til andre angitte vegobjekttyper.

## Angivelse av filter

Parameteren `relasjon` kan benyttes ved søk etter vegobjekter. Filteret angis ved å oppgi id til den vegobjekttypen det skal være en relasjon til.

```
?relasjon=<objekttypeid>
```


Bruk datakatalogen til å finne ut hvilke relasjoner som kan finnes mellom vegobjekttyper.

### Eksempel: Trafikkdeler med relasjon til rekkverk

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/172?overlapp=5
```


## Relasjonsfilter med egenskapsfilter

Relasjonsfilter kan kombineres med egenskapsfilter. Både for vegobjekttypen det spørres etter, og vegobjekttypen det være en relasjon til.

Egenskapsfilter til vegobjekttypen det skal være en relasjon til med, angis innenfor en parentes, rett etter vegobjektypeid.

```
?relasjon=<objekttypeid>(<egenskapsfilter>)
```


### Eksempel: Tunnelløp med høydebegrensning større enn 4,6 meter

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/67?relasjon=591("5277>4.6")
```


## Kombinasjon av flere relasjonsfiltre

Relasjonsfiltre kan kombineres ved å oppgi flere `relasjon`-parametere i samme spørring.

Relasjonsfiltre kombineres alltid med `AND`.

### Eksempel: Tunnelløp med både belysningspunkt og belysningsstrekning

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/67?relasjon=86&relasjon=87
```
