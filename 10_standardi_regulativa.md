# Standardi in Regulativa — FTTH / Telekomunikacije

## 1. ITU-T Standardi (optična vlakna in PON)

### G-serija — Optični sistemi za prenos:

| Standard | Vsebina | Ključno |
|---|---|---|
| **G.652** | Standard SMF | G.652.D = brez OH peaka, za FTTH |
| **G.657** | Bend-insensitive SMF | G.657.A2 = drop kabel, 7.5 mm bend radius |
| **G.651.1** | MMF (50 µm) | Za LAN/datacenter — NE za FTTH |
| **G.984.1** | GPON — splošne zahteve | Split ratio, doseg, arhitektura |
| **G.984.2** | GPON — fizični sloj | Optične zahteve, razredi B+/C+ |
| **G.984.3** | GPON — TC sloj | GEM, T-CONT, DBA, ranging |
| **G.984.4** | GPON — OMCI | Upravljanje ONT |
| **G.984.5** | GPON — razširitev band | CATV overlay, WDM |
| **G.984.6** | GPON — doseg | Razširitev na 60 km |
| **G.9807.1** | XGS-PON | 10G simetrično, DS 1577/US 1270 nm |
| **G.989.1** | NG-PON2 — splošno | TWDM, 4×10G |
| **G.989.2** | NG-PON2 — fizični sloj | Optične zahteve |
| **G.989.3** | NG-PON2 — TC sloj | Protokol |

### G.657 podtip detajli:

| Podtip | Min. upogib (enkraten) | Min. upogib (večkraten) | Macrobend pri 1550 nm |
|---|---|---|---|
| G.657.A1 | 10 mm | 15 mm | ≤ 0.5 dB |
| G.657.A2 | 7.5 mm | 10 mm | ≤ 0.5 dB |
| G.657.B2 | 7.5 mm | 10 mm | ≤ 0.2 dB (strožji) |
| G.657.B3 | 5 mm | 7.5 mm | ≤ 0.2 dB |

---

## 2. IEEE Standardi

| Standard | Vsebina |
|---|---|
| **802.3ah** | EPON — 1 Gbps Ethernet PON |
| **802.3av** | 10G-EPON — 10/10 ali 10/1 Gbps |
| **802.3bt** | PoE++ — 90W Power over Ethernet (za indoor ONT?) |
| **802.1Q** | VLAN tagging |
| **802.1ad** | Provider Bridges (QinQ, S-VLAN) |
| **802.1p** | Traffic priority (vgrajen v 802.1Q) |
| **802.3** | Ethernet splošno |
| **802.11** | WiFi (za ONT wireless) |

---

## 3. ETSI / EN / IEC Standardi (instalacija)

### EN 50174 — Instalacija informacijske kabelske infrastrukture:
- **EN 50174-1**: Specifikacije in zagotavljanje kakovosti
- **EN 50174-2**: Planiranje instalacije in prakse znotraj stavb
- **EN 50174-3**: Instalacija zunaj stavb
- Ključno za: projekt instalacije, testiranje in dokumentacija

### EN 50173 — Strukturirano kabliranje:
- EN 50173-1: Splošne zahteve
- EN 50173-4: Domači prostori (FTTH do stanovanja)
- Definira kategorije (Cat 5e, Cat 6, optika) in testne zahteve

### IEC 61754 — Optični konektorji:
- IEC 61754-4: SC konektor
- IEC 61754-20: LC konektor
- Dimenzije, zahteve za vstavne izgube, mehansko vzdržljivost

### IEC 61300 — Pasivne optične komponente:
- Testne metode za splitterje, konektorje, adapterje

### IEC 60825 — Varnost laserskih naprav:
- IEC 60825-1: Klasifikacija (razredi 1, 1M, 2, 3, 4)
- PON sistemi = **razred 1M** (brez instrumena varen, z instrumentom nevaren)

### SIST EN 50341 — Nadzemni električni vodi:
- Velja za izračun mehanskih obremenitev drogov in kablov
- Upošteva: veter, žled, temperatura

---

## 4. Regulativa v Sloveniji

### ZEKom-2 — Zakon o elektronskih komunikacijah
*(Uradni list RS, št. 130/22)*

**Ključne določbe za projektanta:**

- **Pravica do gradnje infrastrukture** (čl. 137): operaterji imajo pravico polagati kable po javnih površinah
- **Skupna raba infrastrukture** (čl. 139): operaterji morajo dovoliti skupno rabo obstoječe infrastrukture tretjim
- **Gradnja v novih stavbah** (čl. 148): nove stavbe morajo imeti optično infrastrukturo (VHCN ready)
- **Operaterji z značilno tržno močjo (SMP)**: Telekom SLO ima obveznost objave referenčnih ponudb za dostop

### Pravilnik o minimalnih tehničnih zahtevah (2016, spremenjen):
- Vse nove stanovanjske stavbe (>1 enota) morajo imeti optično kabelsko instalacijo
- Zahteva: centralna točka (FTTH splitter), vertikalni vod, priključek v vsaki enoti

### AKOS — Agencija za komunikacijska omrežja in storitve:
- Regulator elektronskih komunikacij v RS
- **Registracija omrežja**: operaterji morajo prijaviti infrastrukturo
- **Analiza trga**: AKOS določi SMP operaterje in obveznosti
- **Reševanje sporov**: med operaterji (npr. glede skupne rabe)
- **Frekvence**: dodeljevanje radijskih frekvenc (mobilni operaterji)
- Nadzor implementacije ZEKom-2
- Kontakt za soglasja: ne neposredno AKOS, ampak infrastrukturni lastniki

### Gradbena zakonodaja:
- **GZ-1 (Gradbeni zakon)**: postopek pridobivanja gradbenih dovoljenj
  - Enostavni objekt (majhna kabelska kanalizacija): brez gradbenega dovoljenja
  - Zahtevni posegi: PGD + GD obvezno
- **ZUreP-3 (Zakon o urejanju prostora)**: prostorski načrti, namenska raba
- **Uredba o enotni metodologiji** za kabelsko kanalizacijo: poenostavitev dovoljenj

### Upravljavci infrastrukture — soglasja:

| Upravljavec | Infrastruktura | Soglasje |
|---|---|---|
| **DRSI** | Državne ceste (AC, magistrale, regionalne) | Tehnično soglasje + dovoljenje |
| **Občina** | Občinske ceste, parki, javne površine | Soglasje oz. odločba |
| **DARS** | Avtoceste in hitre ceste | Soglasje + pogodba |
| **SODO** | Elektrodistribucijski drogovi | Soglasje + pogodba o skupni rabi |
| **Elektro podjetja** | Elektro infrastruktura v bližini | Soglasje za varnost |
| **SŽ (Slovenian Railways)** | Železnica | Soglasje za prečkanje |
| **ARSO** | Vodotoki, varovani pasovi | Vodno soglasje |
| **ZVKDS** | Kulturna dediščina | Soglasje za posege |

---

## 5. EU Regulativa

### European Electronic Communications Code (EECC — Direktiva 2018/1972):
- Horizontalni regulatorni okvir za vse EU države
- Prenešeno v slovensko pravo prek ZEKom-2
- Ključno: skupna raba infrastrukture, dostop do omrežij, varstvo potrošnikov

### Gigabit Society Communication (2016):
EU cilji za širokopasovni dostop:

| Cilj | Leto |
|---|---|
| 100 Mbps za vse gospodinjstva (nadgradljivo na gigabit) | 2025 |
| Gigabit za vse socialno-ekonomske gonilnike (šole, bolnice, javni organi) | 2025 |
| 5G pokritost vseh urbanih področij in prometnih koridorjev | 2025 |
| Gigabit za vsa gospodinjstva, ruralna in urbana | **2030** |
| 5G pokritost vseh naseljenih območij | 2030 |

### Digital Decade Policy Programme 2030 (Odločba 2022/2481):
- 2030: 100% pokritost z gigabitnimi omrežji
- 2030: 100% 5G pokritost

### State Aid Rules (pravila državnih pomoči):
- EU strogo nadzoruje subvencije za gradnjo omrežij
- Dovoljena državna pomoč samo na tržno neuspešnih področjih (bela področja)
- **Bela področja**: < 30 Mbps dostop, ni investicij v naslednjih 3 letih
- Telemach/United Fiber tekmuje za EU/državne razpise za ruralna področja

### Broadband Cost Reduction Directive (2014/61/EU):
- Olajšanje skupne rabe infrastrukture med operaterji in z upravljavci druge komunalne infrastrukture
- Dostop do geodetskih podatkov o obstoječi infrastrukturi
- Slovenija: implementirano v ZEKom-2 in podzakonske akte

---

## 6. Hitri povzetek — kar morate znati na razgovoru

1. G.652.D = standard FTTH kabel, brez OH peak, za WDM kompatibilnost
2. G.657.A2 = drop kabel, upogib do 7.5 mm — za instalacijo v stavbah
3. G.984.x serija = GPON standardi (G.984.2 = fizični sloj, B+/C+ razredi)
4. G.9807.1 = XGS-PON standard (10G simetrično)
5. ZEKom-2 daje pravico gradnje po javnih površinah in skupno rabo
6. AKOS = telekomunikacijski regulator RS, registracija omrežij
7. Nove stavbe morajo imeti optično instalacijo (pravilnik 2016)
8. DRSI za državne ceste, občina za lokalne, SODO za drogove
9. EU cilj 2030: gigabit za vsa gospodinjstva
10. Bela področja = < 30 Mbps, možna državna pomoč za gradnjo
