# Pasivne Komponente v FTTH Omrežjih

## 1. Optični splitterji

Splitter je **pasivna naprava** ki eno vlakno razdeli na N izhodnih vlaken.
Brez napajanja, brez elektronike — samo optika.

### PLC vs FBT

| Lastnost | PLC (Planar Lightwave Circuit) | FBT (Fused Biconic Taper) |
|---|---|---|
| Princip | Planarna valovniška vezja | Zlivanje vlaken |
| Split ratio | 1:4 do 1:64 (standardno) | 1:2 do 1:64 |
| Enakomerna delitev | ✅ Zelo enakomerna | ❌ Manj enakomerna pri N>8 |
| Pasovna širina | Široka (1260–1650 nm) | Ozka (optimizirana na eno λ) |
| Dimenzije | Majhna, kompaktna | Večja |
| Cena | Nižja pri višjih split ratio | Nižja pri nizkih split ratio |
| Standard za PON | ✅ | Pri visokih razmerjih manj |

**Za FTTH se standardno uporablja PLC splitter.**

### Vstavna izguba (Insertion Loss) po razmerju:

| Split ratio | Teoretična izguba | Tipična PLC izguba |
|---|---|---|
| 1:2 | 3.01 dB | 3.5–3.8 dB |
| 1:4 | 6.02 dB | 7.0–7.2 dB |
| 1:8 | 9.03 dB | 10.2–10.5 dB |
| 1:16 | 12.04 dB | 13.3–13.7 dB |
| 1:32 | 15.05 dB | 16.7–17.0 dB |
| 1:64 | 18.06 dB | 20.0–20.5 dB |
| 1:128 | 21.07 dB | 23.5–24.0 dB |

> Razlika med teoretičnim in dejanskim = **excess loss** splitterja (tipično 0.5–1 dB na nivo).

### Kaskadni splitterji (2-nivojski)

Namesto enega 1:64 splitterja v CO — 1:8 v FDH in 1:8 pri vsaki ODP.

**Skupna izguba kaskade:**
```
1:8 splitter:  10.4 dB
1:8 splitter:  10.4 dB
────────────────────
Skupaj:        20.8 dB  (enako kot en 1:64 splitter ≈ 20.5 dB)
```

**Prednosti kaskade:**
- Splitterji bližje strankam → krajši drop kabli
- Lažja fazna gradnja (sprva 1:8, pozneje dodaš 2. nivo)
- Bolj fleksibilno za nadgradnjo

**Slabosti:**
- Več spojnih mest → več možnih napak
- Dva fizična splitterja → višja cena komponent

---

## 2. Konektorji

### SC/APC — Standard za PON

- **Zelena barva** ohišja
- **8° polirani** konec vlakna (angled physical contact)
- ORL: **> 60 dB** (odboj je odklonjen stran od osi)
- Vstavna izguba: < 0.5 dB (tipično 0.3 dB)
- **Obvezna izbira za vse PON trase** — zaščita pred odboji v laser OLT/ONT

```
SC/APC priključek:
        ____
       |    | ← 8° kot
  ─────┤    ├───── vlakno
       |____|
```

### SC/UPC

- **Modra barva** ohišja
- Ravno polirani konec (ultra physical contact)
- ORL: > 50 dB
- Vstavna izguba: < 0.5 dB
- Uporaba: merjenje (OTDR), testne zanke, kjer odboji niso kritični
- **NE za PON trase** — manjši ORL lahko destabilizira laserje

### LC/APC in LC/UPC

- Manjši format (half size v primerjavi s SC)
- LC/APC = zeleni, LC/UPC = modri
- Pogost v patch panelih in aktivni opremi (SFP+, CFP moduli)
- Vstavna izguba: < 0.3 dB

### Vstavna izguba konektorjev v link budgetu:
```
Tipično: 0.5 dB na konektor
V paru (plug-in): 0.5–1.0 dB skupaj
```

---

## 3. Varjenje vlaken (Splicing)

### Fusion Splicing (termično varjenje)
1. Vlakno se olupijo, očisti z alkoholom
2. Vlakno se prereže s preciznim rezalnikom (cleaver) — natančen rez <0.5°
3. Vlakni se poravnata v varjelnem stroju (splicer)
4. Električni lok zlije vlakni skupaj
5. Stroj izmeri kakovost spoja (ocenjena izguba)
6. Zaščita z heat-shrink zaščito

**Izgube fusion splice:**
- Tipično: **0.02–0.05 dB** (odlični splicer-ji in operaterji)
- Sprejemljivo: < 0.1 dB
- Max dovoljena: 0.5 dB (po ITU-T)

### Mechanical Splice
- Mehanska spojka drži vlakni skupaj z gel-om
- Hitrejše, brez strojev
- Izguba: 0.2–0.5 dB
- Začasna rešitev ali v situacijah brez splicer-ja

### Splice Loss v link budgetu:
```
10 spojev × 0.1 dB = 1.0 dB  (konzervativno)
10 spojev × 0.05 dB = 0.5 dB (realno z dobrim splicer-jem)
```

---

## 4. Optični kabli

### Loose Tube (GT — Gel-Tube) kabel

```
    Zunanja zaščita (PE/HDPE)
       │
    Kevlar/steklena vlakna (mehanska zaščita)
       │
    Polietilenska cev (cevka)
       │
    Hidrofobni gel (preprečuje vdor vlage)
       │
    12× optično vlakno (barve: modra, oranžna, zelena, ...)
```

- Vlakna lebdijo v gelu — zaščita pred vlago in mehanskim stresom
- Primerno za: **podzemno polaganje, nadzemno**, v kanalih, direktno zakopano
- Standardni kabel za feeder in distribution segment

### Tight Buffer kabel

- Vlakno direktno obdano s plastično zaščito (900 µm)
- Brez gela, bolj togo
- Primerno za: **indoor instalacije**, patchkabli
- Lažje delo brez čiščenja gela

### Blown Fiber (Vlakno za vpihavanje)

- Ultra lahka vlakna v mikromodulih
- Se vpihavajo v mikrokanale s kompresorjem
- Prednosti: vlakna se dodajajo naknadno (scalability), hitra zamenjava
- Primerno za: mikrokanal sisteme v urbanih okoljih

### ADSS — All Dielectric Self-Supporting

- Brez kovinskih delov — dielektrični kabel
- Vgrajen napenjalni element (aramid/FRP = Glass Reinforced Polymer)
- Za **nadzemno obešanje** — ne potrebuje ločenega napetostnega kabla
- Odporno na elektromagnetne motnje (blizu VN daljnovodov)

### Mini/Micro Kabel

- Majhen premer (6–14 mm)
- Za **mikrotranseje** in mikrokanale
- Vsebuje 12–96 vlaken kljub majhni velikosti
- "Ribbone" format: vlakna v trakovih

### Drop Kabel (odcepni kabel)

- Od ODP do ONT pri stranki
- **G.657.A2** vlakna — odporna na upogib
- Tipično: 2 ali 4 vlakna
- FRP napenjalni element (brez kovine)
- Premer: 3–5 mm
- Max dolžina: 200 m (upoštevaj link budget)
- Zaključi se z SC/APC konektorjem

---

## 5. Zaključni elementi

### Splice Enclosure (muffa)

- Zaščita varjenih spojev v terenu
- **Podzemna muffa**: IP68, cilindrična ali ovalna, reentry možna
- **Nadzemna muffa**: IP55, obešanje na drog
- Vsebuje: splice tray-e (pladnji za spoje), tlačno zapiranje
- Tipi: dome (kupola), flat (plošča)
- Kapaciteta: 12–288 vlaken

### FDH omara (Fiber Distribution Hub)

- Zunanja ali notranja omara
- Vsebuje:
  - Splice tray-i (zaključevanje feeder kablov)
  - Splitter moduli (1. ali 2. nivo)
  - Patch panel (pigtails + adapterji SC/APC)
  - Patchkabli OLT port → splitter vhod
- Kapaciteta: 32, 64, 128, 576 portov
- IP55 za zunanjost

### ODP (Outdoor Distribution Point)

- Majhna omarica na fasadi, drogu, v jašku
- Vsebuje splitter (tipično 1:8 ali 1:16) in priključnice za drope
- SC/APC konektorji — zaprašeni do priklopa stranke (dust cap)
- Kapaciteta: 8–32 izhodnih portov

### ONT Montaža

```
Zunaj:  ODP ──[drop kabel G.657.A2]──► Fasada ──► notranjost
Znotraj: kabel do ONT ──► SC/APC v ONT ──► Ethernet/WiFi
```

- ONT tipično na steni blizu električne vtičnice
- Napajalni adapter: 12V ali 220V direktno
- Baterija za VoIP (opcijsko, 4–8 ur backup)

---

## 6. Hitri povzetek — kar morate znati na razgovoru

1. PLC splitter = enakomerna delitev, za PON standard, 1260–1650 nm
2. 1:32 splitter ≈ 17 dB izguba, 1:64 ≈ 20.5 dB izguba
3. SC/APC (zeleni) = PON obligatorno — ORL >60 dB varuje laser
4. SC/UPC (modri) = za merjenje/testiranje, NE za PON trase
5. Fusion splice: tipično 0.05 dB, max 0.5 dB
6. Loose tube = outdoor, gel zaščita, feeder/distribution
7. G.657.A2 drop kabel = bend insensitive, od ODP do ONT
8. ADSS = nadzemni samosanoseči kabel, brez kovine
9. Muffa = zaščita varjenih spojev, IP68 za podzemje
10. ODP = zunanja razdelilna točka s splitterjem, SC/APC priključki
