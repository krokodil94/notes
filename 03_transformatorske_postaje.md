# 3. Transformatorske postaje (TP)

---

## 3.1 Vloga in funkcija transformatorske postaje

Transformatorska postaja (TP) pretvori srednjo napetost (SN, 20 kV) na nizko napetost (NN, 0,4 kV) in razdeli električno energijo do končnih odjemalcev.

```
SN omrežje (20 kV)
     ↓
[VN stikalno polje]
     ↓
[Transformator 20/0,4 kV]
     ↓
[NN razvodni garnitur - RG]
     ↓
NN kablovodi do odjemalcev
```

---

## 3.2 Tipi transformatorskih postaj

### Glede na izvedbo

| Tip | Opis | Uporaba |
|---|---|---|
| Prostostoječa zidana | Zidana stavba, lastno TP poslopje | Mesta, večja TP |
| Vgrajena (stolpna) | Vgrajena v stavbo ali stolp | Mestna jedra |
| Tipska kovinska (kiosk) | Jeklena omara, tipizirana | Primestje, industrijska območja |
| Stolpna TP | Na betonskem ali lesenem drogu | Podeželje, SN nadzemni vodi |
| Kompaktna / zaprta (GIS) | SF6 izolirana, kompaktna | Kjer je malo prostora |

### Glede na lastnika
- **Javna TP** (v lasti Elektro Ljubljana / SODO): napaja gospodinjstva in podjetja
- **Zasebna TP** (v lasti odjemalca): industrijsko podjetje ima lastno TP

---

## 3.3 Transformator

### Osnovno delovanje
Transformator deluje na principu elektromagnetne indukcije. Magnetni tok skozi skupno železno jedro inducira napetost v obe navitji.

```
U1/U2 = N1/N2 = I2/I1

U1 — primarna napetost (VN stran, 20 kV)
U2 — sekundarna napetost (NN stran, 0,4 kV)
N1, N2 — število ovojev
```

### Vektorna skupina transformatorja
Opisuje fazo med primarnim in sekundarnim navitjem ter način vezave.

| Oznaka | Vezava primarnega | Vezava sekundarnega | Zamik faze |
|---|---|---|---|
| Dyn11 | Trikot (Delta) | Zvezda z nevtralo | 330° (=−30°) |
| YNyn0 | Zvezda z nevtralo | Zvezda z nevtralo | 0° |
| Yzn11 | Zvezda | Cik-cak z nevtralo | 330° |

**Dyn11** je najpogostejša vektorna skupina za distribucijske TP v Sloveniji.

### Izgube transformatorja

| Vrsta izgub | Simbol | Vzrok | Odvisnost |
|---|---|---|---|
| Izgube v železu (No-load losses) | P0 (Pfe) | Histereza + vrtinčni tokovi | Konstantne (neodvisno od obremenitve) |
| Izgube v bakru (Load losses) | Pk (Pcu) | Ohmske izgube v navitjih | Proporcionalne I² (odvisne od obremenitve) |

```
Skupne izgube = P0 + (S/Sn)² · Pk

S  — trenutna navidezna moč [kVA]
Sn — nazivna moč transformatorja [kVA]
```

### Parametri transformatorja

| Parameter | Opis | Tipična vrednost |
|---|---|---|
| Sn | Nazivna moč | 100 / 160 / 250 / 400 / 630 kVA |
| Un1 / Un2 | Nazivna napetost prim. / sek. | 20 kV / 0,4 kV |
| uk% | Kratko-stična napetost | 4 % (≤ 630 kVA), 6 % (> 630 kVA) |
| P0 | Praznotekne izgube | 0,3–1,5 kW |
| Pk | Kratko-stične izgube | 1–10 kW |
| i0% | Praznotekni tok | 0,5–2 % |

### uk% — kratko-stična napetost
- Napetost na primarni strani, pri kateri teče I_n pri kratko-stičenem sekundarnem navitju
- Vpliva na tok kratkega stika na sekundarni strani:
```
I"k = In / uk% · c

Večji uk% → manjši kratki stik → boljša selektivnost zaščit
Manjši uk% → večji kratki stik → slabša selektivnost, večje dinamične sile
```

### Dimenzioniranje transformatorja

1. Izračun skupne priključne moči (vsota odjemalcev)
2. Upoštevanje hkratnostnega faktorja (kf ≈ 0,5–0,8 za gospodinjstva)
3. Varnostni faktor: transformator načeloma obremenjen na **≤ 80 %** Sn
4. Upoštevanje prihodnje rasti obremenitve

```
Sn ≥ (P_skupaj · kf) / (cos φ · 0,80)
```

---

## 3.4 VN stikalno polje (SN stran TP)

### Tipi VN celic

| Tip | Opis |
|---|---|
| Vhodna celica (priključna) | Priključitev SN kabla |
| Zbiralna celica | Zbiralnice |
| Transformatorska celica | Zaščita in priklop transformatorja |
| Merilna celica | Meritev energije (za obračun) |

### Stikalne naprave v VN celicah

**Odklopnik (Circuit breaker)**
- Odpira tokokrog pri normalnem toku IN pri kratkem stiku
- Tipi: vakuumski (najpogosteje za SN), SF6 (za VN in kompaktne GIS)
- Odklopna moč: npr. 16 kA pri 20 kV

**Ločilnik (Disconnector / Isolator)**
- Galvanska ločitev — zagotavlja vidno odprtino
- Odpira samo brez bremena
- Varnostni predpis: najprej odpri odklopnik, potem ločilnik

**Bremenstikalo (Load break switch)**
- Odpira pod bremenom, NE pri kratkem stiku
- Brez zaščitne funkcije

**VN varovalo (HV fuse)**
- Topi element, ki prekine tokokrog pri prekoračitvi toka
- Tipično v kombinaciji z bremenstikal (bremenstikalo + varovalo = "switch-fuse")
- Prednost: poceni, zanesljivo
- Slabost: po pregorevanju je treba zamenjati vložek

---

## 3.5 NN razvodni garnitur (RG)

### Naloga
- Razdeli NN energijo iz transformatorja v posamezne NN izvode
- Vsak izvod varuje NH varovalo ali odklopnik

### Tipična sestava RG

```
[NN sponke transformatorja]
        ↓
[Zbiralne NN šine (Cu ali Al)]
        ↓
[NH varovalni izpusti → NN kablovodi]
[Merjenje (energetski števec)]
[Stikalo NN zbiralk]
```

### NH varovalo (NH-Sicherung)
- Nožasto varovalo za NN (do 1 kV)
- Velikosti: 000, 00, 0, 1, 2, 3
- Tokovi: 16 A–1250 A

---

## 3.6 Hladilni sistem transformatorja

| Tip | Oznaka (IEC) | Opis |
|---|---|---|
| Suho (naravna konvekcija) | AN | Hladilni medij: zrak, naravna konvekcija |
| Oljno (naravna konvekcija) | ONAN | Mineralno olje, naravna konvekcija |
| Oljno s prisilnim hlajenjem | ONAF | Olje + ventilatorji |

**Distribucijske TP** večinoma: **oljni transformatorji (ONAN)** ali **suhi transformatorji (AN)** v notranjih prostorih.

### Oljna posoda transformatorja
- Izolacijski medij: mineralno ali sintezno olje
- Raztezna posoda (konzervator) — kompenzira spremembo volumna olja
- Buchholz relej — detekcija notranje okvare (plini v olju)
- Temperaturni rele — nadzor temperature

---

## 3.7 Vzdrževanje transformatorske postaje

### Redni pregledi (periodično vzdrževanje)
- Vizualni pregled: iztekanje olja, korozija, poškodbe
- Meritev temperature transformatorja
- Preizkus zaščitnih relejev
- Meritev ozemljilnega upora
- Čiščenje izolatorjev

### Preizkusi transformatorja
- Merjenje izolacijske upornosti (megohmeter)
- Merjenje upora navitij
- Analiza olja (vsebnost vlage, kisline, plini)
- Meritev razmerja navitij (TTR test)

---

## Povzetek — ključni podatki

| Podatek | Vrednost |
|---|---|
| Tipična moč distribucijske TP | 160, 250, 400, 630 kVA |
| Primarna napetost (SN stran) | 20 kV |
| Sekundarna napetost (NN stran) | 0,4 kV (400/230 V) |
| Tipična vektorna skupina | Dyn11 |
| Kratko-stična napetost uk% | 4 % (≤630 kVA) |
| Obremenjenost transformatorja | ≤ 80 % Sn (normalni pogoji) |
