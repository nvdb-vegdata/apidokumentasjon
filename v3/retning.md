# Retning på vegsystemreferanse

## Veglenkesekvenser
Veglenkesekvenser og de segmenterte veglenkesekvensene viser vegnettet slik det er, uten å snu hverken geometri, 
posisjon, noder eller lenkenes feltkoding. Der metreringsretning er motsatt av lenkeretning gjenspeiles dette i 
retningsbeskrivelsen for Vegsystemreferansen på det segmenterte vegnettet.

## Beregning av meterverdier
På det segmenterte vegnettet beregnes det meterverdier på strekninger, sideanleggsdeler og kryssdeler. 
Det er lengden på de enkelte lenkene i vegnettet som er grunnlaget for meterverdiene som beregnes. 
Der metreringsretning på Vegsystemreferansen er lik lenkeretning summeres meterverdier fra posisjon 0 → 1 fra 
stedfestingen til strekningen på lenkesekvensen. Dersom metreringsretning på Vegsystemreferansen er motsatt av 
lenkeretning summeres meterverdiene fra posisjon 1 → 0 fra stedfestingen til strekningen på lenkesekvensen. 
Dette gjør at meterverdi kan være større for posisjon 0 enn for posisjon 1 i stedfestingen av et 
strekningsobjekt(vegobjekttype 916) på en gitt veglenkesekvens, men for Vegsystemreferansen er meterverdien 
sammenhengende og stigende for strekning, kryssdel eller sideanleggsdel.

Eksempel på meter hvor strekning er stedfestet mot lenkeretning
![Segmentering]({{site.baseurl}}/assets/retning_meter.png)

Utdrag fra responsen til LES som viser hvordan eksempelet over vil se ut:

```xml
<startposisjon>0.0</startposisjon>

<sluttposisjon>0.3</sluttposisjon>
...
<fra_meter>0</fra_meter>
<til_meter>300</til_meter>
<retning>MOT</retning>
</strekning>
<kortform>RV25 S1D1 m0-300</kortform>
```



Et eksempel på hvordan retning påvirker meterverdier. Her er deler av strekningen stedfestet mot lenkeretningen, angitt med rødt. 
Meterverdiene følger metreringsretningen.
![Segmentering]({{site.baseurl}}/assets/metrering_klostergata.png)
