# Tehnična priprava na razgovor: Sistemski inženir II – Elektro Celje (Služba telekomunikacij)

RTP - Razdelilna transformatorska postaja | 110 kV / 20kV | Priključitev na prenosno omrežje (ELES), transformacija na distribucijsko napetost
RP  - Razdelilna postaja                  | 20kV          | Stikalna postaja brez transformatorjev, razvod 20kV
TP  - Transformatorska postaja            | 20kV / 0,4kV  | Transformacija za odjemalce (gospodinjstva, podjetja) 

V vsakem RTP/RP je telekomunikacijska oprema (stikala, routerji, RTU, komunikacijski strežniki).
Telekomunikacijska omrežja so hrbtenica upravljanja (SCADA) celotnega distribucijskega omrežja.

SCADA (Supervisory Control and Data Acquisition) je nadzorni in upravljalski sistem za daljinsko vodenje elektroenergetskega omrežja.

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

