

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
