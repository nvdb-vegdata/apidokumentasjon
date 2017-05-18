---
layout: page
title: Vegreferanse
---

Vegreferanse er et lineært referansesystem som brukes til stedfesting av vegobjekter og administrativ klassifisering av vegnettet.

For vegobjekter kan vegreferanse returneres som den av del responsen, og vegreferansen kan benyttes som et avgrensende områdefilter.

## Vegreferanse i respons

Følgende objekt returneres som en del av vegobjekter, og som respons i andre endepunkter.

```json
{
    "vegreferanse": {
        "fylke": 16,
        "kommune": 0,
        "kategori": "E",
        "status": "V",
        "nummer": 6,
        "hp": 1,
        "meter": 2024,
        "kortform": "1600 Ev6 hp1 m2024"
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
<td>fylke</td>
<td>Tosifret fylkesnummer.</td>
</tr>
<tr>
<td>kommune</td>
<td>Tosifret kommunenummer.  
For europa-, riks- og fylkesveger er kommunenummeret alltid 0.</td>
</tr>
<tr>
<td>kategori</td>
<td>Angir vegkategori.
<ul>
<li><b>E</b> - Europaveg<>
<li><b>R</b> - Riksveg<>
<li><b>F</b> - Fylkesveg<>
<li><b>K</b> - Kommunal veg<>
<li><b>P</b> - Privat veg<>
<li><b>S</b> - Skogsbilveg<>
</dl>
</td>
</tr>
<tr>
<td>status</td>
<td>Angir vegstatus.
<ul>
<li><b>V</b> - Eksisterende veg<>
<li><b>W</b> - Midlertidig veg<>
<li><b>T</b> - Midlertidig status bilveg<>
<li><b>S</b> - Eksisterende ferjestrekning<>
<li><b>G</b> - Gang-/sykkelveg<>
<li><b>U</b> - Midlertidig status gang-/sykkelveg<>
<li><b>B</b> - Beredskapsveg<>
<li><b>M</b> - Serviceveg<>
<li><b>X</b> - Rømningstunnel<>
<li><b>A</b> - Anleggsveg<>
<li><b>H</b> - Gang-/sykkelveg anlegg<>
<li><b>P</b> - Vedtatt veg<>
<li><b>E</b> - Vedtatt ferjestrekning<>
<li><b>Q</b> - Vedtatt gang-/sykkelveg<>
</dl>
</td>
</tr>
<tr>
<td>nummer</td>
<td>Angir vegnummer.</td>
</tr>
<tr>
<td>hp</td>
<td>Angir parsell.
<ul>
<li><b>1–49</b> - Hovedparseller<>
<li><b>50–69</b> - Armer<>
<li><b>70–199</b> - Ramper<>
<li><b>400–599</b> - Rundkjøringer<>
<li><b>600–699</b> - Skjøteparseller<>
<li><b>800–998</b> - Trafikklommer, rasteplasser<>
</dl>
</td>
</tr>
<tr>
<td>meter</td>
<td>Angir posisjon i hele meter, regnet fra parsellens start.</td>
</tr>
<tr>
<td>kortform</td>
<td>Sammenslått versjon av vegreferansen.</td>
</tr>
</tbody>
</table>

For _strekninger_ returneres `fra_meter` og `til_meter` i stedet for `meter`.

Dersom et vegobjekt er stedfestet på mer enn én vegstrekning, returneres det flere vegreferanseobjekter.

## Vegreferanse som parameter

Flere av endepunktene aksepterer en vegreferanse som parameter. Vegreferansen kan angis som et punkt eller en strekning.

For å gjøre presise avgrensninger av hvilket vegnettet det skal hentes vegobjekter innenfor, er det mulig å angi deler av vegreferanse på ulike måter.

<table>
<thead>
<tr>
<th>Eksempel</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>E</td>
<td>Kun vegkategori.</td>
</tr>
<tr>
<td>?v</td>
<td>Kun vegstatus.</td>
</tr>
<tr>
<td>Ev</td>
<td>Vegkategori og vegstatus.</td>
</tr>
<tr>
<td>E6</td>
<td>Vegkategori og vegnummer.</td>
</tr>
<tr>
<td>Ev6</td>
<td>Vegkategori, vegstatus og vegnummer.</td>
</tr>
<tr>
<td>Ev6hp1</td>
<td>Angivelse av hovedparsell.</td>
</tr>
<tr>
<td>Ev6hp1-hp4</td>
<td>Angivelse av flere hovedparseller.</td>
</tr>
<tr>
<td>Ev6hp1m100</td>
<td>Angivelse av et punkt.</td>
</tr>
<tr>
<td>Ev6hp1m100-200</td>
<td>Angivelse av en strekning.</td>
</tr>
<tr>
<td>Ev6hp1m100-hp2m200</td>
<td>Angivelse av strekning over flere hovedparseller.</td>
</tr>
</tbody>
</table>

Parameteren er case-insensitiv, og mellomrom fjernes automatisk.

## Vegreferanse som unik nøkkel

Vegnummer for FKPS-veger er ikke unike. Fylkesveg 950 finnes for eksempel både i Nordland, Sør-Trøndelag og Vestfold, og du finner kommunalveg 1640 flere steder i landet.

Hovedparseller er heller ikke unike, og strekningen Ev6 hp1 befinner seg i hele 10 ulike fylker.

For å angi et unikt punkt ved å bruke vegreferanse, må derfor fylkes- og kommunenummer angis.

Eksempel: `1600Ev6hp1m2024`

Endepunktet [/veg](#/get/veg) støtter kun vegreferanser som angis på denne måten.

## Mer informasjon

For utfyllende informasjon om vegreferansen, se [Håndbok V830: Nasjonalt vegreferansesystem](http://www.vegvesen.no/_attachment/61505).
