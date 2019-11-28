# Segmentering og metrering

### Segmentering
I API Les har vi komponenten NVDBIND som står for lesing fra NVDB-databasen og legger det inn i Solr-indeksen. Når vegnettet behandles segmenteres det basert på vegsystemreferansen, samt riksvegrute og kontraktområde. Slik forholder hvret vegnettsegment seg bare til en lenke, et vegsystemobjekt og et strekning/kryssdel/sideanleggsdel-objekt, men flere riksvegruter og kontraktområder siden disse overlapper. Vegsystemreferanse med start- og sluttmeter beregnes for hvert segment (se eget avsnitt). Vegnettssegmentene brukes igjen for å segmentere vegobjektene slik at de blir lett filtrerbare og får vegsystemreferanse med meterverdier.

Segmentering i detaljer
Før NVDBIND begynner å lese inn vegnettet legger den alle objekttypene som inngår i segmenteringsprosessen i en cache (en H2-database). Deretter leses veglenkesekvensene inn bolkvis, for å segmentere en og en veglenke på hver veglenkesekvensene. For hver bolk hentes de overlappende segmenteringsobjektene inn i minnet fra cachen, slik at de er lett tilgjengelige ved segmentering av veglenkene. Først segmenteres veglenka og alle segmenteringsobjektene på tid, og hvert tidssegment får med seg de objektene som var gyldige i det tidsrommet. Deretter segmenteres hver av tidssegmentene i rom.

I illustrasjonen over ser vi hvordan vegenke, vegsystem (915)

###Metrering
