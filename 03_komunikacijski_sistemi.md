# Komunikacijski sistemi, Modemi & Omrežja

## 1. Serijska komunikacija

### RS-485
- Diferencialna dvovodna napeljava (A/B žici)
- Half-duplex; do 32 naprav na eno linijo (z repeaterji do 256)
- Hitrost: 9600–115200 baud tipično; do 10 Mbps kratke razdalje
- Max razdalja: 1200 m pri nizkih hitrostih
- **Terminator**: 120Ω na obeh koncih linije – brez tega refleksije!
- Tipično za: Modbus RTU, PROFIBUS

```
[Master]---[Dev1]---[Dev2]---[Dev3]---[120Ω]
  120Ω                A/B vodnika
```

### RS-232
- Enožično (GND, TX, RX); točka-točka samo
- Max 15 m, 20 kbps
- Danes redko; USB-RS232 adapterji za legacy opremo

### CAN bus
- Diferencialni par (CAN_H, CAN_L)
- Multi-master; 1 Mbps do 40m, 125 kbps do 500m
- Odlična zanesljivost; avtomobilska industrija + BMS
- Terminator: 120Ω na obeh koncih

## 2. Modbus protokol (KLJUČNO za solarno industrijo)

### Modbus RTU (serijski)
```
[Slave address 1B][Function code 1B][Data][CRC 2B]
```
- Binarni; kompakten; najpogostejši v BESS/PV
- Naslovi: 1–247 naprav

### Modbus TCP (Ethernet)
```
[MBAP header 6B][Function code 1B][Data]
Port: 502
```
- Modbus znotraj TCP/IP paketa
- Lažje za diagnostiko (Wireshark!)

### Najpomembnejše funkcijske kode
| Koda | Ime | Opis |
|------|-----|------|
| 01 | Read Coils | Branje digitalnih izhodov |
| 02 | Read Discrete Inputs | Branje digitalnih vhodov |
| 03 | Read Holding Registers | Branje 16-bit registrov (najpogostejše) |
| 04 | Read Input Registers | Branje meritev |
| 06 | Write Single Register | Pisanje enega registra |
| 16 | Write Multiple Registers | Pisanje več registrov |

### SunSpec – standardiziran Modbus za solar
- Register map standardiziran za inverterje, baterije, merilnike
- Start: register 40001 = SunSpec ID (0x53756e53)
- Model 101/111 = single/three phase inverter
- Model 124 = storage
- Podprto v: SMA, Fronius, SolarEdge, Huawei...

## 3. Ethernet & IP omrežja

### Osnove TCP/IP
```
IP naslov: 192.168.1.100  (IPv4, 32-bit)
Subnet:    255.255.255.0  = /24 (254 naprav)
Gateway:   192.168.1.1    (router)
DNS:       8.8.8.8
```

### Protokoli
| Protokol | Port | Uporaba |
|----------|------|---------|
| Modbus TCP | 502 | Inverterji, merilniki |
| HTTP/HTTPS | 80/443 | Nadzorni portali, API |
| MQTT | 1883/8883 | IoT telemetrija |
| SNMP | 161 | Omrežna oprema monitoring |
| SSH | 22 | Oddaljen dostop |
| Telnet | 23 | Legacy (izogni se!) |
| FTP/SFTP | 21/22 | Prenos datotek |
| NTP | 123/UDP | Sinhronizacija časa |

### Switch vs Router vs Firewall
- **Switch (L2)**: poveže naprave v isti VLAN; MAC naslovi
- **Router (L3)**: poveže omrežja; IP naslovi; NAT
- **Managed switch**: VLAN, STP, port mirroring, SNMP monitoring
- **Firewall**: filtriranje prometa; NAT; VPN endpoint

### VLAN
- Virtualna segmentacija L2 omrežja
- Tipično: VLAN 10 = OT naprave (inverterji), VLAN 20 = IT, VLAN 30 = management

## 4. Modemi in mobilna komunikacija

### Tipi modemov za solarno elektrarne
| Tip | Opis | Primerno za |
|-----|------|-------------|
| **4G/LTE industrijski** | SIM kartica, rugged, DIN rail | Terenske elektrarne brez fiber |
| **5G** | Visoka hitrost, nizka latenca | Novo nameščene, urbano |
| **DSL/ADSL** | Telefonska linija | Kjer je xDSL dostop |
| **Fiber (FO)** | Nizka latenca, visoka BW | Večje elektrarne, zanesljivo |
| **Wireless (WiFi/LTE)** | Brezžično po objektu | Short-range do data loggerja |

### Industrijski 4G router – konfiguracija
```
APN nastavitve:        (odvisno od operaterja)
  APN: internet / data.si / ...
  Auth: PAP/CHAP
  User/Pass: (odvisno od SIM)

Firewall pravila:
  Inbound: dovoli SSH od management IP
  Inbound: dovoli HTTPS do nadzornega portala
  Default: DROP vse

VPN tunel (OpenVPN/IPSec/WireGuard):
  Za oddaljeni dostop do lokalnega omrežja elektrarne
```

### Pogosti problemi z modemi
- **Brez signala**: antena pozicija, frekvenca pas (B3/B7/B20), SIM aktivna?
- **Visoka latenca**: preobremenjena celica, napačen APN
- **Tunel pada**: MTU mismatch (nastavi MTU 1400 za VPN), keepalive
- **SIM PIN lock**: nastavi SIM brez PIN ali konfiguriraj PIN v routerju
- **Watchdog**: nastavitev auto-restart ob izgubi povezave

### Protokoli za oddaljeni dostop
- **OpenVPN**: SSL-based, prehaja firewall, zanesljiv
- **WireGuard**: novejši, hiter, preprostejši
- **IPSec/IKEv2**: enterprise standard
- **SSH tunel**: preprost za enkratni dostop
- **Remote desktop (RDP/VNC)**: za HMI dostop

## 5. Data logger / Gateway naprave
Vmesnik med napravami in oblakom:

```
[Inverter RS485] ─┐
[Meter RS485]    ─┤─[Data Logger/Gateway]─── Cloud/SCADA
[BMS CAN]        ─┤    (Modbus → MQTT/HTTP)
[Sensor digital] ─┘
```

### Popularni data loggerji
- **Solare Datensysteme (Solar-Log)** – solarni specialist
- **Sungrow Logger 1000** – za Sungrow inverterje
- **Carlo Gavazzi UWP 3.0** – multi-protocol gateway
- **Moxa UC series** – industrijski Linux gateway
- **Raspberry Pi + Node-RED** – custom rešitev

### Konfiguracija data loggerja
1. Nastavi RS485 port: baud rate, parity, stop bits
2. Dodaj naprave: Modbus slave address, model
3. Konfiguriraj polling interval (tipično 60s ali 300s)
4. Nastavi cloud endpoint: URL, API ključ, protocol (MQTT/HTTP)
5. Preveri register map ujemanje

## 6. Omrežna diagnostika

### Osnovna orodja
```bash
ping 192.168.1.100          # Ali naprava živi?
traceroute 192.168.1.100    # Pot do naprave
nmap -p 502 192.168.1.0/24  # Poišči Modbus naprave
telnet 192.168.1.100 502    # Test Modbus TCP port
ssh user@192.168.1.100      # SSH dostop
curl http://192.168.1.100/api/status  # Test HTTP API
```

### Modbus diagnostika
```
Tool: mbpoll, ModRSsim2, Modbus Poll, QModMaster

# Preberi holding registers od naprave 1, register 40001, 10 registrov
mbpoll -a 1 -r 40001 -c 10 -t 4 192.168.1.100

Tipični problemi:
- Timeout: naprava ne odgovori → preveri address, kabliranje, baud rate
- Exception 01: naprava ne pozna function code
- Exception 02: napačen register naslov
- Exception 03: napačna vrednost
```

### Wireshark – analiza omrežnega prometa
- Filter za Modbus: `tcp.port == 502`
- Filter za MQTT: `tcp.port == 1883`
- Pokaže request/response pare; identificira napake

## 7. Varnost OT omrežij
- **OT/IT segmentacija**: industrijske naprave ločene od IT omrežja
- **Default credentials**: VEDNO zamenjaj tovarniškaena gesla!
- **Firmware updates**: redno posodabljaj routerje, data loggerje
- **VPN za oddaljeni dostop**: nikoli direktno odpri Modbus/SSH na internet
- **Port forwarding**: izogni se; raje VPN
- **Logging**: beleženje dostopov za audit
