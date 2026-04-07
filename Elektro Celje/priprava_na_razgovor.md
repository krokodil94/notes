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

- **Zvezdasta** – RTP je center, RP/TP so veje (preprosta, a brez redundance)
- **Obroč (Ring)** – vsaka postaja je del obroča; izpad ene povezave ne povzroči izpada vozlišča
- **Mrežasta (Mesh)** – visoka redundanca, kompleksno upravljanje

- Elektro podjetja tipično gradijo **obroče s Spanning Tree / RSTP** ali **SDH obroče**
Spanning Tree Protocol (STP) in Rapid Spanning Tree Protocol (RSTP, IEEE 802.1w) sta protokola, ki omogočata redundantno mrežno topologijo brez zanke v Ethernet omrežju.


