# Tehnična priprava na razgovor: Sistemski inženir II – Elektro Celje (Služba telekomunikacij)

### Hierarhija omrežja Elektro Celje

| Oznaka  |   Naziv                              | Napetostni nivo| Vloga |
|---------|--------------------------------------|----------------|-------|
| **RTP** | Razdelilna transformatorska postaja | 110 kV / 20 kV | Priključitev na prenosno omrežje (ELES), transformacija na distribucijsko napetost |
| **RP** | Razdelilna postaja | 20 kV | Stikalna postaja brez transformatorja, razvod 20 kV |
| **TP** | Transformatorska postaja | 20 kV / 0,4 kV | Transformacija za odjemalce (gospodinjstva, podjetja) |

### Kaj mora sistemski inženir v telekomunikacijah o tem vedeti?
- V vsakem RTP/RP je telekomunikacijska oprema (stikala, routerji, RTU, komunikacijski strežniki).
- Telekomunikacijska omrežja so hrbtenica upravljanja (SCADA) celotnega distribucijskega omrežja.
- Razumeti moraš, zakaj je zanesljiva komunikacija do vsake postaje kritična (izpad komunikacije = slepota v SCADA).

## 2. SCADA SISTEMI IN SISTEMI VODENJA

### Kaj je SCADA?
**SCADA** (Supervisory Control and Data Acquisition) je nadzorni in upravljavski sistem za daljinsko vodenje elektroenergetskega omrežja.

### Arhitektura SCADA sistema

```
[Dispečerski center / Control Center]
        |
   [SCADA Server / MTU]
        |  (komunikacijsko omrežje)
   [RTU / IED naprave v RTP/RP/TP]
        |
   [Terenska oprema: stikala, odklopniki, merilniki]
```

- **MTU** (Master Terminal Unit) – centralni strežnik SCADA v dispečerskem centru
- **RTU** (Remote Terminal Unit) – naprava v oddaljeni postaji, ki zbira meritve in izvaja ukaze
- **IED** (Intelligent Electronic Device) – pametna zaščitna ali merilna naprava (npr. zaščitni rele)
- **HMI** (Human-Machine Interface) – grafični vmesnik za operaterje
- **Historian** – podatkovna baza za arhiviranje časovnih vrst meritev


### Komunikacijski protokoli v SCADA/energetiki (OBVEZNO ZNANJE)


#### IEC 60870-5 serija
- **IEC 60870-5-101** – serijsko (RS-232/RS-485), za komunikacijo med MTU in RTU prek počasnih linij
- **IEC 60870-5-104** – isti protokol kot 101, vendar prek TCP/IP omrežja (Ethernet/IP)
- Podpira: enkratne ukaze, dvojne ukaze, merjene vrednosti, časovne žige, spontane prenose

#### IEC 61850
- Sodoben standard za komunikacijo med IED napravami v RTP/RP
- Dve plasti komunikacije:
  - **MMS** (Manufacturing Message Specification) – za nadzor in kontrolo prek TCP/IP
  - **GOOSE** (Generic Object Oriented Substation Events) – za hitro zaščitno signalizacijo prek Ethernet (sub-milisekunda)
- Logični vozli (Logical Nodes): XCBR (odklopnik), XSWI (ločilnik), MMXU (meritve)...
- Prednost: interoperabilnost različnih proizvajalcev, standardizirana konfiguracija prek **SCL** datotek (`.icd`, `.scd`, `.cid`)

#### Modbus
- **Modbus RTU** – serijsko (RS-485)
- **Modbus TCP** – prek IP omrežja
- Register-based protokol; preprost, zelo razširjen pri PLC-jih in merilnikih
- Master/Slave arhitektura

#### SNMP (Simple Network Management Protocol)
- Za nadzor in upravljanje telekomunikacijske omrežne opreme (stikala, routerji, multipleksorji)
- Verzije: v1, v2c, **v3** (edini s šifriranjem – priporočen za varnost)
- Trap: asinhrono sporočilo naprave ob alarmu



## 3. TELEKOMUNIKACIJSKA OMREŽJA V ELEKTRODISTRIBUCIJI

### Topologije

- **Zvezdasta** – RTP je center, RP/TP so veje (preprosta, a brez redundance)
- **Obroč (Ring)** – vsaka postaja je del obroča; izpad ene povezave ne povzroči izpada vozlišča
- **Mrežasta (Mesh)** – visoka redundanca, kompleksno upravljanje

- Elektro podjetja tipično gradijo **obroče s Spanning Tree / RSTP** ali **SDH obroče**
Spanning Tree Protocol (STP) in Rapid Spanning Tree Protocol (RSTP, IEEE 802.1w) sta protokola, ki omogočata redundantno mrežno topologijo brez zanke v Ethernet omrežju.
Tipično se uporablja v LAN omrežjih ali industrijskih omrežjih, kjer obstaja potreba po rezervni poti, če primarna povezava odpove.
Kako deluje?
Mreža z več povezanimi stikali lahko ustvari zanke. STP:
Identificira “root bridge” (glavno stikalo)
Izračuna minimalni set povezav, da ne nastanejo zanke
Drugi povezavi postavi v blocking mode, dokler primarna ne odpove
RSTP je hitrejša verzija STP, ob napaki preklopi poti v sekundah, ne v minutah.
Prednosti
Preprosta implementacija.
Dovolj za manj kritične obroče ali kjer so Ethernet linki relativno poceni.
Ni potrebna specializirana oprema.
Slabosti
Hitrost preklopa (STP: 30–50s, RSTP: ~1–5s) je lahko prepočasna za kritične elektro obroče, kjer je stabilnost ključna.
Ni optimizirana za sinhronizacijo ali transport velikih količin podatkov, kot je SCADA ali telemetrija.


2. SDH obroči (Synchronous Digital Hierarchy)
Kaj je to?
SDH je telekomunikacijski standard za prenos podatkov po optičnih vlaknih.
Omogoča gradnjo obročev z redundanco, kjer lahko signal teče v obe smeri (dual ring), in ob napaki samodejno preusmeri tok.
Pogosto se uporablja za kritične elektro omrežne aplikacije, SCADA sisteme, daljinske telemetrije in nadzor elektro distribucije.
Kako deluje?
Signal teče v obroču, običajno v dveh smereh: primarna in rezervna.
Ob izpadu primarne poti SDH obroč samodejno preklopi na drugo smer (hitro: v milisekundah).
Ponuja visoko zanesljivost (availability 99,999%).
Prednosti
Hitre odzivne čase ob napaki (ms).
Sinhronizacija za SCADA, telemetrijo, zaščito daljnovodov.
Omogoča QoS in različen prenos (telefonija, Ethernet, telemetrija) preko iste infrastrukture.
Slabosti
Dražja oprema (SDH multiplexerji).
Več kompleksnosti pri upravljanju.

Elektro podjetja običajno uporabljajo SDH obroče za kritične povezave med daljnovodi, trafostanicami in SCADA sistemi zaradi hitrega preklopa in zanesljivosti. STP/RSTP Ethernet obroči se uporabljajo predvsem tam, kjer so potrebe po kritičnosti manjše ali za interno omrežje z več preprostimi napravami.


### Prenosne tehnologije

#### Optična vlakna (fiber optics)
- **Enomodni (Single-Mode, SMF, G.652)** – dolge razdalje (>2 km), 1310 nm in 1550 nm, tanek core (~9 µm)
- **Večmodni (Multi-Mode, MMF)** – kratke razdalje (<550 m za 10G), debelejši core (50/62,5 µm)
- Elektrodistribucija večinoma gradi **OPGW** (Optical Ground Wire – optika v ozemljitveni vrvici daljnovodov) ali **ADSS** (All-Dielectric Self-Supporting – optika v nekovinskem kablu, obešenem med drogovi)
- **Konektorji**: SC/APC (zeleni, kot 8°, manj odboja – za distribucijo signala), SC/UPC (modri), LC, FC
- **Splicing**: fuzijsko varjenje vlaken, mehanski spoji



