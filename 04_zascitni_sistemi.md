# 4. Zaščitni sistemi (Protection Systems)

---

## 4.1 Namen in zahteve zaščite

Zaščitni sistem mora:
1. **Zaznati** okvaro (kratki stik, zemeljski stik, prekoračitev toka)
2. **Izolirati** okvarjen del omrežja v najkrajšem možnem času
3. **Ohraniti** napajanje maksimalnemu številu odjemalcev
4. **Zaščititi** opremo pred termalnimi in mehanskimi poškodbami

### Zahteve dobre zaščite
| Zahteva | Opis |
|---|---|
| Selektivnost | Odpre se samo najbližji zaščitni element okvarjenemu mestu |
| Hitrost | Dovolj hitra, da omeji škodo |
| Zanesljivost | Deluje, ko je treba; ne deluje po nepotrebnem |
| Občutljivost | Zazna minimalni kratki stik |
| Okrepitev (backup) | Nadomesti nadrejeni zaščitni element, ki ni deloval |

---

## 4.2 Nadtokovne zaščite (Overcurrent protection)

### Karakteristike zaščitnih relejev

**Definitna (independent time) karakteristika**
- Čas izklopa je neodvisen od velikosti toka
- Nastavitev: I> in t (tok in čas)
```
Če I > I_nastavljeno → izklop po t_nastavljenem
```

**Inverzna (inverse time) karakteristika**
- Manjši tok → daljši čas izklopa
- Večji tok → krajši čas izklopa
- Posnemanje karakteristike varovala

Tipi po IEC 60255:
| Oznaka | Tip | Formula časa |
|---|---|---|
| NI | Normalno inverzna (Normal Inverse) | t = 0,14 / (I/Is)^0,02 − 1 |
| VI | Zelo inverzna (Very Inverse) | t = 13,5 / (I/Is − 1) |
| EI | Ekstremno inverzna (Extremely Inverse) | t = 80 / (I/Is)² − 1 |

### Stopnje nadtokovne zaščite

**I> (prekoračitev toka — overload)**
- Nastavitev: 1,0–1,5 · In
- Čas: 0,1–1 s

**I>> (kratki stik — high-set)**
- Nastavitev: 3–10 · In
- Čas: 0,1–0,5 s

**I>>> (hiter izklop — instantaneous)**
- Nastavitev: > 10 · In
- Čas: ≤ 0,05 s

---

## 4.3 Koordinacija zaščit (Protection coordination / Selektivnost)

### Namen
- Vsaka napaka izklopi SAMO najbližji zaščitni element napakam
- Zaščite na višjih nivojih so upočasnjene (gradientna metoda)

### Gradnja selektivnosti — primer

```
Odjemalec → Varovalka 63 A (takojšnji izklop)
    ↓
TP RG → NH varovalo 400 A (malo kasnejši)
    ↓
SN izvod → Relej I> 300 A, 0,3 s
    ↓
RTP SN zbiralnica → Relej I> 600 A, 0,6 s
    ↓
RTP VN stran → Relej I> 1200 A, 1,0 s
```

### Selektivnost med varovalom in relejem
- Upoštevaš karakteristiko varovala in jo primerjaš z relejem
- Relej mora biti nad karakteristiko varovala (počasnejši pri enakem toku)

### Metoda prenatezanja časa (Time grading)
- Med sosednjima zaščitnima elementoma: **Δt ≥ 0,2–0,3 s**
- Upošteva čas delovanja odklopnika + toleranco relejne naprave + varnostna rezerva

---

## 4.4 Zemeljska zaščita (Earth fault protection)

### Enofazni zemeljski stik v SN omrežju
- SN omrežje z izolirano nevtralo (IT) ali resonančno zemeljsko zaščito (Petersen coil)
- Pri enofaznem stiku: tok stika je majhen → ne predstavlja takojšnje nevarnosti
- Omrežje obratuje naprej (do 1 uro)

### Zaščita pri zemeljski stiku
- **Wattmetrična zaščita** (directional earth fault): zazna smer toka zemeljske napake
- **Rezidualni tok** (I0 = I1 + I2 + I3): vsota tokov vseh treh faz ≠ 0 pri zemeljski napaki

### Petersonova dušilka (Petersen coil / Rezonančno ozemljitev)
- Induktivna dušilka med nevtralo in zemljo
- Kompenzira kapacitivni zemeljski stik → tok stika ≈ 0
- Odpravi samo izolirane zemeljske stike — omrežje ostane v obratovanju
- Zahteva zemeljsko relejno zaščito za odkrivanje okvarjenega izvoda

---

## 4.5 Diferenčna zaščita (Differential protection)

### Princip
Primerja tok na vstopu in izstopu iz varovanega elementa.

```
Id = I1 - I2

Normalno: I1 ≈ I2, Id ≈ 0
Notranja napaka: I1 ≠ I2, Id > nastavljeno → izklop
```

### Diferenčna zaščita transformatorja
- Primerja tok na VN in NN strani (ob upoštevanju prestavnega razmerja in vektorne skupine)
- Zelo hitra (< 20 ms)
- Zazna: medovojna kratica (interturn fault), zemeljski stik v navitju, kratki stik

### Buchholz relej
- Mehanska zaščita oljnega transformatorja
- Zazna pline, ki nastajajo pri notranji okvari (električna iskra v olju)
- **Plinska stopnja (alarm)**: zbiranje plina → alarm
- **Tokovnja stopnja (trip)**: hitro prhanje olja (eksplozivna notranja okvara) → takojšnji izklop

---

## 4.6 Distančna zaščita (Distance protection)

### Princip
Izmeri impedanco med zaščitnim relejem in mestom napake.

```
Z_napake = U_faza / I_kratki stik

Manjša Z → napaka bližje
Večja Z → napaka dlje
```

### Cone zaščite (Zones)

| Cona | Doseg | Čas |
|---|---|---|
| Cona 1 | 80 % dolžine voda | Takojšnji izklop (0,0–0,1 s) |
| Cona 2 | 120 % dolžine voda | 0,3–0,5 s |
| Cona 3 | 150–200 % | 0,6–1,0 s |

- Cona 1 < 100 %: varnost pred napačnim dosegom pri napaki na koncu voda
- Cona 2 in 3: rezervna zaščita sosednjih elementov

---

## 4.7 RCD — Zaščita pred udarnim tokom (Residual Current Device)

### Princip
Meri razliko med tokom v faznem in nevtralnem vodniku. Razlika = tok skozi zemljo.

```
I_diferenčni = IL - IN

Normalno: IL ≈ IN
Ob okvaritvi: IL > IN → izklopni tok I_Δn
```

### Tipi RCD po obliki toka

| Tip | Zazna |
|---|---|
| AC | Le izmenični diferenčni tok (50 Hz) |
| A | AC + pulzirajoči enosmerni tok (za VFD, frekvenčni pretvorniki) |
| B | AC + DC diferenčni tok (za polnilnice EV, medicinska oprema) |
| F | Tip A + mešani frekvenci |

### Vrednosti I_Δn

| I_Δn | Uporaba |
|---|---|
| 10 mA | Zaščita pred dotikom v vlažnih prostorih |
| 30 mA | Splošna zaščita oseb (obvezna v stanovanjskih instalacijah) |
| 100 mA | Požarna zaščita |
| 300–500 mA | Zaščita kablov (selektivna, nadrejena) |

### Selektivnost RCD (časovne stopnje)
- Normalni RCD: izklop < 40 ms pri I_Δn
- Časovni zakasnitveni RCD (S-tip): izklop po 60–200 ms (nadrejeni)
- S tipi: G (general) — brez zakasnitve; S (selective) — z zakasnitvijo

---

## 4.8 Prenapetostna zaščita (Overvoltage protection)

### Vzroki prenapetosti
- Udar strele (atmospheric overvoltage)
- Stikalne prenapetosti (switching overvoltage)
- Zemeljski stik v omrežju (power frequency overvoltage)

### Zaščitne naprave

**Odvodnik (Surge arrester)**
- Metal oxide varistor (MOV): zinkoksid ZnO
- Tok odvaja v zemljo pri prekoračitvi prirobne napetosti (Uc)
- Primer: 20 kV odvodnik: Uc = 24 kV, Up ≤ 75 kV

**Varistor (SPD — Surge Protection Device)**
- Za zaščito NN instalacij
- Tipi po IEC 61643-11:
  - Tip 1 (Class I): zaščita pred strelo (za vtičnico v strelovodni instalaciji)
  - Tip 2 (Class II): zaščita pred stikalnimi prenapetostmi (za glavno stikalno polje)
  - Tip 3 (Class III): finalna zaščita naprav

### Koordinacija prenapetostnih zaščit
Tip 1 → Tip 2 → Tip 3 (od vtičnice navznoter)
Razdalja med tipi: ≥ 10 m kabelske trase ali zakasnilna dušilka

---

## 4.9 Reklozer (Recloser / AVR — Automatic Voltage Regulator)

### Namen
Večina napak na nadzemnih vodih je **prehodnih** (veja na vodu, strela). Reklozer po izklopi samodejno ponovi vklop.

### Tipični cikel ponovnega vklopa
```
Napaka → Izklopni signal → 0,3 s odmor → Vklop (1. AVR)
Napaka ostane → Izklopni signal → 5 s odmor → Vklop (2. AVR)
Napaka ostane → Trajni izklop (napaka je stalna)
```

- Na nadzemnih SN vodih: 70–80 % napak reši 1. ali 2. AVR
- Reklozerja NE smemo nameščati za kablovode (napake v kablu so stalne)

---

## 4.10 SCADA (Supervisory Control And Data Acquisition)

### Komponente

| Komponenta | Opis |
|---|---|
| MTU (Master Terminal Unit) | Centralni strežnik — dispečerski center |
| RTU (Remote Terminal Unit) | Lokalna naprava v polju — pošilja podatke |
| IED (Intelligent Electronic Device) | Pametni relej z vgrajeno komunikacijo |
| DMS (Distribution Management System) | Programje za vodenje distribucijskega omrežja |
| SCADA HMI | Grafični vmesnik za dispečerja |

### Komunikacijski protokoli
- **IEC 60870-5-101/104**: standard za daljinski nadzor TP
- **IEC 61850**: sodobni standard (GOOSE sporočila, SV vzorci)
- **DNP3**: pogost v ZDA, del obstoječih sistemov
- **Modbus**: starejše SCADA naprave

### Podatki, ki se prenašajo (SCADA telemetrija)
- Meritve: napetost, tok, moč (P, Q), cos φ, frekvenca
- Stanja: odklopnik odprt/zaprt, stikalo odprto/zaprto
- Alarmi: prenapetost, kratki stik, izpad transformatorja
- Ukazi: vklop/izklop stikalne naprave iz dispečerskega centra

---

## Povzetek — zaščitni releji

| Zaščita | IEC koda | Namen |
|---|---|---|
| Nadtokovna | 50 / 51 | Kratki stik / prekoračitev toka |
| Zemeljski stik | 50N / 51N / 67N | Zemeljski stik |
| Diferenčna | 87 | Notranja okvara (transformator, vodnik) |
| Distančna | 21 | Kratki stik na vodu — impedančna metoda |
| Podnapetostna | 27 | Izguba napetosti |
| Nadnapetostna | 59 | Prekoračitev napetosti |
| Prekoračitev frekvence | 81 | f> ali f< (OVE zaščita) |
| Buchholz | 63 | Notranja okvara oljnega transformatorja |
