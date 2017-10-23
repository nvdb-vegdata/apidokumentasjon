---
title: Egenskapsfilter
category: Parameter
---

Ved hjelp av et egenskapsfilter er det mulig å søke frem vegobjekter etter hvilke egenskaper de har.

## Angivelse av filter

Parameteren `egenskap` kan benyttes ved søk etter vegobjekter. Filteret angis av en streng, som består av egenskapstype, operator og verdi.

```
?egenskap="<egenskapstype><operator><verdi>"
```


### Egenskapstype

Bruk datakatalogen for å finne vegobjektenes egenskapstyper.

For øyeblikket støttes _kun_ `type-id` for å angi egenskapstype.

### Operator

Det er støtte for følgende operatorer:

<ul>
<li><b>=</b> - lik
<li><b>!=</b> - ulik
<li><b><</b> - større enn
<li><b>></b> - mindre enn,
<li><b>>=</b> - større enn, eller lik
<li><b><=</b> - mindre enn, eller lik
</ul>

Større enn- og mindre enn-operatorene er kun relevant for egenskapstyper av type tall eller dato.

### Verdi

Verdien skal være i henhold til egenskapstypens datatype, og er som oftest en tekst eller et tall. Tekst og tidspunkt må markeres med enkle anførselstegn.

For egenskapstyper med forhåndsdefinerte verdier, er det for øyeblikket kun mulig å bruke verdiens `id`.

Bruk `null` som verdi for å finne objekter som har, eller ikke har, verdi på bestemte egenskapstyper.

Wildcard `*` kan benyttes for tekst og datoer.

### Kombinasjon av flere egenskapsfiltre

Syntaksen for spørrespråket støtter bruk av paranteser og AND/OR-sammenhenger.

## Eksempler

### Bomstasjoner med takst større eller lik 20 kr

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/45?egenskap="1820>=20"
```


«1820» er id til egenskapstypen «Takst liten bil»

### Bomstasjoner med takst lik 20 eller 50 kr

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/45?egenskap="1820=20 OR 1820=50"
```


### Bomstasjoner med takst lik 20 eller 50 kr og eier lik Stat

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/45?egenskap="(1820=20 OR 1820=50) AND 7992=10258"
```


«7992» er id til egenskapstypen «Eier».

«10258» er id til den forhåndsdefinerte verdien «Stat».

### Tunneler med navn som starter med «Gudvang»

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="5225='Gudvang*'"
```


«5225» er id til egenskapstypen «Navn».

### Tunneler uten verdi på sykkelforbud

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="9518=null"
```


«9518» er id til egenskapstypen «Sykkelforbud».

### Tunneler med verdi på sykkelforbud

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="9518!=null"
```


«9518» er id til egenskapstypen «Sykkelforbud».

### Antall trafikkulykker som har skjedd etter 2015-01-01

Egenskapsfilteret kan også kombineres med statistikk-endepunktet for vegobjekter.

```
https:/www.vegvesen.no/nvdb/api/v2/vegobjekter/570/statistikk?egenskap="5055>'2015-01-01'"
```


«5055» er id til egenskapstypen «Ulykkesdato».

### Antall trafikkulykker som har skjedd klokken 12:00

Egenskapsfilteret støtter også filtrering på klokkeslett som heltall.

```
https://www.utv.vegvesen.no/nvdb/api/v2/vegobjekter/570/statistikk?egenskap="5056=1200"
```


«5056» er id til egenskapstypen «Ulykkestidspunkt».
