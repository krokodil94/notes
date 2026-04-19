# Intervju – Vprašanja & Odgovori

## TEHNIČNA VPRAŠANJA

### Solarni sistemi

**V: Razloži razliko med string in central inverterjem.**
> String inverter: en MPPT na string žic modulov. Central: en velik inverter za celo elektrarno (>500 kW), vsi stringi vzporedno. String: boljši pri delni zasenčenosti, lažje vzdrževanje. Central: cenejši na kW pri velikih elektrarnah.

**V: Kaj pomeni MPPT in kako deluje?**
> Maximum Power Point Tracking. Algoritem (Perturb & Observe) neprestano malo spreminja napetost in meri moč. Ko P pade, obrne smer. Tako sledi maksimalni točki I-V karakteristike kljub spremenljivi sončni svetlobi.

**V: Zakaj je temperaturni koeficient napetosti negativen?**
> Višja temperatura → večje termično gibanje kristalov → atomi motijo gibanje elektronov drugače. Bandgap se zmanjša → Voc pade ≈ −0.3%/°C. Pozornost pri zimskem zagonu: napetost stringa je višja!

**V: Kaj je ground fault/insulation fault na solarni elektrarni?**
> DC kabel se dotakne ozemljene kovine (okvir, kabel tray). Na negativnem polu PV sistema nastane pot do ozemljitve → tok mimo normalnega tokokroga. Nevarno (požar, elektroúdar). Detekcija: izolacijski monitor, GFDI. Test: Megger meritev.

**V: Elektrana je imela nenadoma padec PR za 15%. Kaj preveriš?**
> 1. Irradiance: ali je bil oblačen dan (potrdi z pyranometerom)?
> 2. Portal: kateri inverter/string je padel?
> 3. Temperatura: overtemp limit?
> 4. Alarmi: insulacija, AC fault, MPPT error?
> 5. Terenska kontaminacija: umazanija po nevihti?
> 6. String current imbalance v monitoringu?

---

### Baterijski sistemi

**V: Razloži razliko med LFP in NMC baterijo.**
> LFP (LiFePO₄): varnejši (ne gori spontano), 3000+ ciklov, nižja energijska gostota, idealen za stacionarni BESS. NMC: višja gostota (manjše pakiranje), 1000-2000 ciklov, termično manj stabilen. Za solarno BESS je LFP standard.

**V: Kaj je thermal runaway in kako ga preprečimo?**
> Eksotermna kemijska reakcija v celici, ki sama sebe pospešuje → temperatura raste eksponentno → požar/eksplozija. Preprečitev: BMS preprečuje overcharge/overtemp, HVAC sistem ohranja temperaturo, VOC/smoke detektorji za zgodnje zaznavanje, fire suppression (Novec 1230).

**V: Baterijski sistem ne komunicira z inverterjem. Koraki?**
> 1. Fizično: preveriti CAN/RS485 kabel, konektor
> 2. BMS power: ali BMS sploh vklopljen?
> 3. Protokol parametri: baud rate, parnost, Modbus address
> 4. Terminator: ali je 120Ω na obeh koncih?
> 5. Log iz BMS: ali BMS sam javlja napako?
> 6. Preizkus z izoliranim orodjem (Modbus Poll, CAN analyzer)

**V: Kaj je SoC kalibracija in zakaj je potrebna?**
> BMS računa SoC iz napetosti in toka (Coulomb counting). Napaka se akumulira. Kalibracija: polni polnjenje do 100% (all cells balanced) → praznjenje do 0% → ponovi. BMS si popravi referenčne točke. Brez kalibracije: SoC drift → sistem prerano ustavlja ali prekorači DoD limite.

---

### Komunikacija in modemi

**V: RS485 linija ne deluje zanesljivo – občasno napake. Kaj preveriš?**
> 1. Terminator: 120Ω na obeh koncih?
> 2. Kabliranje: parica za A/B, skupna ozemljitev
> 3. Baud rate ujemanje na vseh napravah
> 4. Dolžina linije vs. baud rate
> 5. Elektromagnetne motnje: kabel preblizu AC kablov
> 6. Ground loops: SG (Signal Ground) pin
> 7. Naprave: ali ena naprava drži linijo pokonci (no tri-state)?

**V: Razloži Modbus register map.**
> Modbus ima 4 tipe registrov:
> - Coils (0x): digitalni izhodi, R/W, FC01/05
> - Discrete Inputs (1x): digitalni vhodi, R-only, FC02
> - Holding Registers (4x): 16-bit, R/W, FC03/06/16 ← najpogostejše
> - Input Registers (3x): 16-bit, R-only (meritve), FC04
> SunSpec začne pri 40001 (holding register base).

**V: Kako nastavljaš APN na industrijskem modem routerju?**
> Admin panel routerja → WAN/Cellular → APN nastavitve:
> - APN: npr. "internet" ali operater-specifično
> - Auth type: PAP ali CHAP
> - User/password: če zahteva operater
> - PIN: vnesi SIM PIN ali onemogoči PIN na SIM
> Potrditi z AT komandami: `AT+CGDCONT?` za pregled, `AT+CSQ` za signal.

**V: Zakaj VPN raje kot direkten port forwarding?**
> Port forwarding: exposira specifični port na javni IP → napadalci ga skenirajo (Shodan!). Modbus nima avtentikacije. VPN: šifrirano, avtenticirano, dostop samo za overjene stranke. Celotna seja je tunelirana. Modbus ostane interno.

---

### Monitoring

**V: Elektrarno dodajamo na portal. Kakšen je postopek?**
> 1. Ustvari site: GPS, tilted angle, azimut, tip modulov
> 2. Konfiguriraj data logger/gateway: Modbus mapa za inverterje
> 3. Registriraj naprave: inverterji, merilniki, baterija, pyranometer
> 4. Preveri live podatke: trenutna moč, napetost, tok
> 5. Nastavi alarmne pragove: PR, temperature, komunikacija
> 6. Nastavi obveščanje: email/SMS za operaterje
> 7. 24h test run: preveri konsistentnost podatkov

**V: Portal kaže 0 kW produkcije od polnoči. Kako diagnosticiraš?**
> 1. Preveriti komunikacijo: data logger online?
> 2. Zadnji timestamp podatkov: kdaj je portal zadnjič prejel?
> 3. VPN/SSH na data logger: ali bere inverterje?
> 4. Inverter log: morda grid fault ali overtemperature?
> 5. Fizično: izpad napajanja na lokaciji (AC breaker)?
> 6. Ura: ali je NTP sinhroniziran (napačen čas → napačni grafi)?

---

## SITUACIJSKA VPRAŠANJA

**V: Prišli ste na teren, inverter je ugasnjen. Kaj storite korak za korakom?**
> 1. Varnost: preveriti AC/DC disconnect, izmeriti napetosti pred dotikanjem
> 2. LED indikatorji: error koda?
> 3. Display: alarm sporočilo
> 4. Log v inverterju (serijski port/ethernet)
> 5. Preveriti napajanje (AC vhod), omrežno napetost
> 6. Preveriti DC stran: Voc stringov (tipično 200-800V)
> 7. Izolacijski test DC kabliranja
> 8. Reboot: ali se zažene in pade spet?
> 9. Kontaktirati tech support proizvajalca z error kodo

**V: Stranki se pritožuje, da elektrarna producira manj kot pričakovano. Pristop?**
> 1. Določi referenčno vrednost: energetski elaborat/PVsyst simulacija
> 2. Zberemo podatke: dejanska produkcija, irradiance (pyranometer ali satelitski)
> 3. Izračunaj PR: če < 80% → problema
> 4. Identificiraj vzrok: monitoring analiza stringov, alarmov, temperatura
> 5. Terenska inšpekcija: umazanija, senčenje (nova vegetacija?), vizualni pregled
> 6. Meritve: Voc/Isc per string, IR termografija modulov
> 7. Poročilo s konkretnimi ugotovitvami in ukrepi

---

## VPRAŠANJA ZATE (za konec intervjuja)

- Kateri monitoring portal/SCADA platforma BISOL pretežno uporablja?
- Kateri inverterji in BESS sistemi so v portfoliju (SMA, Fronius, Huawei, Sungrow)?
- Kako je organizirano terensko vs. daljinsko vzdrževanje?
- Kolikšen delež časa je teren vs. pisarna?
- Kakšna je uvajalna pot – mentor, izobraževanja?
- Kakšni projekti so načrtovani – nove elektrarne, nadgradnje?

---

## MEHKA VPRAŠANJA

**V: Zakaj vas zanima to delovno mesto?**
> Kombinacija IT (komunikacije, nadzor) in energetike (solar, BESS) je zanimiva. BISOL je vodilni evropski proizvajalec – vedeti kako moduli dejansko delujejo v terenu doda globino. Dinamično delo, del od energetske tranzicije.

**V: Opišite situacijo, ko ste reševali kompleksen tehnični problem.**
> [Pripravite konkreten primer iz lastnih izkušenj: diagnostika, sistematičen pristop, rešitev]

**V: Kako se spopadate z delom na terenu v neugodnih razmerah?**
> [Konkretno: oprema, PPE, komunikacija, dokumentacija, varnostni protokoli]

---

## HITRI POJMOVNI PREGLED

| Kratica | Pomen |
|---------|-------|
| PV | Photovoltaic |
| MPPT | Maximum Power Point Tracking |
| STC | Standard Test Conditions |
| PR | Performance Ratio |
| BMS | Battery Management System |
| EMS | Energy Management System |
| PCS | Power Conversion System |
| LFP | Lithium Iron Phosphate |
| SoC | State of Charge |
| SoH | State of Health |
| DoD | Depth of Discharge |
| RTU | Remote Terminal Unit |
| SCADA | Supervisory Control and Data Acquisition |
| FCR | Frequency Containment Reserve |
| SPD | Surge Protection Device |
| AFCI | Arc Fault Circuit Interrupter |
| VPN | Virtual Private Network |
| OT | Operational Technology |
| IT | Information Technology |
| VLAN | Virtual Local Area Network |
| NTP | Network Time Protocol |
| APN | Access Point Name |
