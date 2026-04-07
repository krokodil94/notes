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

![Screenshot 2026-04-07 055229.png](/api/files/Elektro Celje/Screenshot 2026-04-07 055229.png)

Varnostna dokumentacija, ki jo mora sistemski inženir vzdrževati, vključuje tudi sezname sredstev (asset management) in sheme omrežij, kar omogoča hitro identifikacijo ranljivih točk v primeru pojava nove kibernetske grožnje.


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


### Projekt NEDO

Cilji projekta so vključevali:Upravljanje napetosti: Razvoj naprednih algoritmov za koordinirano vodenje napetosti v distribucijskem omrežju, kar omogoča priključitev večjega števila sončnih elektrarn brez investicij v fizično krepitev vodov.Avtomatska lokalizacija napak: Uporaba naprednih sekundarnih naprav za hitro identifikacijo mesta okvare in avtomatsko rekonfiguracijo omrežja, s čimer se skrajša čas izpada za odjemalce.Hranilniki energije: Preizkušanje baterijskih sistemov za uravnavanje konic in zagotavljanje sistemskih storitev, kot je bila namestitev baterij v Idriji in Ljubljani v kasnejših fazah projekta.Sistemski inženir sodeluje pri integraciji teh naprednih rešitev v obstoječi SCADA sistem podjetja, kar zahteva poznavanje oblačnih rešitev in centralno vodenih platform. V obdobju 2023–2026 Elektro Celje vlaga znatna sredstva iz naslova REPowerEU in Načrta za okrevanje in odpornost v digitalizacijo RTP postaj, kar pomeni, da bo novi sodelavec vpet v projekte visoke tehnološke vrednosti.


### Delovne naloge in odgovornosti sistemskega inženirja II

Upravljanje sistemov in omrežij
Glavna odgovornost je zagotavljanje delovanja zahtevnejših sistemov, za katere izvaja skrbništvo. To vključuje:

Redno spremljanje delovanja komunikacijskih naprav in strežniške infrastrukture.
Izvajanje nastavitev naprav (parametrizacija RTU, konfiguracija stikal in usmerjevalnikov).
Preventivno vzdrževanje, ki vključuje nadgradnje programske opreme (firmware) za odpravo varnostnih ranljivosti.
Odpravo okvar na terenu, kar zahteva uporabo službenega vozila (B kategorija) in prenašanje merilne opreme v RTP/TP postaje.




