

# Tehnični razgovor — Projektant fiksnih omrežij
## Telemach / United Fiber — Studijski vodič

---

## Kazalo datotek

| Datoteka | Tema | Prioriteta |
|---|---|---|
| `01_osnove_optike.md` | Optična vlakna, dB, valovne dolžine | ⭐⭐⭐ |
| `02_ftth_arhitekture.md` | FTTx topologije, P2P vs PON, segmentacija | ⭐⭐⭐ |
| `03_gpon_xgspon_pon.md` | GPON, XGS-PON, OLT/ONT, DBA | ⭐⭐⭐ |
| `04_pasivne_komponente.md` | Splitterji, konektorji, kabli, varjenje | ⭐⭐⭐ |
| `05_projektiranje_omrezja.md` | Projektni proces, IDZ/PGD/PZI, soglasja | ⭐⭐⭐ |
| `06_osp_zunanja_gradnja.md` | Transe, mikrotranse, jaški, drogovi | ⭐⭐⭐ |
| `07_link_budget_izracuni.md` | Link budget, OTDR, izračuni z nalogami | ⭐⭐⭐ |
| `08_ip_ethernet_sloj.md` | VLAN, QoS, PPPoE, triple play | ⭐⭐ |
| `09_hfc_docsis.md` | HFC, DOCSIS 3.1/4.0, migracija → FTTH | ⭐⭐ |
| `10_standardi_regulativa.md` | ITU-T, IEEE, ZEKom-2, AKOS | ⭐⭐ |
| `11_orodja_gis.md` | QGIS, AutoCAD, OTDR, dokumentacija | ⭐ |
| `12_vprasanja_odgovori.md` | Intervju Q&A — vaja pred razgovorom | ⭐⭐⭐ |

---

## Priporočen vrstni red učenja

### Dan 1 — Osnove (fizični sloj)
1. `01_osnove_optike.md` — razumeš svetlobo, dB, valovne dolžine
2. `04_pasivne_komponente.md` — splitterji, konektorji, kabli
3. `07_link_budget_izracuni.md` — znaš izračunati link budget

### Dan 2 — Arhitektura in design
4. `02_ftth_arhitekture.md` — razumeš FTTx, segmentacijo, topologije
5. `03_gpon_xgspon_pon.md` — GPON/XGS-PON v globino
6. `05_projektiranje_omrezja.md` — projektni proces, dokumentacija

### Dan 3 — Gradnja in kontekst
7. `06_osp_zunanja_gradnja.md` — terenska gradnja
8. `09_hfc_docsis.md` — Telemach legacy omrežje
9. `10_standardi_regulativa.md` — zakoni, standardi

### Dan 4 — Dopolnitev in vaja
10. `08_ip_ethernet_sloj.md` — IP/Ethernet sloj
11. `11_orodja_gis.md` — orodja
12. `12_vprasanja_odgovori.md` — **samotestiranje pred razgovorom**

---

## Ključne teme po fazah razgovora

### HR razgovor
- Zakaj Telemach / United Fiber?
- Kaj je United Fiber in kakšna je njegova vloga znotraj Telemach Group?
- Izkušnje z infrastrukturnimi projekti
- Razumevanje razlike HFC ↔ FTTH

### Tehnični razgovor (1. krog)
- GPON arhitektura: OLT → splitter → ONT
- Link budget: znaš izračunati od OLT do ONT
- FTTx terminologija: FTTH, FTTB, ODP, FDH, feeder/distribution/drop
- Pasivne komponente: splitter tipi, konektor tipi, vstavne izgube

### Tehnični razgovor (2. krog / praktični)
- Nariši topologijo za 500 stanovanjski objekt (blokovsko naselje)
- Izračunaj link budget za dano topologijo
- Pojasni projektni proces od IDZ do PZI
- Katera soglasja potrebuješ za gradnjo v javnem prostoru?

---

## Ključni pojmi — hiter glosar

| Pojem | Razlaga |
|---|---|
| OLT | Optical Line Terminal — aktivna oprema v CO |
| ONT/ONU | Oprema pri stranki (Optical Network Terminal/Unit) |
| PON | Passive Optical Network — brez aktivne opreme v terenu |
| GPON | Gigabit PON, ITU-T G.984, 2.5G DS / 1.25G US |
| XGS-PON | 10G Symmetric PON, ITU-T G.9807.1 |
| ODP | Optical Distribution Point — zunanja razdelilna točka |
| FDH | Fiber Distribution Hub — omara s splitterji |
| Splitter | Pasivni optični delilnik signala (1:N) |
| SC/APC | Zeleni konektor, 8° kot, nizek odboj — standard za PON |
| OTDR | Optical Time Domain Reflectometer — merilnik vlakna |
| IDZ | Idejna zasnova — predprojektna faza |
| PGD | Projekt za gradbeno dovoljenje |
| PZI | Projekt za izvedbo |
| AKOS | Agencija za komunikacijska omrežja in storitve RS |
| ZEKom-2 | Zakon o elektronskih komunikacijah |
| HFC | Hybrid Fiber-Coaxial — Telemach legacy |
| DOCSIS | Data Over Cable Service Interface Spec — protokol za HFC |
