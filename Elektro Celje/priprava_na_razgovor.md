 Kaj se zgodi, ko pošlješ ping?

Ko “pošlješ ping”, računalnik preverja, ali je druga naprava na omrežju dosegljiva in kako hitro odgovori. To je ena najbolj osnovnih diagnostičnih metod za internet ali lokalno omrežje.








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

