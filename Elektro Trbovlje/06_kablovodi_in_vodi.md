# 6. Kablovodi in nadzemni vodi

---

## 6.1 Kabelski sistemi — osnove

Kabel prenaša električno energijo med TP, RTP in odjemalci. Sestava kabla:
```
[Vodnik] → [Izolacija] → [Zaščitni plašč/oklop] → [Zunanji plašč]
```

### Materiali vodnikov
| Material | Simbol | ρ [Ω·mm²/m] | Prednosti | Slabosti |
|---|---|---|---|---|
| Baker (Cu) | Cu | 0,01786 | Manjši presek, bolj prilagodljiv | Dražji |
| Aluminij (Al) | Al | 0,02857 | Cenejši, lažji | Večji presek, oksidira |

**Distribucijsko omrežje**: pretežno aluminijevi kabli (cena, teža).

---

## 6.2 Vrste izolacije

| Oznaka | Material | Maks. temperatura | Uporaba |
|---|---|---|---|
| PVC (V) | Polivinilklorid | 70 °C | NN kabli, stari SN kabli |
| XLPE (X / 2X) | Zamreženi polietilen | 90 °C (trajno), 250 °C (kratki stik) | SN in VN kabli, NN |
| EPR | Etilen propilen guma | 90 °C | Prožni kabli |
| HEPR | Trda EPR | 90 °C | Kabli za vlago/kemikalije |

---

## 6.3 Oznake kablov (Nomenklatura)

### NN kabli

| Oznaka | Opis |
|---|---|
| **N** | Standardni kabel (nemška oznaka) |
| **A** | Aluminijevi vodniki (brez A = Cu) |
| **Y** | PVC izolacija |
| **2X** | XLPE izolacija |
| **H** | Brez halogena (LSZH) |
| **Y** (na koncu) | PVC zunanji plašč |
| **F** | Jeklena vrv armatura |
| **R** | Jeklene žice armatura (okrogla) |

**Primeri:**

| Oznaka | Pomen |
|---|---|
| NYY | Cu + PVC izolacija + PVC plašč |
| NAYY | Al + PVC + PVC |
| NA2XY | Al + XLPE + PVC |
| NA2XH | Al + XLPE + LSZH plašč (brez halogena) |
| NAYY-J | Al + PVC + PVC + PE (J = PE zunanji plašč) |

### SN kabli (srednja napetost)

| Oznaka | Pomen |
|---|---|
| NA2XS(F)2Y | Al + XLPE + Cu oklop + PE plašč |
| NA2XSY | Al + XLPE + Cu žični oklop + PVC plašč |
| NA2XS2Y | Al + XLPE + Cu folie oklop + PE plašč |

**Tipični SN kabel za 20 kV**: `NA2XS2Y 1×240/25 12/20 kV`
- 1 jedro, 240 mm² Al vodnik, 25 mm² Cu oklop, 12/20 kV

---

## 6.4 Ampaciteta (Current-carrying capacity)

Ampaciteta = maksimalni trajno dovoljeni tok pri določenih pogojih polaganja.

### Osnovna ampaciteta (iz tabel — SIST HD 60364)

Primer: kabel NA2XY 4×150 mm² Al, položen v tla:
- Osnovna ampaciteta ≈ 290 A

### Korekcijski faktorji

Ampaciteta se korigira z množilnimi faktorji:

| Faktor | Opis | Vrednosti |
|---|---|---|
| k1 | Temperatura tal | k1 = 1,0 (20 °C); k1 = 0,89 (25 °C) |
| k2 | Toplotna upornost tal | k2 = 1,0 (standardno); k2 < 1 (pesek, suha tla) |
| k3 | Skupinski faktor (số kablov v jarku) | k3 = 0,80 (2 kabla); 0,70 (3); 0,65 (4) |

```
I_dopustno = I_osnova · k1 · k2 · k3
```

### Primer izračuna

Kabel NA2XY 3×240 mm² Al, temperatura tal 25 °C, 3 kabli v jarku:
```
I_osnova = 420 A (iz tabele)
k1 = 0,89 (25 °C)
k3 = 0,70 (3 kabli skupaj)

I_dopustno = 420 · 0,89 · 0,70 = 261 A
```

---

## 6.5 Padec napetosti (Voltage drop)

### Formula (trifazno)
```
ΔU [V] = √3 · I · L · (R · cos φ + X · sin φ)

R = r0 · L     [Ω]   (r0 = specifična upornost na m)
X = x0 · L     [Ω]   (x0 = specifična reaktanca na m)

ΔU% = ΔU / Un · 100
```

### Specifična upornost in reaktanca

| Vodnik | Presek [mm²] | r0 [Ω/km] @ 70 °C | x0 [Ω/km] |
|---|---|---|---|
| Al | 50 | 0,868 | 0,09 |
| Al | 95 | 0,443 | 0,085 |
| Al | 150 | 0,293 | 0,082 |
| Al | 240 | 0,185 | 0,08 |

### Mejne vrednosti padca napetosti
| Omrežje | Meja |
|---|---|
| NN omrežje (od TP do hišnega priključka) | ≤ 4 % (SIST HD 60364) |
| NN notranja instalacija | ≤ 4 % |
| SN omrežje | ≤ 5 % |

### Primer izračuna ΔU%
```
Odsek: NA2XY 150 mm² Al, L = 300 m, I = 180 A, cos φ = 0,9, Un = 400 V

r0 = 0,293 Ω/km = 0,000293 Ω/m
x0 = 0,082 Ω/km = 0,000082 Ω/m

R = 0,000293 · 300 = 0,0879 Ω
X = 0,000082 · 300 = 0,0246 Ω

sin φ = √(1 - 0,9²) = 0,436

ΔU = √3 · 180 · (0,0879 · 0,9 + 0,0246 · 0,436)
ΔU = 1,732 · 180 · (0,079 + 0,0107)
ΔU = 1,732 · 180 · 0,0897 = 27,95 V

ΔU% = 27,95 / 400 · 100 = 6,99 % → PREKORAČENA MEJA (> 4 %)
→ Povečaj presek kabla!
```

---

## 6.6 Termična obremenitev pri kratkem stiku

Kabel mora prenesti toploto kratko-stičnega toka dokler zaščita ne izklopi.

### Formula
```
A_min = (I_kc · √t_kc) / k

A_min — minimalni presek [mm²]
I_kc  — tok kratkega stika [A]
t_kc  — čas trajanja kratkega stika [s]
k     — koeficient materiala
         Cu: k = 143 (PVC), 176 (XLPE)
         Al: k = 94 (PVC), 116 (XLPE)
```

### Primer
```
I_kc = 10 kA, t_kc = 0,5 s, Al vodnik XLPE

A_min = (10 000 · √0,5) / 116 = (10 000 · 0,707) / 116 = 61 mm²

→ Kabel 95 mm² Al je dovolj.
```

---

## 6.7 Polaganje zemeljskih kablov

### Zahteve za polaganje (Pravilnik o tehničnih pogojih)

| Parameter | Zahteva |
|---|---|
| Globina polaganja NN kabla | ≥ 0,6 m (normalno), ≥ 1,0 m (pod cesto) |
| Globina SN kabla | ≥ 0,8 m (normalno), ≥ 1,2 m (pod cesto) |
| Pesek/gramoz pod in nad kablom | 10 cm sloj |
| Opozorilni trak | Rdeča barva (NN), rumena (SN), 25 cm nad kablom |
| Min. odmik od vodovoda | 0,5 m vzporedno, 0,3 m pri prečkanju |
| Min. odmik od plinovoda | 1,0 m vzporedno |
| Min. radij upogibanja | ≥ 15 × zunanji premer kabla |

### Zaščitne cevi
- PVC, PE ali betonske cevi pri prehodih pod cestami, stavbami
- Premer cevi ≥ 1,5 × zunanji premer kabla

---

## 6.8 Nadzemni vodi (Overhead lines)

### NN nadzemni vodi

**Samonosni snop (SNS / ABC — Aerial Bundled Conductor)**
- Skup 4 izoliranihAluminijevih vodnikov (3 faze + N)
- Izolirani → brez razmika od stavb, dreves
- Tipični preseki: 16, 25, 50, 70, 95 mm² Al

**Goli vodi (redko, stari):**
- Al/Fe (aluminijast vodnik z jekleno ojačitvijo)
- Označba: npr. Al 70/11 (70 mm² Al, 11 mm² Fe)

### SN nadzemni vodi

**Goli vodi:**
- Al/Fe vrvi, tipični preseki: 35, 50, 70, 95, 120 mm²
- Linijska razdalja (razpon) med drogovi: 80–150 m

**Izolirani SN vodi:**
- Izolirani AlFe vodi (delno izolirani — zaščiteni pred dotikom vej)
- Zmanjšajo število prekinitev (manj napak od dreves)

### Drogovi
| Tip | Material | Uporaba |
|---|---|---|
| Leseni drog | Impregniran bor | Manj obremenjena področja |
| Betonski drog | Prednapeti beton | Standardni v SN omrežju |
| Jekleni drog | Cevasta konstrukcija | Velike razpetine, koti |

### Razdalje za SN nadzemni vod (20 kV goli)

| Situacija | Min. razdalja |
|---|---|
| Nad cesto (normalna) | ≥ 6 m |
| Nad avtocesto | ≥ 7 m |
| Od zgradbe (stran) | ≥ 2 m |
| Med vodi (med fazami) | ≥ 1 m |

---

## 6.9 Zaščita kablov

### Mehanska zaščita
- Armatura (jeklene žice ali folija)
- PVC ali PE zunanji plašč

### Zaščita pred vlago
- Polietilenska bariera (PE plašč)
- Alu-PE laminat oklop

### Katodna zaščita
- Za jeklene cevovode in oklope dolžinskih kablov
- Naložena napetost prepreči korozijo

---

## Povzetek — izbira preseka kabla

1. **Ampaciteta**: I_vodnik ≥ I_obratovalni (upoštevaj korekcijske faktorje)
2. **Padec napetosti**: ΔU% ≤ 4 % (NN)
3. **Termična trdnost**: preveriti pri I_kc in t_kc zaščite
4. **Selektivnost zaščit**: preveriti koordinacijo z nadrejenim zaščitnim elementom

Izberi večji presek od vseh zgornji pogojev.
