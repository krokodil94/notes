# Link Budget in Optični Izračuni

## 1. Osnove link budgeta

**Optical Power Budget** = razlika med oddajno močjo in sprejemno občutljivostjo.

```
Budget (dB) = P_TX (dBm) − P_RX_min (dBm)
```

Vsota vseh izgub na traktu mora biti **manjša** od budgeta:
```
Budget ≥ Σ Izgub_komponente + Varnostna_marža
```

---

## 2. GPON razredi moči

### ITU-T G.984.2 optični razredi:

| Razred | TX OLT | RX OLT (sens.) | TX ONT | RX ONT (sens.) | Budget |
|---|---|---|---|---|---|
| **B+** | +1.5 do +5 dBm | −28 dBm | −1 do +4 dBm | −27 dBm | **28 dB** |
| **C+** | +3 do +7 dBm | −32 dBm | −1 do +4 dBm | −30 dBm | **32 dB** |
| **C++** | +3 do +7 dBm | −35 dBm | −1 do +4 dBm | −33 dBm | **35 dB** |

> **Praktično:** večina deploymentov = razred B+ (za 1:32 do 10 km) ali C+ (za 1:64 ali daljše trase).

### XGS-PON razredi (ITU-T G.9807.1):

| Razred | Budget |
|---|---|
| N1 | 29 dB |
| N2 | 31 dB |
| E1 | 33 dB |
| E2 | 35 dB |

---

## 3. Komponente izgub

### Referenčne vrednosti za izračun:

| Komponenta | Izguba |
|---|---|
| Fusion splice | 0.05–0.1 dB (tipično 0.1 dB konzervativno) |
| Konektor SC/APC (par) | 0.3–0.5 dB (tipično 0.5 dB) |
| Vlakno G.652.D @ 1310 nm | 0.35 dB/km |
| Vlakno G.652.D @ 1490 nm | 0.25 dB/km |
| Vlakno G.652.D @ 1550 nm | 0.20 dB/km |
| Splitter 1:2 PLC | 3.7 dB |
| Splitter 1:4 PLC | 7.1 dB |
| Splitter 1:8 PLC | 10.5 dB |
| Splitter 1:16 PLC | 13.7 dB |
| Splitter 1:32 PLC | 17.0 dB |
| Splitter 1:64 PLC | 20.5 dB |
| WDM combiner | 0.5–1.0 dB |

### Varnostna marža (Safety Margin):
- **Priporočena: 3 dB** za staranje komponent, degradacijo konektorjev
- Nekateri operaterji: 2 dB (bolj optimistično)
- Za visoko-zanesljive trase: 4–5 dB

---

## 4. Primer 1 — Osnovni izračun (1:32, 3 km)

**Topologija:**
```
OLT → konektor → feeder 3 km → FDH (splitter 1:32) → 200 m drop → ONT
```

**Komponente izgub:**

| Komponenta | Izguba |
|---|---|
| Konektor OLT izhod | 0.5 dB |
| Feeder kabel 3 km @ 1490 nm × 0.25 dB/km | 0.75 dB |
| Fusion splice v feederju (15 × 0.1 dB) | 1.5 dB |
| Konektor pred splitterjem | 0.5 dB |
| Splitter 1:32 | 17.0 dB |
| Konektor za splitterjem | 0.5 dB |
| Drop kabel 200 m @ 1490 nm × 0.25 dB/km | 0.05 dB |
| Konektor ONT | 0.5 dB |
| **SKUPAJ** | **21.3 dB** |

**Preverba z razredom B+:**
```
Budget B+:     28.0 dB
Skupne izgube: 21.3 dB
Marža:         28.0 − 21.3 = 6.7 dB
Varnostna (3 dB):  6.7 − 3.0 = 3.7 dB rezerva ✅
```

**Zaključek:** Razred B+ zadostuje.

---

## 5. Primer 2 — 1:64 split, 5 km, ali B+ zadostuje?

**Topologija:**
```
OLT → konektor → feeder 5 km → FDH (1:4) → 1 km distribution → ODP (1:16) → 100 m drop → ONT
```

**Kaskadni splitter: 1:4 × 1:16 = 1:64**

**Komponente izgub:**

| Komponenta | Izguba |
|---|---|
| Konektor OLT izhod | 0.5 dB |
| Feeder 5 km @ 1490 nm | 1.25 dB |
| Splice feeder (25 × 0.1) | 2.5 dB |
| Konektor pri FDH | 0.5 dB |
| Splitter 1:4 (FDH) | 7.1 dB |
| Konektor za splitterjem | 0.5 dB |
| Distribution kabel 1 km | 0.25 dB |
| Splice distribution (5 × 0.1) | 0.5 dB |
| Konektor pri ODP | 0.5 dB |
| Splitter 1:16 (ODP) | 13.7 dB |
| Konektor za splitterjem | 0.5 dB |
| Drop kabel 100 m | 0.025 dB |
| Konektor ONT | 0.5 dB |
| **SKUPAJ** | **27.8 dB** |

**Preverba z razredom B+:**
```
Budget B+:     28.0 dB
Skupne izgube: 27.8 dB
Surova marža:  0.2 dB — PREMALO!
Varnostna (3 dB):  0.2 − 3.0 = −2.8 dB ❌ FAIL
```

**Preverba z razredom C+:**
```
Budget C+:     32.0 dB
Skupne izgube: 27.8 dB
Marža:         4.2 dB
Varnostna (3 dB):  4.2 − 3.0 = 1.2 dB rezerva ✅ (tesno)
```

**Zaključek:** Za to topologijo potrebuješ **razred C+** ali zmanjšaš dolžino feederja / splitter nivo.

---

## 6. Primer 3 — Co-existence GPON + XGS-PON

Obe tehnologiji na istem vlaknu:

**GPON downstream @ 1490 nm:**
```
OLT (1490 nm) → WDM Coupler (0.5 dB izguba) → splitter → ONT
```

**XGS-PON downstream @ 1577 nm:**
```
OLT (1577 nm) → WDM Coupler (0.5 dB izguba) → splitter → ONT
```

Pri link budgetu za koeksistenco dodaj **0.5 dB** za WDM coupler!

---

## 7. OTDR Merjenje

### Princip (Time Domain Reflectometry):

```
OTDR pošlje laserski pulz ──────────────────────►
                                   ↩ rayleigh sipanje (šibek odboj) 
                         ↩ konektor ali spoj (odboj)
                                                ↩ konec vlakna (fresnel odboj)
```

OTDR izmeri čas od pošiljanja do prejema odbitega signala:
```
Razdalja = (c/n × t) / 2
```
- c = hitrost svetlobe (3×10⁸ m/s)
- n = lomni količnik vlakna (≈1.468 za SMF)
- t = čas potovanja tam in nazaj

### Odčitavanje OTDR trace:

```
dBm
 |
 |─────╮          ← Fresnel odboj pri konektorju
 |      ╲
 |       ╲────────╮   ← Izguba na spojnici/splicu
 |                 ╲
 |                  ╲─────────────────────────── ← Rayleigh sipanje (naklon = slabitev)
 |                                              ↑ konec vlakna
 +──────────────────────────────────────────────►  razdalja [km]
```

**Kar iščeš na OTDR trace:**
- Naklon = slabitev kabla (dB/km)
- "Step down" = izguba na konektorju ali splicu
- "Step up" = napaka (gainer event) — verjetno mehanski spoj ali vlaga
- Konec vlakna = izrazit odboj ali padec

### OTDR parametri:

| Parameter | Tipična vrednost |
|---|---|
| Wavelength | 1310 nm (US), 1490 nm (DS) ali 1550 nm |
| Pulse width | 10 ns (kratke razdalje) do 1000 ns (dolge) |
| Range | 20–100 km |
| Event deadzone | 1–5 m (ne vidiš dveh bližnjih eventov) |
| Attenuation deadzone | 5–50 m |

### Kdaj meriti:

| Faza | Meritev |
|---|---|
| Sprejem kabla | OTDR preverba kabla — primerjava s tovarniškimi protokoli |
| Po polaganju | OTDR celotne trase — odkrivanje poškodb pri gradnji |
| Po varjenju | OTDR potrditev splices < 0.1 dB |
| Ob predaji | Celoten prevzemni protokol (OTDR + power meter) |
| Ob okvari | Lokalizacija napake (razdalja do napake) |

### OTDR za PON — izzivi:

OTDR ne more izmeriti čez splitter direktno (splitter uniči signal za nazaj).

**Rešitve:**
1. Meriti vsak arm splitterja posebej (dostop pri ODP)
2. Uporabiti PON OTDR mode (posebni instrumenti)
3. OTDR z monitoringom z OLT side (nekateri OLT-ji imajo)

---

## 8. Power Meter meritev

Poleg OTDR se vedno izmeri dejanska optična moč:

```
Merilnik moči (Power Meter) na ONT koncu:
  → Izmeri dejansko prejeto moč v dBm
  → Primerjaj z izračunanim link budgetom
  → Razlika > 2 dB = poišči napako
```

**Sprejemljivi rang za GPON ONT:**
- Min: −27 dBm (razred B+)
- Max: −8 dBm (saturacija — preblizu OLT ali preskocil splitter)
- Alarm: zunaj tega ranga = napaka

---

## 9. Naloga — Co-preverba

**Podatki:**
- OLT GPON razred C+, TX = +5 dBm
- Feeder: 8 km, G.652.D @ 1490 nm
- Splitter v FDH: 1:8
- Splitter v ODP: 1:8 (kaskada = 1:64)
- Drop kabel: 300 m
- Konektorji: 4 para SC/APC
- Splice-i: 40 skupaj (feeder + distribution + drop)

**Izračunaj: ali razred C+ zadostuje z varnostno maržo 3 dB?**

**Rešitev:**

| Komponenta | Izguba |
|---|---|
| 4 konektorji × 0.5 dB | 2.0 dB |
| Feeder 8 km × 0.25 dB/km | 2.0 dB |
| 40 splice × 0.1 dB | 4.0 dB |
| Splitter 1:8 (FDH) | 10.5 dB |
| Splitter 1:8 (ODP) | 10.5 dB |
| Drop 300 m × 0.25 dB/km | 0.075 dB |
| **SKUPAJ** | **29.1 dB** |

```
Budget C+:  32 dB
Izgube:     29.1 dB
Marža:      2.9 dB
Varnostna:  2.9 − 3.0 = −0.1 dB  ← TESNO! Praktično ni marže.
```

**Zaključek:** Razred C+ komaj zadostuje. Priporočam:
- Zmanjšaj feeder razdaljo (boljši splitter placement)
- Poveži stranke bližje ODP (krajši drop)
- Ali poveča razred na C++ (budget 35 dB) za zadostno maržo

---

## 10. Hitri povzetek — kar morate znati na razgovoru

1. Budget = TX − RX_sensitivity; izgube morajo biti < budget − marža
2. B+ budget ≈ 28 dB, C+ ≈ 32 dB
3. Splitter 1:32 = 17 dB, 1:64 = 20.5 dB
4. Konektor ≈ 0.5 dB, splice ≈ 0.1 dB, vlakno @ 1490 nm ≈ 0.25 dB/km
5. Varnostna marža 3 dB vedno dodaj
6. OTDR meri razdaljo in slabitev z laserskim pulzom
7. OTDR ne meri čez splitter — meriti vsak krak posebej
8. Power meter = dejanska prejeta moč v dBm
9. GPON ONT sprejemni rang: −8 do −27 dBm (razred B+)
10. Če link budget ne zadostuje: krajši feeder, nižji split, višji razred OLT
