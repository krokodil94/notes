# HFC Omrežje in DOCSIS — Telemach Legacy

## 1. HFC — Hybrid Fiber-Coaxial

Telemach je zgradil HFC omrežje za kabelsko TV in internet. Danes gradi FTTH vzporedno.

### Arhitektura HFC:

```
Headend (CO)
    │
    ▼ optika (monomodna)
Optical Node (fiber node)
    │
    ▼ koaksial (do 500 m razdalje)
    ├── Amplifier (ojačevalnik) ──► nadaljnji koaksial
    │       └── Amplifier ──► nadaljnji koaksial
    │               └── Coax drop ──► Cable modem (CM) pri stranki
    └── Direktni drop ──► Cable modem pri stranki
```

**Optični node** pretvori optični signal v RF (Radio Frequency) signal na koaksialnem kablu in obratno.

### Koaksialni kabel:
- Impedanca: **75 Ω** (za razliko od računalniških LAN — 50 Ω)
- Frekvenčni pas (legacy HFC):
  - **Upstream: 5–65 MHz** (stari standard)
  - **Downstream: 85 MHz – 1 GHz** (tipično do 750 MHz ali 1 GHz)
- DOCSIS 3.1 razširi:
  - Upstream: do 204 MHz
  - Downstream: do 1.218 GHz

### Amplifierji (ojačevalniki):
- Kompenzirajo slabitev koaksialnega kabla
- HFC omrežje ima 3–5 amplifierjev v kaskadi (tipično)
- Vsak amplifier = napajanje, vzdrževanje, potencialna napaka
- **Problem:** amplifierji povzročajo šum in hkratno oddajanje napak (noise funneling)

### Noise funneling (šum v upstream):
```
Stranka A ──► šum
Stranka B ──► šum    → vsi šumi se seštevajo v amplifier in node
Stranka C ──► šum
```
Upstream kakovost slabša od downstream — omeji upstream hitrosti.

---

## 2. DOCSIS — Data Over Cable Service Interface Specification

### Generacije DOCSIS:

| Verzija | DS kanali | US kanali | DS max | US max | Modulacija |
|---|---|---|---|---|---|
| DOCSIS 2.0 | 1 | 1 | 38 Mbps | 30 Mbps | QAM-64/256 |
| **DOCSIS 3.0** | do 32 bonded | do 8 bonded | ~1.2 Gbps | ~200 Mbps | QAM-256 |
| **DOCSIS 3.1** | OFDM | OFDMA | ~10 Gbps | ~1 Gbps | 4096-QAM |
| DOCSIS 4.0 | FDX | FDX | ~10 Gbps | ~6 Gbps | FDX OFDM |

### DOCSIS 3.0 — Channel Bonding:
- **32 downstream** kanali po 6 MHz (38 Mbps cada) → skupaj ~1.2 Gbps DS
- **8 upstream** kanali → skupaj ~200 Mbps US
- Kanali se vežejo (bond) v en logični tok za stranko
- Praktično: stranke dobijo 200–400 Mbps DS (deljeno z drugimi)

### DOCSIS 3.1 — OFDM:
- Namesto fiksnich 6 MHz kanalov: **OFDM** (Orthogonal Frequency Division Multiplexing)
- DS: 192 MHz OFDM kanal (96 MHz do 1218 MHz)
- US: OFDMA z 96 MHz
- Modulacija do **4096-QAM** (vs 256-QAM pri 3.0)
- Nižji overhead, boljša spektralna učinkovitost
- **Teoretični max: ~10 Gbps DS, ~1 Gbps US**

### DOCSIS 4.0 — Full Duplex (FDX):
- Upstream in downstream **hkrati na istih frekvencah**
- Zahteva eco-cancellation (odpravljanje lastnega odmeva)
- **10 Gbps DS + 6 Gbps US** simetrično na HFC!
- Zahteva zamenjavo nodeov in amplifierjev
- Alternativa: Extended Spectrum DOCSIS (ESD) — US do 684 MHz, DS do 1.8 GHz

---

## 3. CMTS — Cable Modem Termination System

**CMTS** je oprema v Headend-u (CO):
- Terminira DOCSIS protokol
- Dodeljuje bandwidth cable modemom (CM)
- Izvaja QoS (service flows)
- Poveže HFC access s core omrežjem

```
Internet ──► Core Router ──► CMTS ──► optika ──► Node ──► koaksial ──► CM
```

**Modernejši arhitekturi:**
- **Remote PHY (R-PHY):** fizični sloj preseljen iz CMTS v node, CMTS ostane v headend
- **Remote MACPHY:** MAC + PHY preseljeni v node → "distributed access architecture"
- Prednost: zmanjšanje analognega optičnega dela, digitalni optični signal do noda

---

## 4. Cable Modem (CM) pri stranki:

- Analogno: prima RF signal iz koaksiala
- Demodulira DOCSIS signal
- Poveže se na internet prek Ethernet (ali WiFi z vgrajenim routerjem)
- DOCSIS registracija:
  1. CM skenira frekvence, najde DS kanal
  2. Pridobi čas in konfiguracijsko datoteko z TFTP
  3. CMTS izmeri ranging (razdalja) za US timing
  4. CM se registrira in dobi IP
  5. Promet teče

---

## 5. Node Segmentation (N+x)

Trenutno stanje Telemach HFC: tipično N+3 ali N+4 (3–4 amplifierji za nodom).

**Problem:** Vsak node streže 200–500 strank. Kapaciteta omejena.

**Rešitev — Node Splitting (N+0):**
```
Staro: 1 node → 4 amplifier kaskade → 500 strank
Novo:  4 manjši nodeji → 0 amplifierjev → 125 strank vsak
```

- Krajša koaksialna pot = manj šuma = boljši US
- Manj strank na node = več bandwidth per stranka
- Zahteva optiko do vsakega novega noda (fiber deep)
- **N+0** = 0 amplifierjev za nodom = fiber do vsake skupinice hiš

---

## 6. HFC → FTTH Migracija pri Telemachu

### Zakaj United Fiber gradi FTTH vzporedno z HFC?

1. **DOCSIS 3.1 ne doseže FTTH paritet** za upstream (1G vs 10G)
2. **DOCSIS 4.0 zahteva drago HFC upgrade** (novi nodeji, amplifierji)
3. **FTTH OPEX nižji** — brez amplifierjev, brez HFC vzdrževanja
4. **Regulatorne zahteve** — EU gigas cilj: >1 Gbps do 2025
5. **Kompetitivni tlak** — Telekom Slovenije in T-2 gradita FTTH

### Migracijska strategija:

```
Faza 1: Gradi FTTH vzporedno z obstoječim HFC
         → Stranke se prostovoljno selijo
         
Faza 2: Ko FTTH penetracija > 70% v nekem področju
         → HFC infrastruktura postane neekonomična
         
Faza 3: HFC izklopitev (network retirement)
         → Vsi preostali na FTTH migrirani (forced migration)
         → Koaksial infrastruktura odprodana ali likvidirana
```

### Remote PHY kot vmesna rešitev:
- Telemach ne zavrže HFC takoj — amortizacija
- Remote PHY poveča kapaciteto obstoječega HFC
- Hkratna gradnja FTTH v novih in strateških področjih

---

## 7. HFC vs FTTH Primerjava

| Lastnost | HFC DOCSIS 3.1 | FTTH GPON | FTTH XGS-PON |
|---|---|---|---|
| DS hitrost | ~10 Gbps (skupno) | 2.5 Gbps/port | 10 Gbps/port |
| US hitrost | ~1 Gbps (skupno) | 1.25 Gbps/port | 10 Gbps/port |
| Latenca | 5–15 ms | 1–5 ms | 1–5 ms |
| Amplifierji | Da (3–5) | Ne | Ne |
| Napajanje v terenu | Da (amplifierji) | Ne | Ne |
| OPEX | Visok | Nizek | Nizek |
| Max doseg | ~30 km node to node | 20 km | 20 km |
| Nadgradnja | Zamenjava CMTS/CM | Zamenjava OLT/ONT | Zamenjava OLT/ONT |

---

## 8. Hitri povzetek — kar morate znati na razgovoru

1. HFC = optika do noda, koaksial do stranke — Telemach legacy
2. Koaksial impedanca 75 Ω, DS 85 MHz–1 GHz, US 5–65 MHz
3. DOCSIS 3.0: bonded channels, ~1.2G DS; DOCSIS 3.1: OFDM, ~10G DS
4. CMTS v headend termina DOCSIS, dodeljuje BW cable modemom
5. Noise funneling: upstream šumi se seštevajo — US bolj omejen od DS
6. Node splitting (N+0): manj strank na node, manj amplifierjev, boljši US
7. Remote PHY: PHY preseli v node, CMTS ostane — "fiber deep"
8. United Fiber gradi FTTH ker: višje hitrosti, nižji OPEX, konkurenca, EU cilji
9. Migracijska strategija: vzporedna gradnja → prostovoljni prehod → forced migration
10. FTTH latenca 1–5 ms vs HFC 5–15 ms — prednost za gaming, real-time
