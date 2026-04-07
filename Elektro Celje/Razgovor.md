# Razgovor


### Komunikacijski protokoli v energetski avtomatizaciji
Jedro tehničnega znanja za razpisano delovno mesto predstavlja poznavanje protokolov prenosa podatkov, ki omogočajo delovanje SCADA sistemov (Supervisory Control and Data Acquisition). V elektroenergetiki prevladujejo standardi Mednarodne elektrotehniške komisije (IEC), ki zagotavljajo interoperabilnost med opremo različnih proizvajalcev.


### Komunikacijski protokoli v energetski avtomatizaciji

Jedro tehničnega znanja za razpisano delovno mesto predstavlja poznavanje protokolov prenosa podatkov, ki omogočajo delovanje SCADA sistemov (Supervisory Control and Data Acquisition).

Protokol IEC 60870-5-104Standard IEC 60870-5-104 (znan kot IEC 104) predstavlja nadgradnjo serijskega protokola IEC 101 za uporabo v omrežjih TCP/IP. To je primarni protokol, ki ga sistemski inženir uporablja za komunikacijo med nadzornim centrom (Master station) in oddaljenimi enotami (RTU) v RTP in TP postajah.

Tehnična struktura protokola IEC 104 temelji na Application Protocol Data Unit (APDU), ki se deli na:

APCI (Application Protocol Control Information): Vsebuje kontrolne podatke, kot so dolžina paketa, zaporedne številke sporočil za preprečevanje izgube ali podvajanja ter tipe okvirjev (I, S, U).
ASDU (Application Service Data Unit): Vsebuje dejanske procesne podatke, kot so meritve, stanja stikal in ukazi. Ključni elementi ASDU so Type Identification (tip podatka), Cause of Transmission (vzrok prenosa, npr. spontano ali ciklično) in Information Object Address (IOA), ki določa specifičen podatek znotraj naprave.

Protokol IEC 104 uporablja vrata (port) 2404 po standardu, vendar sodobni gonilniki omogočajo konfiguracijo poljubnih vrat, če je to potrebno zaradi varnostnih nastavitev požarnih zidov. Sistemski inženir mora biti sposoben konfigurirati te parametre na nivoju RTU naprave in na nivoju SCADA strežnika.

Standard IEC 61850 in digitalna postaja
Medtem ko se IEC 104 uporablja za komunikacijo na dolge razdalje (WAN), standard IEC 61850 definira komunikacijo znotraj same razdelilne postaje (LAN). Ta standard uvaja koncept objektno orientiranega modeliranja podatkov, kjer se namesto številčnih naslovov (IOA) uporablja logično poimenovanje naprav in njihovih funkcij (npr. "Circuit Breaker" ali "Protection Relay").

Kandidat za delovno mesto mora poznati dve ključni storitvi znotraj IEC 61850:MMS (Manufacturing Message Specification): Uporablja se za vertikalno komunikacijo med inteligentno elektronsko napravo (IED) in lokalnim SCADA sistemom ali prehodom (gateway).GOOSE (Generic Object Oriented Substation Event): Uporablja se za horizontalno, peer-to-peer komunikacijo med napravami za zaščito in vodenje.GOOSE sporočila so kritična za varnost sistema, saj omogočajo prenos informacij o okvari v manj kot 3 milisekundah, kar je bistveno hitreje od klasičnega bakrenega ožičenja med binarnimi vhodi in izhodi naprav. Uporaba Ethernet omrežja namesto bakrenih žic zmanjšuje stroške izgradnje in omogoča stalno nadziranje komunikacijske poti; če naprava preneha pošiljati periodična "heartbeat" GOOSE sporočila, sistem takoj zazna napako.

# Tehnologija in oprema v postajah

Sistemski inženir v Sektorju za obratovanje in razvoj neposredno upravlja s sodobno strojno opremo, ki omogoča avtomatizacijo. Primer takšne naprave je Iskra CAU 380, ki deluje kot bay computer in RTU enota za nadzor in meritve v srednjenapetostnih in visokonapetostnih celicah.Tehnične specifikacije takšne opreme vključujejo:Veliko število digitalnih vhodov (do 154) in izhodov (32) za zajem stanj in izvajanje ukazov.Analogni vhodi za neposredno priključitev tokovnih in napetostnih merilnih transformatorjev (CT in VT).Podpora za širok nabor protokolov: IEC 61850 (certifikat KEMA Level A), IEC 101, 103, 104, DNP3 in Modbus.Grafični zaslon za lokalno upravljanje v objektu.

Poleg RTU naprav mora inženir poznati tudi delovanje zaščitnih elementov v RTP postajah. Zaščitni releji so tisti, ki ob zaznavi kratkega stika v milisekundah sprožijo izklop odklopnika. Naloga sistemskega inženirja je zagotoviti, da se vsi ti dogodki pravilno časovno ožigosajo (timestamping) in prenesejo v center vodenja za kasnejšo analizo vzrokov dogodkov, kar je ena izmed njegovih eksplicitnih nalog.


### Kibernetska varnost in zakonodajni okvir (NIS2 in ZInfV-1)

Ena izmed ključnih odgovornosti razpisanega mesta je zagotavljanje ustreznega nivoja informacijske in kibernetske varnosti. V letu 2026 je to področje pod strogim nadzorom nove slovenske zakonodaje, ki implementira evropsko direktivo NIS2.

