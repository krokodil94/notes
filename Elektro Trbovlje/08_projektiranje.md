# 8. Elektro projektiranje

---

## 8.1 Vloge v gradbenem projektu

### Projektant (Designer)
- Pripravi projektno dokumentacijo (risbe, izračune, opise)
- Podpiše s pooblaščenem inženirjem (žig IZS)
- Odgovoren za skladnost projekta z zakoni in standardi

### Pooblaščeni inženir (Responsible Engineer)
- Vpisan v imenik IZS
- Prevzame strokovno odgovornost za projekt
- Podpiše in žigosa projektno dokumentacijo

### GIP — Glavni izvajalec projekta
- Koordinira gradnjo (ne projektiranja)
- Imenovan pri pridobivanju gradbenega dovoljenja

### Nadzornik (Construction supervisor)
- Nadzira gradnjo v skladu z PZI
- Mora biti vpisan v imenik IZS
- Podpiše PID (Projekt izvedenih del)

---

## 8.2 Faze projektne dokumentacije

### IDZ — Idejna zasnova
- **Namen**: preveritev izvedljivosti investicije
- **Vsebina**: groba skica rešitve, opis, ocena stroškov
- **Ni obvezna** za pridobitev dovoljenja, a priporočljiva za večje projekte
- Pridobitev **smernic** od soglasodajalcev

### IDP — Idejni projekt
- **Namen**: pridobitev **gradbenega dovoljenja** (za zahtevne objekte)
- **Vsebina**: situacijski načrt, tlorisi, prerezi, opis, energetska bilanca
- Priloži se vlogi za gradbeno dovoljenje
- Soglasja soglasodajalcev (Elektro Ljubljana, SODO, občina, DRSI...)

### PZI — Projekt za izvedbo
- **Namen**: podlaga za **gradnjo**
- **Vsebina**:
  - Tehnični opis
  - Situacijski načrte (katastrski prikaz tras)
  - Sheme (enopolna shema, shema zemljitve)
  - Detajlni načrti (prečni prerezi jarkov, detajli TP)
  - Izračuni (padec napetosti, kratki stik, ozemljilni upor)
  - Popisi del in materiala (BOQ — Bill of Quantities)
- Žig pooblaščenega inženirja obvezen

### PID — Projekt izvedenih del
- **Namen**: dokumentacija **dejansko izvedenih del**
- **Vsebina**: PZI s vrisanimi dejanskimi izmiki od projekta
- Priloži se vlogi za **uporabno dovoljenje**
- Podpiše nadzornik

### POV — Projekt za obratovanje in vzdrževanje
- **Namen**: navodila za vzdrževanje
- **Vsebina**: tehnični listi opreme, sheme, navodila za varno delo

---

## 8.3 Elektro projektna dokumentacija — vsebina

### Vodilna mapa
- Kazalo
- Splošni podatki o objektu
- Soglasja in pogoji priključitve
- Gradbeno dovoljenje (kopija)
- Podatki o odgovornem projektantu

### Tehnični opis
- Opis obstoječega stanja
- Opis predvidenih del
- Utemeljitev tehničnih rešitev
- Navezava na standarde in predpise

### Izračuni
- Padec napetosti na novih odsekih
- Tok kratkega stika (za dimenzioniranje zaščit in opreme)
- Ozemljilni upor (predračun in preveritev)
- Dimenzioniranje transformatorja
- Koeficient sočasnosti (za obremenitev)

### Risbe in načrti

| Vrsta risbe | Opis |
|---|---|
| Situacijski načrt | Potek tras v prostoru (M 1:500 ali 1:1000) |
| Enopolna shema (Single-line diagram) | Grafična predstavitev el. sheme |
| Shema ozemljitve | Ozemljitveni sistem objekta |
| Prečni prerez jarka | Detajl polaganja kabla |
| Tloris TP | Razporeditev opreme v TP |
| Detajlne risbe | Spojke, priključki, oznake |

---

## 8.4 Enopolna shema (Single-line diagram)

Grafična predstavitev elektroenergetskega sistema z eno linijo namesto treh faz.

### Simboli v enopolni shemi

| Simbol | Element |
|---|---|
| Navpična črta | Zbiralnice (busbar) |
| Horizontalna puščica | Izvod / dovod |
| Krog z X | Odklopnik |
| Krog brez X | Bremenstikalo |
| Ravna črta z diagonalno | Ločilnik |
| Trikotnik / zvezda | Transformator |
| Trikotnik | Varovalo |
| Kvadrat z diagonalo | Meritev |

### Primer enopolne sheme NN razvoda TP

```
[20 kV SN kabel] → [VN stikalno polje] → [Transformator 630 kVA, Dyn11]
                                                ↓
                                    [NN RG zbiralnice]
                                    /     |      \      \
                               [A1]    [A2]   [A3]   [B1]
                             400A NH  400A NH  160A NH  160A NH
                             (kabel  (kabel   (kabel   (kabel
                              SQ1)    SQ2)    SQ3)    SQ4)
```

---

## 8.5 Energetsko soglasje za priključitev (ESS)

### Postopek pridobitve priključka na distribucijsko omrežje

**1. Vloga za priključitev:**
- Oddana pri Elektro Ljubljana / SODO
- Priložiti: parcelna številka, lokacijska informacija, opis objekta, zahtevana moč

**2. Projektni pogoji (soglasje za priključitev):**
- Elektro Ljubljana izda pogoje za priključitev
- Določa: mesto priključitve, tip kabla / voda, zahtevana zaščita, merilno mesto

**3. Projekt priključka (elektro projektant):**
- Pripravi projekt priključka (SN ali NN) v skladu s pogoji Elektro Ljubljana
- PZI za priključitev

**4. Soglasje k projektu:**
- Elektro Ljubljana / SODO pregleda projekt
- Izda soglasje k projektu

**5. Gradnja priključka:**
- Izvede pooblaščeni izvajalec (elektro podjetje z ustreznimi pooblastili)
- Nadzor — nadzornik

**6. Tehnični pregled in priključitev:**
- Elektro Ljubljana izvede pregled
- Ob ustreznosti: priključitev na omrežje, montaža merilne naprave

---

## 8.6 Soglasodajalci in koordinacija

Pri projektiranju elektroenergetskih objektov je potrebno pridobiti soglasja:

| Soglasodajalec | Področje |
|---|---|
| Elektro Ljubljana / SODO | Priključitev na distribucijsko omrežje |
| Telekomunikacijski operaterji | Telekomunikacijski vodi |
| DRSI | Državne ceste (prečkanja, vzporedni poti) |
| Občina / OPPN | Lokacijski pogoji (GJI — gospodarska javna infrastruktura) |
| Komunala | Vodovod, kanalizacija, plinovod (odmiki, prečkanja) |
| Ministrstvo za okolje | Varstvo narave, EGS (ekološko omrežje) |
| Ministrstvo za obrambo | Obrambni pas, koridorji |

---

## 8.7 Varstvo pri delu v elektroenergetiki

### Varnostne cone pri NN (do 1 kV)

| Cona | Razdalja | Pogoji |
|---|---|---|
| Prepovedana cona | 0 m (neposreden dotik) | Prepovedano brez galvanske ločitve |
| Cona neposrednega dela | 0–0,3 m | Le z osebno zaščitno opremo (OZO) |
| Opozorilna cona | > 0,3 m | Previdnost |

### Varnostne cone pri SN (20 kV)
- Razdalja brez napetosti: ≥ 0,5 m (galvanska ločitev = ločilnik + ozemljitev)
- Varno delo: postopek: IZKLOPITI — ZAVAROVATI — PREVERITI — OZEMLJITI

### Postopek galvanske ločitve (5 korakov)
1. **Izklopiti** (odklop od napetosti)
2. **Zavarovati** pred ponovnim vklopom (ključavnica, tablica)
3. **Preveriti odsotnost napetosti** (voltmeter, indikator napetosti)
4. **Ozemljiti in kratko-stičiti** (vzpostaviti delovni ozemljitveni spoj)
5. **Zaščititi** pred sosednjimi napetostmi (ograje, prepreke)

---

## 8.8 GIS — Geografski informacijski sistem

### Vloga GIS pri Elektro Ljubljana
- Evidenca omrežnih elementov (kabli, transformatorji, TP, drogovi)
- Prostorski prikaz omrežja na geodetski podlagi
- Osnova za planiranje in projektiranje
- Integracija s SCADA (stanja stikalnih naprav)

### Podatki v GIS
- Tip in presek kablov / vodov
- Dolžine odsekov
- Lokacije TP, RTP, stikalnih naprav
- Priključene odjemalce (merilna mesta)
- Hkratna obremenitev (s SCADA integracijo)

---

## Povzetek — koraki elektro projekta

```
1. Zbiriti podloge (kataster, GIS, podatki o obstoječem omrežju)
2. Pridobiti pogoje (Elektro Ljubljana, SODO, soglasodajalci)
3. Projektna rešitev (tehnični opis, izračuni)
4. Risbe (situacija, sheme, detajli)
5. Popisi del in materiala
6. Pridobiti soglasja k projektu
7. Podpis pooblaščenega inženirja (žig IZS)
8. Izvedba (PZI → gradnja → nadzor → PID)
9. Tehnični pregled in priključitev
```
