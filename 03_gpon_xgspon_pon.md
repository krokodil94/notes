# PON Tehnologije — GPON, XGS-PON, NG-PON2

## 1. Primerjalna tabela PON tehnologij

| Lastnost | GPON | EPON | XGS-PON | NG-PON2 |
|---|---|---|---|---|
| Standard | ITU-T G.984 | IEEE 802.3ah | ITU-T G.9807.1 | ITU-T G.989 |
| DS hitrost | 2.488 Gbps | 1.25 Gbps | 10 Gbps | 4×10 Gbps |
| US hitrost | 1.244 Gbps | 1.25 Gbps | 10 Gbps | 4×10 Gbps |
| DS valovna dolžina | 1490 nm | 1490 nm | 1577 nm | TWDM |
| US valovna dolžina | 1310 nm | 1310 nm | 1270 nm | TWDM |
| Max split ratio | 1:128 | 1:64 | 1:256 | 1:256 |
| Tipični split | 1:32, 1:64 | 1:32 | 1:64, 1:128 | 1:128 |
| Max doseg | 60 km | 20 km | 40 km | 40 km |
| Tipični doseg | 20 km | 10 km | 20 km | 20 km |
| Deployed | ✅ Masovno | Azija | ✅ Raste | Prihodnost |

**GPON** = dominantna tehnologija danes v Evropi (tudi Telemach/United Fiber).
**XGS-PON** = prehod za 10G, koeksistira z GPON na isti infrastrukturi.

---

## 2. GPON — Gigabit Passive Optical Network

### Standard: ITU-T G.984 (G.984.1 do G.984.6)

### Hitrosti in multipleksiranje
- **Downstream** (OLT → ONT): **2.488 Gbps** na enem PON portu
- **Upstream** (ONT → OLT): **1.244 Gbps** deli se med vsemi ONT na portu
- **WDM ločevanje smeri**: DS @ 1490 nm, US @ 1310 nm — po istem vlaknu hkrati
- **Downstream = broadcast**: OLT pošilja vsem, ONT sprejme samo svoje pakete (šifriranje AES-128)
- **Upstream = TDMA**: vsak ONT dobi časovne reže (time slots)

### OLT — Optical Line Terminal
- Stoji v CO/POP
- Tipično: 8, 16, ali 32 PON portov na linijsko kartico
- 1 PON port = 1 optično vlakno = do 128 ONT
- Uplink: 10GE, 25GE, ali 100GE do agregacijske mreže
- Proizvajalci: Nokia (ISAM), Huawei (MA5800), ZTE, Calix

### ONT/ONU — Optical Network Terminal/Unit
- Stoji pri stranki (stanovanje, pisarna)
- Pretvori optični PON signal v Ethernet/WiFi/VoIP/RF
- Napajanje: ~7W, iz električne vtičnice
- Tipični porti: 1× SC/APC, 4× GE, 2× FXS, WiFi
- **ONT** = integrirana naprava za rezidencialne stranke
- **ONU** = samo optični del, brez router funkcije (za poslovne z lastnim routerjem)

### GEM Port (GPON Encapsulation Method)
- GPON ne prenaša "golo" Ethernet — enkapsulira v GEM okvirje
- Vsak GEM port = logični kanal za določeno vrsto prometa
- Primer: GEM 1 = internet, GEM 2 = IPTV, GEM 3 = VoIP

### T-CONT — Transmission Container
- Logična enota za **upstream bandwidth allocation**
- 4 tipe T-CONT (fiksni, zagotovljeni, zajamčeni, best-effort)
- Vsak T-CONT dobi bandwidth od OLT prek DBA

### DBA — Dynamic Bandwidth Allocation
- OLT dinamično dodeljuje upstream kapaciteto vsaki ONT glede na potrebe
- ONT sporoča OLT koliko bufferja ima (DBRu — Dynamic Bandwidth Report)
- OLT izda GRANT — dovoljenje za oddajanje v določeni časovni reži
- Latenca DBA: tipično 125 µs do 1 ms

### Ranging
- Fizična razdalja od OLT do vsake ONT je različna → različne zakasnitve
- OLT izmeri razdaljo vsakega ONT in dodeli **equalization delay**
- Vsi ONT dobijo isto logično razdaljo → usklajeno TDMA oddajanje
- Proces ob aktivaciji ONT, dokler ONT ne dobi "ranged" statusa

### PLOAM — Physical Layer Operations, Administration, Maintenance
- Sporočila za upravljanje PON sloja
- ONT aktivacija, ranging, šifriranje, alarmi

### OMCI — ONT Management and Control Interface
- Upravljanje višjih slojev ONT (Ethernet, VoIP, QoS, VLAN)
- OLT pošlje OMCI sporočila ONT prek GEM porta
- Konfiguracija: GEM porti, T-CONT, VLAN mapiranje, SIP parametri

---

## 3. XGS-PON — 10-Gigabit Symmetric PON

### Standard: ITU-T G.9807.1

### Zakaj XGS-PON?
- **10 Gbps simetrično** — GPON: 2.5G/1.25G asimetrično
- Poslovne stranke (B2B) zahtevajo simetrične hitrosti
- 4K IPTV, cloud gaming, work-from-home povečuje zahteve
- Koeksistenca z GPON: **isti ODN (vlakno + splitter)**, različne valovne dolžine

### Valovne dolžine XGS-PON:
```
DS: 1577 nm  (GPON DS je 1490 nm — ne kolizija)
US: 1270 nm  (GPON US je 1310 nm — ne kolizija)
```

### WDM filter pri OLT:
```
OLT GPON port ──┐
                ├── WDM Coupler ── skupno vlakno → splitter → stranke
OLT XGS port ──┘
```
Isti splitter služi obema tehnologijama!

### Migracija GPON → XGS-PON:
1. Dodaj XGS-PON kartice v obstoječ OLT
2. WDM coupler ni potreben — OLT ima vgrajeno WDM ločevanje
3. Zamenjaj ONT pri stranki z XGS-PON ONT
4. Obstoječe GPON stranke nadaljujejo brez sprememb

### XGS-PON link budget:
- Razred N1: 29 dB (za 1:64 split na kratkih razdaljah)
- Razred N2: 31 dB (za 1:64 split do 20 km)
- Razred E1: 33 dB
- Razred E2: 35 dB (za 1:128 split ali daljše razdalje)

---

## 4. EPON — Ethernet PON (za splošno znanje)

### Standard: IEEE 802.3ah
- Razvila IEEE (ne ITU-T) → bolj popularen v Aziji
- 1.25 Gbps simetrično (DS in US enako)
- Ethernet native (ne GEM enkapsulacija)
- Manj razširjen v Evropi

### 10G-EPON: IEEE 802.3av
- 10/10 Gbps ali 10/1 Gbps
- Koeksistenca s klasično EPON

---

## 5. NG-PON2 — Next Generation PON 2

### Standard: ITU-T G.989
- **TWDM-PON** (Time and Wavelength Division Multiplexing)
- 4 pare valovnih dolžin × 10 Gbps = **skupaj 40 Gbps na vlakno**
- ONT se nastavi na eno od 4 valovnih dolžin (tunabilni oddajnik)
- Doseg: 40 km, split: 1:256
- Status: standardiziran, komercialna deployments redka (draga ONT)
- Prihodnost: verjetno XGS-PON → NG-PON2 prehod po 2030

---

## 6. PON Aktivacija ONT — korak po korak

```
1. ONT priključi vlakno in napajanje
2. ONT pošlje SERIAL_NUMBER v upstream @ 1310 nm
3. OLT prejme serial number, dodeli ONU-ID
4. OLT sproži ranging — izmeri zakasnitev do ONT
5. OLT dodeli equalization delay ONT
6. OLT pošlje šifrirni ključ (AES-128)
7. OMCI konfiguracija: GEM porti, T-CONT, VLAN
8. ONT je "operational" — promet teče
```

---

## 7. GPON Framing

### Downstream (2.488 Gbps, kontinuirano oddajanje):
```
[PCBd Header][GEM Frame 1][GEM Frame 2][...][GEM Frame N]
```
- PCBd = Physical Control Block downstream (sync, ranging, bandwidth grants)
- Vsak GEM frame nosi podatke za točno določen GEM port (Port-ID)
- ONT filtrira samo svoje GEM porte

### Upstream (1.244 Gbps, TDMA burst):
```
[Tišina][ONT-3 burst][Tišina][ONT-7 burst][Tišina][ONT-1 burst]
```
- OLT prek GRANT sporočil določi kdaj katera ONT oddaja
- Guard time med burst-i preprečuje kolizije
- Laser ONT se vklaplja/izklaplja za vsak burst

---

## 8. QoS v GPON — T-CONT tipi

| Tip | Ime | Opis | Primer |
|---|---|---|---|
| 1 | Fixed | Fiksna pasovna širina, vedno na voljo | TDM emulacija |
| 2 | Assured | Zagotovljena min. BW, brez max. | VoIP |
| 3 | Non-assured | Min. zagotovljeno + možnost porabe prostega | Video |
| 4 | Best-Effort | Prosta kapaciteta po T-CONT 1–3 | Internet |
| 5 | Hybrid | Kombinacija assured + best-effort | Poslovni |

---

## 9. Hitri povzetek — kar morate znati na razgovoru

1. GPON: 2.5G DS / 1.25G US, DS@1490nm, US@1310nm, ITU-T G.984
2. XGS-PON: 10G simetrično, DS@1577nm, US@1270nm, ITU-T G.9807.1
3. Koeksistenca: GPON + XGS-PON na istem ODN (vlakno/splitter) — različni λ
4. OLT je v CO, ONT je pri stranki
5. Downstream = broadcast + AES-128, Upstream = TDMA
6. GEM port = logični kanal (ločen za internet/IPTV/VoIP)
7. T-CONT = upstream bandwidth container, DBA = dinamična dodelitev
8. Ranging = sinhronizacija razdalj vseh ONT na PON portu
9. OMCI = upravljanje ONT konfiguracije iz OLT
10. Tipični split: mestno 1:64 (1:4 FDH × 1:16 ODP), primestno 1:32
