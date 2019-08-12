---
title: Lokasjonsfilter
category: Parameter
---

Ved hjelp av områdefilter er det mulig å velge hvilke områder det skal søkes innenfor.

## Parametere

For de fleste parametere skal områdenes _nummer_ angis som verdi.

Alle områder, inkludert navn og nummer, er tilgjengelig i [område-endepunktet](../endepunkt/omrader.md).

### Region

Velg én eller flere regioner ved å angi regionenes nummer.

```
?region=1
?region=1,2
?region=1&region=2
```


### Fylke

Velg én eller flere fylke ved å angi fylkenes nummer.

```
?fylke=16
?fylke=16,17
?fylke=16&fylke=17
```


### Vegavdeling

Velg én eller flere vegavdelingenes ved å angi vegavdelingenes nummer.

```
?vegavdeling=4
?vegavdeling=3,4
?vegavdeling=3&vegavdeling=4
```


### Kommune

Velg én eller flere kommuner ved å angi kommunenes nummer.

```
?kommune=5001
?kommune=5001,5002
?kommune=5001&kommune=5002
```


### Riksvegrute

Velg én eller flere riksvegruter ved å angi riksvegrutenes navn og periode, atskilt med et mellomrom.

```
?riksvegrute="RUTE2A 2014-2023"
?riksvegrute="RUTE2A 2014-2023","3 2006-2009"
?riksvegrute="RUTE2A 2014-2023"&riksvegrute="3 2006-2009"
```


**NB! Riksvegrute-parameteren kan ikke angis for vegnett.**

### Kontraktsområde

Velg én eller flere kontraktsområder ved å angi kontraktsområdenes navn.

```
?kontraktsomrade="1538 Indre Romsdal - Tunnelrenhold 2014-2018"
?kontraktsomrade="1538 Indre Romsdal - Tunnelrenhold 2014-2018", "2003 NORDKAPP 2011-2016"
?kontraktsomrade="1538 Indre Romsdal - Tunnelrenhold 2014-2018"&kontraktsomrade="2003 NORDKAPP 2011-2016"
```


**NB! Kontraktsområde-parameteren kan ikke angis for vegnett.**

### Vegreferanse

Velg én eller flere vegreferanser. Les [dokumentasjonen av vegreferanse](../verdi/vegreferanse.md) for en oversikt over hvordan en vegreferanse kan formuleres.

```
?vegreferanse=Ev6
?vegreferanse=E,R,F
?vegreferanse=E&vegreferanse=R&vegreferanse=F
```


### Veglenke

Velg én eller flere veglenker. Les [dokumentasjonen av veglenke](../verdi/veglenke.md) for en oversikt over hvordan en veglenke kan oppgis.

```
?veglenke=1337
?veglenke=1337,0.123-0.456@1226
```


### Kartutsnitt

Velg et rektangulært karutsnitt det skal søkes innenfor. Les [dokumentasjonen av geometri](../verdi/geometri.md) for en oversikt over hvordan et kartutsnitt kan oppgis.

```
?kartutsnitt=5.159,60.211,5.441,60.333&srid=4326
```


## Kombinasjoner

*   Når det angis flere verdier på samme områdetype, settes verdiene sammen med en ELLER-operator.
*   Kommune, fylke og region settes sammen med en ELLER-operator.
*   Kartutsnitt, kontraktsområde, riksvegrute, og vegreferanse legges til søket med en OG-operator.
*   Veglenke kan ikke kombineres med andre områdefilter.
