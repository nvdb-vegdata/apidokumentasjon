---
layout: page
title: Veglenke
---

Vegleker er an av bestanddelene i NVDBs topologisk vegnettverk.

For vegobjekter kan veglenkeposisjoner returneres som den av del responsen, og veglenker kan benyttes som et avgrensende områdefilter.

## Stedfesting

Vegobjekters stedfesting til det topologiske vegnettverket angis ved å oppgi en relativ posisjon på en spesifikk veglenke, og samtidig angi informasjon om felt, sideposisjon og retning.

### Eksempel: Punkt

```json
{
    "stedfesting": {
        "veglenkeid": 320689,
        "posisjon": 0.25899,
        "sideposisjon": "H",
        "felt": "NULL",
        "retning": "MED",
        "kortform": "0.25899@320689"
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
<td>id</td>
<td>Angir veglenkens unike id.</td>
</tr>
<tr>
<td>posisjon</td>
<td>Angir relativ posisjon på veglenken. Flyttall mellom 0 og 1.</td>
</tr>
<tr>
<td>sideposisjon</td>
<td>
Angir posisjon i forhold til vegens senterlinje:
<ul>
<li><b>V</b> - Til venstre
<li><b>H</b> - Til høyre
<li><b>M</b> - I midten av vegen
<li><b>K</b> - Krysser vegen
<li><b>MV</b> - Til venstre på midtrabatt
<li><b>MH</b> - Til høyre på midtrabatt
<li><b>VT</b> - I avkjørsel til venstre
<li><b>HT</b> - I avkjørsel til høyre
<li><b>R0</b> - På øy i rundkjøring
<li><b>L</b> - Langs vegen
</ul>
</td>
</tr>
<tr>
<td>felt</td>
<td>Angir eventuell stedfesting til felt</td>
</tr>
<tr>
<td>retning</td>
<td>Angir stedfesting i forhold til veglenkens retning.
<ul>
<li><b>MED</b> - Stedfesting med veglenken
<li><b>MOT</b> - Stedfesting mot veglenken
</ul>
</td>
</tr>
<tr>
<td>kortform</td>
<td>Sammenslått versjon av veglenkeposisjonen.</td>
</tr>
</tbody>
</table>

### Eksempel: Strekning

For strekningsobjekter angis det to posisjoner på en veglenke.

```json
{
    "stedfesting": {
        "veglenkeid": 1337,
        "fra_posisjon": 0.123,
        "til_posisjon": 0.456,
        "felt": "1#2",
        "retning": "MED",
        "kortform": "0.123-0.456@1337"
    }
}
```

Dersom et vegobjekt er stedfestet på mer enn én veglenke, returneres det flere veglenkeposisjoner.

## Veglenkeposisjon

I noen tilfeller det relevant å oppgi posisjon på en veglenke, uten informasjon om sideposisjon og felt.

```json
{
    "veglenke": {
        "id": 72811,
        "posisjon": 0.21279373,
        "kortform": "0.21279373@72811"
    }
}
```

Flere av endepunktene aksepterer én eller flere veglenker som parameter. Parameteren inneholder kun veglenkeid og veglenkeposisjon.

<table>
<thead>
<tr>
<th>Eksempel</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>1337</td>
<td>En hel veglenke.</td>
</tr>
<tr>
<td>0.123@1337</td>
<td>Punkt på veglenke.</td>
</tr>
<tr>
<td>0.123-0.456@1337</td>
<td>Strekning på veglenke.</td>
</tr>
</tbody>
</table>
