# 10. Druga delovna mesta pri Elektro Ljubljana

---

## 10.1 Dispečer (Dispatcher / Network Controller)

### Vloga
Dispečer vodi distribucijsko omrežje v realnem času iz dispečerskega centra. Odgovoren za zanesljivo in varno napajanje odjemalcev.

### Naloge
- Nadzor stanja omrežja prek SCADA sistema
- Ukazi za stikalne manoevre (vklop/izklop odklopnikov in stikal)
- Preurejanje omrežja po okvarah (FDIR — ročno ali polavtomatizirano)
- Koordinacija terenskih ekip pri odpravljanju okvar
- Vodenje delovnih nalogov in dovoljenj za delo (zemeljska dovoljenja)
- Poročanje o dogodkih (izpadi, okvare, prekoračitve)

### Ključna znanja

**SCADA in DMS:**
- Beranje SCADA HMI (grafični prikaz omrežja)
- Interpretacija merilnih vrednosti (U, I, P, Q, cos φ)
- Alarmni sistem — prioritizacija alarmov
- Ukazi na daljavo (RTU/IED)

**Stikalni manevri:**
- Postopek odpiranja/zapiranja odklopnikov in ločilnikov
- Galvanska ločitev — 5 korakov (glejte poglavje 8.7)
- Priključevanje/izključevanje SN izvodov

**Obratovalne sheme:**
- Normalna shema omrežja (NO stikala, odprti iztoki)
- Rezervne napajalne sheme (preurejanje pri okvari)
- Napajanje iz alternativnega RTP pri izpadu

**Varstvo pri delu:**
- Protokol za zemeljska dovoljenja (ZDD)
- Komunikacija s terensko ekipo (ukazi, potrditve)
- IEC 60364 in pravilnik o varnosti pri delu z napetostjo

**Protokoli:**
- IEC 60870-5-101 / 104 (telemetri)
- DNP3
- IEC 61850 (GOOSE, MMS)

### Tipična izobrazba
- Elektrotehnik (SSS ali VSŠ) ali elektro inženir
- Usposabljanje na delovnem mestu (šolanje dispečerja)
- Pooblastilo za upravljanje SN omrežja

---

## 10.2 Vzdrževalec elektro naprav

### Vloga
Vzdrževalec skrbi za redno in investicijsko vzdrževanje elektroenergetske opreme (TP, kablovodi, nadzemni vodi, RTP).

### Naloge
- Redni pregledi TP (vizualni, meritve)
- Vzdrževanje SN stikalnih naprav (mazanje, čiščenje kontaktov)
- Vzdrževanje transformatorjev (meritve izolacije, analiza olja)
- Vzdrževanje zaščitnih naprav (funkcionalni preizkusi relejev)
- Popravila okvar na kablovodih in nadzemnih vodih
- Meritve ozemljilnih uporov

### Ključna znanja

**Elektro meritve:**
- Meritev izolacijske upornosti (megger / megohmeter)
  - Napetost preizkusa: 500 V (NN), 2,5 kV (SN), 5 kV (VN)
  - Min. vrednost: ≥ 1 MΩ (NN), višje za SN/VN
- Meritev ozemljilnega upora (metoda 3 točk, Wenner)
- Meritev upora kontaktov (mikro-ohmmeter)
- Meritev delovnih in brezdelnih izgub transformatorja
- Meritev razmerja navitij transformatorja (TTR)
- Termografska kontrola (IR kamera) — iskanje presegretih kontaktov

**Visoko-napetostna oprema:**
- Vakuumski odklopniki — vzdrževanje, preizkušanje
- SF6 odklopniki — ravnanje s SF6 plinom (GWP faktor, varnostni protokoli)
- Izolatorji — čiščenje, vizualni pregled
- VN varovalo — zamenjava taljive vložke

**Kabelska dela:**
- Montaža kabelskih spojk (termokrčne, hladnokrčne, litokrčne)
- Montaža kabelskih glav (terminacij)
- Lokalizacija okvar kabla (TDR — Time Domain Reflectometry, razsvetljavna metoda)

**Nadzemni vodi:**
- Delo na drogovih (plezalna oprema, košara dvigala)
- Zamenjava izolatorjev in VN vrvi
- Napenjanje vrvi (sag calculation)
- Montaža ozemljilnega vodnika (grounding wire)

### Tipična izobrazba
- Elektrotehnik (SSS)
- Pooblastilo za delo pod napetostjo ali brez napetosti
- IPAF / MEWP certifikat (za dvig z košaro)
- Veljavni pregled delovne opreme in OZO

---

## 10.3 Merilni tehnik

### Vloga
Merilni tehnik vzdržuje sistem merjenja električne energije: montaža, kalibracija, odčitavanje in analiza merilnih naprav.

### Naloge
- Montaža in zamenjava energetskih števcev (AMI — Advanced Metering Infrastructure)
- Preveritev točnosti meritev (primerjalne meritve)
- Odčitavanje podatkov (daljinsko / ročno)
- Analiza kakovosti električne energije (PQ analiza)
- Pregled in vzdrževanje merilnih transformatorjev (MT — merilni transformatorji toka in napetosti)
- Ugotavljanje netehničnih izgub (kraje energije)

### Ključna znanja

**Merilne naprave:**
- Induktivni števci (stara generacija)
- Elektronski števci (nova generacija)
- AMI — pametni števci (smart meters): daljinsko odčitavanje, 15-minutni intervali
- Merilni transformatorji toka (MTT — Current Transformer, CT)
  - Razmerje: npr. 200/5 A
  - Razred točnosti: cl. 0,2; 0,5; 1; 3
- Merilni transformatorji napetosti (MTV — Voltage Transformer, VT)
  - Razmerje: npr. 20 000/100 V
  - Razred točnosti: cl. 0,2; 0,5

**Kakovost električne energije (PQ — Power Quality):**
- Meritve po SIST EN 50160
- THD (Total Harmonic Distortion) — harmonske motnje
- Flikanje (flicker): Pst (kratkotrajno), Plt (dolgotrajno)
- Napetostni useki in prenapetosti
- Neravnovesje napetosti (voltage unbalance)
- Orodja: Fluke 435/437, PQ analizator

**Obračun energije:**
- Dejavna energija: Wh / kWh
- Jalova energija: varh / kvarh
- Tarifna razmerja: višja in nižja tarifa, konice

### Tipična izobrazba
- Elektrotehnik (SSS)
- Usposabljanje za ravnanje z merilnimi napravami

---

## 10.4 Tehnik za zaščite in meritve (Protection & Relay Engineer)

### Vloga
Skrbi za nastavljanje, preizkušanje in vzdrževanje zaščitnih relejev in instrumentacije v RTP in TP.

### Naloge
- Nastavitev parametrov zaščitnih relejev (IED)
- Funkcionalni preizkusi zaščitnih relejev
- Komisioning novih RTP in TP (preizkus opreme pred prvim vklopom)
- Analiza delovanja zaščit po okvari (post-fault analysis, event records)
- Vzdrževanje SCADA/RTU naprav

### Ključna znanja

**Zaščitni releji (IED):**
- Nastavitev parametrov (pickup current, time multiplier, zone reaches)
- Komunikacija: IEC 61850, IEC 60870-5, Modbus
- Preizkuševalna oprema: OMICRON CMC, Megger MPRT

**Preizkušanje relejev:**
- Preizkus delovanja pri nastavljenem toku (pickup test)
- Preizkus časa delovanja (timing test)
- Preizkus selektivnosti (selectivity test)
- Preizkus meritve (CT/VT test)

**Merilni transformatorji:**
- Razred točnosti, razmerje
- Preizkus saturacije (CT saturation test)
- Polarnost (polarity check)

**Analiza okvar:**
- Event records iz IED (digitalni osciloskop)
- Fault distance estimation
- Fault classification (1F, 2F, 3F)

### Tipična izobrazba
- Elektrotehnik (SSS) ali elektro inženir (VSŠ/UNI)
- OMICRON usposabljanje
- Izkušnje z zaščitnimi releji (SEL, Siemens, GE, ABB)

---

## 10.5 Inženir za razvoj omrežja (Network Development Engineer)

### Vloga
Planira dolgoročni razvoj distribucijskega omrežja — kapacitetne analize, investicijsko načrtovanje, priključevanje OVE.

### Naloge
- Analize obremenitve omrežja (sedanje in prihodnje)
- Planiranje novih TP, kablovodov, rekonstrukcij
- Pripravljanje investicijskega programa
- Priključevanje OVE (sončne elektrarne, vetrnice, baterijski sistemi)
- Koordinacija s SODO in AGEN
- Energetske študi (feasibility study, load flow studies)

### Ključna znanja

**Planiranje omrežja:**
- Load flow analiza (ETAP, DIgSILENT, Sincal)
- N-1 kriterij (omrežje mora napajati vse odjemalce ob izpadu enega elementa)
- Kapacitetne analize (cable/transformer loading %)
- Prihodnja obremenitev: rast odjemalcev, EV polnilnice, toplotne črpalke

**Priključevanje OVE:**
- Napetostni dvig pri priključevanju sončnih elektrarn
- Q-U regulacija, P-f regulacija
- Grid code zahteve (SIST EN 50549)

**Investicijsko načrtovanje:**
- CAPEX (Capital Expenditure) — investicijska sredstva
- OPEX (Operational Expenditure) — obratovalni stroški
- Stroškovna-koristna analiza (CBA)
- Regulatorne omejitve (AGEN — RAB, regulirani donos)

**Regulativa:**
- Uredba o metodologiji za določitev omrežnine (AGEN)
- Razvojna načrta SODO (5-letni načrt)
- EU direktive: Clean Energy Package, RED II

### Tipična izobrazba
- Elektro inženir UNI / MAG
- Izkušnje z energetsko analizo
- Zaželena: vpis v IZS

---

## 10.6 Skupne kompetence vseh delovnih mest

### Varstvo pri delu
- Pravilnik o varnosti in zdravju pri delu z nevarnostjo el. udara
- Osebna varovalna oprema (OZO): izolirne rokavice, čelada, varnostni čevlji
- Usposabljanje za varno delo (§10 VZD)

### Komunikacija
- Jasna komunikacija s terenskimi ekipami (radio, telefon)
- Standardni protokoli poročanja o okvarah in stanjih
- Vodenje delovnih nalogov

### Elektro osnove
- Vsi zaposleni morajo razumeti osnove: napetostni nivoji, varnostne razdalje, prepoved dela pod napetostjo brez pooblastila

---

## Povzetek — primerjava delovnih mest

| Delovno mesto | Izobrazba | Ključno znanje | Orodja |
|---|---|---|---|
| Elektro projektant | UNI/MAG EE | Projektiranje, standardi, IZS | AutoCAD, ETAP |
| Dispečer | SSS/VSŠ EE | SCADA, stikalni manevri | SCADA DMS |
| Vzdrževalec | SSS EE | Meritve, mehansko vzdrževanje | Megger, IR kamera |
| Merilni tehnik | SSS EE | Števci, PQ analiza | PQ analizator, AMI |
| Tehnik zaščit | SSS/VSŠ EE | IED nastavitve, preizkušanje | OMICRON |
| Razvojni inženir | UNI/MAG EE | Load flow, planiranje | ETAP, DIgSILENT |
