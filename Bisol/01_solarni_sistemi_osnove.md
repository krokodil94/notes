# Solarni PV sistemi – Osnove

## 1. Fotonapetostni efekt
- Sončna svetloba (fotoni) izbija elektrone iz polprevodnika (Si)
- p-n spoj ustvari električno polje → enosmerni tok (DC)
- 1 celica ≈ 0.5–0.6 V; moduli serija/vzporedno za višje napetosti/tokove

## 2. Tipi solarnih modulov
| Tip | Izkoristek | Opomba |
|-----|-----------|--------|
| Monokristalni Si | 20–23% | Najboljši izkoristek, najdražji |
| Polikristalni Si | 16–19% | Kompromis cena/izkoristek |
| Tankoplastni (CdTe, CIGS) | 10–14% | Slabši izkoristek, fleksibilni |
| Bifacial | +5–25% extra | Spredaj + zadaj |

## 3. Električne karakteristike modula
- **Voc** – napetost odprtega tokokroga (no-load)
- **Isc** – kratkostični tok
- **Vmp / Imp** – napetost/tok pri max. moči
- **Pmax = Vmp × Imp**
- **Fill Factor (FF)** = Pmax / (Voc × Isc); idealno > 0.75
- **STC** – Standard Test Conditions: 1000 W/m², 25°C, AM 1.5

## 4. Temperaturni koeficienti
- Višja temperatura → nižja napetost (≈ −0.3%/°C za Voc)
- Nižja temperatura → višja napetost → pozor pri dimenzioniranju inverterja!
- NOCT – Nominal Operating Cell Temperature (tipično 45°C)

## 5. Komponente sistema

### Grid-tied (omrežni)
```
Moduli → String kabel → DC Combiner Box → Inverter → AC panel → Omrežje
                                              ↑
                                         MPPT regulator (v inverterju)
```

### Off-grid
```
Moduli → Charge Controller (MPPT/PWM) → Baterija → Inverter → Porabniki
```

### Hibridni
```
Moduli → Hibridni inverter ←→ Baterija
              ↕
           Omrežje / Porabniki
```

## 6. Inverterji
- **String inverter** – 1 MPPT na string; en shadow → vse prizadeto
- **Central inverter** – za velike elektrarne (>100 kW); centraliziran
- **Micro inverter** – 1/modul; dražji, boljši pri senci
- **Power optimizer** – modul-level DC/DC; centralni inverter ostane

### MPPT – Maximum Power Point Tracking
- Algoritem (P&O, InCond) neprestano išče točko max. moči
- Perturb & Observe: mala sprememba V → izmeri P → ponovi
- Vhodni razpon MPPT ≠ celoten Voc razpon – ključno pri načrtovanju!

## 7. Stringing – dimenzioniranje
- **Max string V** = Voc (STC) × koef. temp. (min. temp.) × N modulov < Vmax inverterja
- **Min string V** = Vmp × koef. temp. (max. temp.) × N > Vmin MPPT
- **Število vzporednih stringov** = Imax inverterja / Isc stringa

## 8. Izgube sistema
| Vzrok | Tipična izguba |
|-------|---------------|
| Temperatura modula | 5–10% |
| Senčenje | variabilno |
| Umazanija | 1–5% |
| Kabelske izgube | 1–3% |
| Inverter izkoristek | 2–5% |
| Mismatch modulov | 1–2% |

**PR (Performance Ratio)** = dejanska produkcija / teoretična produkcija; dober sistem > 80%

## 9. Varnostni sistemi
- **DC disconnect** – ločitev od modulov
- **AC disconnect** – ločitev od omrežja
- **Anti-islanding** – inverter zaustavi ob izpadu omrežja (VDE-AR-N 4105, EN 50549)
- **Surge Protection Device (SPD)** – strela/prenapetost
- **AFCI** – Arc Fault Circuit Interrupter (požarna varnost DC)
- **Fuse/breaker** per string

## 10. Standardi in certifikati
- **IEC 61215** – kristalni Si moduli (mehansko, električno testiranje)
- **IEC 61730** – varnost modulov
- **IEC 62109** – varnost inverterjev
- **IEC 60364-7-712** – PV instalacije
- **EN 50549** – zahteve priključitve na omrežje (EU)
- **VDE-AR-N 4105** – nemška omrežna pravila

## 11. Ključni pojmi za intervju
- **kWp** – kilowatt peak (nazivna moč pri STC)
- **kWh/kWp** – specifična produkcija (yield)
- **GHI** – Global Horizontal Irradiance
- **POA** – Plane of Array irradiance (dejansko na modul)
- **PR** – Performance Ratio
- **CUF** – Capacity Utilization Factor = dejanska kWh / (kWp × 8760h)
- **LCOE** – Levelized Cost of Energy (€/kWh skozi življenjsko dobo)
