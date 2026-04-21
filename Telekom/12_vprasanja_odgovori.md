# Intervju Q&A — Vprašanja in Modelni Odgovori

## 1. Osnove optičnih vlaken

**V: Razloži razliko med SMF in MMF. Kdaj uporabiš katero?**

> SMF (Single-Mode Fiber) ima jedro 8–10 µm — svetloba potuje po enem načinu, ni modalne disperzije, razdalje do 80 km+. MMF (Multi-Mode Fiber) ima jedro 50 ali 62.5 µm, več načinov hkrati, omejena razdalja (do 2 km) in pasovna širina. Za FTTH vedno SMF — dolge razdalje, laser oddajniki. MMF samo za LAN in datacenter short-reach.

---

**V: Zakaj za PON obvezno SC/APC in ne SC/UPC?**

> GPON/XGS-PON oddajniki so laserji DFB ali FP — občutljivi na povratne odboje. SC/UPC (ravna poliran konec) ima ORL > 50 dB. SC/APC (8° koten konec) ima ORL > 60 dB — odboj je odklonjen stran od osi vlakna. Razlika 10 dB manj odboja zadostuje, da laser ne "vidi" lastnega odboja in ostane stabilen.

---

**V: Kaj je slabitev optičnega vlakna in od česa je odvisna?**

> Slabitev = izguba moči svetlobe vzdolž vlakna, merjeno v dB/km. G.652.D: 0.35 dB/km @ 1310 nm, 0.20 dB/km @ 1550 nm. Vzroki: Rayleigh sipanje (prevladujoč pri 1310 nm), absorpcija OH ionov (voda), makrobend (preveč upognjen kabel), mikrobend. Daljša valovna dolžina = manj sipanja = manjša slabitev.

---

**V: Kaj je ORL in zakaj je pomemben?**

> ORL = Optical Return Loss — mera koliko svetlobe se odbije nazaj k viru. Enota dB, višja vrednost = manj odboja = boljše. PON laserji so občutljivi na odboje → destabilizacija, šum. Zato SC/APC (ORL > 60 dB) vs SC/UPC (ORL > 50 dB). Pri merjenju OTDR slab ORL pomeni problem na konektorju.

---

## 2. FTTx Arhitektura

**V: Nariši tipično FTTH PON topologijo za blokovsko naselje.**

```
POP / CO
  │
  │ (feeder kabel — 1 vlakno na OLT port)
  ▼
FDH omara v kleti bloka
  │  Splitter 1:4
  ├──► ODP na nadstropju 1 [Splitter 1:16]
  │       ├── Drop → ONT stan. 1.1
  │       ├── Drop → ONT stan. 1.2
  │       └── ... (do 16 stanovanj)
  ├──► ODP na nadstropju 2 [Splitter 1:16]
  └──► ...
```
Skupni split: 1:4 × 1:16 = **1:64**

---

**V: Kaj je razlika med FDH in ODP?**

> FDH (Fiber Distribution Hub) = večja omara s splitterji 1. nivoja, splice tray-i in patch paneli. Stoji v kleteh blokov ali ulično omarico. ODP (Optical Distribution Point) = majhna zunanja razdelilna točka pri stranki (na fasadi, drogu, v jašku), vsebuje splitter 2. nivoja in SC/APC priključke za drop kable. FDH je pred ODP v hierarhiji.

---

**V: Kdaj izbereš centraliziran splitter (v CO) vs porazdeljen (FDH/ODP)?**

> Centraliziran: manj opreme v terenu, enostavnejše upravljanje, primerno za kratke razdalje (<2 km). Problem: feeder mora biti 64 vlaken za 1:64 split, višja izguba (splitter + dolg drop) — pogosto preseže link budget. Porazdeljen: splitter bližje strankam = krajši drop = boljši link budget, fazna gradnja možna, bolj fleksibilen. **Priporočam porazdeljen za realna omrežja.**

---

## 3. PON Tehnologije

**V: Razloži kako GPON ločuje promet za različne stranke na istem vlaknu.**

> Downstream: OLT broadcast pošilja vsem ONT na vlaknu. Vsak GEM frame nosi Port-ID — ONT sprejme samo frame-e z lastnim Port-ID. Zaščita: AES-128 šifriranje. Upstream: TDMA — vsaka ONT oddaja samo v svojem časovnem okencu, ki ga OLT dodeli prek GRANT sporočil. Guard time prepreči kolizije med burst oddajanjem.

---

**V: Kaj je DBA in zakaj je potreben?**

> DBA = Dynamic Bandwidth Allocation. Upstream kapaciteta GPON porta (1.244 Gbps) se deli med vsemi ONT. Brez DBA bi vsaka ONT dobila fiksno kvoto ne glede na dejanske potrebe. Z DBA ONT sporoča OLT koliko bufferja ima (DBRu), OLT pametno dodeljuje timeslote glede na promet in QoS prioritete (T-CONT tipi). Rezultat: boljša izkoriščenost kapacitete.

---

**V: Zakaj prehod na XGS-PON? Kaj moraš zamenjati?**

> XGS-PON daje 10G simetrično (vs GPON 2.5G/1.25G asimetrično). Potrebno za B2B stranke, 4K IPTV, cloud-first aplikacije. Zamenjati moraš samo OLT kartice in ONT pri stranki — pasivna infrastruktura (vlakna, splitterji) ostane enaka! Koeksistenca na istem ODN prek WDM ločevanja valovnih dolžin (XGS-PON DS @ 1577 nm, GPON DS @ 1490 nm — ne interferirajo).

---

## 4. Link Budget in Izračuni

**V: Izračunaj link budget za 1:32 split, feeder 4 km, drop 150 m.**

> Komponente izgub:
> - 2 konektorja × 0.5 dB = 1.0 dB
> - Feeder 4 km × 0.25 dB/km @ 1490 nm = 1.0 dB  
> - Splice-i 20 × 0.1 dB = 2.0 dB
> - Splitter 1:32 = 17.0 dB
> - Drop 150 m × 0.25 dB/km = 0.04 dB
> - Konektor ONT = 0.5 dB
> - **Skupaj: 21.54 dB**
> 
> B+ budget = 28 dB. Marža = 28 − 21.54 = **6.46 dB**. Odštejemo varnostno 3 dB → 3.46 dB rezerve. ✅ Zadostuje z razredom B+.

---

**V: Kdaj potrebuješ razred C+ namesto B+?**

> Ko skupne izgube presežejo 28 dB − 3 dB varnostna marža = 25 dB. Tipično pri: 1:64 split (20.5 dB samo splitter), daljši feeder (>5 km), ali kombinacija. C+ doda 4 dB budgeta (skupaj 32 dB). Primer: 1:64 split + 5 km feeder → izgube ~28–30 dB → C+ potreben.

---

**V: Kaj narediš, ko link budget ne zadostuje?**

> Možnosti po vrsti (od najcenejšega):
> 1. Zmanjšaj število splice-ov (boljše varjenje, manj spojev)
> 2. Skrajšaj drop kabel (prestavi ODP bližje stranki)
> 3. Zmanjšaj split ratio (1:32 namesto 1:64) — manj strank na port
> 4. Preseli splitter bližje stranki (porazdeljena topologija)
> 5. Poveča razred OLT (B+ → C+) — zamenjava opreme
> 6. Prestavi POP bližje (skrajša feeder) — drago, nova lokacija

---

## 5. Projektiranje in Gradnja

**V: Kakšna je razlika med IDZ, PGD in PZI?**

> IDZ (Idejna zasnova): najzgodnejša faza, principielna rešitev, groba trasa, stroškovna ocena — za odločitev o investiciji. PGD (Projekt za gradbeno dovoljenje): podlaga za gradbeno dovoljenje, podrobna trasa na katastru, soglasja upravljavcev, pripravi pooblaščen projektant (IZS). PZI (Projekt za izvedbo): detajlni izvedbeni načrti za gradbišče, kabelska knjiga, specifikacije materiov, navodila za testiranje.

---

**V: Katera soglasja potrebuješ za FTTH gradnjo v urbanem okolju?**

> Odvisno od trase, tipično:
> - **DRSI**: posegi v državne ceste (regionalne, magistralne)
> - **Občina**: občinske ceste, parki, javne površine
> - **SODO**: obešanje na elektro drogove
> - **Telekom / T-2**: skupna raba obstoječe kanalizacije
> - **Lastniki parcel**: za zasebna zemljišča
> - Morda: DARS (AC), SŽ (železnica), ARSO (vodotoki)
> ZEKom-2 daje operaterjem pravico gradnje po javnih površinah — ni "prositi", je pravica.

---

**V: Kdaj izbereš mikrotraso namesto klasičnega rova?**

> Mikrotrasa: obstoječ asfalt, urbana ulica, hitrost gradnje prioriteta, proračun omejen. Prednost: 3–5× cenejše, hitro, manj motenj prometa. Slabost: omejena globina (zamrzovanje!), ni za zelenice, zahteva vpihavanje vlaken. Klasičen rov: zelenice, nova gradbišča, kjer ni asfalta, kjer je potreb po večji globini (zaščita pred zmrzovanjem ali kasnejšimi deli na cesti).

---

## 6. Telemach / United Fiber Specifično

**V: Zakaj Telemach gradi United Fiber FTTH, čeprav ima obstoječe HFC omrežje?**

> HFC z DOCSIS 3.1 doseže ~10 Gbps skupno, a je asimetrično in deli bandwidth med strankami. Upgrade na DOCSIS 4.0 zahteva drago zamenjavo nodeov in amplifierjev. FTTH XGS-PON daje 10G simetrično per stranko, brez amplifierjev (nižji OPEX), nižje latence. Konkurenci (Telekom SLO, T-2) gradita FTTH. EU cilj 2030: gigabit za vsa gospodinjstva. Dolgoročno FTTH nudi nižji OPEX in neomejeno nadgradljivost (zamenjava samo OLT/ONT, infrastruktura ostane).

---

**V: Kaj je N+0 in zakaj je relevantno za Telemach?**

> N+0 = HFC topologija z 0 amplifierji za optical nodom. Namesto amplifierjev, optika gre do vsake skupinice hiš. Prednosti: ni šuma amplifierjev, boljši upstream, manj vzdrževanja. Relevantno za Telemach kot vmesna rešitev: Remote PHY nodeji + N+0 poveča kapaciteto HFC brez polnega FTTH rollout-a. Hkrati gradi United Fiber FTTH — dolgoročno HFC se umika.

---

**V: Prednosti XGS-PON za poslovne stranke?**

> 10G simetrično: poslovni kupci potrebujejo visok upload (backup v cloud, video konference, VPN). GPON daje samo 1.25G US na port — pri 1:32 split = ~40 Mbps per stranka v peak. XGS-PON pri 1:32 split = ~300 Mbps US per stranka. SLA možnost: nižji split ratio (1:4 ali 1:8) za B2B → garantirane hitrosti. Latenca: 1–2 ms (XGS-PON) vs 5+ ms HFC.

---

## 7. Mehke Kompetence

**V: Kako koordiniraš pridobivanje soglasij za večjo FTTH traso?**

> Vzporedno pošiljanje vlog vsem upravljavcem takoj po pripravi PGD načrtov — ne zaporedno. Vsak upravljavec ima zakonske roke (DRSI 30–60 dni). Medtem se pripravi PZI, da ni izpada časa ko soglasja pridejo. Slediti posameznim vlogam, opominjati, eskalirati pri zamudah. Kdaj upravljavci postavljajo pogoje: vgradi v PZI in stroškovno oceno.

---

**V: Opiši tipičen projekt FTTH od začetka do konca.**

> 1. Tržna analiza: kateri areal, koliko gospodinjstev, penetracija  
> 2. IDZ: arhitektura omrežja, okvirna trasa, investicijska ocena  
> 3. GIS analiza: obstoječa infrastruktura, terenska ogleda  
> 4. PGD: podrobna trasa na katastru, soglasja, gradbeno dovoljenje  
> 5. PZI: kabelska knjiga, izvedbeni načrti, specifikacije  
> 6. Razpis in izbor izvajalcev  
> 7. Gradnja: trasa, jaški, FDH, ODP — fazna gradnja po prioritetnih ulicah  
> 8. Testiranje: OTDR vsak kabel, power meter, protokoli  
> 9. Aktivacija OLT, ONT pri prvih strankah  
> 10. As-built dokumentacija, GIS vnos, predaja omrežja obratovanju  

---

**V: Kaj narediš, ko stranka poroča, da nima interneta in sumisš optično napako?**

> 1. Preveri OLT: ali je ONT na portu "operational" ali "down"?  
> 2. Preveri optično moč na OLT strani (RSSI za ta ONT)  
> 3. Če nizka moč ali ONT down: problem na optičnem traktu  
> 4. Z OTDR izmeri od FDH do ODP — lokaliziraj napako (razdalja do napake)  
> 5. Pošlji tehnika na lokacijo: preveri konektor, drop kabel, muffo  
> 6. Popravi (splice ali zamenjava kabla), preveri z OTDR in power meter  
> 7. ONT se sama registrira ko je signal v redu  
> 8. Dokumentiraj napako in popravilo v sistemu  

---

## 8. Trik vprašanja

**V: Kakšen je dejanski throughput, ki ga stranka dobi na GPON 1:64 splitu?**

> GPON port: 2.488 Gbps DS. Pri 1:64 split in 40% penetraciji = ~26 aktivnih strank. Peak concurrent usage (80/20 pravilo): ~20 hkratnih. 2488 Mbps ÷ 20 = ~124 Mbps per stranka v peak. V realnosti: 300–1000 Mbps ker je overbooking realen (ne vsi hkrati na full), plus DBA učinkovito izkorišča kapaciteto.

---

**V: Ali je GPON res "pasivno" omrežje?**

> PON = Passive Optical Network — pasivno se nanaša na to da v terenu (med OLT in ONT) ni aktivnih elektronskih elementov, samo pasivna optika (vlakna, splitterji). OLT v CO in ONT pri stranki sta aktivni napravi. "Pasivno" znači: brez napajanja v terenu, brez vzdrževanja elektronike zunaj, večja zanesljivost.

---

**V: Koliko vlaken potrebuješ v feeder kablu za 500 stanovanj pri 1:64 splitu?**

> 500 stanovanj ÷ 64 = 7.8 → **8 OLT portov** → 8 vlaken v feeder kablu (1 vlakno per OLT port). Dodaj rezervo: 20–50% = **12–16 vlaken skupaj**. Standardni kabel: 12F ali 24F. Izberi 24F za prihodnostno kapaciteto.
