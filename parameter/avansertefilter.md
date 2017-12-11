---
title: Avanserte filtre
---
API-et kan utføre komplekse spørringer som filtrerer på relaterte objekter og objekter som overlapper hverandre. For å spesifisere spørringer med avansert funksjonalitet benyttes et enkelt spørrespråk. Dette spørrespråket er støttet i [https://www.vegvesen.no/nvdb/api/v2/vegobjekter](#/get/vegobjekter) endepunktet.

Avanserte spørringer må brukes dersom man vil utføre spørringer som involverer flere objekttyper. API-et støtter filtrering på objekter som overlapper hverandre:

_Alle **trafikkulykker** på strekninger med **fartsgrense** over 80 km/t_

I tillegg støttes filtrering på relaterte objekter (mor/datter relasjoner):

_Alle **trafikkulykker** med **ulykkesinvolert person** over 70 år_

Man kan også bruke overlapp og relasjoner i samme spørring:

_Alle **trafikkulykker** på strekninger med **fartsgrense** over 80 km/t og **ulykkesinvolert person** over 70 år_

Avanserte spørringer krever at brukeren av API-et har inngående kunnskaper om hvordan datakatalogen modellerer objekter i NVDB og hvordan objektene er relatert til hverandre via relasjoner og via stedfesning på vegnettet i NVDB. Datakatalog ID-er brukes som parametere på typer, egenskaper og enum verdier for å sikre at spørringer fortsatt er gyldige selv om objekttyper eller egenskaper endrer navn.

## Innhold

*   [Eksempler](#eksempler)
*   [Filtrering på egenskaper](#egenskaper)
*   [Filtrering på relasjoner](#relasjoner)
*   [Filtrering på objekter som er stedfestet på samme sted (overlapp)](#overlapp)
*   [API Parametere](#parametere)
*   [Syntaks](#syntaks)

## Eksempler

Her er noen eksempler på bruk av API-et og avansert filtrering. For detaljer og spesifikasjon av filtre se dokumentasjon under.

_Trafikkulykker med skadegrad "alvorlig skadet" på strekning med fartsgrense 80 km/t_

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/570?egenskap="egenskap(5074)=6429"  
&overlapp=105(egenskap(2021)=2738)"
```
Trafikkulykke har Datakatalog ID 570, egenskapen Skadegrad har egenskap ID 5074 og er av type enum der "Alvorlig skadet" har enum ID 6429\. _egenskapfilter_ filtrerer hovedobjektet (trafikkulykke), mens _overlappfilter_ filtrerer fartsgrense (ID 105) som er lokalisert på samme veglenke som trafikkulykken. Egenskapen fartsgrense har ID 2021 og 2738 er enum ID til 80 km/t.

_Tunneler på fylkesvei med høydebegrensning <4m_

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap=relasjon(67, relasjon(591, egenskap(5277)<4))&vegreferanse="F"
```

Tunneler (581) har Tunnelløp (67) som har en relasjon til Høydebegrensning (591) der egenskap "Skilta høyde" (5277) blir filtrert på mindre enn 4m. _vegreferanse_ filtrerer på fylkesvei (kategori "F").

## Filtrering på egenskaper

Filtrering på egenskaper gjøres ved bruk av funksjonen _egenskap_. Funksjonen tar egenskap ID som parameter og returnerer verdien til egenskapen for objektet. Eksempel på filtrering av bruer bygget etter år 2000:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/60?egenskap="egenskap(10278)>=2000"
```

Man kan også kombinere og filtrere på flere egenskaper ved å bruke operatorene AND og OR:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/60?egenskap="egenskap(10278)>=2000 AND egenskap(1313)<=100"
```

Her filtreres bruer etter byggeår (10278) og lengde (1313). Filtrering på egenskaper av type enum må gjøres med enum ID. Man kan f.eks. ikke filtrere Fartsgrense (105) ved å bruke `egenskap(2021)=80`. Man må bruke enum ID:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/105?egenskap="egenskap(2021)>=2738 AND egenskap(1313)<=100"
```

## Filtrering på relasjoner

Filtrering på egenskaper i relaterte objekter gjøres også i egenskapsfilteret. Objekter er relatert ved at de har relasjoner til andre objekter. Foreløpig støtter API-et kun filtrering på datter-objekter. Relaterte objekter filtreres ved bruk av funksjonen _relasjon_. Denne funksjonen tar en objekttype ID som første parameter, og et nytt egenskapsfilter som andre parameter. API-et finner selv ut hvilken relasjon/sammenheng ID som kobler sammen objekttypene.

Eksempel på bruk av _relasjon_ i egenskapsfilteret:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="relasjon(67, egenskap(1317)>2000"
```

Her filtreres det på Tunneler (581) som har Tunnelløp (67) med Lengde (1317) over 2 km. API-et finner at tunneler er har en datter relasjon med ID 710 til tunnelløp. Man kan også nøste relasjoner:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="relasjon(67, relasjon(591, egenskap(5277)<4))"
```
Her finner man tunneler med tunnelløp som har Høydebegrensning (591) under 4 meter. Filtrering med relasjoner kan kombineres med filtrering på egenskaper ved å bruke operatoren AND:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/581?egenskap="relasjon(67, egenskap(1317)>2000 AND relasjon(591, egenskap(5277)<4))"
```

## Filtrering på objekter som er stedfestet på samme sted (overlapp)

API-et kan også filtrere på objekter som er stedfestet på samme sted i vegnettet. Dette gjøres i _overlapp_-parameteren.

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


_overlapp_ trenger ikke inneholde egenskapsfilter. For å angi at alle objekter som overlapper med hovedobjektet skal returneres uten ytterlige filtrering:

```
https://www.vegvesen.no/nvdb/api/v2/vegobjekter/571?overlapp="105(egenskap(2021)=2738)"&overlapp=540
```


## API Parametere

I tillegg til de ordinære API parameterene på [https://www.vegvesen.no/nvdb/api/v2/vegobjekter](#/get/vegobjekter/) brukes følgende parameter.

<table>
<tbody>
<tr>
<td><em>overlapp</em></td>
<td>Filtrering på objekter som overlapper, tar et overlappfilter som parameter. F.eks. 105 eller 105(egenskap(2021)=2741)</td>
</tr>
</tbody>
</table>

_egenskaper_-parameteren er også utvidet til å støtte filtrering på relaterte objekter.

## Syntaks

Spørrestråket består av hovedsakelig to funksjoner med AND og OR mellom. Datakatalog ID-er må brukes som parametere da navn på typer og egenskaper kan endres.

<table>
<tbody>
<tr>
<td><em>egenskaper</em></td>
<td>
Filtrering på egenskaper, tar en egenskapstype ID som parameter.
<code class="highlighter-rouge">egenskap(2021) = 2738</code>
</td>
</tr>
<tr>
<td><em>relasjon</em></td>
<td>
Filtrering på datter objekter, første parameter er type ID til relatert objekt, andre argument er et nytt filter. Merk at OR er ikke støttet for relasjoner, kun AND.
<code class="highlighter-rouge">relasjon(581, egenskap(1234) = 1)</code>
</td>
</tr>
</tbody>
</table>

_egenskap_ funksjonen returnerer verdien til egenskapen, og kan brukes med operatorene under for å filtrere på egenskapsverdi. Operatorer er ikke tilgjengelig for _relasjon_ da den ikke returnerer en verdi.

<table>
<tbody>
<tr>
<td>= !=</td>
<td>lik/ulik</td>
</tr>
<tr>
<td>> >=</td>
<td>Større enn/større enn eller lik.  
Kan brukes på egenskaper av type heltall, desimaltall og strenger, men ikke for enum egenskaper.</td>
</tr>
<tr>
<td>< <=</td>
<td>Mindre enn/mindre enn eller lik.  
Kan brukes på egenskaper av type heltall, desimaltall og strenger, men ikke for enum egenskaper.</td>
</tr>
<tr>
<td>in</td>
<td>Brukes for å sjekke om egenskapen er en av verdiene spesifisert i en liste.  
Eksempel: <code class="highlighter-rouge">egenskap(2021) in [11576,2728,2726]</code></td>
</tr>
<tr>
<td>notin</td>
<td>Her ønsker du alle verdier for egenskapen som ikke er spesifisert i listen. 
Eksempel: <code class="highlighter-rouge">egenskap(2021) notin [11576,2728]</code></td>
</tr>
<tr>
<td>AND OR</td>
<td>Boolsk algebra, brukes mellom funksjoner. <code class="highlighter-rouge">egenskap(2021)=2738 OR egenskap(2021)=2741</code></td>
</tr>
</tbody>
</table>

Punktum må brukes i desimaltall. " eller ' må brukes for strenger.  
`313 3.14 "hello world"`

`null` kan brukes for å filtrere på om en egenskap har verdi eller ikke. `egenskap(2010) = null`

Spørrespråket støtter også bruk av parenteser. F.eks. Trafikkulykke på lørdag eller søndag med skadegrad "Alvorlig skadd": `(egenskap(5054)=6248 OR egenskap(5054)=6249) AND egenskap(5074)=6429)`
