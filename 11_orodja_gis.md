# Orodja za Projektiranje — GIS, CAD, Testiranje

## 1. GIS Orodja

### QGIS (Open Source)
- Brezplačen, odprtokoden GIS
- Deluje na Windows/Linux/Mac
- **Koordinatni sistem za Slovenijo: D96/TM (EPSG:3794)**
  - Tudi starejši: D48/GK (Gauss-Krüger, EPSG:3912) — zastareva
  - Pretvorba: `Settings → CRS`

**Ključne funkcije za FTTH:**
- Uvoz katasterskih podatkov (SHP, GeoPackage)
- Risanje tras na ortofotu (DOF — Digitalni Ortofoto, ARSO)
- Merjenje dolžin tras
- Prostorske analize (buffer zone, bližina obstoječe infra)
- Izvoz za AutoCAD (DXF format)

**Podatkovni viri za Slovenijo:**
- **ARSO**: geoportal.arso.gov.si — DOF, DEM, vodni kataster
- **GURS** (Geodetska uprava RS): kataster, DTK (digitalna topografska karta)
  - eprostor.gov.si — WMS servisi
- **DRSI**: podatki o cestah in infrastrukturi
- **iObčina / PISO**: prostorski načrti občin

### ArcGIS (Esri)
- Komercialni standard pri večjih operaterjih
- ArcGIS Pro (desktop), ArcGIS Online (cloud)
- Bolje integrirano z enterprise sistemih
- Licence: drage, tipično pri večjih podjetjih (Telekom SI, SODO)

### Google Earth Pro
- Hitra vizualizacija tras na satelitskih posnetkih
- Brezplačen (bila plačljiva, zdaj brezplačna)
- Primerno za: terenska ogleda predpriprava, prezentacije naročniku
- NI primerno za: natančne meritve (koordinatna natančnost ±1–5 m)

---

## 2. CAD Orodja

### AutoCAD (Autodesk)
- Industrijski standard za tehnične načrte
- Ključne datoteke: DWG (nativni), DXF (izmenjava)
- Za FTTH projektiranje:
  - Situacijski načrt na podlagi ortofota ali katastra (georeferencirani DWG)
  - Prečni prerezi tras (kje cev, na kateri globini)
  - Vzdolžni profili (terenska višinska kota vs globina polaganja)
  - Detajli prečkanj (pod cesto, reko)
  - Shematski načrti omrežja

**Tipičen workflow:**
```
QGIS: trasa v GIS → DXF izvoz
AutoCAD: DXF uvoz, dodaj prereze, kotiranja, legende, žig projektanta
```

### MicroStation (Bentley)
- Alternativa AutoCAD-u
- Pogost v infrastrukturnih projektih (ceste, železnice)
- Manj pogost za telekomunikacije v SLO

---

## 3. Fiber Management / Network Inventory Sistemi

### Kaj so to?
Sistemi ki hranijo kompletne podatke o optičnem omrežju:
- Lokacija vsakega vlakna, konektorja, splitterja, opreme
- Logične povezave (OLT port → ONT)
- Kapaciteta (prosta vlakna, zasedeni porti)
- Servisne podatke (katera stranka je na kateri ONT)

### Komercialni sistemi:

| Sistem | Vendor | Opis |
|---|---|---|
| **NEMO** | Nokia | GIS-based fiber inventory, pogost v Evropi |
| **Smallworld** | GE (zdaj Verisk) | Telco GIS, enterprise raven |
| **OSPInsight** | FiberLocator | Cloud-based, manjše operaterji |
| **Vetro FiberMap** | Vetro | Cloud GIS za fiber |
| **GPON.io** | — | Odprtokodna alterativa |

**Telemach/United Fiber**: verjetno lasten ali prilagojen sistem, vprašaj na razgovoru.

### Ključni koncepti omrežnega inventarja:
- **Node** = vsak fizični element (kabel, muffa, ODP, OLT port)
- **Circuit** = logična pot od A do B (end-to-end)
- **Fiber record** = vsako vlakno ima ID, barvo, kabel, pozicijo v kablu
- **As-built vnos** = po gradnji vnesi dejanske podatke

---

## 4. Merilni Instrumenti

### OTDR (Optical Time Domain Reflectometer)

**Vodilni proizvajalci:**
- EXFO (FTB-1 Pro, MaxTester serija) — standard v Evropi
- Viavi Solutions (SmartOTDR, T-BERD)
- Yokogawa (AQ7280)
- AFL (NOYES serija)

**Ključni parametri:**
- Valovna dolžina: 1310/1490/1550/1625 nm
- Dinamični doseg: 30–50 dB (določi max razdaljo merjenja)
- Event deadzone: 1–5 m
- Attenuation deadzone: 5–50 m

**Praktični nasveti:**
- Za PON merjenje: priključi OTDR na OLT stran FDH
- Vsak arm splitterja meri posebej (dostop pri ODP)
- Vedno shrani trace (SOR format — Bellcore standard)
- Trace analiza: EXFO FastReporter, Viavi FiberTrace

### Power Meter + Light Source

- Najenostavnejša meritev: TX moč na A koncu, RX moč na B koncu
- Razlika = vstavna izguba trase
- Za prevzem pred OTDR meritvijo
- Cena: 200–500 EUR za set

### VFL — Visual Fault Locator

- Vidna rdeča laserska svetloba (650 nm)
- Vidna s prostim očesom na vlaknu (do 5 km)
- Primerna za: iskanje preloma vlakna, identifikacija vlakna v kablu
- **Nikoli ne gledaj direktno v konektor** — čeprav VFL "šibkejši", vseeno nevaren

### Spectrum Analyzer (za HFC)

- Meri RF signal na koaksialnem kablu
- Preveri DS in US frekvence, moč, šum
- Prisoten pri HFC node vzdrževanju
- Brands: Anritsu, Rohde & Schwarz, Lektro

### Fiber Identifier

- Ugotovi ali vlakno nosi signal (brez prekinitve)
- Zaznava tok signala skozi upogib vlakna
- Varno za: identifikacijo živih vlaken pred delom

---

## 5. Dokumentacija — Standardi in Prakse

### Kabelska knjiga
Temeljni dokument omrežja. Vsebuje za vsak kabel:

| Polje | Vsebina |
|---|---|
| ID kabla | Unikatna oznaka |
| Od – Do | Lokacija začetka in konca |
| Tip kabla | G.652.D, G.657.A2, itd. |
| Število vlaken | 12, 24, 48... |
| Vlakna | Vsako vlakno: ID, barva, cevka, OTDR izguba |
| Splici | Lokacija, izguba vsakega spoja |
| Konektorji | Tip, lokacija |
| Status | Prosto / zasedeno / rezervirano |

### Situacijski načrt
- Koordinatno georeferencirani načrt
- Merilo: 1:500 (urbano) do 1:5000 (ruralno)
- Vsebuje: tras, jaški, FDH, ODP, prečkanja
- Format: DWG + PDF

### Šablona poročila OTDR meritve
Po ITU-T L.40 ali EN 61280-4-2:
- Tip instrumenta, datum, operater
- Valovna dolžina, pulzna širina
- Trace graph
- Tabela eventov (razdalja, izguba, komentar)
- Skupna izguba trase
- Podpis in žig

---

## 6. Hitri povzetek — kar morate znati na razgovoru

1. QGIS = brezplačen GIS, za SLO koordinatni sistem D96/TM (EPSG:3794)
2. AutoCAD = situacijski načrti, prečni prerezi, projektna dokumentacija
3. Fiber management sistem = inventar vsakega vlakna, konektorja, opreme
4. OTDR = merjenje slabitve in lokalizacija napak po časovni domeni
5. Power meter + light source = enostavna meritev vstavne izgube
6. VFL = vidna rdeča svetloba za iskanje prelomov (do 5 km)
7. EXFO, Viavi, Yokogawa = vodilni OTDR proizvajalci
8. As-built dokumentacija: GIS vnos + kabelska knjiga + OTDR protokoli
9. SOR format = standard za shranjevanje OTDR trace podatkov
10. DOF (ortofoto) + kataster + GIS = osnova za trasiranje v Slovenij
