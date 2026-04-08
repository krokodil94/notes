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




#### SNMP (Simple Network Management Protocol)
- Za nadzor in upravljanje telekomunikacijske omrežne opreme (stikala, routerji, multipleksorji)
- Verzije: v1, v2c, **v3** (edini s šifriranjem – priporočen za varnost)
- Trap: asinhrono sporočilo naprave ob alarmu


### Topologije

- **Zvezdasta** – RTP je center, RP/TP so veje (preprosta, a brez redundance)
- **Obroč (Ring)** – vsaka postaja je del obroča; izpad ene povezave ne povzroči izpada vozlišča
- **Mrežasta (Mesh)** – visoka redundanca, kompleksno upravljanje

- Elektro podjetja tipično gradijo **obroče s Spanning Tree / RSTP** ali **SDH obroče**

