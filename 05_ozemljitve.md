# 5. Ozemljitve in zaščita pred udarnim tokom (Earthing Systems)

---

## 5.1 Namen ozemljitve

Ozemljitev (earthing / grounding) zagotavlja:
1. **Varnost oseb** — omeji napetost dotika ob okvari
2. **Zaščita opreme** — zagotovi pot za odvodnico strele in prenapetostne zaščite
3. **Referenčni potencial** — električni nič za omrežje
4. **Selektivnost zaščit** — zagotovi dovolj velik tok okvare za delovanje zaščit

---

## 5.2 Tipi ozemljilnih sistemov (po SIST HD 60364-1)

Oznaka je sestavljena iz dveh črk:
- **1. črka**: odnos omrežja (transformatorja) do zemlje: **T** = direktno ozemljeno, **I** = izolirano
- **2. črka**: odnos izpostavljenih prevodnih delov (instalacije) do zemlje: **T** = direktno ozemljeno, **N** = priključeno na nevtralo

---

### TN sistem

Nevtrala transformatorja je direktno ozemljena. Izpostavljeni prevodni deli so priključeni na zaščitni vodnik PE, ki je priključen na ozemljitev omrežja.

#### TN-C (kombinirani PEN vodnik)
```
Transformator:  N ——— PE (skupaj = PEN)
Instalacija:    Izpostavljeni deli ——— PEN
```
- Nevtralni in zaščitni vodnik sta združena v **PEN** vodniku
- Prednost: manj vodnikov
- Slabost: ni mogoče namestiti RCD (IFD) za celotni krog
- Prepovedan za nove instalacije (le v obstoječih)

#### TN-S (ločeni N in PE)
```
Transformator:  N ——— PE (ločeni iz transformatorja naprej)
Instalacija:    Izpostavljeni deli ——— PE
                Nevtrala ——— N (ločena od PE)
```
- N in PE sta ločeni skozi celotno instalacijo
- Obvezen za **RCD zaščito** (diferenčni zaščitnik)
- Standard za nove NN instalacije

#### TN-C-S (kombinirani → ločeni)
```
Od transformatorja: PEN vodnik
V objektu (PEN razdeli se): N + PE (ločena)
```
- Najpogostejši v obstoječih slovenskim stanovanjih
- PEN se razdeli pri vstopu v objekt (NN priključek, GMD)

#### Napetost dotika ob okvari (TN)
```
Ud = (ZPE / Ztot) · U0

ZPE — impedanca zaščitnega vodnika
Ztot — skupna impedanca kratko-stičnega tokokroga
U0 — fazna napetost (230 V)
```
- Zahteva: Ud ≤ 50 V (suhi prostori), ≤ 25 V (vlažni prostori)
- Zagotovi s hitrimi zaščitami: varovalo, RCD, odklopnik

---

### TT sistem

Nevtrala transformatorja je ozemljena neodvisno od ozemljitev izpostavljenih prevodnih delov instalacije.

```
Transformator: N ——— RA (ozemljitev omrežja)
Instalacija:   Izpostavljeni deli ——— RB (ozemljitev instalacije)
```

#### Značilnosti TT sistema
- Tok napake teče skozi obe ozemljitvi (RA in RB) in zemljo
- Tok napake je majhen → zaščita z RCD je obvezna
- Varovalka ali odklopnik ne moreta zagotoviti zaščite (tok napake premajhen)

#### Zahteva za RCD v TT sistemu
```
I_Δn ≤ 50 V / RB

RB — ozemljilni upor instalacije
Primer: RB = 500 Ω → I_Δn ≤ 50/500 = 100 mA → vzamemo 30 mA
```

#### Uporaba TT sistema
- Premični objekti (počitniški domovi, gradbiščne priključnice)
- Ko ni mogoče zagotoviti kakovostne NN instalacije (oddaljena območja)
- Stara NN omrežja brez skupne ozemljitve

---

### IT sistem

Nevtrala transformatorja je **izolirana** od zemlje ali priključena prek visoke impedance (npr. Petersonova dušilka).

```
Transformator: N ——— (impedanca Z ali brez povezave) ——— zemlja
Instalacija:   Izpostavljeni deli ——— RA
```

#### Značilnosti IT sistema
- Pri **prvem** zemeljskem stiku: tok napake ≈ 0, sistem obratuje naprej
- Nadzornik izolacije (IMD — Insulation Monitoring Device) zazna okvaro → alarm
- Ob **drugem** zemeljskem stiku na drugi fazi: nastane trofazni kratki stik!
- Zahteva takojšnje odpravljanje prve okvare

#### Področja IT sistema
- Medicinska oprema (operacijske sobe, ICU — SIST HD 60364-7-710)
- Nevarna področja (ATEX — eksplozivne cone)
- Rudniki (rudniška elektrarna)
- Omrežja z Petersonovo dušilko (SN distribucijsko omrežje)

---

## 5.3 Ozemljilni upor (Earth resistance)

### Zahteve (SIST HD 60364)
| Namen | Zahtevani RA |
|---|---|
| Ozemljitev nevtrale TP | ≤ 1 Ω (velika TP), ≤ 5 Ω |
| Strelovod | ≤ 10 Ω |
| NN instalacija (TT) | ≤ 50 V / I_Δn |
| SN TP (skupna ozemljitev) | Izračun glede na tok in Un |

### Vrste ozemljilnih elektrod

| Tip | Opis | Tipični upor |
|---|---|---|
| Ozemljilna palica | Jeklena / Cu galvanizirana, L = 1,5–3 m | 20–100 Ω |
| Trakasta elektroda | Cu ali jeklen trak, zakopan na globini 0,5–1 m | 5–50 Ω |
| Temeljska elektroda | Jeklene armature v betonskih temeljih | 1–10 Ω |
| Mreža (grid) | Medsebojno povezane elektrode | < 1 Ω |

### Paralelno vezane elektrode
```
1/R_skupaj = 1/R1 + 1/R2 + ...   (ob upoštevanju faktorja interference)
```

---

## 5.4 Meritev ozemljilnega upora

### Metoda treh točk (Fall of potential method)
Standardna metoda za meritev ozemljilnih elektrod.

```
Postopek:
1. Ozemljitvena elektroda E (merjeno)
2. Tokovni elektroda C — postavi se na razdalji D od E (D ≥ 5× premer elektrode)
3. Napetostna elektroda P — postavi se med E in C (D1 = 0,618 · D)
4. Naprava izmeri: R = U_EP / I_EC
```

### Wenner metoda (4-elektrode)
Meri specifično električno upornost tal (ρ, Ω·m):
```
ρ = 2π · a · R_meritev

a — razdalja med elektrodami (m)
```

---

## 5.5 Izenačitev potencialov (Equipotential bonding)

### Namen
Izenačitev potencialov prepreči, da bi se med dvema prevodnim deloma pojavila nevarno visoka potencialna razlika.

### Glavna izenačitev potencialov (GPE / MEB — Main Equipotential Bonding)
Mestu priključitve: GMD (Glavna ozemljitvena doza)

Priključiti na GPE:
- Kovinska cev vodovoda (vstop v objekt)
- Kovinska cev plina (vstop v objekt)
- Kovinska cev centralnega ogrevanja
- Kovinska konstrukcija stavbe
- Zaščitni vodnik PE NN instalacije
- Strelovod

### Dopolnilna (lokalna) izenačitev potencialov (LEB — Local Equipotential Bonding)
- V kopalnicah (SIST HD 60364-7-701): obvezno
- V bazenih, saunah
- V medicinskih prostorih

### Kopalnica — izenačitvene cone (SIST HD 60364-7-701)
```
Cona 0: notranjost kadi/tuša — BREZ električne opreme
Cona 1: neposredno nad kadjo — samo IPX4 oprema (SELV 12 V)
Cona 2: do 0,6 m od kadi — IPX4 oprema
Zunaj con: normalna instalacija
```

---

## 5.6 Napetost dotika in koračna napetost

### Napetost dotika (Touch voltage, Ut)
Napetost med dostopnim prevodnim delom in točko, kjer oseba stoji (potencialni gradient tal).

```
Ut = Id · (ZPE + Zosebe_in_tal)
```

Mejne vrednosti:
- **50 V AC** — suhi prostori (splošni)
- **25 V AC** — vlažni prostori, gradbišča
- **12 V AC** — potopljeni deli (bazeni)

### Koračna napetost (Step voltage, Us)
Napetost med dvema točkama tal, razdalja 1 m (dolžina koraka).

Nevarno pri: neposrednem udaru strele, visoki zemeljski napetosti pri kratkem stiku v TP.

**Zaščitni ukrep**: preprečiti dostop do nevarne cone (ograja), izravnalna mreža, korak z nogami skupaj ali skakanje.

---

## 5.7 Ozemljitev v distribucijskem omrežju

### Ozemljitev transformatorske postaje
- Skupna ozemljitev VN in NN strani (SIST HD 60364)
- Pri skupni ozemljitvi: R_skupaj mora omejiti napetost dotika
- Ozemljilna mreža pod TP

### SN ozemljitev (razdeljena ozemljitev)
- Ko napetost dotika ob zemeljski napaki v SN omrežju preseže 50 V
- Ločitev VN in NN ozemljitve
- NN zaščitni vodnik se ne sme priključiti na VN ozemljitev

---

## Povzetek — primerjava sistemov

| Lastnost | TN-S | TT | IT |
|---|---|---|---|
| Nevtrala transformatorja | Ozemljena | Ozemljena | Izolirana |
| Zaščita ob 1. okvari | Varovalka / RCD | RCD obvezno | Alarm (IMD) |
| Ob 2. okvari | — | — | Kratki stik |
| RCD obveznost | Priporočljivo | Obvezno | Obvezno (IMD) |
| Primerna za | NN stanovanja, pisarne | Mobilne enote | Medicinska, IT omrežja |
