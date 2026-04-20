# Solarni PV sistemi – Osnove

## 1. Fotonapetostni efekt

- Sončna svetloba (fotoni) izbija elektrone iz polprevodnika(Si)
- p-n spoj ustvari električno polje → enosmerni tok (DC)
- 1 celica ≈ 0.5–0.6 V; moduli serija/vzporedno za višje napetosti/tokove

Čisti silicij je slab prevodnik. Da postane uporaben za fotonapetostni efekt, ga moramo namenoma "onesnažiti". (proces imenovan doping)


- N-tip (negativni): Siliciju dodamo fosfor, ki ima en elektron več. To ustvari presežek prostih elektronov.
- P-tip (pozitivni): Siliciju dodamo boron, ki ima en elektron manj. To ustvari "vtičnice" ali luknje, ki čakajo na elektrone

Ko ti dve plasti staknemo skupaj, se na stičišču zgodi:
- Elektroni z N-strani skočijo v luknje na P-strani. To ustvari siromašno območje, kjer nastane močna notranje električno polje.
- To polje deluje kot "enosmerni ventil": dovoli pretok v eno smer, ne pa nazaj.

Ko foton(delec svetlobe) zadane sončno celico, svojo energijo preda elektronu v siliciju.
- Če je energija fotona dovolj visoka (večja od t.i energijske reže), elektron "odskoči" iz svoje vezi.
- Nastane par elektron-luknja.
- Zaradi prej omenjenega električnega polja v p-n spoju so ti prosti elektroni prisiljeni potovati proti N-pasti, luknje pa proti P-plasti.

Ti ločeni elektroni si obupno želijo nazaj k svojim luknjam, vendar jim notranje polje poti ne dopušta. Edina pot nazaj je skozi zunanji elektročni krog (tvoje porabnike ali baterijo).
- Ta neprekinjen tok elektronov v eno smer imenujemo enosmerni tok (DC)

Ena celica proizvede približno 0.5-0.6V. To je fizikalna omejitev silicija. Za polnjenje 12V akumulatorja bi potreboval vsaj 36 celic vezanih zaporedno.
Tok je odvisen predvsem od velikosti celice in intenzivnosti svetlobe. Za večji tok celice vežemi vzporedno.
  
Sončna celica je osnovni gradnik in proizvede 0.5V. Fotovoltaični modul.
Fotovoltaični modul je skupina 60-72 celic v enem okvirju in proizvede 30-45V.
PV niz je več modulov povezanih na strehi in proizvede 300-800V.

## 2. Tipi solarnih modulov

| Tip | Izkoristek | Opomba |
|------------------|--------|---------------------------------|
| Monokristalni Si | 20–23% | Najboljši izkoristek, najdražji |
| Polikristalni Si | 16–19% | Kompromis cena/izkoristek       |
| Tankoplastni     | 10–14% | Slabši izkoristek, fleksibilni  |
| Bifacial         | +5–25% | Spredaj + zadaj                 |

## 3. Električne karakteristike modula
- **Voc** – napetost odprtega tokokroga (no-load)
- **Isc** – kratkostični tok
- **Vmp / Imp** – napetost/tok pri max. moči
- **Pmax = Vmp × Imp**
- **Fill Factor (FF)** = Pmax / (Voc × Isc); idealno > 0.75
- **STC** – Standard Test Conditions: 1000 W/m², 25°C, AM 1.5

## 4. Temperaturni koeficienti
Pri fotonapetostnih sistemih je temperatura paradoksalen faktor: Čeprav potrebujemo sonce(toploto), je vročina dejansko sovražnik učinkovitosti. 
  - Vzbujanje elektronov: Ko se silicij segreje, elektroni že zaradi toplote postanejo "nemirni": To zmanjša razloki v energijskih nivojih med p-n spojme.
  - Notranje upornosti: Povišana temperatura poveča vibracije atomov v kristalni mreži silicija, kar otežuje potovanje elektronov (poveča se upornost)
  - Rezultat: Najbolj trpi napetost odprtih sponk (Voc). Medtem ko se električni tok(Isc) ob vročini malenkostno celo poveča, je pa padec napetosti tako silovit, da skuphna izhodna moč pade. (P = UI)

- Višja temperatura → nižja napetost (≈ −0.3%/°C za Voc) - pomeni da za vsako stopinjo nad referenčno temperaturo (25 stopinj) modul izgubi 0.3% svoje napetosti.

Nevarnost pozimi (Mraz = Visoka napetost) - To je kritična točka za vsakega projektanta. Inverterji imajo strogo določeno maksimalno vhodno napetost. Če sistem načrtuješ poleti pri 30 stopinjah, bo napetost nizka. Ko pride jasen zimski dan, in temperature padejo pa napetost panelov naraste, ker je koeficient negativen. 
Posledica: Če nisi pustil dovolj rezerve, lahko napetostni sunek ob mrzlem jutru trajno skuri inverter.
Pravilo: Pri izračunu števila panelov v nizu se vedno uporabi najnižja zgodovinska temperatura na tisti lokaciji.

- Nižja temperatura → višja napetost → pozor pri dimenzioniranju inverterja!

V tehničnih listih opaziš dve meritvi: STC in NOCT. 
STC - Standard Test Conditions - Laboratorijski pogoji (25 stopinj, 1000 W/m2). Ti pogoji so v praksi skoraj nemogoči, saj se črn panel na soncu takoj segreje čez 25 stopinj.
- NOCT – Nominal Operating Cell Temperature (tipično 45°C) - Pove nam, na kakšno temperaturo se bo celica segrela v realnih pogojih.
  - Temperatura zraka: 20 stopinj
  - Sonce: 800 W/m2
  - Veter: 1m/s (ki hladi panele)
- Tipična vrednost : 45 stopin. To pomeni, da ko je zunaj prijetnih 20 stopinj, so celice v resnici že na 45 stopinj. To je tista "delovna temperatura", ki jo uporabiš za realen izračun donosa energije.

Ker je temperatura tako pomembna, se v praksi uporablja nekaj trikov:
1. Zračna reža: Paneli na strehi ne smejo biti nalepljeni direktno na kritino. Potrebujejo vsaj 10-15cm razmika, da pod njimi kroži zrak.
2. Plavajoče elektrarne: Postavljanje panelov na vodo, kjer izhlapevanje vode naravno hladi module.
3. Barva okvirja: Črni okvirji so estetski, a se segrejejo za kakšno stopinjo več kot srebrni

## 5. Komponente sistema

### Grid-tied (omrežni)

```
Moduli → String kabel → DC Combiner Box → Inverter → AC panel → Omrežje
                                              ↑
                                         MPPT regulator (v inverterju)
```

1. Moduli (sončni paneli)

To so generatorji energije. Prevajajo sončno sevanje v enosmerni električni tok (DC).
Vloga: Proizvodnja surove električne energije. Več panelov se veže zaporedno v "string", da dibomi dovolj visoko napetost za učinkovito delo inverterja. Več panelov se veže zaporedno v "string", da dobimo dovolj visoko napetost za učinkovito delo inverterja.

2. String kabel (solarni kabel)

- UV odporni: da izolacija po nekaj letih na soncu ne razpade
- Temperaturno vdržljivi: Na strehi se lahko segrejejo tudi čez 80 stopinj.
- Dvojno izolirani: Zaradi varnosti, saj prenašajo visoke napetosti (tudi do 1000 V).

3. DC Combiner box (Združevalna omarica)

- Če imaš na strehni več nizov (npr. en niz na vzhodni in eden na zahodni strani), se ti kabli srečajo tukaj.
- Varnost: vsebuje varovalke za vsak niz posebej in prenapetostno zaščito (SPD), ki ščiti inverter pred udarom strele.
- Stikalo: Običajno vsebuje glavno DC ločilno stikalo, ki omogoča, da varno odklopiš panele od ostalega sistema. (npr. med servisom)

4. MPPT Regulator (Maximum Power Point Tracking)
To so "možgani" sistema, ki so danes skoraj vedno integrirani neposredno v inverterju.
- Vloga: Sonce se čez dan spreminja(oblaki, kot sevanja). MPPT nenehno (večkrat na sekundo) prilagaja razmerje med napetostjo in tokom tako, da iz panelov iztisne maksimalno možno moč.
- Analogija: MPPT je kot menjalnik v avtomobilu - skrbi, da motor(paneli) vedno teče v optimalnih obratih glede na pogoje na cesti.

5. Inverter (Razsmernik)

Srce sistema. Njegova glavna naloga je pretvorba DC(enosmernega toka) iz panelov v AC(izmenični tok,230V/400V), ki ga uporabljajo gospodinski aparati.
- Sinhronizacija: Inverter mora svojo frekvenco (50 Hz) in fazo popolnoma uskladiti z javnim omrežjem.
- Varnost: Če v javnem omrežju zmanjka elektrike, se mora omrežni inverter takoj izklopiti. To preprečuje, da bi elektrarna pošiljala elektriko v žice, na katerih morda ravno takrat delajo monterji elektro podjetja.

6. AC panel (Elektro omarica z varovalkami)

Tukaj se poti srečajo. Izmenični tok iz inverterja vstopi v tvojo hišno inštalacijo.
  - Prednostna poraba: Energija iz sonca najprej napaja tvoje trenutne porabnike
  - Dvosmerno merjenje: Tukaj je nameščen pametni števec, ki beleži koliko energije si vzel iz omrežja in koliko viškov si vanj oddal.


7. Omrežje

V grid-tied sistemu omrežje deluje kot tvoj stabilizator.
- Podnevi: Viški energije odtekajo v omrežje sosedom.
- Ponoči/pozimi: Ko sonca ni, energijo črpaš nazaj iz omrežja.

### Off-grid
```
Moduli → Charge Controller (MPPT/PWM) → Baterija → Inverter → Porabniki
```
Pri off-grid sistemih se pravila igre spremenijo. Tukaj nimaš varnostne mreže javnega omrežja, zato mora biti sistem popolnoma samostojen in sposoben preživeti "energetsko sušo". (noč ali oblačne dni).

1. Moduli (Sončni sistemi)

Vloga je ista kot pri omrežnem sistemu, vendar je pri off-grid sistemih ključno pre-dimenzioniranje. Ker ne moreš uvažati energije iz omrežja, morajo paneli tudi ob slabem vremenu proizvesti dovolj, da pokrijejo porabo in hkrati napolnijo baterije.

2. Charge C
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
| Vzrok              | Tipična izguba |
|--------------------|----------------|
| Temperatura modula |  5–10%         |
| Senčenje           | variabilno     |
| Umazanija          |    1–5%        |
| Kabelske izgube    |    1–3%        |
| Inverter izkoristek|    2–5%        |
| Mismatch modulov   |    1–2%        |

**PR (Performance Ratio)** = dejanska produkcija / teoretična produkcija; dober sistem > 80%

## 9. Varnostni sistemi
- **DC disconnect** – ločitev od modulov
- **AC disconnect** – ločitev od omrežja
- **Anti-islanding** – inverter zaustavi ob izpadu omrežja (VDE-AR-N 4105, EN 50549)
- **Surge Protection Device (SPD)** – strela/prenapetost
- **AFCI** – Arc Fault Circuit Interrupter (požarna varnost DC)
- **Fuse/breaker** per string

## 11. Ključni pojmi za intervju
- **kWp** – kilowatt peak (nazivna moč pri STC)
- **kWh/kWp** – specifična produkcija (yield)
- **GHI** – Global Horizontal Irradiance
- **POA** – Plane of Array irradiance (dejansko na modul)
- **PR** – Performance Ratio
- **CUF** – Capacity Utilization Factor = dejanska kWh / (kWp × 8760h)
- **LCOE** – Levelized Cost of Energy (€/kWh skozi življenjsko dobo)

