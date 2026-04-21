# Osnove optičnih vlaken

## 1. Kako svetloba potuje po vlaknu

Optično vlakno izkorišča **totalni notranji odboj** (Total Internal Reflection):
- Jedro (core) ima višji lomni količnik (n₁) kot plašč (cladding, n₂)
- Svetloba se pri kotih večjih od kritičnega kota odbija nazaj v jedro
- Svetloba potuje brez izhoda vzdolž vlakna

```
         n₂ (cladding, nižji n)
    ─────────────────────────────
    →→→→→→→→→→→→→→→→→→→→→→→→→→→  jedro (n₁, višji n)
    ─────────────────────────────
         n₂ (cladding)
```

**Numerična apertura (NA):**
```
NA = √(n₁² − n₂²)
```
- Tipična vrednost: NA ≈ 0.12–0.14 za SMF
- Večja NA = večji kot sprejema svetlobe

---

## 2. Monomodna (SMF) vs multimodalna vlakna (MMF)

| Lastnost | SMF (Single-Mode) | MMF (Multi-Mode) |
|---|---|---|
| Premer jedra | 8–10 µm | 50 ali 62.5 µm |
| Premer plašča | 125 µm | 125 µm |
| Razdalja | do 80+ km | do 2 km |
| Pasovna širina | neomejena (praktično) | omejena (modalna disperzija) |
| Cena vlakna | nižja | višja |
| Cena oddajnika | višja (laserji) | nižja (LED, VCSEL) |
| Tipična uporaba | Telco, WAN, FTTx | LAN, podatkovni centri |

**Za FTTH se vedno uporablja SMF** — dolge razdalje, laser oddajniki.

---

## 3. Ključni standardi vlaken

### ITU-T G.652 — Standard SMF
Najpogosteje uporabljena vlakna za dostopovna omrežja.

| Podtip | Lastnost | Uporaba |
|---|---|---|
| G.652.A | Osnovno SMF | Splošno |
| G.652.B | Nizka PMD | Visoke hitrosti |
| G.652.C | Nizka slabitev @ 1383 nm (OH-peak free) | WDM |
| G.652.D | Kombinacija B+C | **Standard za FTTH** |

### ITU-T G.657 — Bend-Insensitive Fiber
Vlakno odporno na upogib — **ključno za FTTH drop kable in instalacijo v stavbah.**

| Podtip | Min. polmer upogiba | Prekoračitev slabitve |
|---|---|---|
| G.657.A1 | 10 mm | ≤0.5 dB @ 1550 nm |
| G.657.A2 | 7.5 mm | ≤0.5 dB @ 1550 nm |
| G.657.B2 | 7.5 mm | Strožji |
| G.657.B3 | 5 mm | Najstrožji — za instalacijo v vogalih |

**Praktično:** drop kabel od ODP do ONT = G.657.A2 ali boljši.

---

## 4. Slabitev (Attenuation)

Slabitev je izguba moči svetlobe vzdolž vlakna, izražena v **dB/km**.

### Tipične vrednosti za G.652.D:

| Valovna dolžina | Slabitev |
|---|---|
| 1310 nm | ≤ 0.35 dB/km |
| 1383 nm (OH peak) | ≤ 0.4 dB/km (G.652.D je brez tega!) |
| 1490 nm | ≤ 0.25 dB/km |
| 1550 nm | ≤ 0.20 dB/km |
| 1625 nm | ≤ 0.24 dB/km |

**Zakaj 1550 nm za dolge razdalje?** Najnižja slabitev.
**Zakaj 1310 nm za PON upstream?** Poceni oddajniki, sprejemljiva slabitev.

### Vzroki slabitve:
- **Absorpcija** — OH ioni (voda v vlaknu), UV/IR absorpcija materiala
- **Rayleigh sipanje** — sipanje na mikroskopskih nehomogenostih silicija
- **Makro upogib** — prevelik radij upogiba vlakna
- **Mikro upogib** — mikroskopske deformacije osi vlakna

---

## 5. Disperzija

Disperzija = razširjanje svetlobnega pulza → omeji pasovno širino.

### Kromatična disperzija (CD)
Različne valovne dolžine potujejo z različnimi hitrostmi.
- Enota: ps/(nm·km)
- G.652: ≤18 ps/(nm·km) @ 1550 nm
- Problem pri: WDM, dolge razdalje, visoke hitrosti

### Modalna disperzija
- Samo pri MMF — različni modi potujejo po različnih poteh
- Pri SMF ni modalnih težav (samo en mod)

### Polarizacijska modna disperzija (PMD)
- Dve polarizaciji potujeta z rahlo različno hitrostjo
- Problem pri 10G+ in 40G+
- G.652.B/D ima nizek PMD koeficient

---

## 6. Optical Return Loss (ORL)

**ORL** = mera odboja svetlobe nazaj proti viru.

```
ORL (dB) = 10 × log₁₀(P_vhod / P_odboj)
```

Večji ORL = manj odboja = **boljše**.

| Konektor | ORL |
|---|---|
| SC/UPC (ravna pola) | > 50 dB |
| SC/APC (8° kot) | > 60 dB |

### Zakaj SC/APC za PON?
GPON OLT oddajnik je Fabry-Perot ali DFB laser — **občutljiv na odboje**.
Odboji povzročijo nestabilnost laserja, šum, napake.
SC/APC (zeleni konektor) z 8° polirano površino odbije svetlobo stran od osi = >60 dB ORL.

> **Pravilo:** vse PON povezave = SC/APC. Nikoli SC/UPC na traktu do stranke.

---

## 7. Valovne dolžine v PON omrežjih

### GPON (ITU-T G.984.2)

```
OLT → ONT (Downstream):  1490 nm
ONT → OLT (Upstream):    1310 nm
CATV (opcija):           1550 nm (RF overlay)
```

### XGS-PON (ITU-T G.9807.1)

```
OLT → ONT (Downstream):  1577 nm
ONT → OLT (Upstream):    1270 nm
```

### Koeksistenca GPON + XGS-PON na isti infrastrukturi

```
1270 nm ──────────────────────────────── XGS-PON US
1310 nm ──────────────────────────────── GPON US
1490 nm ──────────────────────────────── GPON DS
1577 nm ──────────────────────────────── XGS-PON DS
```

WDM filter pri OLT ločuje valovne dolžine → isti splitter, isto vlakno, različne stranke!

---

## 8. dB in dBm — računanje

### dBm = absolutna moč

```
P(dBm) = 10 × log₁₀(P_mW / 1 mW)
```

| mW | dBm |
|---|---|
| 0.001 mW | −30 dBm |
| 0.1 mW | −10 dBm |
| 1 mW | 0 dBm |
| 2 mW | +3 dBm |
| 10 mW | +10 dBm |

### dB = relativna vrednost (izguba ali ojačanje)

```
Izguba(dB) = P_vhod(dBm) − P_izhod(dBm)
```

### Ključno pravilo:
- **dBm − dB = dBm** (odštejemo izgube od moči)
- **dBm − dBm = dB** (razlika dveh moči = izguba)

### Praktični primer:
```
TX moč OLT:          +5 dBm
Slabitev kabla 3 km: −1.05 dB  (3 × 0.35)
Splitter 1:32:       −17 dB
Konektor × 2:        −1 dB
────────────────────────────
Prejeta moč:         +5 − 1.05 − 17 − 1 = −14.05 dBm
RX občutljivost ONT: −27 dBm
Marža:               −14.05 − (−27) = 12.95 dB ✓
```

---

## 9. Hitri povzetek — kar morate znati na razgovoru

1. SMF jedro = 8–10 µm, za dolge razdalje, za PON
2. G.652.D = standard FTTH feeder/distribution kabel
3. G.657.A2 = drop kabel, odporen na upogib
4. Slabitev @ 1310 nm ≈ 0.35 dB/km, @ 1550 nm ≈ 0.20 dB/km
5. SC/APC (zeleni) za PON — zakaj: ORL >60 dB, laserji občutljivi na odboj
6. GPON DS = 1490 nm, US = 1310 nm
7. XGS-PON DS = 1577 nm, US = 1270 nm
8. dBm je absolutna moč, dB je razlika/izguba
9. Izguba splitterja 1:32 ≈ 17 dB
