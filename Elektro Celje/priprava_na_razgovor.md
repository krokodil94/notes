
## 3. TELEKOMUNIKACIJSKA OMREŽJA V ELEKTRODISTRIBUCIJI

### Topologije

- **Zvezdasta** – RTP je center, RP/TP so veje (preprosta, a brez redundance)
- **Obroč (Ring)** – vsaka postaja je del obroča; izpad ene povezave ne povzroči izpada vozlišča
- **Mrežasta (Mesh)** – visoka redundanca, kompleksno upravljanje

- Elektro podjetja tipično gradijo **obroče s Spanning Tree / RSTP** ali **SDH obroče**
Spanning Tree Protocol (STP) in Rapid Spanning Tree Protocol (RSTP, IEEE 802.1w) sta protokola, ki omogočata redundantno mrežno topologijo brez zanke v Ethernet omrežju.
Tipično se uporablja v LAN omrežjih ali industrijskih omrežjih, kjer obstaja potreba po rezervni poti, če primarna povezava odpove.
Kako deluje?
Mreža z več povezanimi stikali lahko ustvari zanke. STP: Identificira “root bridge” (glavno stikalo), Izračuna minimalni set povezav, da ne nastanejo zanke .Drugi povezavi postavi v blocking mode, dokler primarna ne odpove
RSTP je hitrejša verzija STP, ob napaki preklopi poti v sekundah, ne v minutah.
Prednosti: Preprosta implementacija. Dovolj za manj kritične obroče ali kjer so Ethernet linki relativno poceni. Ni potrebna specializirana oprema.
Slabosti
Hitrost preklopa (STP: 30–50s, RSTP: ~1–5s) je lahko prepočasna za kritične elektro obroče, kjer je stabilnost ključna. Ni optimizirana za sinhronizacijo ali transport velikih količin podatkov, kot je SCADA ali telemetrija.


SDH obroči (Synchronous Digital Hierarchy)

SDH je telekomunikacijski standard za prenos podatkov po optičnih vlaknih. Omogoča gradnjo obročev z redundanco, kjer lahko signal teče v obe smeri (dual ring), in ob napaki samodejno preusmeri tok. Pogosto se uporablja za kritične elektro omrežne aplikacije, SCADA sisteme, daljinske telemetrije in nadzor elektro distribucije.
Signal teče v obroču, običajno v dveh smereh: primarna in rezervna. Ob izpadu primarne poti SDH obroč samodejno preklopi na drugo smer (hitro: v milisekundah). Ponuja visoko zanesljivost (availability 99,999%).
Prednosti
Hitre odzivne čase ob napaki (ms). Sinhronizacija za SCADA, telemetrijo, zaščito daljnovodov. Omogoča QoS in različen prenos (telefonija, Ethernet, telemetrija) preko iste infrastrukture.
Slabosti
Dražja oprema (SDH multiplexerji). Več kompleksnosti pri upravljanju.

Elektro podjetja običajno uporabljajo SDH obroče za kritične povezave med daljnovodi, trafostanicami in SCADA sistemi zaradi hitrega preklopa in zanesljivosti. STP/RSTP Ethernet obroči se uporabljajo predvsem tam, kjer so potrebe po kritičnosti manjše ali za interno omrežje z več preprostimi napravami.


### Prenosne tehnologije

#### Optična vlakna (fiber optics)
- **Enomodni (Single-Mode, SMF, G.652)** – dolge razdalje (>2 km), 1310 nm in 1550 nm, tanek core (~9 µm)
- **Večmodni (Multi-Mode, MMF)** – kratke razdalje (<550 m za 10G), debelejši core (50/62,5 µm)
- Elektrodistribucija večinoma gradi **OPGW** (Optical Ground Wire – optika v ozemljitveni vrvici daljnovodov) ali **ADSS** (All-Dielectric Self-Supporting – optika v nekovinskem kablu, obešenem med drogovi)
- **Konektorji**: SC/APC (zeleni, kot 8°, manj odboja – za distribucijo signala), SC/UPC (modri), LC, FC
- **Splicing**: fuzijsko varjenje vlaken, mehanski spoji



#### Ključne meritve in parametri optičnih vlaken
| Parameter | Tipična vrednost | Pomen |
|-----------|------------------|-------|
| Slabljenje (attenuation) | ≤ 0,35 dB/km @ 1310 nm; ≤ 0,2 dB/km @ 1550 nm | Izguba signala |
| Disperzija | ps/(nm·km) | Razmazanost pulzov, omejuje pasovno širino |
| Odboj (reflectance) | < -55 dB (APC) | Odbiti signal nazaj k viru |
| **Optični proračun (link budget)** | Tx moč – celotno slabljenje ≥ Rx občutljivost | Preveriti pred vsako inštalacijo |


#### OTDR (Optical Time Domain Reflectometer)
- **Najpomembnejše merilno orodje za optiko**
- Deluje na principu radarskega echa: pošlje pulz, meri odboje nazaj
- Iz dobljene krivulje razbereš: lokacijo preloma, slabljenje spojk, dolžino vlakna, slabljenje konektorjev
- Znati moraš interpretirati OTDR trace: normalen Fresnelov odboj, Rayleighevo sipanje, prelom


#### SDH (Synchronous Digital Hierarchy)
- Standard za prenos po optičnih vlaknih, star ampak še pogosto prisoten v energetiki
- Hierarhija: **STM-1** (155 Mbit/s), STM-4 (622 Mbit/s), STM-16 (2,5 Gbit/s)
- Ključna prednost: deterministična zakasnitev, vgrajena zaščita (APS – Automatic Protection Switching)
- Obroči: **SNCP** (SubNetwork Connection Protection) in **MS-Spring**
- Zamenjuje ga Carrier Ethernet / IP/MPLS

#### Carrier Ethernet / L2 omrežja
- **IEEE 802.1Q** – VLAN označevanje
- **IEEE 802.1ad** – Q-in-Q (double tagging, provider bridges)
- **IEEE 802.1D / 802.1w RSTP** – Spanning Tree za preprečevanje zank; RSTP konvergira v <1 s
- **IEEE 802.1s MSTP** – Multiple Spanning Tree, različne instance za različne VLAN-e
- **ERPS (G.8032)** – Ethernet Ring Protection Switching, sub-50 ms zaščita obroča

#### IP/MPLS omrežja
- **MPLS** (Multiprotocol Label Switching) – prenos paketov po oznakah, ne IP naslovih
- **LSP** (Label Switched Path) – vnaprej določena pot v MPLS domeni
- **PE/CE** (Provider Edge / Customer Edge) router
- **L3 VPN (RFC 4364)** in **L2 VPN (VPWS, VPLS)** – segmentacija prometa
- **LDP / RSVP-TE** – protokola za vzpostavljanje LSP
- Zakaj je MPLS primeren za energetiko: deterministične poti, QoS, TE (traffic engineering)

#### Radijske (mikrovalovne) povezave
- **Point-to-Point (PtP)** mikrovalovi: 6–38 GHz (pogosto 7, 13, 15, 18, 23 GHz za distribucijo)
- **Frekvenčni pas** določa zmogljivost in doseg: nižji pas = večji doseg, manjša pasovna širina
- Sestavni deli: antena (parabolična), IDU (Indoor Unit – modem/radio), ODU (Outdoor Unit – RF del)
- **Link budget**: EIRP – FSL – slabljenje ozračja – ostale izgube ≥ RSL (Received Signal Level), z ustrezno rezervo (fade margin, tipično 25–30 dB)
- **Modulacije**: QPSK, 16/64/128/256/1024-QAM – višja modulacija = večja hitrost, a manjša odpornost na motnje
- **ATPC** (Automatic Transmit Power Control) – avtomatska regulacija oddajne moči
- **Frekvenčni koordinacija**: obvezna pri AKOS (Agencija za komunikacijska omrežja in storitve RS)
- **Antenske postaje**: dostop omejen, varnost pri delu na višini, RF nevarne cone

#### LTE/4G privatna omrežja (Private LTE)
- Nekateri distribucijski operaterji gradijo lastne LTE mreže za daljinsko odčitavanje in avtomatizacijo (pametno omrežje)
- **Frekvence**: PPDR pasovi (npr. 800 MHz za dobro pokritost)
- **eNodeB**, **EPC** (Evolved Packet Core): MME, SGW, PGW, HSS


## 4. OMREŽNE TEHNOLOGIJE IN KONFIGURACIJE

### TCP/IP model (osvežitev)
| Plast | Protokoli | Naprave |
|-------|-----------|---------|
| Aplikacijska | HTTP, HTTPS, SFTP, SSH, SNMP, Syslog, NTP, DNP3-TCP, IEC 104 | – |
| Transportna | TCP, UDP | – |
| Omrežna | IP (v4/v6), ICMP, OSPF, BGP | Router |
| Podatkovna | Ethernet, 802.1Q, PPP, HDLC | Switch, Bridge |
| Fizična | Fiber, bakreni kabel, radio | Kabel, antena |

### Usmerjevalni protokoli
- **OSPF** (Open Shortest Path First) – link-state, hiter, za notranje AS omrežje; areas (backbone area 0)
- **BGP** (Border Gateway Protocol) – za medoperaterske povezave, policy-based routing
- **IS-IS** – alternativa OSPF, pogostejši v telekomunikacijskih jedrnih omrežjih


### QoS (Quality of Service)
- Kritično za energetiko: SCADA promet mora imeti prioriteto pred video/podatki
- **DiffServ**: DSCP oznake v IP glavi (EF = Expedited Forwarding za visoko prioriteto)
- **802.1p**: CoS oznake v Ethernet glavi (0–7)
- Mehanizmi: PQ (Priority Queuing), WFQ, CBWFQ, policing, shaping


### NTP (Network Time Protocol)
- Sinhronizacija časa je v energetiki KRITIČNA za pravilno časovno žigosanje SCADA dogodkov
- **IEEE 1588 PTP** (Precision Time Protocol) – sub-mikrosekundna natančnost za zahtevne aplikacije (IEC 61850 GOOSE, PMU meritve)
- Hierarhija: **Stratum 0** (GPS/GNSS ura) → Stratum 1 (NTP server) → Stratum 2 (naprave)


## 5. INFORMACIJSKA IN KIBERNETSKA VARNOST (ICS/OT Security)


### Zakaj je OT varnost drugačna od IT varnosti?
- V OT (Operational Technology) je **razpoložljivost (Availability)** na prvem mestu (ne zaupnost kot v IT)
- Naprave imajo dolgo življenjsko dobo (20+ let) – nimajo rednih varnostnih posodobitev
- Motnje so fizično nevarne (izpad električne energije, poškodba infrastrukture)

### Ključni standardi
- **IEC 62443** – mednarodni standard za varnost industrijskih komunikacijskih omrežij in sistemov
  - Definira **Security Levels (SL 1–4)** in **Zones & Conduits** arhitekturo
- **NERC CIP** (Critical Infrastructure Protection) – ameriški standard, referenčni okvir tudi v EU
- **NIS2 Direktiva (EU)** – direktiva o varnosti omrežij in informacijskih sistemov; operaterji energetske infrastrukture so "essential entities"
- **ISO/IEC 27001** – splošni standard za upravljanje z informacijsko varnostjo (ISMS)

### Varnostna arhitektura (Zones & Conduits)
```
[Corporate IT] <---Firewall/DMZ---> [Control Network (SCADA)] <----> [Field Devices]
     Zone 4              Zone 3              Zone 2                      Zone 1/0
```
- **DMZ** (Demilitarized Zone) – ločitvena cona med IT in OT
- **Data Diode** – enosmerni prenos podatkov (iz OT v IT, nikoli obratno)
- **Industrial Firewall**: npr. Fortinet FortiGate, Cisco ASA, Hirschmann EAGLE, Tofino Xenon

### Najpogostejše grožnje in ukrepi
| Grožnja | Ukrep |
|---------|-------|
| Nepooblaščen dostop | MFA, AAA (RADIUS/TACACS+), segmentacija VLAN |
| Malware / Ransomware | Aplikacijska bela lista (whitelisting), odsotnost nepotrebnih storitev |
| Man-in-the-Middle | Šifriranje (TLS 1.2/1.3, IPsec VPN), certifikati |
| Fizični dostop | Zaklepanje omar, CCTV, evidence dostopa |
| Napadi na daljavo | IDS/IPS, syslog centralizacija, SIEM |
| USB/removable media | Politika prepovedi, skeniranje |


### VPN tehnologije
- **IPsec VPN**: tunelsko (ESP/AH) ali transportno, IKEv2, za site-to-site
- **SSL/TLS VPN**: za oddaljen dostop vzdrževalcev
- Pravilo: **princip najmanjših privilegijev** – dostop samo do tistega, kar vzdrževalec potrebuje

### Upravljanje identitet
- **RADIUS** – centralizirana avtentikacija za omrežne naprave (login v switch/router)
- **TACACS+** – podobno kot RADIUS, a z ločeno avtorizacijo in računovodstvom; Cisco-centric
- **Active Directory** – za Windows okolja, LDAP integracija

## 6. MERILNA OPREMA IN VZDRŽEVANJE

### OTDR (že opisano – za optiko)
### Spektralni analizator
- Meri moč signala v odvisnosti od frekvence
- Uporaba: preverjanje radijskih kanalov, iskanje interferenc, EMC testi
### Omrežni analizator (Network Analyzer / Protocol Analyzer)
- **Wireshark** – brezplačno orodje za zajem in analizo omrežnega prometa (PCAP datoteke)
- Znati moraš: filtrirati po protokolu (ip.addr, tcp.port), slediti TCP toku, identificirati anomalij
- ### Optični močnostni merilec (Optical Power Meter)
- Meri optično moč v dBm; skupaj z laserskim izvorom za merjenje slabljenja
- 
### Reflektometrija (TDR) za Baker
- Locira prekinitve in napake na koaksialnih ali bimetalna kablih

### Multimeter in kabelski tester
- Merjenje napetosti, toka, upora; preverba kablov

### Tipična vzdrževalna dela
1. **Preventivno vzdrževanje**: pregled konektorjev (čistost!), meritve optičnih moči, pregled alarmov v NMS
2. **Korektivno vzdrževanje**: lokalizacija okvar z OTDR, zamenjava opreme, konfiguracijske spremembe
3. **Dokumentacija**: vsaka sprememba mora biti evidentirana – vzdržuj aktualne kataster, sheme, konfiguracije

---

### Splošna električna varnost v RTP/RP
- Delovna napetost tipično 24 VDC ali 48 VDC za telekomunikacijsko opremo v postajah
- Zavedaj se bližine visoke napetosti (20 kV, 110 kV) – varna razdalja, delovni nalogi, usklajevanje z vzdrževalci EE opreme

## 8. UPRAVLJANJE OMREŽJA (NMS/EMS)

### Tipična orodja
- **Cisco Prime / DNA Center** – za Cisco infrastrukturo
- **PRTG, Zabbix, Nagios** – splošni NMS, pogosti v manjših organizacijah
- **Solarwinds NPM** – komercialni NMS
- **OSS/BSS sistemi** – za telekomunikacijske operaterje


### Funkcije, ki jih moraš razumeti
- **Fault Management**: alarm management, korelacija alarmov, eskalacija
- **Configuration Management**: varnostne kopije konfiguracije (npr. z Oxidized/RANCID), management sprememb
- **Performance Management**: monitoring pasovne zasedenosti, zakasnitev, izgube paketov
- **SNMP traps vs. polling**: trapi so asinhroni alarmi; polling je periodično spraševanj

## 10. KLJUČNE TEHNOLOGIJE IN BLAGOVNE ZNAMKE V SEKTORJU

### Pogosti proizvajalci opreme v elektrodistribuciji (EU)
| Kategorija | Proizvajalci |
|------------|-------------|
| SCADA/EMS | ABB (MicroSCADA), Siemens (SICAM), Schneider Electric (ArcFM), GE Grid Solutions |
| RTU / IED | ABB, Siemens, Schneider, SEL (Schweitzer), Easergy |
| Optični multipleksorji (SDH/MSPP) | ECI Telecom, Ericsson (ex-Marconi), Nokia, Huawei |
| Ethernet stikala (industrijsko) | Cisco IE serija, Hirschmann (Belden), Westermo, Moxa, Ruggedcom |
| Mikrovalovne povezave | Ericsson MINI-LINK, Nokia, Huawei, Cambium, Siae |
| Zaščitni releji | ABB (REF, REC, RET serije), Siemens SIPROTEC, Schneider Sepam |
| Optični merilniki | EXFO, JDSU/Viavi, Anritsu |


## 11. POGOSTA VPRAŠANJA NA RAZGOVORU (z odgovori)

### "Kaj je IEC 61850 in zakaj je pomemben?"
> IEC 61850 je mednarodni standard za komunikacijo v elektroenergetskih postajah. Definira standardizirane logične modele naprav in komunikacijske protokole (MMS za nadzor, GOOSE za hitro zaščitno signalizacijo). Ključna prednost je interoperabilnost – naprave različnih proizvajalcev komunicirajo po istem standardu. GOOSE sporočila so brez zakasnitev (sub-ms), kar je kritično za zaščitne funkcije

### "Razloži razliko med IEC 60870-5-101 in 104."
> IEC 60870-5-101 je serijsko-based protokol (RS-232/485) za SCADA komunikacijo, primeren za počasne in zanesljive povezave. IEC 60870-5-104 je nadgradnja, ki isti aplikacijski protokol prenaša prek TCP/IP omrežja. Danes večina novih sistemov uporablja 104, saj ima vsako postaje IP povezavo prek optike ali radia.

### "Kako zagotoviš visoko razpoložljivost telekomunikacijskega omrežja?"
> Redundanca na vseh nivojih: dvojne optične poti (obroči), redundantni napajalni sistemi (UPS, baterije), dual-homing (naprava priključena na dve stikali), RSTP/G.8032 za hitro okrevanje omrežja. Redno preverjanje backup poti, alarmi ob izpadih, testiranje načrtov ob nepredvidenih situacijah.






### "Kako zagotoviš visoko razpoložljivost telekomunikacijskega omrežja?"
> Redundanca na vseh nivojih: dvojne optične poti (obroči), redundantni napajalni sistemi (UPS, baterije), dual-homing (naprava priključena na dve stikali), RSTP/G.8032 za hitro okrevanje omrežja. Redno preverjanje backup poti, alarmi ob izpadih, testiranje načrtov ob nepredvidenih situacijah.

### "Kaj je OTDR in kako ga uporabiš?"
> OTDR (Optical Time Domain Reflectometer) je merilni instrument za diagnostiko optičnih vlaken. Deluje podobno kot radar – v vlakno pošlje kratke svetlobne pulze in meri odboje. Iz dobljene krivulje (trace) razberemo dolžino vlakna, lokacijo prelomov ali napak, slabljenje spojk in konektorjev. Pred meritvijo nastavimo valovni dolžini (1310/1550 nm), dolžinsko območje in impulzno širino.

### "Kako bi ravnal ob izpadu SCADA komunikacije do postaje?"
> 1. Preverim alarm v NMS – kateri segment je prizadet. 2. Preverim fizično plast – optika, konektorji, napajanje aktivne opreme. 3. Preverim L2/L3 – ping, MAC tabele, routing tabele. 4. Preverim SCADA protokol – log sporočila na RTU in strežniku. 5. Dokumentiram potek okvarovaske analize in ukrepe. 6. Vzpostavim ustrezne nadomestne poti, če obstajajo.

### "Kaj razumeš pod pojmom kibernetska varnost v OT okolju?"
> V OT je razpoložljivost sistema prioriteta – izpad pomeni fizičen izpad omrežja. Varnost gradim v slojih (defense in depth): segmentacija omrežja z VLAN in firewall, kontrola dostopa (AAA, MFA), nadzor in detekcija (SIEM, IDS), obvladovanje ranljivosti (patch management z upoštevanjem omejitev OT okolja), in fizična varnost. Sledim standardu IEC 62443.

---

## 12. DODATNI NASVETI ZA RAZGOVOR

### Kaj poudariti
- Razumeš **kritičnost** telekomunikacij v elektrodistribuciji – nisi samo IT tehnik, razumeš kontekst energetike.
- Pripravljenost na **terensko delo** (RTP/RP obisk, antenna mast) in **dežurstvo/urgence**.
- Primerite izkušnje z **vzdrževanjem in odpravljanjem napak** – konkretni primeri.
- Zavedanje o **dokumentaciji** – vsaka sprememba mora biti evidentirana (kataster omrežja).

### Kaj vprašati na koncu
- Katere SCADA platforme in telekomunikacijska oprema je v uporabi?
- Ali podjetje prehaja na IP/MPLS ali SDH omrežje?
- Kakšne so načrtovane investicije v telekomunikacijsko infrastrukturo?
- Kako je organizirano dežurstvo?
- Kakšen je program uvajanja in mentorstva?

---

## 13. KRATEK SEZNAM POJMOV (za hitro osvežitev)

| Kratica | Polni naziv | Opomba |
|---------|-------------|--------|
| SCADA | Supervisory Control and Data Acquisition | Nadzorni sistem |
| RTU | Remote Terminal Unit | Naprava v postaji |
| IED | Intelligent Electronic Device | Pametni rele/merilnik |
| MTU | Master Terminal Unit | Centralni SCADA strežnik |
| GOOSE | Generic Object Oriented Substation Event | Hitra zaščitna sporočila (IEC 61850) |
| MMS | Manufacturing Message Specification | SCADA komunikacija (IEC 61850) |
| SDH | Synchronous Digital Hierarchy | Optični prenosni standard |
| MPLS | Multiprotocol Label Switching | Paketno usmerjevanje |
| VLAN | Virtual Local Area Network | Logična segmentacija omrežja |
| RSTP | Rapid Spanning Tree Protocol | Preprečevanje zank v L2 |
| ERPS | Ethernet Ring Protection Switching | Zaščita Ethernet obroča |
| OTDR | Optical Time Domain Reflectometer | Merilnik za optična vlakna |
| OSPF | Open Shortest Path First | Notranji usmerjevalni protokol |
| QoS | Quality of Service | Prioritizacija prometa |
| NTP/PTP | Network/Precision Time Protocol | Sinhronizacija časa |
| SNMP | Simple Network Management Protocol | Upravljanje omrežnih naprav |
| IEC 62443 | – | Standard za varnost industrijskih omrežij |
| NIS2 | Network and Information Security Directive 2 | EU direktiva za kibernetsko varnost |
| OPGW | Optical Ground Wire | Optični kabel v ozemljitveni vrvici |
| ADSS | All-Dielectric Self-Supporting | Nekovinski visečni optični kabel |
| RTP | Razdelilna transformatorska postaja | 110/20 kV |
| RP | Razdelilna postaja | 20 kV stikalna postaja |
| TP | Transformatorska postaja | 20/0,4 kV |
| PtP | Point-to-Point | Mikrovalovna zveza |
| ATPC | Automatic Transmit Power Control | Avtomatska regulacija oddajne moči |
| NMS | Network Management System | Upravljanje omrežja |

---

*Pripravljeno: april 2026 | Delovno mesto: Sistemski inženir II – Elektro Celje, Služba telekomunikacij*



 Tukaj je pregled tega, kar sem vključil in zakaj je vsak del pomemben za tvoj razgovor:

  Zakaj te teme:

  Elektro Celje je distribucijsko elektro podjetje. Telekomunikacijska služba skrbi za komunikacijsko hrbtenico, ki
  omogoča daljinsko vodenje celotnega omrežja (postaje RTP/RP/TP). Brez telekomunikacij ni SCADA, brez SCADA ni nadzora
  nad omrežjem.

  Najpomembnejše področje za ta razgovor je kombinacija:
  1. SCADA protokoli – IEC 60870-5-101/104 in IEC 61850 sta standarda, ki jih Elektro Celje zagotovo uporablja. Razumeti
   moraš razliko in zakaj se jih uporablja.
  2. Optična vlakna + OTDR – verjetno boš delal z optičnimi kabli (OPGW po daljnovodih), OTDR meritve so osnova
  vzdrževanja.
  3. Ethernet omrežja / VLAN / RSTP / MPLS – moderna telekomunikacijska omrežja v postajah.
  4. Kibernetska varnost OT – razpis izrecno omenja kibernetsko varnost; IEC 62443 in NIS2 sta ključni referenci.
  5. RTP/RP/TP – razumeti moraš, kaj se dogaja v postajah, ki jih servisiraš.

  Za razgovor posebej priporoči, da si prebereš o IEC 61850 in GOOSE protokolu – to je moderni standard, ki ga verjetno
  uvajajo ali načrtujejo, in bo pokazal, da si res "up-to-date".



  Za pripravo na razgovor za delovno mesto SISTEMSKI INŽENIR II v Sektorju za obratovanje in razvoj – Službi telekomunikacij v Elektro Celje, se je dobro osredotočiti na tehnične veščine, znanja in kompetence, ki jih razpis posebej omenja, pa tudi na splošno področje sistemov, omrežij in telekomunikacij. Tukaj je strukturiran pregled, kaj se pripravljati:

1. Osnovno razumevanje sistemov in omrežij
Razumevanje tipov omrežij (LAN, WAN, radijska omrežja, optična omrežja).
Konfiguracija in karakteristike omrežij (IP naslavljanje, podomrežja, VLAN, routing, switching).
Monitoriranje in diagnostika omrežij (ping, traceroute, SNMP, logi).
Prepoznavanje in odpravljanje napak v sistemih in omrežjih.
2. Telekomunikacijski sistemi in naprave
Osnovno poznavanje radijskih postaj, anten, TP/RP/RTP postaj.
Razumevanje delovanja SCADA sistemov in sistemov vodenja (supervisory control).
Poznavanje protokolov za prenos podatkov (npr. TCP/IP, UDP, SNMP, Modbus, MQTT… odvisno od podjetja).
Delovanje in konfiguracija merilne opreme ter zaščitnih elementov.
3. Vzdrževanje in diagnostika
Preventivno vzdrževanje in nadzor naprav (opravila na daljavo ali lokalno).
Analiza napak, priprava poročil, prognoz in ukrepov.
Nastavitve naprav, posodabljanje firmware-a in programske opreme.
Delo s SCADA ali drugimi aplikacijami za nadzor in upravljanje omrežij.
4. Tehnična dokumentacija
Razumevanje in priprava tehnične dokumentacije.
Evidentiranje nastavitev naprav, izvedenih posegov, poročil o incidentih.
Skladnost s standardi podjetja in regulativo.
5. Programska orodja in računalniške aplikacije
Uporaba standardnih IT orodij (Excel, Word, baze podatkov, SQL, MS Teams, Jira… odvisno od podjetja).
Razumevanje in uporaba specifičnih orodij za nadzor omrežij, SCADA in telekomunikacije.
Morda osnovno programiranje ali skriptanje za avtomatizacijo (Python, Bash, PowerShell).
6. Varnost in varovanje
Osnovni koncepti informacijske in kibernetske varnosti.
Varno delo na višini in z napravami, kjer obstaja nevarnost laserskega sevanja.
Uporaba zaščitne opreme pri delu na stolpih ali radijskih postajah.
7. Dodatna znanja (prednost, ne obvezno)
Projektno vodenje (načrtovanje del, koordinacija ekip).
Poznavanje naprednejših telekomunikacijskih protokolov.
Usposobljenost za delo v dinamičnem in večopravilnem okolju.
8. Praktični nasveti za razgovor
Pripraviti konkretne primere, kjer ste reševali težave s sistemi ali omrežji.
Omeniti izkušnje s SCADA, omrežji ali vzdrževanjem naprav.
Če imate izkušnje z meritvami ali konfiguracijo TP/RP/RTP postaj, to izpostavite.
Pripravite se na vprašanja o varnostnih postopkih in preventivnem vzdrževanju.
Pripravite se na hipotetične situacije: “Kaj bi naredil, če pride do izpada TP postaje?”

Če želiš, ti lahko pripravim konkretno tehnično “cheat sheet” s seznamom vprašanj in odgovorov, ki jih zelo verjetno lahko dobite na razgovoru, da se lahko točno ciljno pripravljaš.

🌐 OMREŽJA – tipična vprašanja
1️⃣ Kaj se zgodi, ko pošlješ ping?

Kaj preverjajo: ali razumeš TCP/IP stack.

Kaj omeniti:

ICMP Echo Request / Echo Reply
ARP (če ni MAC v cache)
Routing tabela
TTL
Kaj pomeni če ping dela / ne dela

💡 Lep odgovor (kratko):

Host preveri ARP → pošlje ICMP Echo → router forwarda → cilj odgovori → meri se RTT.

Možna podvprašanja:

Zakaj ping dela, ampak web ne?
DNS problem
firewall blokira TCP/80 ali 443
routing problem
2️⃣ Razlika TCP vs UDP

To je 100 % vprašanje.

Ključne točke:
TCP:

connection oriented
reliable (ACK, retransmission)
ordered delivery
več overhead

UDP:

connectionless
brez garancije dostave
nizka latenca

Industrijski primeri:

SCADA pogosto uporablja TCP
real-time telemetrija → UDP
3️⃣ Kaj je subnet maska in zakaj jo potrebujemo?

Primer vprašanja:
👉 Koliko hostov ima 192.168.1.0/24?

Odgovor:

/24 = 255.255.255.0
256 naslovov
usable hosti = 254

Lahko dobijo nalogo:
👉 Ali sta 192.168.1.10 in 192.168.2.10 v istem subnetu?

4️⃣ Kaj je VLAN?

Zelo verjetno vprašanje.

Poudari:

logična segmentacija omrežja
izolacija prometa
več varnosti
zmanjšanje broadcast domen

Praktični primer:
SCADA omrežje mora biti ločeno od pisarniškega.

5️⃣ Kaj je NAT?
prevajanje privatnih IP → javni IP
varnost
varčevanje z IPv4
6️⃣ Kaj je routing?

Razlika:

switch → L2 (MAC)
router → L3 (IP)

Kaj je routing tabela?
Kaj je default gateway?

📡 INDUSTRIJSKI / SCADA PROTOKOLI

Tu se lahko res pokažeš.

7️⃣ Kaj je SCADA?

Odgovor:

Supervisory Control And Data Acquisition
nadzor in vodenje energetskih sistemov
RTU, PLC, HMI, center vodenja

Tipična arhitektura:
RTU → komunikacija → SCADA center

8️⃣ Katere industrijske protokole poznaš?

To je ZELO verjetno vprašanje.

Minimalno poznaj:

MODBUS

Najpomembnejši.

Modbus RTU (serial)
Modbus TCP (Ethernet)
master/slave (client/server)

Kaj prenaša:

registre (coils, holding registers)

👉 Če omenjaš Modbus TCP → dobiš točke.

IEC 60870-5-104

Če to omeniš → zelo plus.
Uporaba:

elektro distribucija
komunikacija RTP/TP ↔ center vodenja
temelji na TCP/IP
MQTT (bonus!)

Ker si ga že delal → omeniti!

publish/subscribe
telemetrija, IoT
9️⃣ Kaj je latenca vs jitter?

Za radijska omrežja pomembno.

latenca = zakasnitev
jitter = variacija zakasnitve

Zakaj pomembno:

real-time nadzor
🔐 KIBERNETSKA VARNOST (bo vprašanje)
10️⃣ Kako zaščititi industrijsko omrežje?

Omeniti:

segmentacija (VLAN)
firewall
VPN
ločitev IT in OT omrežja
monitoring

Magic phrase:
👉 "air gap ali vsaj segmentacija OT omrežja"

🛠 PRAKTIČNA VPRAŠANJA (zelo verjetna)
11️⃣ SCADA postaja ne komunicira – kaj narediš?

Idealna struktura odgovora:

Preverim fizično povezavo
Ping gateway
Ping oddaljeno napravo
Preverim routing/VLAN
Preverim port/protokol
Preverim loge
Izoliram napako

To je ZLATO vprašanje.

12️⃣ Razlika med hub / switch / router

Hitro:

hub → broadcast vse
switch → MAC tabela
router → IP routing
🎯 BONUS vprašanja (možna)
Kaj je DNS?
Kaj je DHCP?
Kaj je SNMP?
Kaj je redundancy (RSTP ring)?
Kaj je packet loss?

