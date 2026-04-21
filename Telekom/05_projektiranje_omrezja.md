# Projektiranje FTTH Omrežja — Proces in Dokumentacija

## 1. Faze projekta od A do Ž

```
┌──────────────────────────────────────────────────────────┐
│ 1. ANALIZA IN PREDPRIPRAVA                               │
│    Tržna analiza, GIS, terenska ogleda                   │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 2. IDEJNA ZASNOVA (IDZ)                                  │
│    Groba trasa, arhitektura omrežja, stroškovna ocena    │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 3. PROJEKT ZA GRADBENO DOVOLJENJE (PGD)                  │
│    Podrobna trasa, soglasja, pravni del                  │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 4. PRIDOBIVANJE SOGLASIJ IN DOVOLJENJ                    │
│    AKOS, občina, DRSI, SODO, DARS, lastniki             │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 5. PROJEKT ZA IZVEDBO (PZI)                              │
│    Izvedbeni načrti, kabelska knjiga, specifikacije      │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 6. GRADNJA                                               │
│    Izvajalci, nadzor, fazna gradnja                      │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 7. TESTIRANJE IN PREVZEM                                 │
│    OTDR meritve, link budget preverba, protokoli         │
└────────────────────────┬─────────────────────────────────┘
                         ▼
┌──────────────────────────────────────────────────────────┐
│ 8. AS-BUILT DOKUMENTACIJA                                │
│    Kot-izvedeno, GIS vnos, kabelska knjiga update        │
└──────────────────────────────────────────────────────────┘
```

---

## 2. Analiza in predpriprava

### Tržna analiza (Demand Forecasting)
- **Penetracija**: koliko % gospodinjstev bo vzelo storitev?
  - Tipično 30–60% pri FTTH v SLO urbanem okolju
  - Višje v novih naseljih, nižje tam kjer je že kabelski ali ADSL
- **Gostota**: gospodinjstev/km² → določa ekonomičnost projekta
  - Urbano: >200 GDH/km² → rentabilno
  - Ruralno: <50 GDH/km² → pogosto EU/državne subvencije
- **ARPU** (Average Revenue Per User): 20–40 EUR/mes tipično

### GIS analiza
- Katasterski načrt (zemljišča, lastniki)
- Obstoječa infrastruktura (kanali, kabli, drogovi)
- Terenska ogleda — fotografije, problematične točke
- Projekcija D96/TM (koordinatni sistem za Slovenijo)

---

## 3. Projektna dokumentacija (slovensko pravo)

### IDZ — Idejna Zasnova
- Najzgodnejša faza
- Prikaže **principielno rešitev** brez detajlov
- Vsebuje: groba trasa, predlagana arhitektura, ocena strank/km²
- Ni podlaga za gradbeno dovoljenje
- Zahtevano za: odločitev o investiciji, iskanje soglasij v principu

### PGD — Projekt za Gradbeno Dovoljenje
- Podlaga za **gradbeno dovoljenje** (GD)
- Vsebuje:
  - Situacijski načrt M 1:500 ali 1:1000 (trasa na ortofotu/katastru)
  - Opis omrežja in tehničnih rešitev
  - Soglasja upravljavcev komunalne in prometne infrastrukture
  - Vpliv na okolje
  - Požarni elaborat (za objekte)
- Pripravi pooblaščeni projektant (IZS licenca)

### PZI — Projekt za Izvedbo
- Detajlni **izvedbeni načrti** za gradbišče
- Vsebuje:
  - Detajlni profili tras (vzdolžni in prečni prerezi)
  - Kabelska knjiga (vsako vlakno, vsak spoj, vsaka cevi)
  - Shematski načrt logične topologije
  - Specifikacije materialov in opreme
  - Navodila za gradnjo
  - Zahteve za testiranje (OTDR parametri, acceptance criteria)

### As-Built dokumentacija
- **Dokumentacija kot-izvedeno** — odraža dejansko izvedbo
- Popravki glede na PZI (dejanska trasa ≠ načrtovana trasa)
- GIS vnos v omrežni informacijski sistem
- Kabelska knjiga update
- OTDR protokoli za vsak kabel
- Predaja naročniku + arhiviranje

---

## 4. Pridobivanje soglasij

### Ključni upravljavci in soglasja:

| Upravljavec | Soglasje za | Rok |
|---|---|---|
| **DRSI** (Direkcija RS za infrastrukturo) | Posegi v državne ceste | 30–60 dni |
| **Občina** | Posegi v občinske ceste, javne površine | 15–30 dni |
| **DARS** | Posegi ob avtocestah | 30–60 dni |
| **SODO** | Obešanje na elektro drogove | 30–90 dni |
| **Telekom Slovenije** | Skupna raba kanalizacije | Pogodbeno |
| **GZS / lastniki** | Polaganje po zasebnih parcelah | Individualno |
| **AKOS** | Registracija omrežja | — |
| **ZOJC** | Varstvo kulturne dediščine (stara mesta) | 30 dni |

### Zakon o cestah in telekomunikacijah:
- **ZEKom-2** daje pravico do polaganja kablov po javnih površinah
- Operater mora obvestiti lastnika infrastrukture
- **Načelo skupne rabe** — prednost obstoječi infrastrukturi pred novogradnjo

### Praktični postopek soglasij:
1. Pripravi PGD z načrti tras
2. Pošlji vloge vsem upravljavcem hkrati (vzporedno!)
3. Zberi soglasja (pogosto z roki in pogoji)
4. Vgradi pogoje soglasij v PZI
5. Med gradnjo obvesti upravljavce (začetek, konec del)
6. Po koncu: primopredajni zapisnik z upravljavci

---

## 5. Dimenzioniranje omrežja

### Kapacitetno planiranje — splitter nivo

**Vprašanje:** Koliko strank na en OLT port?

```
OLT port kapaciteta (GPON): 2.488 Gbps DS / 1.244 Gbps US
Ciljni throughput na stranko: 200 Mbps DS / 100 Mbps US
Predvidena penetracija:       40%
Overbooking ratio:            10:1 (realno) do 20:1

Strank na splitter 1:64:      64 fizičnih priključkov
Aktivnih strank (40%):        64 × 0.4 = ~26 aktivnih
Peak concurrent usage:        26 × 0.3 = ~8 hkratnih (80/20 pravilo)
Povprečna poraba:             8 × 200 Mbps = 1.6 Gbps  → GPON zadostuje
```

### Splitter placement strategija

**Centralizirana (1 splitter v CO):**
```
CO [1:64] ──────────────────────────── 64 strank
```
- + Manj opreme v terenu
- − Feeder mora imeti 64 vlaken do CO
- − Visoka odvisnost od enega splitterja
- − Menjava splitterja = izpad vseh 64 strank

**Porazdeljena (splitterji v FDH + ODP):**
```
CO ─── feeder 1 vlakno ─── FDH [1:4] ─┬─ ODP [1:16] ─ 16 strank
                                        ├─ ODP [1:16] ─ 16 strank
                                        ├─ ODP [1:16] ─ 16 strank
                                        └─ ODP [1:16] ─ 16 strank
```
- + Krajša feeder razdalja → boljši link budget
- + Fleksibilnejša nadgradnja
- + Manjše vlakno izpad pri okvari splitterja
- − Več opreme v terenu

**Priporočilo za United Fiber / Telemach:** porazdeljena 2-nivojska topologija.

---

## 6. Kapacitetno planiranje za blok (primer)

**Naloga:** Blokovsko naselje 10 blokov × 50 stanovanj = 500 stanovanj

**Rešitev:**

```
POP (v enem od blokov ali zunaj)
│
├── FDH v kleti bloka A ──── 2× OLT port × 1:4 splitter
│       ├── ODP nadstropje 1: 1:16 → 16 stanovanj
│       ├── ODP nadstropje 2: 1:16 → 16 stanovanj
│       ├── ODP nadstropje 3: 1:16 → 16 stanovanj
│       └── ODP nadstropje 4+: 1:16 → 12 stanovanj
│                                       Skupaj: 60 stanovanj/FDH
│
└── Podobno za vsak blok...
```

**Dimenzioniranje:**
- 1 OLT port GPON = 1:64 split = 64 strank max
- 500 stanovanj ÷ 64 = **8 OLT portov** (zaokroži na 10 + rezerva)
- 1 OLT linijska kartica = 8–16 portov → 1 kartica zadostuje
- 10 blokov × 1 FDH = **10 FDH omar**

---

## 7. Načrtovanje tras

### Prioriteta izbire trase:
1. **Obstoječa kanalizacija** (Telekom, T-2, Telemach, občinska) — najcenejše
2. **Skupni kablovod** z drugimi komunalnimi vodi
3. **Mikrotransa** vzdolž asfaltirane ceste
4. **Klasičen rov** v zelenicah ali cestah z nizkim prometom
5. **Nadzemno** — po obstoječih drogovih SODO ali Telekom

### Merila za trasiranje:
- Najkrajša pot med CO in strankami
- Izognitev problematičnim prečkanjem (vodotoki, železnice, AC)
- Minimizacija HDD-jev (drag)
- Upoštevanje bodoče gradnje (ceste, stavbe)
- Skupna raba z drugimi operaterji (ZEKom-2 obveznost)

---

## 8. Hitri povzetek — kar morate znati na razgovoru

1. IDZ → PGD (gradbeno dovoljenje) → PZI (izvedba) → as-built
2. Soglasja: DRSI (drž. ceste), občina (obč. ceste), SODO (drogovi)
3. ZEKom-2: pravica do polaganja po javnih površinah, skupna raba
4. Porazdeljen splitter (FDH + ODP) = boljša rešitev od centraliziranega
5. GPON port: 2.5G DS, pri 1:64 split in 40% penetraciji OK za rezidenčno
6. As-built = obvezna dokumentacija po gradnji, vnos v GIS
7. Fazna gradnja: najprej FDH, potem ODP, potem drop po naročilu
8. Prečkanja cest: HDD (vrtanje) ali zaščitna cev pod voziščem
