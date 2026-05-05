
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

