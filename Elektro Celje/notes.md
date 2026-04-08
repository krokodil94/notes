# Tehnična priprava na razgovor: Sistemski inženir II – Elektro Celje (Služba telekomunikacij)


| **RTP** | Razdelilna transformatorska postaja | 110 kV / 20 kV | Priključitev na prenosno omrežje (ELES), transformacija na distribucijsko napetost |
| **RP**  | Razdelilna postaja                  | 20 kV          | Stikalna postaja brez transformatorja, razvod 20 kV                                |
| **TP**  | Transformatorska postaja            | 20 kV / 0,4 kV | Transformacija za odjemalce (gospodinjstva, podjetja) 



### Komunikacijski protokoli v energetski avtomatizaciji

Jedro tehničnega znanja za razpisano delovno mesto predstavlja poznavanje protokolov prenosa podatkov, ki omogočajo delovanje SCADA sistemov (Supervisory Control and Data Acquisition).

**SCADA** (Supervisory Control and Data Acquisition) je nadzorni in upravljavski sistem za daljinsko vodenje elektroenergetskega omrežja.

      ```
      [Dispečerski center / Control Center]
              |
         [SCADA Server / MTU]
              |  (komunikacijsko omrežje)
         [RTU / IED naprave v RTP/RP/TP]
              |
         [Terenska oprema: stikala, odklopniki, merilniki]
      ```
- **MTU** (Master Terminal Unit) – centralni strežnik SCADA v dispečerskem centru
- **RTU** (Remote Terminal Unit) – naprava v oddaljeni postaji, ki zbira meritve in izvaja ukaze
- **IED** (Intelligent Electronic Device) – pametna zaščitna ali merilna naprava (npr. zaščitni rele)
- **HMI** (Human-Machine Interface) – grafični vmesnik za operaterje
      
### Protokol IEC 60870-5-104
- **IEC 60870-5-101** – serijsko (RS-232/RS-485), za komunikacijo med MTU in RTU prek počasnih linij
- - **IEC 60870-5-104** – isti protokol kot 101, vendar prek TCP/IP omrežja (Ethernet/IP)
- Podpira: enkratne ukaze, dvojne ukaze, merjene vrednosti, časovne žige, spontane prenose
Standard IEC 60870-5-104 (znan kot IEC 104) predstavlja nadgradnjo serijskega protokola IEC 101 za uporabo v omrežjih TCP/IP. To je primarni protokol, ki ga sistemski inženir uporablja za komunikacijo med nadzornim centrom (Master station) in oddaljenimi enotami (RTU) v RTP in TP postajah.

Tehnična struktura protokola IEC 104 temelji na Application Protocol Data Unit (APDU), ki se deli na:

APCI (Application Protocol Control Information): Vsebuje kontrolne podatke, kot so dolžina paketa, zaporedne številke sporočil za preprečevanje izgube ali podvajanja ter tipe okvirjev.
ASDU (Application Service Data Unit): Vsebuje dejanske procesne podatke, kot so meritve, stanja stikal in ukazi. Ključni elementi ASDU so Type Identification (tip podatka), Cause of Transmission (vzrok prenosa, npr. spontano ali ciklično) in Information Object Address (IOA), ki določa specifičen podatek znotraj naprave.
Protokol IEC 104 uporablja vrata (port) 2404 po standardu, vendar sodobni gonilniki omogočajo konfiguracijo poljubnih vrat, če je to potrebno zaradi varnostnih nastavitev požarnih zidov.

### Standard IEC 61850 in digitalna postaja
- Sodoben standard za komunikacijo med IED napravami v RTP/RP
Medtem ko se IEC 104 uporablja za komunikacijo na dolge razdalje (WAN), standard IEC 61850 definira komunikacijo znotraj same razdelilne postaje (LAN). Ta standard uvaja koncept objektno orientiranega modeliranja podatkov, kjer se namesto številčnih naslovov (IOA) uporablja logično poimenovanje naprav in njihovih funkcij (npr. "Circuit Breaker" ali "Protection Relay").

MMS (Manufacturing Message Specification): Uporablja se za vertikalno komunikacijo med inteligentno elektronsko napravo (IED) in lokalnim SCADA sistemom ali prehodom (gateway)  – za nadzor in kontrolo prek TCP/IP.
GOOSE (Generic Object Oriented Substation Event): 
Uporablja se za horizontalno, peer-to-peer komunikacijo med napravami za zaščito in vodenje. GOOSE sporočila so kritična za varnost sistema, saj omogočajo prenos informacij o okvari v manj kot 3 milisekundah, kar je bistveno hitreje od klasičnega bakrenega ožičenja med binarnimi vhodi in izhodi naprav. Uporaba Ethernet omrežja namesto bakrenih žic zmanjšuje stroške izgradnje in omogoča stalno nadziranje komunikacijske poti; če naprava preneha pošiljati periodična "heartbeat" GOOSE sporočila, sistem takoj zazna napako. -za hitro zaščitno signalizacijo prek Ethernet (sub-milisekunda)
- Logični vozli (Logical Nodes): XCBR (odklopnik), XSWI (ločilnik), MMXU (meritve)...
- Prednost: interoperabilnost različnih proizvajalcev, standardizirana konfiguracija prek **SCL** datotek (`.icd`, `.scd`, `.cid`)

# Optična komunikacijska omrežja in merilna tehnika

Služba telekomunikacij v Elektro Celje upravlja z razvejanim optičnim omrežjem, ki je primarni medij za prenos podatkov med RTP postajami. Optična vlakna so integrirana v zaščitne vrvi daljnovodov (OPGW - Optical Ground Wire) ali položena v kabelsko kanalizacijo ob elektroenergetskih kablih.


# Merjenje in vzdrževanje optike

Sistemski inženir mora obvladati uporabo merilne opreme za optična omrežja, saj je odgovoren za odpravo okvar na komunikacijskih povezavah. Osrednji instrument je OTDR (Optical Time-Domain Reflectometer), ki deluje na principu povratnega sipanja laserske svetlobe.

S pomočjo OTDR meritev lahko inženir ugotovi:
  Celotno dolžino optične poti med dvema postajama.
  Slabljenje (atenuacijo) na celotni trasi, izraženo v dB/km.
  Lokacijo in resnost dogodkov, kot so zvari (splices), konektorji ali mikrougibi kabla.
  Natančno razdaljo do mesta prekinitve vlakna v primeru mehanske poškodbe kabla.

Sodobni sistemi za nadzor optičnih kablov (OLM) omogočajo avtomatsko spremljanje 24 ur na dan. Ti sistemi v realnem času analizirajo stanje vlaken in sprožijo alarm, še preden se komunikacija popolnoma prekine, kar omogoča preventivno vzdrževanje, ki je ena izmed dolžnosti na tem delovnem mestu.


#### OTDR (Optical Time Domain Reflectometer)
- **Najpomembnejše merilno orodje za optiko**
- Deluje na principu radarskega echa: pošlje pulz, meri odboje nazaj
- Iz dobljene krivulje razbereš: lokacijo preloma, slabljenje spojk, dolžino vlakna, slabljenje konektorjev
- Znati moraš interpretirati OTDR trace: normalen Fresnelov odboj, Rayleighevo sipanje, prelom



#### SNMP (Simple Network Management Protocol)
- Za nadzor in upravljanje telekomunikacijske omrežne opreme (stikala, routerji, multipleksorji)
- Verzije: v1, v2c, **v3** (edini s šifriranjem – priporočen za varnost)
- Trap: asinhrono sporočilo naprave ob alarmu


### Topologije

- **Zvezdasta** – RTP je center, RP/TP so veje (preprosta, a brez redundance)
- **Obroč (Ring)** – vsaka postaja je del obroča; izpad ene povezave ne povzroči izpada vozlišča
- **Mrežasta (Mesh)** – visoka redundanca, kompleksno upravljanje

- Elektro podjetja tipično gradijo **obroče s Spanning Tree / RSTP** ali **SDH obroče**

Spanning Tree Protocol (STP) in Rapid Spanning Tree Protocol (RSTP, IEEE 802.1w) sta protokola, ki omogočata redundantno mrežno topologijo brez zanke v Ethernet omrežju. Tipično se uporablja v LAN omrežjih ali industrijskih omrežjih, kjer obstaja potreba po rezervni poti, če primarna povezava odpove.
Kako deluje?

Mreža z več povezanimi stikali lahko ustvari zanke. STP: Identificira “root bridge” (glavno stikalo), Izračuna minimalni set povezav, da ne nastanejo zanke .Drugi povezavi postavi v blocking mode, dokler primarna ne odpove
RSTP je hitrejša verzija STP, ob napaki preklopi poti v sekundah, ne v minutah.
Prednosti: Preprosta implementacija. Dovolj za manj kritične obroče ali kjer so Ethernet linki relativno poceni. Ni potrebna specializirana oprema.
Slabosti
Hitrost preklopa (STP: 30–50s, RSTP: ~1–5s) je lahko prepočasna za kritične elektro obroče, kjer je stabilnost ključna. Ni optimizirana za sinhronizacijo ali transport velikih količin podatkov, kot je SCADA ali telemetrija.



SDH obroči (Synchronous Digital Hierarchy)

SDH je telekomunikacijski standard za prenos podatkov po optičnih vlaknih. Omogoča gradnjo obročev z redundanco, kjer lahko signal teče v obe smeri (dual ring), in ob napaki samodejno preusmeri tok. Pogosto se uporablja za kritične elektro omrežne aplikacije, SCADA sisteme, daljinske telemetrije in nadzor elektro distribucije. Signal teče v obroču, običajno v dveh smereh: primarna in rezervna. Ob izpadu primarne poti SDH obroč samodejno preklopi na drugo smer (hitro: v milisekundah). Ponuja visoko zanesljivost (availability 99,999%).
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

! To je narobe - TCP ima samo 4 plasti - poglej še bolj detailno
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

## 5. INFORMACIJSKA IN KIBERNETSKA VARNOST (ICS/OT Security)

- **NIS2 Direktiva (EU)** – direktiva o varnosti omrežij in informacijskih sistemov; operaterji energetske infrastrukture so "essential entities"

- ### Varnostna arhitektura (Zones & Conduits)



[Corporate IT] <---Firewall/DMZ---> [Control Network (SCADA)] <----> [Field Devices]
     Zone 4              Zone 3              Zone 2                      Zone 1/0

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

### Spektralni analizator
- Meri moč signala v odvisnosti od frekvence
- Uporaba: preverjanje radijskih kanalov, iskanje interferenc, EMC testi
### Omrežni analizator (Network Analyzer / Protocol Analyzer)
- **Wireshark** – brezplačno orodje za zajem in analizo omrežnega prometa (PCAP datoteke)
- Znati moraš: filtrirati po protokolu (ip.addr, tcp.port), slediti TCP toku, identificirati anomalij

- ### Optični močnostni merilec (Optical Power Meter)
- Meri optično moč v dBm; skupaj z laserskim izvorom za merjenje slabljenja



### Splošna električna varnost v RTP/RP
- Delovna napetost tipično 24 VDC ali 48 VDC za telekomunikacijsko opremo v postajah
- Zavedaj se bližine visoke napetosti (20 kV, 110 kV) – varna razdalja, delovni nalogi, usklajevanje z vzdrževalci EE opreme



## 11. POGOSTA VPRAŠANJA NA RAZGOVORU (z odgovori)

### "Kaj je IEC 61850 in zakaj je pomemben?"
> IEC 61850 je mednarodni standard za komunikacijo v elektroenergetskih postajah. Definira standardizirane logične modele naprav in komunikacijske protokole (MMS za nadzor, GOOSE za hitro zaščitno signalizacijo). Ključna prednost je interoperabilnost – naprave različnih proizvajalcev komunicirajo po istem standardu. GOOSE sporočila so brez zakasnitev (sub-ms), kar je kritično za zaščitne funkcije

### "Razloži razliko med IEC 60870-5-101 in 104."
> IEC 60870-5-101 je serijsko-based protokol (RS-232/485) za SCADA komunikacijo, primeren za počasne in zanesljive povezave. IEC 60870-5-104 je nadgradnja, ki isti aplikacijski protokol prenaša prek TCP/IP omrežja. Danes večina novih sistemov uporablja 104, saj ima vsako postaje IP povezavo prek optike ali radia.

### "Kako zagotoviš visoko razpoložljivost telekomunikacijskega omrežja?"
> Redundanca na vseh nivojih: dvojne optične poti (obroči), redundantni napajalni sistemi (UPS, baterije), dual-homing (naprava priključena na dve stikali), RSTP/G.8032 za hitro okrevanje omrežja. Redno preverjanje backup poti, alarmi ob izpadih, testiranje načrtov ob nepredvidenih situacijah.

### "Kaj je OTDR in kako ga uporabiš?"
> OTDR (Optical Time Domain Reflectometer) je merilni instrument za diagnostiko optičnih vlaken. Deluje podobno kot radar – v vlakno pošlje kratke svetlobne pulze in meri odboje. Iz dobljene krivulje (trace) razberemo dolžino vlakna, lokacijo prelomov ali napak, slabljenje spojk in konektorjev. Pred meritvijo nastavimo valovni dolžini (1310/1550 nm), dolžinsko območje in impulzno širino.

### "Kako bi ravnal ob izpadu SCADA komunikacije do postaje?"
> 1. Preverim alarm v NMS – kateri segment je prizadet. 2. Preverim fizično plast – optika, konektorji, napajanje aktivne opreme. 3. Preverim L2/L3 – ping, MAC tabele, routing tabele. 4. Preverim SCADA protokol – log sporočila na RTU in strežniku. 5. Dokumentiram potek okvarovaske analize in ukrepe. 6. Vzpostavim ustrezne nadomestne poti, če obstajajo.



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


