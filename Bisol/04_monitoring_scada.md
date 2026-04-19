# Monitoring Portali, SCADA in Daljinski Nadzor

## 1. Nivoji nadzora solarnih elektrarn

```
┌─────────────────────────────────────────┐
│  Cloud / Nadzorni portal (L4)           │  ← Fleet management, poročila
├─────────────────────────────────────────┤
│  SCADA / EMS (L3)                       │  ← Nadzor, krmiljenje elektrarne
├─────────────────────────────────────────┤
│  Data logger / Gateway (L2)             │  ← Zbiranje podatkov, protokol konverzija
├─────────────────────────────────────────┤
│  Naprave: inverterji, BMS, merilniki (L1)│  ← Fizični nivo
└─────────────────────────────────────────┘
```

## 2. Monitoring portali v solarni industriji

### Najpopularnejši portali
| Portal | Proizvajalec | Opombe |
|--------|-------------|--------|
| **mySMA / Sunny Portal** | SMA | Standard za SMA inverterje |
| **Fronius Solar.web** | Fronius | Vgrajen v IG Plus/Primo |
| **SolarEdge Monitoring** | SolarEdge | Modul-level monitoring |
| **Huawei FusionSolar** | Huawei | Za Huawei Sun2000 |
| **Solar-Log** | Solare Datensysteme | Multi-brand aggregator |
| **Sungrow iSolarCloud** | Sungrow | Za Sungrow inverterje |
| **AlsoEnergy (PowerTrack)** | AlsoEnergy | Enterprise, multi-site |
| **Locus Energy** | Locus | Portfolio management |
| **PVcase Remote** | PVcase | EU focused |
| **SCADA breskovica** | Custom | Za večje elektrarne |

### Ključne funkcionalnosti portala
- **Real-time dashboard**: trenutna moč, energija danes/mesec/leto
- **Alarmni sistem**: email/SMS ob napakah, threshold alerting
- **Performance analitika**: PR, yield, dostopnost (availability)
- **Primerjava z referenco**: dejansko vs. pričakovano (irradianca-based)
- **String-level monitoring**: odkrivanje slabih stringov
- **API dostop**: JSON/REST za integracijo z drugimi sistemi

## 3. KPI – Ključni kazalniki zmogljivosti

### Performance Ratio (PR)
```
PR = Dejanska energija (kWh) / Referenčna energija (kWh)
   = E_ac / (E_poa × P_installed)

E_poa = irradiance na ravnino modulov (kWh/m²)
P_installed = inštalirana moč (kWp)

PR > 80% = dober sistem
PR < 75% = preiskava potrebna
```

### Specific Yield (Specifična produkcija)
```
Specific Yield = E_ac (kWh) / P_installed (kWp)
Tipično: 900–1400 kWh/kWp/leto (odvisno od lokacije)
```

### Availability (Razpoložljivost)
```
Availability = čas delovanja / skupni čas × 100%
Target: > 98% za komercialne elektrarne
```

### BESS Specifični KPI
- **Round-trip efficiency**: kWh_out / kWh_in (cilj: > 90%)
- **Cycle count**: skupno število polnih ciklov
- **SoH trend**: upadanje kapacitete v %
- **Response time**: čas od ukaza do dejanske moči

## 4. Alarmiranje in napake

### Tipi alarmov (prioritete)
```
CRITICAL:  Inverter izpad, grid fault, požarni alarm BESS
ERROR:     String napaka, komunikacijska napaka, overtemperature
WARNING:   Zmanjšana produkcija, visoka temperatura, nizek SoC
INFO:      Vzdrževanje, firmware update, konfiguracija
```

### Pogosti alarmi inverterjev
| Alarm | Vzrok | Rešitev |
|-------|-------|---------|
| AC overvoltage | Previsoka napetost omrežja | Check grid, zaščitni relej |
| AC undervoltage | Nizka omrežna napetost | Preveriti priključek |
| Grid frequency fault | Frekvenca zunaj meja (49.5-50.5 Hz) | Grid problem, ni napaka inverterja |
| Insulation fault | DC uzemljitev (Ground fault) | Preveri izolacijo kabliranja |
| MPPT overcurrent | Preveč paralelnih stringov | Preveriti dimenzioniranje |
| Overtemperature | Slabo hlajenje | Čiščenje, zamenjava ventilatorja |
| PV reverse polarity | Zamenjani + / − | Preveriti polariteto |

### Alarmni workflow
```
1. Alert pride → kategorizacija (kritično/nekritično)
2. Preveri portal: kdaj je nastalo, katero naprava, vzorec?
3. Daljinski dostop: SSH/VPN do data loggerja/inverterja
4. Diagnostika: log analiza, vrednosti registrov
5. Odločitev: daljinska resolucija ali terenska intervencija
6. Resolucija + dokumentacija
7. Preveri da je alarm izginil in produkcija normalna
```

## 5. SCADA osnove

### Definicija
SCADA = Supervisory Control And Data Acquisition
- Centralni nadzorni sistem za industrijsko infrastrukturo
- Zbira, prikazuje in beleži podatke iz terena
- Omogoča krmiljenje naprav

### Komponente SCADA
```
[RTU/PLC na terenu] ←→ [Communication network] ←→ [SCADA server]
                                                          ↓
                                                    [HMI/dashboard]
                                                    [Database (historian)]
                                                    [Alarm management]
                                                    [Reporting]
```

### Protokoli SCADA
- **Modbus TCP/RTU** – najpreprostejši, solar standard
- **DNP3** – energetika; robustnost, timestamp, zabezpečenost
- **IEC 60870-5-101/104** – evropski energetski standard
- **IEC 61850** – pametne elektrarne, substation automation
- **OPC UA** – industrijski IoT standard; varnostni model vgrajen

### Popularni SCADA sistemi
- **Ignition (Inductive Automation)** – moderni, tag-based, MQTT native
- **AVEVA System Platform (Wonderware)** – enterprise
- **Siemens WinCC** – Siemens ekosistem
- **GE iFIX/Cimplicity** – GE ekosistem
- **Grafana + InfluxDB** – open-source, narašča v popularnosti

## 6. Daljinski nadzor – praktično

### VPN dostop do elektrarne
```
Elektric: [Naprave] → [Switch] → [Router/Modem 4G] → [Internet]
                                                           ↓
Vzdrževalec: [Laptop] ← [VPN tunel] ← [VPN Server/Router]
```

### Tipičen workflow daljinskega vzdrževanja
1. Vzpostavi VPN tunel do elektrarne
2. Preveri dosegljivost data loggerja: `ping 192.168.1.10`
3. SSH na data logger; preveri loge: `tail -f /var/log/syslog`
4. Preveri Modbus komunikacijo z inverterji
5. Preveri vrednosti registrov (aktualnamoč, stanje, alarmi)
6. Nastavi parametre oz. reboot napravo če potrebno
7. Preveri portal da se vrednosti normalizirajo
8. Zapiši v servisni log

### Diagnostika pri izpadu komunikacije
```
Izpad komunikacije → Preveriti:
1. Modem online? (Portal pokaže "communication lost" timestamp)
2. SIM kartica: kredit, APN, signal?
3. Router restart? (watchdog log)
4. Lokalna moč napajanja? (UPS log)
5. Data logger running? (watchdog, ping z druge naprave v LAN-u)
6. Fizična napaka kabla/konektorja?
```

## 7. Poročila in analitika

### Standardna poročila
- **Dnevno**: produkcija kWh, PR, alarmi
- **Mesečno**: primerjava z budgetom, SLA poročilo
- **Letno**: degradacija, življenjski cikel, OPEX analiza

### Zaznavanje težav z analitiko
- **PR nenaden padec** → shadow (sezonski), umazanija, napaka stringa
- **PR postopen padec** → degradacija modulov, akumulacija umazanije
- **String razlika** → en string bistveno manj → napaka modula, AFCI, konektor
- **Noćna poraba** → inverter ne gre v sleep → nastavitve
- **BESS round-trip pada** → celična degradacija, temperaturni problem

## 8. Vzdrževanje nadzornih portalov

### Redne naloge
- Preveritev komunikacij: vse elektrarne online?
- Pregled alarmov: nerešene napake
- PR pregled: outlierji (pod pričakovanji)
- Firmware posodobitve: data loggerji, routerji, inverterji
- Certifikat posodobitve: HTTPS certs za lokalne portale
- Backup konfiguracije: router, data logger, SCADA

### Konfiguracija nadzornega portala
1. Dodaj elektrarne: GPS koordinate, orientacija, naklonski kot
2. Vnesi spec moduli in inverterji: Pmax, Voc, Isc
3. Nastavi irradiance senzor (pyranometer) ali uporabi GHI bazo
4. Konfiguriraj alarmne pragove: PR < 70%, string imbalance > 10%
5. Nastavi obveščanje: email, SMS, webhook
6. Dodaj uporabnike, nastavi dostopne pravice
