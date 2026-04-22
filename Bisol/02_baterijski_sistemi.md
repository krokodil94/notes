# Baterijski sistemi (BESS) – Battery Energy Storage Systems

## 1. Tipi baterij za BESS

### Litij-ionske (dominantne v solarnih aplikacijah)
| Kemija | Polno ime | Varnost | Energijska gostota | Tipična uporaba |
|--------|-----------|---------|-------------------|----------------|
| **LFP** | LiFePO₄ | ★★★★★ | srednja | Stacionarni BESS, dolga življ. doba |
| **NMC**-Nikelj-mangan-kobalt | LiNiMnCoO₂ | ★★★ | visoka | EV, manjši BESS | - ima višjo energijsko gostoto (več energije v manjšem/lažjem ohišju), to pri hišni bateriji, ki stoji v kleti/garaži ni ključno. Pomembnejši dejavniki so:
| **NCA** | LiNiCoAlO₂ | ★★ | visoka | Tesla Powerwall |
| **LTO** | Li₄Ti₅O₁₂ | ★★★★★ | nizka | Hitro polnjenje, dolga življ. |

**BISOL verjetno uporablja LFP** – industrijski standard za stacionarne aplikacije.
NB
### Svinčene (še prisotne v starejših sistemih)
- **AGM** – absorbent glass mat; vzdrževanje-prosto
- **OPzV/OPzS** – gel/tabularne; dolga življenjska doba, drago

## 2. Ključni parametri baterije
- **Kapaciteta**: kWh (energija) ali Ah @ nominalna napetost
- **C-rate**: hitrost polnjenja/praznjenja
  - 1C = polna kapaciteta v 1 uri
  - 0.5C = v 2 urah, 2C = v 30 min
  - LFP tipično: 0.5C–1C kontinuirno
- **DoD** – Depth of Discharge: koliko % kapacitete uporabimo
  - LFP: do 80–90% DoD
  - Svinčene: max 50% DoD
- **SoC** – State of Charge (0–100%)
- **SoH** – State of Health: staranje kapacitete (100% = novo)
- **Round-trip efficiency**: LFP ≈ 95–98%; svinčene ≈ 80–85%
- **Ciklično življenje**: LFP > 4000–6000 ciklov; svinčene ≈ 500–1200

## 3. BMS – Battery Management System

### Funkcije BMS
```
Merjenje:    Napetost vsake celice, tok, temperatura
Zaščita:     Overcharge, over-discharge, overcurrent, overtemp, short circuit
Balansiranje: Pasivno (disipacija) / Aktivno (prenos energije)
Komunikacija: CAN bus, RS485/Modbus, CANopen, BACnet
Poročanje:   SoC, SoH, alarmi, history
```

### Balansiranje celic
- **Pasivno** – presežna energija se sipa kot toplota (poceni, izgube)
- **Aktivno** – energija se prenaša med celicami (drago, učinkovito)
- Brez balansiranja: celice divergirajo → zmanjšana kapaciteta → BMS zaustavi prezgodaj

## 4. Topologije BESS

### Baterijski rack/cabinet
```
Celice → Moduli (parallel) → Rack (series) → DC bus
                                    ↑
                                   BMS per rack
```

### Kontejnerski BESS (>100 kWh)
```
[Rack 1] [Rack 2] ... [Rack N]
        ↓
   Master BMS / EMS
        ↓
   Battery Inverter (PCS – Power Conversion System)
        ↓
   AC bus / omrežje
```

## 5. PCS – Power Conversion System
- Bidirektionalni inverter: polnjenje (AC→DC) in praznenje (DC→AC)
- Tipični proizvajalci: SMA, Fronius, Sungrow, KACO, Ingeteam, Victron
- Vmesnik z BMS: CAN ali Modbus; PCS sledi ukazom BMS/EMS

## 6. EMS – Energy Management System
Nadrejeni sistem, ki upravlja celoten BESS + PV + omrežje:

### Strategije delovanja
- **Self-consumption** – porabi lokalno, shranjuj presežek, kupuj ko manjka
- **Peak shaving** – reži konic porabe (zmanjšaj priključno moč)
- **Time-of-use** – polni ko je elektrika poceni, prazni ko je draga
- **Grid services** – frekvenčna regulacija (FCR, aFRR), rezerve
- **Backup/UPS** – napajanje ob izpadu omrežja

## 7. Zagon BESS – Postopek

### Pred zagonom (pre-commissioning checks)
1. Vizualni pregled: mehanske poškodbe, pritrditev, kabliranje
2. Izolacijska odpornost (Megger test): DC kabliranje
3. Preveritev polaritete vseh rack-ov
4. BMS firmware verzija in konfiguracija
5. Komunikacijski test: BMS → PCS ping

### Zagon (commissioning)
1. Vklop BMS (brez DC moči)
2. Počasen predfazni test: parcialno polnjenje
3. Kalibracija SoC (polni polnjenje do 100% → praznjenje do 0% → ponovi)
4. Alarmni test (simulacija fault stanja)
5. Komunikacijski test z EMS/SCADA
6. FAT/SAT dokumentacija

### Pogosti problemi pri zagonu
- **Cell voltage imbalance** → pasivno/aktivno balansiranje
- **Communication timeout** → preveri Modbus address, baud rate, terminator
- **BMS trips prematurely** → napačna konfiguracija SoC limitov
- **PCS ne komunicira z BMS** → CAN ID mismatch ali wrongbus termination

## 8. Varnost pri BESS
- **Thermal runaway** – eksotermna reakcija, samookrevanje toplote
  - Sprožilci: overcharge, fizična poškodba, defekt celice
  - Detekcija: temperatura, VOC senzorji (HF, CO)
- **Fire suppression**: Novec 1230, CO₂, aerosol za kontejnerje
- **HVAC** – hlajenje/ogrevanje za optimalno temperaturo (15–35°C)
- **PPE**: dielektrične rokavice (1000V), zaščitna očala, izolacijska orodja

## 9. Standardni protokoli za baterije
- **Modbus RTU/TCP** – najpogostejši za BMS komunikacijo
- **CAN bus** – hitrejši, zanesljivejši za celični nivo
- **CANopen** – protokol nad CAN; pogost v industrijskih BMS
- **OCPP** – EV polnjenje (manj relevantno)
- **SunSpec** – standardiziran Modbus register map za solarno industrijo

## 10. Ključni pojmi za intervju
- **kWh vs kWp**: kWh = shranjeno; kWp = inštalirana moč modulov
- **C/10 test**: standardni kapacitetni test za validacijo SoH
- **SOC window**: razpon SoC pri katerem sistem deluje (npr. 10–90%)
- **Usable capacity**: dejanska kapaciteta znotraj SOC window
- **Cycle life at DoD**: LFP pri 80% DoD > 4000 ciklov; pri 20% DoD > 10000 ciklov
