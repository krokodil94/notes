

### MPPT – Maximum Power Point Tracking




Max DC Input Voltage (Vmax ali Voc meja)
To je absolutna varnostna meja, ki je ne smeš preseči niti za milivolt.  Pozimi pri nizkih temperaturah napetost niza Voc naraste. Če niz panelov v teoriji daje 950V pri 25 stopinjih, bo pozimi pri mrazu zlahka presegel 1000V in uničil vhodno stopnjo inverterja.

Težava: Več vrhov (Globalni vs. Lokalni MPP)

V primeru delnega zasenčenja se I-V krivulja popači in dobi več "grbin". 
- Lokalni MPP: "Lažni" vrh, kjer se enostaven P&O algoritem lahko ustavi, misleč da je na vrhu.
- Globalni MPP: Dejanska točka največje moči celotnega niza.
- Sodobni inverterji imajo funkcijo "Global Scan" ali "Shade Fix", ki vsakih nekaj minut preveri celotno krivuljo, da se prepriča, ali ni kje drugje še višji vrh.

Pri načrtovanju vedno poskrbi, da je napetost niza v vročem poletju (najnižja napetost) še vedno znotraj MPPT razpona, hkrati pa, da napetost v najhladnejši zimi ne preseže Max DC napetosti inverterja.

## 7. Stringing – dimenzioniranje
To so tri ključne enačbe, ki ločijo varno in učinkovito napravo od tiste, ki se bo bodisi pokvarila (previsoka napetost), ali pa se poleti sploh ne bo vklopila (prenizka napetost).
  - **Max string V** = Voc (STC) × koef. temp. (min. temp.) × N modulov < Vmax inverterja
  To je varnostna meja. Ta izračun preprečuje uničenje inverterja v mrzlih zimskih jutrih.
  - Temperaturni koeficient - Običajno je nehativen (npr -0.28%/stop. C). Pri izračunu ga upoštevamo tako, da se napetost z znižanjem temperature povečuje.
  - Tmin: Ne uporabi povprečne zimske temperature, ampak zgodovinski minimum na lokaciji (npr. -15 ali -20 stopinj v Sloveniji)
  - Pravilo: Ta vrednost mora biti vedno pod Max DC Input Voltage v tehničnem listu inverterja.

- **Min string V** = Vmp × koef. temp. (max. temp.) × N > Vmin MPPT - Operativna meja
Ta izračun zagotavlja, da bo inverter deloval tudi v najhujši vročini, ko se paneli segrejejo na 60 stopinj ali več
  - Tmax: To je temperatura celice. V vročem poletjue celice dosežejo tudi okoli 70 stopinj.
  - Vloga: Če ta napetost pade pod Vmin MPPT (spodnji prag delovnega območja), bo inverter izgubil točko maksimalne moči ali pa se bo celo izklopil, čeprav sonce močno sije.
  - Nasvet: vedno ciljaj na sredino MPPT območja za optimalen izkoristek.

- **Število vzporednih stringov** = Imax inverterja / Isc stringa - Tokovna omejitev (vzporedno vezanje)
Pri večjih sistemih pogosto vežemo dva ali več stringov vzporedno na isti MPPT vhod.
  -Napetost ostane ista, tok se sešteva: Itotal = Nstrings*Isc
  -Omejitev: Ta seštevek mora biti nižji od Max Input CUrrent (Idc,max) na posameznem MPPT vhodu inverterja.
  -Pozor na "Isc PV": Nekateri inverterji imajo navedeno tudi kratkostično tokovno mejo, ki je ne smeš preseči, da ob morebitni napaki ne pride do poškodb vezja,

Praktičen primer:
Panel z Voc = 40V, in inverter z Vmax = 1000V.
Teoretični max: 1000/40 = 25 panelov
Zimski popravek: Zaradi mraza napetost zraste za cca 15-20%
Varna meja: 25 * 0.85 = 21 panelov ->to je realna zgornja meja

Povzetek: 
Parameter,Kateri podatek gledaš?,Kdaj je kritično?,Cilj načrtovanja
Max Napetost,Voc​ (Open Circuit),Pozimi (mraz),Ne skuri inverterja!
Min Napetost,Vmp​ (Max Power),Poleti (vročina),Ostani v MPPT območju!
Max Tok,Isc​ (Short Circuit),Ob polnem obsevanju,Ne pregrevaj vhodov!

## 8. Izgube sistema
| Vzrok              | Tipična izguba |
|--------------------|----------------|
| Temperatura modula |  5–10%         |
| Senčenje           | variabilno     |
| Umazanija          |    1–5%        |
| Kabelske izgube    |    1–3%        |
| Inverter izkoristek|    2–5%        |
| Mismatch modulov   |    1–2%        |

**PR (Performance Ratio)** = dejanska produkcija / teoretična produkcija; dober sistem > 80%

## 9. Varnostni sistemi
- **DC disconnect** – ločitev od modulov
- **AC disconnect** – ločitev od omrežja
- **Anti-islanding** – inverter zaustavi ob izpadu omrežja (VDE-AR-N 4105, EN 50549)
- **Surge Protection Device (SPD)** – strela/prenapetost
- **AFCI** – Arc Fault Circuit Interrupter (požarna varnost DC)
- **Fuse/breaker** per string

## 11. Ključni pojmi za intervju
- **kWp** – kilowatt peak (nazivna moč pri STC)
- **kWh/kWp** – specifična produkcija (yield)
- **GHI** – Global Horizontal Irradiance
- **POA** – Plane of Array irradiance (dejansko na modul)
- **PR** – Performance Ratio
- **CUF** – Capacity Utilization Factor = dejanska kWh / (kWp × 8760h)
- **LCOE** – Levelized Cost of Energy (€/kWh skozi življenjsko dobo)

