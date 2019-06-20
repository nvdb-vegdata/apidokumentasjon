

# Vegsystemreferanse
Vegsystemreferansen er erstatning for Vegreferanse (vegobjekttype 532). 
Vegsystemreferansen er satt sammen av vegobjekttypene Vegsystem(915), Strekning(916), Kryssystem(917), Kryssdel(918), Sideanlegg(919) og Sideanleggsdel(920).
Meterverdier i en vegsystemreferanse telles fra starten delstrekningen.



Vegsystem + Strekning:
- Vegkategori
  * <b>E</b> - Europaveg
  * <b>R</b> - Riksveg
  * <b>F</b> - Fylkesveg
  * <b>K</b> - Kommunal veg
  * <b>P</b> - Privat veg
  * <b>S</b> - Skogsbilveg
- Fase  
  * <b>V</b> - Eksisterende
  * <b>A</b> - Under bygging
  * <b>P</b> - Planlagt
  * <b>F</b> - Fiktiv
- Vegnummer    (Eks:  6)
- [Strekningsnummer]     (Eks:  S42)
- [Delstrekningsnummer]  (Eks: D11)
- [Meterverdi]  eller  [Meterframeter - tilmeter]  (Eks: M0-132)


<br>         
         
Kryssystem:
- [KryssSystemnummer]    (Eks:   KS1001)  
- [KryssDelnummer  [-   Kryssdelnummer]            (Eks:  KD3-4)  <br>
- [Meterverdi]  eller  [Meterframeter - tilmeter]  (Eks: M0-132)
  

<br>

Sideanlegg:
- [SideAnleggnummer]    (Eks: SA3048) 
- [Metermeterverdi for sideanlegg  (Eks: M312)                                              
- [SideanleggsDelnummer  [- SideanleggsDelnummer]


<br>
  
## Eksempler på vegsystemreferanser:

-  ?vegsystemreferanse=EV6  
   Kategori Europaveg, fase Veg, vegnummer 6
    
-  ?vegsystemreferanse=FV42  
   Kategori  Fylkesveg, fase Veg, vegnummer 42

-  ?vegsystemreferanse=FV911S1-2          
   Kategori  Fylkesveg, fase Vef, Vegnummer 911, Strekning 1-2
   
-  ?vegsystemreferanse=EV6S54D1M30435SD1-10         
   Kategori Europaveg, fase Veg, vegnummer 6, Strekning 54, Delstrekning1,  Pos for sideanlegg meter 30435, SideanleggsDel 1 - 10
 
-  ?vegsystemreferanse=EV18S42D1SA1039SD2-3    <br>
   Sideanlegg: EV 18 Strekning 42, Delstrekning 21, SideAnleggnummer 1039, SideanleggsDel 2 - 3
   
-  ?vegsystemreferanse=EV18S41D1M2403KD3M0-35
   Kryss: EV18, Strekning 41, Delstrekning 1, posisjon sideanlegg Meter 2403, KryssDel 3, meter 0 - 35   
 
  

## Kortform

I resultatene av søk på vegnett / vegobjekter skrives det ut en kortform av vegsystemreferansen.
På kortform oppgis det kun i hele meter og angivelse av kryss og sideanlegg oppgis det meterposisjon for dette (ikke sideanlegg- eller kryssystem-nummer).

Formatet på kortform er identisk med det formatet man angir ved søk på vegsystemreferanse.

Eksempler på kortformer:
* Strekning: FV911 S2D10 m0-3      
* Kryssystem: EV6 S1D1 m4230 KD1 m0-10
* Sideanlegg: EV18 S42D1 m2806 SD3 m0-32  





