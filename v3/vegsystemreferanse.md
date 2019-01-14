

# Vegsystemreferanse


### parametre
* vegreferanse=vegreferansestreng
* arm=true / false    (ikke implementert)



Strekning:
- Vegkategori  (Europaveg, Fylkesveg, Privat ..)   (Eks: E)
- Fase          (Veg, Gangveg ..)                  (Eks: V)
- Vegnummer    (Eks:  6)
- [Trafikantgruppe]  (K = kjørnde, G = gående)
- [Strekningsnummer]     (Eks:  S42)
- [Delstrekningsnummer]  (Eks: D11)
- [Meterverdi]  eller  [Meterframeter - tilmeter]  <br>
  (Eks: M0-132)


<br>         
         
Kryssystem:
- Vegkategori  (Europaveg, Fylkesveg, Privat ..)   (Eks: E)
- Fase          (Veg, Gangveg ..)                  (Eks: V)
- Vegnummer    (Eks:  6)
- [Strekningsnummer]     (Eks:  S42)
- [Delstrekningsnummer]  (Eks: D11)
- [KryssSystemnummer]    (Eks:   KS1001)  
- [KryssDelnummer  [-   Kryssdelnummer]   <br>
  (Eks:  KD3)  <br>
  (Eks:  KD3-4)  <br>
- [Meterverdi]  eller  [Meterframeter - tilmeter]  <br>
  (Eks: M0-132)
  

<br>

Sideanlegg:
- Vegkategori  (Europaveg, Fylkesveg, Privat ..)   (Eks: E)
- Fase          (Veg, Gangveg ..)                  (Eks: V)
- Vegnummer    (Eks:  6)
- [Strekningsnummer]     (Eks:  S42)
- [Delstrekningsnummer]  (Eks: D11)
- [SideAnleggnummer]    (Eks: SA3048) 
- [Metermeterverdi for sideanlegg  (Eks: M312)                                              
- [SideanleggsDelnummer  [- SideanleggsDelnummer]  
  (Eks:  SD3)   <br>
  (Eks:  SD3-4)  <br>

  

<br>
  
## Eksempler på vegsystemreferanser:

-  ?vegsystemreferanse=EV6
   Kategori Europaveg, fase Veg, vegnummer 6
    
-  ?vegsystemreferanse=FV42
   Kategori  Fylkesveg, fase Veg, vegnummer 42

-  ?vegsystemreferanse=FV911S1-2          
   Kategori  Fylkesveg, fase Vef, Vegnummer 911, Strekning 1-2
   
-  ?vegsystemreferanse=EV6S54D1M30435SD1-10        
   Kategori Europaveg, fase Veg, vegnummer 6, Strekning 54, Delstrekning1,  Pos for sideanlegg Meter 30435, SideanleggsDel 1 - 10
 
-  ?vegsystemreferanse=EV18S42D1SA1039SD2-3    
   Sideanlegg: EV 18 Strekning 42, Delstrekning 21, SideAnleggnummer 1039, SideanleggsDel 2 - 3
 
  


