# 7. Standardi in predpisi

---

## 7.1 Hierarhija predpisov v Sloveniji

```
EU direktive in uredbe
        ↓
Zakoni (Državni zbor RS)
        ↓
Uredbe in pravilniki (Vlada RS, ministrstva)
        ↓
Tehnična pravila (SODO, Elektro Ljubljana)
        ↓
Standardi (SIST EN — Slovenian Institute for Standardization)
```

**Standardi v Sloveniji**: SIST je član CENELEC (Evropski elektrotehniški standardizacijski odbor) in IEC (International Electrotechnical Commission). Standardi CENELEC se prevzamejo kot SIST EN.

---

## 7.2 Energetski zakon (EZ-1)

**Zakon o oskrbi z električno energijo** (ZOEE) in **Energetski zakon (EZ-1)** sta temeljni zakonodajni akti za elektroenergetsko področje v Sloveniji.

### Ključne vsebine EZ-1
- Določa pravice in obveznosti distribucijskega operaterja
- Opredeljuje sistemski operater distribucijskega omrežja (SODO)
- Ureja pogoje priključitve odjemalcev in proizvajalcev
- Določa kakovost oskrbe z električno energijo
- Opredeljuje inšpekcijski nadzor (AGEN — Agencija za energijo)

### AGEN (Agencija za energijo)
- Regulatorni organ
- Določa tarifne postavke, regulira kakovost
- Nadzira standarde zanesljivosti (SAIDI, SAIFI)

---

## 7.3 SIST EN 50160 — Kakovost napetosti

Standard določa parametre napetosti v javnem distribucijskem omrežju.

### Parametri za NN omrežje

| Parameter | Zahteva | Opomba |
|---|---|---|
| Frekvenca | 50 Hz ± 1 % (95 % tedna) | ± 6 % (100 % tedna) |
| Napetost Un | 230 V ± 10 % (95 % tedna) | Merjeno kot 10-minutna srednja vrednost |
| Harmonski THD | ≤ 8 % | |
| Flikanje (Plt) | ≤ 1 | Dolgotrajna intenziteta flikanja |
| Neravnovesje | ≤ 2 % | Neravnovesje negativnega zaporedja |
| Odkloni napetosti | ≤ 10 % | Od Un = 230 V |

### Parametri za SN omrežje

| Parameter | Zahteva |
|---|---|
| Napetost | Dogovorjena napetost ± 10 % (95 % tedna) |
| Frekvenca | Enako kot NN |
| THD | ≤ 8 % |

---

## 7.4 SIST HD 60364 — Nizkonapetostne električne instalacije

Serija standardov za projektiranje, gradnjo in preizkušanje NN instalacij.

### Struktura serije

| Številka | Vsebina |
|---|---|
| SIST HD 60364-1 | Splošna načela, definicije |
| SIST HD 60364-4-41 | Zaščita pred udarnim tokom |
| SIST HD 60364-4-43 | Zaščita pred prekoračitvijo toka |
| SIST HD 60364-5-52 | Izbira in montaža el. opreme — kablovodi |
| SIST HD 60364-5-54 | Ozemljitev in zaščitni vodniki |
| SIST HD 60364-6 | Preverjanje instalacij |
| SIST HD 60364-7-701 | Kopalnice in tuši |
| SIST HD 60364-7-712 | Fotovoltaični sistemi |
| SIST HD 60364-7-722 | Polnilne postaje za EV |

### Zaščita pred udarnim tokom (SIST HD 60364-4-41)

**Zaščita pred direktnim dotikom (Basic protection):**
- Izolacija aktivnih delov
- Ohišja in kryti (IP zaščita)

**Zaščita pred indirektnim dotikom (Fault protection):**
- Samodejna prekinitev napajanja (ADS — Automatic Disconnection of Supply)
- Dvojna ali ojačana izolacija
- Električna ločitev (SELV, PELV, FELV)

**Zahtevani časi izklopa (ADS):**

| Sistem | Un | Max. čas izklopa |
|---|---|---|
| TN | 230 V | 0,4 s |
| TN | > 230 V faza-faza | 0,2 s |
| TT | katera koli | 0,2 s (ali IΔn ≤ 30 mA) |

---

## 7.5 SIST EN 50549 — Priključevanje generatorjev

### SIST EN 50549-1 (NN priključitev, ≤ 16 A na fazo)
- Zaščitne nastavitve za mikrogeneratorje (PV, kogeneracija)
- Antiislanding zaščita obvezna
- Napetostne in frekvencne meje:

| Parameter | Meja (Slovenija) |
|---|---|
| U< (podnapetostna) | 0,85 Un, 1,5 s |
| U> (nadnapetostna) | 1,1 Un, 1,5 s |
| f< (podfrekvenca) | 47,5 Hz, 0,5 s |
| f> (nadfrekvenca) | 51,5 Hz, 0,5 s |

### SIST EN 50549-2 (SN priključitev)
- Za večje generatorje (nad 11 kW / fazo)
- Nastavitve zaščite koordinirane z SODO mrežnim pravili

---

## 7.6 Pravilnik o sistemskem obratovanju distribucijskega omrežja

Temeljni pravilnik za obratovanje distribucijskega omrežja v Sloveniji.

### Ključne vsebine
- Pogoji za priključitev odjemalcev in generatorjev
- Tehnični pogoji za priključitev (zaščite, kakovost)
- Kakovost oskrbe in standardi zanesljivosti
- Merilni sistemi in obračun energije
- Postopki za stikalne manoevre
- Varstvo pri delu v distribucijskem omrežju

---

## 7.7 Pravilnik o tehničnih pogojih za gradnjo el. vodov

Ureja tehnične pogoje za gradnjo nadzemnih in zemeljskih elektroenergetskih vodov.

### Ključne vsebine
- Minimalne razdalje za nadzemne vode (od tal, stavb, cest)
- Zahteve za drogove in podporne konstrukcije
- Zahteve za polaganje zemeljskih kablov (globina, pesek, oznake)
- Zahteve za kabelske jaške, omare, spojke

---

## 7.8 Gradbeni zakon (GZ) in projektna zakonodaja

### Gradbeni zakon (GZ-1)
- Ureja gradnjo objektov in pridobivanje gradbenih dovoljenj
- Za elektroenergetske objekte (TP, DV): potrebno gradbeno dovoljenje ali prijava

### Tipi projektne dokumentacije

| Kratica | Ime | Namen |
|---|---|---|
| IDZ | Idejna zasnova | Pred odločitvijo o investiciji |
| IDP | Idejni projekt | Za pridobitev gradbenega dovoljenja |
| PZI | Projekt za izvedbo | Za gradnjo (detajlna dokumentacija) |
| PID | Projekt izvedenih del | Dokumentiranje dejanskih del |
| POV | Projekt za obratovanje in vzdrevaranje | Podlaga za vzdrževanje |

### GIP — Glavni izvajalec projekta
- Odgovoren za koordinacijo gradnje
- Obvezno imel pooblaščenega inženirja

### Vodilna mapa in mapa elaboratov
- **Vodilna mapa**: splošni podatki, kazala, soglasja, dovoljenja
- **Mapa elaboratov**: tehnični opisi, risbe, izračuni (ločene mape za posamezne stroke)

---

## 7.9 IZS — Inženirska zbornica Slovenije

### Pooblaščeni inženir elektroenergetike
Za opravljanje odgovornih nalog projektiranja (podpisovanje projektov) mora inženir biti vpisan v imenik IZS.

**Pogoji za vpis:**
- Ustrezna izobrazba (UNI ali MAG iz elektrotehnike)
- 3 leta delovnih izkušenj (po pridobitvi izobrazbe)
- Opravljen strokovni izpit pri IZS

**Strokovni izpit pri IZS:**
- Zakonodajni del: gradbena in energetska zakonodaja
- Strokovni del: elektroenergetika — projektiranje, standardi, pravilniki

### Kontinuirano izobraževanje
- Po vpisu v IZS: obvezno stalno strokovno izpopolnjevanje (kreditne točke)

---

## 7.10 Drugi relevantni predpisi

| Predpis | Vsebina |
|---|---|
| Pravilnik o varnosti in zdravju pri delu z nevarnostjo el. udara | VPD pri elektroenergetiki |
| Pravilnik o zaščiti pred strelo | Strelodobjemnik (LP), ozemljitev |
| Uredba o elektromagnetni združljivosti (EMC) | Elektromagnetna motnje |
| Pravilnik o varnosti strojev | Električna oprema strojev |
| ATEX direktiva (2014/34/EU) | Električna oprema v eksplozivnih conah |
| Uredba o ekodesignu | Energetska učinkovitost opreme (transformatorji) |

---

## Povzetek — ključni standardi

| Standard | Področje |
|---|---|
| SIST EN 50160 | Kakovost napetosti v distribucijskem omrežju |
| SIST HD 60364 | Nizkonapetostne instalacije (projektiranje, zaščita) |
| SIST EN 50549 | Priključevanje generatorjev (OVE) |
| SIST EN 61936 | Visoko-napetostne instalacije (> 1 kV) |
| SIST EN 60909 | Izračun tokov kratkih stikov |
| SIST EN 60228 | Standardni vodniki za izolirane kable |
| SIST EN 60947 | Nizkonapetostne stikalne naprave |
| IEC 61850 | Komunikacija v elektroenergetskih sistemih |
