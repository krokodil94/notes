# IP / Ethernet Sloj v FTTH Omrežjih

## 1. VLAN — Virtual LAN (IEEE 802.1Q)

### Osnove VLAN tagiranja:

```
Ethernet frame brez VLAN:
[DA 6B][SA 6B][EtherType 2B][Payload][FCS]

Ethernet frame z VLAN tagom (802.1Q):
[DA 6B][SA 6B][0x8100][TCI 2B][EtherType 2B][Payload][FCS]
                       ↑
                  VLAN Tag:
                  PCP (3b) | DEI (1b) | VID (12b)
                  └ prioriteta  └ drop  └ VLAN ID (1–4094)
```

### S-VLAN vs C-VLAN (QinQ — 802.1ad):

```
S-VLAN (Service VLAN / outer tag):  0x88A8  ← operater nivo
C-VLAN (Customer VLAN / inner tag): 0x8100  ← stranka nivo

Frame z double tagom:
[DA][SA][0x88A8][S-VID][0x8100][C-VID][EtherType][Payload][FCS]
```

### VLAN shema za FTTH (tipično):

| S-VLAN | Namen | C-VLAN |
|---|---|---|
| 100 | Internet | per stranka (1001–2000) |
| 200 | IPTV multicast | skupni |
| 300 | VoIP | per stranka |
| 400 | Management (ONT) | per ONT |

**Zakaj ločeni VLAN per stranka?**
- Izolacija med strankami
- Preprostejše troubleshooting
- QoS per stranka možen

### VLAN mapiranje v ONT/OLT:

```
ONT LAN port → C-VLAN 1001 → GEM Port 1 → S-VLAN 100 (internet)
ONT LAN port → C-VLAN 2001 → GEM Port 2 → S-VLAN 200 (IPTV)
ONT FXS port → VoIP GEM    → GEM Port 3 → S-VLAN 300 (VoIP)
```

---

## 2. QoS — Quality of Service

### PCP / CoS (IEEE 802.1p):
3-bitno polje v VLAN tagu → 8 prioritetnih ravni (0–7):

| PCP | Prioriteta | Tipična storitev |
|---|---|---|
| 7 | Nejvišja | Network control (RSTP, LACP) |
| 6 | Kritična | VoIP signalizacija |
| 5 | Visoka | **VoIP govor** |
| 4 | Srednja-visoka | **Video (IPTV)** |
| 3 | Srednja | — |
| 2 | Srednja-nizka | — |
| 1 | Nizka | Background |
| 0 | Best effort | **Internet podatki** |

### DSCP (Differentiated Services Code Point):
6-bitno polje v IP headerju → 64 vrednosti:

| DSCP vrednost | Ime | Uporaba |
|---|---|---|
| 46 (101110) | EF — Expedited Forwarding | VoIP govor |
| 34 (100010) | AF41 | Video (IPTV) |
| 26 (011010) | AF31 | Kritični podatki |
| 0 (000000) | BE — Best Effort | Internet |

### QoS v GPON PON sistemu:
- ONT mapira DSCP/PCP na T-CONT tip (1–4)
- T-CONT 1 (fixed) → VoIP
- T-CONT 2 (assured) → IPTV
- T-CONT 4 (best-effort) → Internet
- OLT DBA upošteva prioritete pri dodeljevanju upstream bandwidth

### IPTV Multicast:
- IPTV kanali se prenašajo z multicastom (1 tok za N gledalcev)
- **IGMP snooping** v OLT: pošilja multicast samo na ONT ki ga gledata
- **IGMP proxy** v ONT: zbira IGMP join/leave iz LAN, pošilja k OLT
- IGMP v2 (IPv4) ali MLD v1/v2 (IPv6)
- Multicast bandwidth: ~10 Mbps per HD kanal, ~25 Mbps per 4K kanal

---

## 3. Protokoli dostopa

### PPPoE — Point-to-Point Protocol over Ethernet

**Postopek:**
```
1. Stranka ONT pošlje PADI broadcast (PPPoE Active Discovery Initiation)
2. BNG odgovori z PADO (Offer)
3. Stranka pošlje PADR (Request)
4. BNG pošlje PADS (Session confirmed) + Session ID
5. PPP LCP pogajanje (MRU, auth method)
6. Avtentikacija: CHAP ali PAP z RADIUS
7. IPCP: BNG dodeli IP naslov stranki
8. Promet teče čez PPP tunel
```

**Prednosti PPPoE:**
- Per-session accounting (RADIUS)
- Jasna identifikacija stranke
- Enostavno session management

**Slabosti PPPoE:**
- 8 byte overhead (MTU problem: 1492 namesto 1500)
- Stateful — session state na BNG
- Manj scalabilno pri milijonih strank

### IPoE — IP over Ethernet (DHCP-based)

```
1. Stranka pošlje DHCP Discover
2. BNG (DHCP relay) posreduje k RADIUS/DHCP serveru
3. DHCP server dodeli IP (Option 82 = identifikacija stranke)
4. Stranka dobi IP naslov, gateway, DNS
5. Promet teče direktno (brez PPP overhead)
```

**Prednosti IPoE:**
- Nižji overhead (1500 MTU)
- Bolj scalabilno
- Hitrejša vzpostavitev (ni PPP handshake)
- **Trend: operaterji migrirajo PPPoE → IPoE**

### RADIUS (Remote Authentication Dial-In User Service)
- Centralizirana avtentikacija, avtorizacija, accounting (AAA)
- BNG pošlje Access-Request → RADIUS server
- RADIUS vrne Access-Accept + atribute (IP, bandwidth profile, VLAN)
- Accounting: Start/Stop/Interim za billing

---

## 4. Triple Play Storitve

### Internet
- Best effort dostava
- Rate limiting na OLT/BNG: CIR/PIR profili
- CIR (Committed Information Rate): zagotovljeni minimum
- PIR (Peak Information Rate): max hitrost ob prostem omrežju
- Primer: 1 Gbps DS / 500 Mbps US

### IPTV
- **Multicast** za linearne kanale (prihranek bandwidth)
- **Unicast** za VOD (video on demand)
- Zahteve: jitter < 50 ms, packet loss < 0.001%, latenca < 100 ms
- Buffer v STB kompenzira jitter
- Zahteva IGMP snooping pravilno konfiguriran

### VoIP (Voice over IP)
- Protokoli: SIP (Session Initiation Protocol) za signalizacijo, RTP za govor
- Zahteve za kakovost:
  - Latenca (one-way delay): < 150 ms
  - Jitter: < 30 ms
  - Packet loss: < 1%
- **MOS** (Mean Opinion Score): 1–5, > 3.5 sprejemljivo
- Codec: G.711 (64 kbps, visoka kakovost), G.729 (8 kbps, kompresija)
- ONT ima FXS porta za analogni telefon

---

## 5. IPv4 vs IPv6

### Problem IPv4 izčrpanosti:
- Vsi javni IPv4 naslovi so bili dodeljeni (~4.3 mrd)
- Operaterji rešitev: **CGNAT** ali prehod na IPv6

### CGNAT — Carrier Grade NAT (Large Scale NAT):
```
Stranka ──► ONT (RFC1918 IP) ──► BNG ──► CGNAT ──► Internet
              192.168.x.x                100.64.x.x  Javni IP
```
- RFC6598: 100.64.0.0/10 rezerviran za CGNAT ("shared address space")
- Slabost: peer-to-peer aplikacije, gaming, VPN problemi
- Slabost: logging (kateri stranka = kateri javni IP v danem trenutku?)

### Prehod na IPv6:

| Metoda | Opis | Prednosti |
|---|---|---|
| **Dual-Stack** | IPv4 + IPv6 hkrati | Enostavno, full compat |
| **DS-Lite** | IPv4 v IPv6 tunelu, 1 CGNAT | Manj CGNAT stanj |
| **MAP-E** | Stateless IPv4/IPv6 | Scalable, brez stanj |
| **Native IPv6** | Samo IPv6 | Prihodnost |

**Telemach/United Fiber trend:** Dual-stack z /56 ali /64 IPv6 bloki za stranke.

---

## 6. Omrežna arhitektura BNG

```
Stranka ONT
    │
    ▼ optika
OLT (Access)
    │ 10GE/25GE uplink
    ▼
Aggregation Switch (L2)
    │ 100GE/400GE
    ▼
BNG — Broadband Network Gateway (L3)
    │  ← PPPoE/IPoE termination
    │  ← RADIUS AAA
    │  ← QoS, rate limiting
    │  ← CGNAT (opcijsko)
    ▼
Core Router / Internet Exchange
```

### BNG funkcije:
- PPPoE/IPoE session termination
- IP address management (DHCP/RADIUS)
- QoS enforcement (policer/shaper per stranka)
- CGNAT
- IPTV multicast routing
- Accounting

### OLT uplink kapacitete:
- GPON 16-port kartica: 8×10GE uplink minimum
- XGS-PON 8-port kartica: 2×25GE uplink
- Modern OLT: 100GE uplink na agregacijo

---

## 7. Hitri povzetek — kar morate znati na razgovoru

1. 802.1Q = VLAN tag, PCP = 3-bit prioriteta, VID = VLAN ID (12b)
2. QinQ (802.1ad): S-VLAN (operater) + C-VLAN (stranka) = double tag
3. VoIP prioriteta: PCP 5, DSCP EF (46); Internet: PCP 0, DSCP BE
4. PPPoE: per-session auth z RADIUS, 8B overhead; IPoE: DHCP, manj overhead
5. IGMP snooping: multicast samo na zainteresirane ONT — varčuje bandwidth
6. VoIP SLA: latenca <150ms, jitter <30ms, packet loss <1%
7. CGNAT: 100.64.0.0/10 za shared address space
8. BNG = točka terminacije PPPoE/IPoE, QoS, RADIUS, CGNAT
9. Triple play: Internet (BE) + IPTV (multicast) + VoIP (priority queue)
10. Dual-stack = IPv4+IPv6 hkrati — trend za nove deploymente
