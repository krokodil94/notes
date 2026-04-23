# 2. Distribucijsko omrežje

---

## 2.1 Struktura distribucijskega omrežja

Distribucijsko omrežje prenaša električno energijo od razdelilnih transformatorskih postaj (RTP) do končnih odjemalcev.

```
Prenosno omrežje (110/220/400 kV)
        ↓
RTP — Razdelilna transformatorska postaja (110/20 kV)
        ↓
SN omrežje (20 kV)
        ↓
TP — Transformatorska postaja (20/0,4 kV)
        ↓
NN omrežje (0,4 kV)
        ↓
Odjemalci (gospodinjstva, podjetja)
```

---

## 2.2 Topologije distribucijskega omrežja

### Radialna (vejična) topologija
- Najcenejša, najpreprosta
- Vsaka TP napajana iz ene smeri
- Slabost: izpad nadrejenega elementa = izpad vseh odjemalcev pod njim
- Uporaba: podeželska območja, redko poseljena področja

```
RTP ——— TP1 ——— TP2 ——— TP3
```

### Zankasta topologija (odprta zanka / open ring)
- Zanka je fizično zaprta, a normalno odprta na enem mestu (NO stikalo)
- Ob okvari: preureditev — odpre se nova stikala, zapre NO stikalo
- Čas preurejanja: ročno 1–4 ure, avtomatizirano < 5 minut
- Uporaba: mestna in primestna območja

```
RTP ——— TP1 ——— TP2 ——[NO]——— TP3 ——— RTP
```

### Mrežna topologija
- Vsaka točka napajana iz več smeri hkrati
- Največja zanesljivost, a drag kabelski sistem
- Zahteva posebno zaščito (usmerjene zaščite)
- Uporaba: mestna jedra, kritična infrastruktura

---

## 2.3 SN omrežje (Srednja napetost / Medium voltage)

### Karakteristike
- Napetost: **20 kV** (Elektro Ljubljana), drugod tudi 10 kV in 35 kV
- Izvedba: **kablovodi** (mesta) ali **nadzemni vodi** (podeželje)
- Normalni obratovalni tok: 200–600 A
- Kratki stik: I"k = 8–16 kA (odvisno od mesta v omrežju)

### Stikalne naprave na SN
| Naprava | Funkcija |
|---|---|
| Odklopnik (Circuit breaker) | Odpira tokokrog pod bremenom in pri kratkem stiku |
| Ločilnik (Disconnector) | Odpira brez bremena (le za galvansko ločitev) |
| Bremenstikalo (Load switch) | Odpira pod bremenom, ne pri kratkem stiku |
| Varovalo (Fuse) | Pregorevanje ob prekoračitvi toka |
| Reklozer (Recloser / AVR) | Samodejna ponovna vklop |

### SN kabli
- Pogosta oznaka: **XLPE izolacija** (zamreženi polietilen)
- Tipični preseki: 50, 95, 150, 240 mm² Al
- Oznake: NA2XS2Y, NA2XSY (kovinsko zaščiteni)

---

## 2.4 NN omrežje (Nizka napetost / Low voltage)

### Karakteristike
- Napetost: **0,4 kV** (400 V med fazami, 230 V faza-nevtrala)
- Izvedba: kablovodi (pogosto) ali nadzemni vodi (samonosni snopi — SNS)
- Dolžina kablovodnih odsekov: tipično 100–500 m
- Dopustni padec napetosti: **≤ 4 %**

### NN kabli
| Oznaka | Izolacija | Vodnik | Uporaba |
|---|---|---|---|
| NAYY | PVC | Al | Zemeljski kabel |
| NA2XY | XLPE | Al | Zemeljski kabel |
| NYY | PVC | Cu | Zemeljski kabel |
| SNS | XLPE | Al | Samonosni nadzemni snop |

### NN zbiralke in RG (Razvodni garnitur)
- Vsaka TP ima nizkonapetostni razvod (RG)
- Iz RG izhajajo NN kablovodi (iztoki) do odjemalcev
- Varovanje iztokov: NH varovalo (NN), odklopnik

---

## 2.5 Razdelilna transformatorska postaja (RTP)

### Funkcija
- Sprejme energijo iz prenosnega omrežja (110 kV)
- Pretvori na SN nivo (20 kV)
- Razdeli v SN omrežje (tipično 10–30 SN izvodov)

### Oprema RTP
- Transformatorji 110/20 kV (10–63 MVA)
- VN stikalno polje (SF6 ali vakuumski odklopniki)
- SN zbiralnice
- Kompenzacijska naprava (kondenzatorji)
- SCADA/RTU oprema
- Releji zaščite

---

## 2.6 Priključevanje OVE (Obnovljivi viri energije)

### Sončne elektrarne (PV sistemi)
- Priključene na NN ali SN omrežje
- Zahteve: SIST EN 50549-1 (NN), SIST EN 50549-2 (SN)
- Pogoji priključitve: energetsko soglasje od Elektro Ljubljana / SODO
- Zahtevana zaščita:
  - Podnapetostna / nadnapetostna zaščita (U< / U>)
  - Podfrekvenca / nadfrekvenca (f< / f>)
  - Zaščita pred otokovanjem (anti-islanding)

### Vpliv OVE na omrežje
- **Povratni tok** (reverse power flow) — tok teče od odjemalca navzgor
- **Napetostni dvig** na koncu kablovoda
- **Zahteve za regulacijo**: cos φ (Q regulacija), P regulacija
- **Konfiguracija zaščite** se prilagodi dvosmernem toku

### Preračun omrežja z OVE
Pri načrtovanju je treba upoštevati:
1. Scenarij brez OVE (max. obremenitev) → preveriti padec napetosti
2. Scenarij z max. OVE (min. obremenitev) → preveriti dvig napetosti

---

## 2.7 Kazalniki kakovosti omrežja

### Zanesljivost napajanja (Reliability)

| Kazalnik | Opis | Enota |
|---|---|---|
| SAIDI | Povprečni čas prekinitve na odjemalca / leto | min/odjemalca |
| SAIFI | Povprečno število prekinitev na odjemalca / leto | prekinitev/odjemalca |
| MAIFI | Število kratkotrajnih prekinitev (< 3 min) | prekinitev/odjemalca |
| ENS | Nedobavljena energija | MWh/leto |

**SAIDI in SAIFI sta regulirana s strani AGEN (Agencija za energijo).**

### Kakovost napetosti (Power quality) — SIST EN 50160
- Frekvenčni pas: 50 Hz ± 1 % (normalni pogoji)
- Napetostni pas: Un ± 10 % (95 % časa v tednu)
- Harmonske motnje: THD ≤ 8 %
- Flikanje (flicker): Plt ≤ 1

---

## 2.8 Preurejanje omrežja (Network reconfiguration)

### Namen
- Izolacija okvarjenega odseka
- Napajanje nenapajanih odjemalcev po alternativni poti
- Uravnovešanje obremenitve

### Postopek ročnega preurejanja
1. Lokalizacija okvare (terenska ekipa / SCADA / závarovalne naprave)
2. Izolacija odseka (odpiranje stikalnih naprav)
3. Preurejanje (zapiranje alternativnih poti)
4. Vzpostavitev napajanja
5. Odpravljanje okvare
6. Povrnitev v normalno stanje

### Avtomatizirano preurejanje (FDIR — Fault Detection, Isolation, Restoration)
- Inteligentna omrežja (smart grid)
- RTU in IED naprave v SN omrežju
- Čas preurejanja: < 5 minut brez človekovega posredovanja

---

## 2.9 Izgube v omrežju

### Vrste izgub
- **Tehnične izgube**: I²R izgube v kablih in transformatorjih
- **Netechnične izgube (NTL)**: kraje energije, napake merjenja

### Zmanjšanje izgub
- Uravnoteženost obremenitve po fazah
- Kompenzacija jalove moči (kondenzatorske baterije)
- Zamenjava preobremenjenih kablov z večjim presekem
- Optimizacija topologije (krajše poti)

---

## Povzetek — ključni pojmi

| Pojem | Razlaga |
|---|---|
| RTP | Razdelilna transformatorska postaja (110/20 kV) |
| TP | Transformatorska postaja (20/0,4 kV) |
| SN | Srednja napetost (10/20/35 kV) |
| NN | Nizka napetost (≤ 1 kV) |
| NO stikalo | Normalno odprto stikalo (v zanki) |
| SAIDI/SAIFI | Kazalniki zanesljivosti napajanja |
| OVE | Obnovljivi viri energije |
| FDIR | Avtomatizirano preurejanje po okvari |
