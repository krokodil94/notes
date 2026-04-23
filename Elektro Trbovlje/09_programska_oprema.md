# 9. Programska oprema za elektro projektante

---

## 9.1 AutoCAD (Autodesk)

### Vloga v projektiranju
- Risanje situacijskih načrtov, detajlov, prečnih prerezov
- Enopolne sheme in instalacijske sheme
- Osnova za večino elektro projektantov v Sloveniji

### Ključne funkcije za elektro projektante
- **Plasti (Layers)**: ločevanje elementov po tipih (kabli, TP, oznake)
- **Bloki (Blocks)**: standardizirani elektro simboli (transformator, odklopnik, varovalo)
- **Xref**: zunanji referenčni načrti (geodetska podlaga, arhitektura)
- **Annotative scales**: dimenzije in besedilo pri različnih merilih
- **PDF/DWG export**: za oddajanje dokumentacije

### Tipično delovno okolje
```
Geodetski posnetek (DWG) → Xref v AutoCAD
Naris trase NN/SN kabla → Layer "kabel_NN" / "kabel_SN"
Polaganje TP simbola → Block "TP_kiosk"
Kotiranje in opis → Layer "kote", "text"
```

### Standardni sloji (Layers) pri Elektro Ljubljana / SODO
- Obstajajo standardizirani predlogi za projekte za distribucijsko omrežje
- Barve in debeline črt po internih navodilih naročnika

---

## 9.2 ETAP (Operation Technology)

### Vloga
Specializirana programska oprema za analizo elektroenergetskih sistemov.

### Ključne analize v ETAP

| Analiza | Namen | Izhod |
|---|---|---|
| Load flow (pretok moči) | Napetosti in tokovi pri normalnem obratovanju | U, I, P, Q, ΔU% na vsakem elementu |
| Short circuit (kratki stik) | Izračun I"k po metodi impedanc | Icc max, Icc min na vsakem zbiralčišču |
| Protection coordination | Koordinacija zaščitnih relejev | Grafikon karakteristik (log-log), selekcija |
| Cable sizing | Dimenzioniranje kablov | Min. presek glede na ampaciteto in ΔU |
| Arc flash | Analiza energije obloka | PPE kategorija za varno delo |
| Harmonics | Analiza harmonskih motenj | THD, individualni harmoniki |

### Izhodni rezultati
- Poročila o pretokih moči (load flow reports)
- Koordinacijski grafikon zaščit (TCC — Time-Current Curve)
- Enopolna shema (Single-line diagram) — avtomatsko generirana

### Alternativne programske rešitve
- **DIgSILENT PowerFactory**: pogosta alternativa ETAP, razširjena v Evropi
- **NEPLAN**: švicarsko programje za elektroenergetske analize
- **PSS/E**: Siemens, za prenosna omrežja
- **Sincal**: ABB, za distribucijska omrežja

---

## 9.3 GIS — Geografski informacijski sistemi

### Esri ArcGIS
- Profesionalni GIS sistem
- Elektro Ljubljana / SODO vodijo omrežni model v GIS
- Prostorski podatki: lokacije TP, tras kablov, drogov

### QGIS (odprtokodna alternativa)
- Brezplačen, odprtokoden
- Branje in urejanje GIS podatkov (shapefile, GeoJSON)
- Priporočljivo za manjše projekte ali analizo obstoječih podatkov

### Vloga GIS pri projektiranju
- Izvoz tras kablov iz GIS → podlaga za načrt
- Analiza prostora (odmiki od obstoječe infrastrukture)
- Integracija z SCADA podatki (stanja omrežja)

---

## 9.4 DIALux

### Vloga
Projektiranje in izračun razsvetljave (zunanja in notranja).

### Področja uporabe pri Elektro Ljubljana
- Razsvetljava transformatorskih postaj in strojnih prostorov
- Projektiranje javne razsvetljave (ulična, cestna svetila)
- Preveritev zahtev standarda EN 12464 (osvetljenost delovnih mest)

### Izračun osvetljenosti (Illuminance)
```
E = Φ · η · UF / A

E  — osvetljenost [lux]
Φ  — svetlobni tok svetilke [lm]
η  — učinkovitost svetilke
UF — faktor izkoriščenosti (utilization factor)
A  — površina [m²]
```

### Zahteve po EN 12464
| Prostor | Min. osvetljenost Em |
|---|---|
| Pisarniški prostor | ≥ 500 lux |
| Transformatorska postaja | ≥ 200 lux |
| Hodnike, hodniki | ≥ 100 lux |
| Zunanja pot | ≥ 20 lux |

---

## 9.5 Kalkulatorji in priročna orodja

### Spletni kalkulatorji
- Padec napetosti (ΔU)
- Ampaciteta kablov
- Dimenzioniranje varoval
- Kratki stik (preprosti primeri)

### Excel tabele
- Tipični elektro projektanti vzdržujejo Excel tabele za:
  - Dimenzioniranje kablov (padec napetosti in ampaciteta hkrati)
  - Popis materialov (BOM — Bill of Materials)
  - Obremenitev po izvodih

### IEC/SIST standardi v PDF
- Preveritev parametrov (korekcijski faktorji, simboli, oznake)
- Dostop prek SIST (plačljivo) ali prek delodajalca

---

## 9.6 Revit MEP (Autodesk)

### Vloga
- BIM (Building Information Modeling) platforma za elektro instalacije
- Večja gradbena podjetja in arhitekturni biroји
- Pri Elektro Ljubljana manj pogosto, bolj v industrijskem projektiranju

### Prednosti BIM
- 3D model instalacij (konflikti med strohami vidni v modelu)
- Avtomatski popisi materialov
- Koordinacija med elektriko, strojništvom, arhitekturo

---

## 9.7 MS Office in dokumentacija

### Word
- Tehnični opisi, poročila
- Vodilna mapa projekta

### Excel
- Izračuni (padec napetosti, kratki stik)
- Popisi del in materiala (popisi pozicij)
- Primerjave ponudb

### PowerPoint
- Prezentacije investitorjem, občinam, razvojni odbori

---

## 9.8 Programska oprema SODO / Elektro Ljubljana

### Interni sistemi (tipično)
- **DMS (Distribution Management System)**: realnočasno vodenje omrežja
- **GIS aplikacija**: upravljanje omrežnega modela
- **SAP / IFS**: poslovni informacijski sistem (naročila, zaloge, vzdrževanje)
- **SCADA**: nadzor in vodenje (SCADA HMI)

---

## Povzetek — programsko orodje glede na nalogo

| Naloga | Orodje |
|---|---|
| Risanje načrtov | AutoCAD |
| Izračun padca napetosti | Excel / ETAP / spletni kalkulator |
| Izračun kratkega stika | ETAP / Excel |
| Koordinacija zaščit | ETAP / DIgSILENT |
| Prostorski prikaz omrežja | ArcGIS / QGIS |
| Dimenzioniranje razsvetljave | DIALux |
| Energetska analiza | ETAP / NEPLAN |
| Projektna dokumentacija | AutoCAD + Word + Excel |
