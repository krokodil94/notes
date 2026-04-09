 Kaj se zgodi, ko pošlješ ping?

Ko “pošlješ ping”, računalnik preverja, ali je druga naprava na omrežju dosegljiva in kako hitro odgovori. To je ena najbolj osnovnih diagnostičnih metod za internet ali lokalno omrežje.

Kaj se dejansko zgodi v ozadju
Ustvari se ICMP paket
Tvoj računalnik pošlje majhen podatkovni paket.
Ta uporablja protokol ICMP (Internet Control Message Protocol).
Sporočilo se imenuje Echo Request.
Paket potuje po internetu
Paket gre skozi usmerjevalnike (routerje).
Vsak usmerjevalnik ga preusmeri proti ciljnemu IP naslovu.
Ciljna naprava odgovori
Če je naprava dosegljiva in dovoljuje ping:
Pošlje nazaj Echo Reply (odmevni odgovor).
Izmeri se čas poti
Tvoj računalnik izmeri čas od pošiljanja do prejema odgovora.
Temu rečemo latenca ali ping time (npr. 20 ms).

Preverjanje MAC naslova (ARP)
Računalnik najprej pogleda, ali ima MAC naslov cilja v ARP cache.
Če ga nima → pošlje ARP request in prejme ARP reply, da ve, kam poslati paket na lokalnem omrežju.
Pošiljanje ICMP paketa
Pošlje se ICMP Echo Request (ping).
Paket vsebuje svoj TTL (Time To Live), ki preprečuje, da bi krožil večno po omrežju.
Forwardanje preko omrežja
Paket potuje skozi routerje, ki gledajo v routing tabelo, da vedo, kam poslati naslednji korak.
TTL se pri vsakem hopu zmanjša za 1; če TTL doseže 0 → paket je zavrnjen.
Odgovor cilja
Ciljna naprava prejme Echo Request → pošlje ICMP Echo Reply nazaj na izvorni naslov.
Merjenje RTT (Round-Trip Time)
Tvoj računalnik izmeri čas od pošiljanja do prejema odgovora → to je latenca.
Host preveri ARP → pošlje ICMP Echo → routerji forwardajo po routing tabeli → cilj odgovori → izmeri se RTT.




Zakaj ping dela, splet pa ne
DNS problem
Ping na IP deluje, ker paket pride do cilja.
Brskalnik ne najde spletne strani, ker ime domene ni prevedeno v IP.
Rešitev: preveri z nslookup ali dig.
Firewall ali blokada vrat
Ping uporablja ICMP → deluje.
HTTP/HTTPS uporabljata TCP 80 in 443, ki sta morda blokirani.
Rešitev: preveri firewall, usmerjevalnik ali korporativne omejitve.
Routing problem za TCP, ne ICMP
Omrežje omogoča ICMP promet, a TCP paketi morda ne pridejo do cilja zaradi napačnih routing tabel.
Običajno se zgodi v kompleksnih omrežjih ali VPN-jih.
Proxy ali NAT omejitve
Nekateri proxy strežniki ali NAT konfiguracije lahko dovolijo ping, a blokirajo HTTP/HTTPS.

💡 Praktični test:

ping 8.8.8.8 → če dela, osnovna povezava je OK
curl -v http://8.8.8.8 → preveri, ali TCP povezava deluje
nslookup google.com → preveri DNS


2️⃣ Razlika med TCP in UDP
TCP (Transmission Control Protocol)
Connection-oriented:
Preden pošlje podatke, TCP vzpostavi povezavo med pošiljateljem in prejemnikom (3-way handshake: SYN → SYN/ACK → ACK).
Zanesljivost (reliability):
TCP uporablja ACK (potrditev prejema) in retransmission → izgubljeni paketi se ponovno pošljejo.
Urejena dostava:
Paketi pridejo v istem vrstnem redu, kot so bili poslani.
Več overheada:
Zaradi handshaka, potrditev in številk paketov je TCP počasnejši od UDP.

Industrijski primeri:

SCADA sistemi, HMI (Human Machine Interface), kjer je kritično, da podatki prispejo točno in v pravem vrstnem redu.
FTP, HTTP/HTTPS, e-pošta.
UDP (User Datagram Protocol)
Connectionless:
Pošilja pakete brez vzpostavljanja povezave → manj zakasnitev.
Brez garancije dostave:
Ni ACK, ni retransmission → izgubljeni paketi ne bodo poslani ponovno.
Brez urejenosti:
Paketi lahko prispejo izven vrstnega reda.
Nizka latenca:
Minimalen overhead → primerno za real-time aplikacije.

Industrijski primeri:

Real-time telemetrija, senzorji, video/glas v živo → hitrost je pomembnejša kot popolna zanesljivost.
DNS, VoIP, streaming podatki.


3️⃣ Kaj je subnet maska in zakaj jo potrebujemo
Subnet maska določa, katere bite IP naslova predstavljajo omrežje in katere hoste.
Omrežje je razdeljeno na network part in host part.
Omogoča:
določanje velikosti omrežja
ločevanje različnih subnetov v istem IP prostoru
boljši nadzor in manj trčenja med napravami
Primer /24
IP: 192.168.1.0/24
/24 pomeni, da je prvih 24 bitov network part, ostalih 8 bitov host part.
Subnet maska: 255.255.255.0
Skupno število naslovov: 2^8 = 256
Uporabniški hosti: 256 − 2 = 254 (prvi = network, zadnji = broadcast)
Preverjanje, ali sta v istem subnetu
IP 1: 192.168.1.10
IP 2: 192.168.2.10
Mask: /24 → primerjamo network del:
192.168.1.10 → network = 192.168.1.0
192.168.2.10 → network = 192.168.2.0
✅ Zaključek: nista v istem subnetu

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

