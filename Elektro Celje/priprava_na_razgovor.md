

5️⃣ Kaj je NAT (Network Address Translation)
Definicija:
NAT prevaja privatne IP naslove v en ali več javnih IP naslovov, da naprave v lokalnem omrežju lahko dostopajo do interneta.
Zakaj ga potrebujemo:
Varčevanje z IPv4:
Več naprav lahko uporablja en sam javni IP, kar rešuje problem omejenih IPv4 naslovov.
Varnost:
Privatni IP naslovi niso neposredno vidni na internetu → zmanjšuje možnost neposrednih napadov.
Omogoča internet povezavo za lokalna omrežja:
Računalniki, telefoni, SCADA sistemi ipd., lahko dostopajo do interneta preko enega javnega IP.
Kako deluje:
Naprava v lokalnem omrežju pošlje paket → NAT router spremeni izvorni IP in port → pošlje na internet.
Odgovor iz interneta → NAT router prevede nazaj → paket pride do pravilne naprave.
Praktičen primer
SCADA omrežje ali pisarniško omrežje ima privatne IP-je: 192.168.x.x
NAT na routerju jih prevaja v javni IP: 85.17.23.10
Vse naprave delijo isti javni IP, internet vidi le NAT naslov, notranji IP-ji ostanejo skriti

💡 En stavek povzetek:
NAT = prevajanje privatnih IP v javni, kar omogoča varnost, internet povezljivost in varčevanje z IPv4 naslovi.
6️⃣ Kaj je routing
Routing je proces, kjer paketi najdejo pot od izvorne naprave do cilja preko različnih omrežij.
Odločanje temelji na IP naslovih (Layer 3).
Switch vs Router
Naprava	Layer	Funkcija
Switch	L2 (Data Link)	Pošilja paket samo na pravi MAC naslov znotraj istega omrežja
Router	L3 (Network)	Pošilja pakete med različnimi IP omrežji (subneti)
Switch → deluje lokalno
Router → omogoča komunikacijo med subneti ali internetom
Routing tabela
Routing tabela je “navodilo” routerja, kam poslati paket glede na ciljni IP naslov.
Vsebina tipične tabele:
Network → ciljni subnet
Next hop → naslednji router ali vrata
Interface → kateri port / vmesnik se uporablja
Router vedno pogleda tabelo in izbere najbolj specifično pot (longest prefix match).
Default gateway
Default gateway je IP naslov routerja, ki ga host uporablja, kadar ciljna naprava ni v istem subnetu.
Primer:
Host: 192.168.1.10/24
Default gateway: 192.168.1.1
Paket na 8.8.8.8 → pošlje se na gateway → router naprej po internetu
Industrijski / SCADA protokoli in routing
SCADA omrežja pogosto uporabljajo static routes, da nadzorujejo promet med PLC-ji, HMI-ji in kontrolnimi sistemi.
Pogosti industrijski protokoli:
Modbus TCP – uporablja TCP/IP za komunikacijo PLC ↔ HMI
DNP3 TCP/UDP – za SCADA telemetrijo
EtherNet/IP – real-time industrijski Ethernet protokol
Routing je kritičen za izolacijo SCADA subnetov od pisarniških omrežij → varnost in zanesljivost.

💡 Povzetek:

Switch: MAC → lokalno omrežje
Router: IP → med subneti / internet
Routing tabela: kam poslati paket
Default gateway: kam poslati pakete zunaj lokalnega subnet-a
SCADA: routing nadzira dostop in izolacijo industrijskih omrežij

7️⃣ Kaj je SCADA

SCADA = Supervisory Control And Data Acquisition

Sistem za nadzor, spremljanje in vodenje industrijskih procesov.
Pogosto se uporablja v:
Energetiki (elektrarne, distribucija)
Vodni in odpadni sistemi
Tovarne in procesna industrija
Ključne komponente
Komponenta	Funkcija
RTU (Remote Terminal Unit)	Oddaljeni modul, ki zbira podatke iz senzorjev in izvaja ukaze
PLC (Programmable Logic Controller)	Krmilnik za avtomatizacijo procesov, lokalno vodenje
HMI (Human Machine Interface)	Uporabniški vmesnik za operaterje, prikaz podatkov in kontrola
SCADA center / Master station	Centralni nadzorni sistem, analitika, zgodovina podatkov
Tipična arhitektura
RTU / PLC → zbira podatke iz senzorjev in aktuatorjev
Komunikacija (Ethernet, Modbus, DNP3, EtherNet/IP) → prenaša podatke
SCADA center / HMI → operater nadzira, analizira, po potrebi pošlje ukaze

💡 Povzetek:
SCADA = centralni nadzor in vodenje industrijskih sistemov preko RTU, PLC in HMI, kjer komunikacija omogoča zbiranje in nadzor podatkov v realnem času.

8️⃣ Katere industrijske protokole poznaš?
1. Modbus (najpomembnejši)
Modbus RTU:
Serial komunikacija (RS-485)
Master / Slave arhitektura
Modbus TCP:
Ethernet verzija
Client / Server arhitektura
Kaj prenaša:
Coils → digitalni izhodi/on-off
Holding registers → analogni podatki / nastavitve
Uporaba: PLC ↔ SCADA HMI, industrijska avtomatizacija

💡 Bonus točke: Če omeniš Modbus TCP → Ethernet, TCP/IP

2. IEC 60870-5-104
Standard za SCADA komunikacijo v elektrodistribuciji
Omogoča komunikacijo Remote Terminal Unit (RTU) ↔ SCADA center
Temelji na TCP/IP
Pogosto uporablja za telemetrijo in nadzor distribucijskih omrežij
3. MQTT (bonus / IoT)
Publish / Subscribe model
Nizka latenca, primeren za telemetrijo in IoT
Odličen za SCADA sisteme, kjer je potrebna real-time posodobitev podatkov

💡 Povzetek:

Protokol	Transport	Arhitektura	Uporaba
Modbus RTU	Serial	Master/Slave	PLC ↔ HMI, industrija
Modbus TCP	Ethernet	Client/Server	Ethernet SCADA, PLC
IEC 60870-5-104	TCP/IP	Client/Server	Elektro distribucija, RTU ↔ center
MQTT	TCP/IP	Pub/Sub	Telemetrija, IoT, SCADA
9️⃣ Kaj je latenca vs jitter?

Za radijska omrežja pomembno.

latenca = zakasnitev
jitter = variacija zakasnitve

Zakaj pomembno:

real-time nadzor
10️⃣ Kako zaščititi industrijsko omrežje?

Ključni ukrepi:

Segmentacija omrežja (VLAN)
Ločitev različnih delov OT omrežja (SCADA, PLC, HMI) in IT omrežja.
Omeji lateralno gibanje napadalcev.
Firewally
Kontrola prometa med segmenti in proti internetu.
Implementacija pravil “allow/deny” glede na protokol in port.
VPN za oddaljen dostop
Za varno delo na daljavo.
Dvosmerna avtentikacija (2FA) je plus.
Ločitev IT in OT omrežja
IT omrežje → office, e-mail, internet
OT omrežje → SCADA, PLC, industrijska oprema
Minimalna integracija preko nadzorovanih gateway-ev.
Monitoring in logging
SIEM, IDS/IPS, redni pregledi logov
Odkrivanje anomalij, sumljivih povezav.

Magic phrase za razgovor:
👉 "air gap ali vsaj segmentacija OT omrežja"

11️⃣ SCADA postaja ne komunicira – kaj narediš?

Zlata struktura odgovora:

Preverim fizično povezavo (kabli, switche, porti)
Ping gateway (lokalni router/firewall)
Ping oddaljeno napravo (PLC ali HMI)
Preverim routing/VLAN konfiguracijo
Preverim port/protokol (TCP/UDP, Modbus, OPC)
Preverim loge (SCADA, PLC, firewall, switch)
Izoliram napako (je na SCADA postaji, OT segmentu ali omrežju)

💡 Tip: vedno reci, da deluješ sistematično in dokumentiraš spremembe.

12️⃣ Razlika med hub / switch / router
Naprava	Kako deluje	Primer uporabe
Hub	Pošlje vse pakete vsem	Staro, manj varno, broadcast vse
Switch	Uporablja MAC tabelo, pošlje paket samo pravemu portu	Standard v LAN omrežjih
Router	Uporablja IP routing, povezuje različna omrežja	Povezovanje LAN → WAN, VLAN routing
🎯 Bonus vprašanja – hiter pregled
DNS (Domain Name System) → Prevede ime naprave (npr. plc1.local) v IP naslov.
DHCP (Dynamic Host Configuration Protocol) → Samodejno dodeljuje IP naslove.
SNMP (Simple Network Management Protocol) → Monitoriranje in upravljanje omrežnih naprav.
Redundancy (RSTP ring) → Preprečuje downtime, hitro preusmerjanje v primeru prekinitve povezave.
Packet loss → Paketi izgubljeni med prenosom → slab signal, napačna konfiguracija ali preobremenjeno omrežje.