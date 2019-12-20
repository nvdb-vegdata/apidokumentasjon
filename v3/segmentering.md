# Segmentering og metrering

### Segmentering
I API Les har vi komponenten NVDBIND som står for lesing fra NVDB-databasen og legger det inn i Solr-indeksen. 
Når vegnettet behandles segmenteres det basert på vegsystemreferansen, samt riksvegrute og kontraktområde. 
Slik forholder hvert vegnettsegment seg bare til en lenke, et vegsystemobjekt og et strekning/kryssdel/sideanleggsdel-objekt, 
men flere riksvegruter og kontraktsområder siden disse overlapper. 
Vegsystemreferanse med start- og sluttmeter beregnes for hvert segment (se eget avsnitt). 
Vegnettssegmentene brukes igjen for å segmentere vegobjektene slik at de blir lett filtrerbare og får vegsystemreferanse med meterverdier.

![Segmentering]({{site.baseurl}}/assets/segmentering.png)

I illustrasjonen over ser vi hvordan veglenker, vegsystem(915) og strekning(916)/kryssdel(918)/sideanleggsdel(920)-objekter, 
kontraktsområder og riksvegruter fører til 5 segmenter med egenskapene som er lista opp i tabellen. 
I tillegg vises et vegobjekt (fartgrense). 
Alle vegobjekter segmenteres i sin tur basert på stedfestinga sin og vegnettssegmentene. 
Dette muliggjør de forskjellige filtrene som er tilgjengelige i API Les.

### Metrering
Meterverdier på vegnettet regnes ut basert på (del)strekning/kryssdel/sideanleggsdel (som vanligvis deles i flere objekter), 
men selve meterlengdeverdiene hentes ut fra veglenkene. 
Når en delstrekning er delt over flere objekter har de stigende sekvensnummer. 
Enkelt oppsummert kan man forklare det slik; Hvis man har et punkt på vegnettet (med strekning), 
må man finne (del-)strekningsobjektet på stedet, samt alle (del-)strekningsobjekter med lavere sekvensnummer. 
Så henter/regner man ut meterverdiene for stedfestingene helt fram til (del-)strekningsstedfestinga hvor punktet man 
ønsker meterverdi for befinner seg. Når man summerer lengdene fra veglenkene, må det klippes for stedfestingene til de 
forskjellige (del-)strekningsobjektene. Til slutt legger man til den siste stedfestingslengen klippet for posisjon.
