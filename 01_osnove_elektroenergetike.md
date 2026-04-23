# 1. Osnove elektroenergetike

---

## 1.1 Enofazni in trifazni sistemi

### Enofazni sistem
- Napetost med fazo in nevtralo: **U = 230 V** (v Sloveniji)
- Frekvenca: **50 Hz**
- Valovna dolžina: 20 ms (T = 1/f)

### Trifazni sistem (Three-phase system)
- Tri sinusne napetosti, zamaknjene za **120°**
- Fazna napetost (Phase voltage): **Up = 230 V**
- Linijska napetost (Line voltage): **UL = Up · √3 ≈ 400 V**
- Razmerje: UL / Up = √3 ≈ 1,732

```
Faze: L1 (rdeča), L2 (rumena), L3 (modra)
Nevtrala: N (modra / siva)
Zaščitni vodnik: PE (rumeno-zelena)
```

---

## 1.2 Električna moč (Electrical Power)

### Vrste moči

| Simbol | Ime | Enota | Opis |
|---|---|---|---|
| P | Dejavna moč (Active power) | W, kW, MW | Koristna moč (toplota, mehanski delo) |
| Q | Jalova moč (Reactive power) | var, kvar, Mvar | Moč za vzpostavljanje magnetnega polja |
| S | Navidezna moč (Apparent power) | VA, kVA, MVA | Vektorska vsota P in Q |

### Zveze med močmi

```
S² = P² + Q²

S = U · I             (enofazno)
S = √3 · UL · IL      (trifazno)

cos φ = P / S         (faktor moči / power factor)
sin φ = Q / S

P = S · cos φ
Q = S · sin φ
```

### Primer: transformator 630 kVA, cos φ = 0,8
```
P = 630 · 0,8 = 504 kW
Q = 630 · 0,6 = 378 kvar
```

### Kompenzacija jalove moči
- Jalova moč bremeni omrežje brez koristnega učinka
- Kompenziramo z **kondenzatorskimi baterijami**
- Cilj: cos φ ≥ 0,95 (zahteva distribucijskega operaterja)

---

## 1.3 Napetostni nivoji v Sloveniji

| Raven | Oznaka | Napetost | Uporaba |
|---|---|---|---|
| Prenosno omrežje | VN (visoka napetost) | 110 kV, 220 kV, 400 kV | Prenos električne energije |
| Distribucijsko omrežje — SN | SN (srednja napetost) | 10 kV, 20 kV, 35 kV | Napajanje TP, industrija |
| Distribucijsko omrežje — NN | NN (nizka napetost) | 0,4 kV (400/230 V) | Gospodinjstva, mali odjemalci |

**Elektro Ljubljana pretežno uporablja 20 kV SN omrežje.**

---

## 1.4 Ohmov zakon in Kirchhoffovi zakoni

### Ohmov zakon
```
U = R · I
I = U / R
R = U / I
```

Za izmenični tok (AC):
```
U = Z · I
Z = √(R² + X²)        (impedanca)
X = XL - XC           (reaktanca)
XL = 2π · f · L       (induktivna reaktanca)
XC = 1 / (2π · f · C) (kapacitivna reaktanca)
```

### 1. Kirchhoffov zakon — tokovni zakon (KCL)
Vsota tokov v vozlišču je nič:
```
∑ I = 0
I_vhod = I_izhod
```

### 2. Kirchhoffov zakon — napetostni zakon (KVL)
Vsota napetosti v zanki je nič:
```
∑ U = 0
```

---

## 1.5 Kratki stik (Short circuit)

### Vrste kratkih stikov

| Vrsta | Opis | Pogostost |
|---|---|---|
| Trifazni (3F) | Kratki stik vseh treh faz | Redek, največji tok |
| Dvofazni (2F) | Kratki stik dveh faz | Pogostejši |
| Dvofazni z zemljo (2FE) | Dve fazi + zemlja | — |
| Enofazni (1F) | Ena faza + zemlja | Najpogostejši |

### Izračun kratkega stika (metoda impedanc)

```
I"k = c · Un / (√3 · Zk)

Zk = √(Rk² + Xk²)     (skupna impedanca kratvstičnega tokokroga)
c  = 1,1               (napetostni faktor za Imax)
c  = 0,95              (napetostni faktor za Imin)
Un = nazivna napetost omrežja
```

### Pomen kratkega stika za projektiranje
- **Icc max** → dimenzioniranje stikalnih naprav (odklopna moč)
- **Icc min** → nastavitev zaščitnih relejev (mora zaznati minimalni kratki stik)
- **Termična obremenitev** → preverjanje kablov in vodnikov (I²t)
- **Dinamična obremenitev** → mehanska trdnost zbiralk

---

## 1.6 Simetrične komponente (Symmetrical Components)

Fortescuejeva metoda za analizo nesimetričnih razmer:

```
Vsak nesimetričen trofazni sistem = vsota treh simetričnih komponent:

Pozitivno zaporedna komponenta (positive sequence): I1 — normalne razmere
Negativno zaporedna komponenta (negative sequence): I2 — nesimetrija
Ničelna zaporedna komponenta (zero sequence):       I0 — zemeljski stik
```

### Praktični pomen
- Ničelna komponenta → teče pri enofaznem kratkem stiku
- Diferenčna zaščita zazna razliko I1 - I2
- IT omrežje: ničelna komponenta ne teče → zaščita ne zazna enofaznega stika

---

## 1.7 Padec napetosti (Voltage drop)

### Izračun
```
ΔU = √3 · I · L · (R · cos φ + X · sin φ)    [V, trifazno]
ΔU% = ΔU / Un · 100                           [%]

R = ρ · L / A      (specifična upornost · dolžina / presek)
ρ(Al) ≈ 0,028 Ω·mm²/m
ρ(Cu) ≈ 0,0175 Ω·mm²/m
```

### Dopustne meje po SIST EN 50160
| Omrežje | Dopustni ΔU% |
|---|---|
| NN omrežje (od TP do priključka) | ≤ 4 % (normalna) |
| SN omrežje | ≤ 5 % |
| Interna NN instalacija | ≤ 4 % (SIST HD 60364) |

---

## 1.8 Specifična upornost materialov

| Material | ρ [Ω·mm²/m] pri 20°C | Korektura na 70°C (α·ΔT) |
|---|---|---|
| Baker (Cu) | 0,01786 | × 1,20 ≈ 0,0214 |
| Aluminij (Al) | 0,02857 | × 1,20 ≈ 0,0343 |
| Jeklo (Fe) | 0,138 | — |

---

## 1.9 Električna energija in moč

```
W = P · t              [Wh, kWh]
1 kWh = 3 600 000 J = 3,6 MJ

Izgube v kablu:
P_izgube = I² · R · L  [W]
```

**Letne izgube v distribucijskem omrežju** so ena od ključnih kazalnikov kakovosti omrežja.

---

## Povzetek — ključne formule

| Formula | Pomen |
|---|---|
| UL = √3 · Up | Linijska ↔ fazna napetost |
| S = √3 · UL · IL | Trifazna navidezna moč |
| cos φ = P / S | Faktor moči |
| I"k = c·Un / (√3·Zk) | Tok kratkega stika |
| ΔU% = ΔU/Un · 100 | Relativni padec napetosti |
