# Solarni PV sistemi – Osnove

## 1. Fotonapetostni efekt

- Sončna svetloba (fotoni) izbija elektrone iz polprevodnika(Si)
- p-n spoj ustvari električno polje → enosmerni tok (DC)
- 1 celica ≈ 0.5–0.6 V; moduli serija/vzporedno za višje napetosti/tokove










- Če je energija fotona dovolj visoka (večja od t.i energijske reže), elektron "odskoči" iz svoje vezi.
- Nastane par elektron-luknja.
- Zaradi prej omenjenega električnega polja v p-n spoju so ti prosti elektroni prisiljeni potovati proti N-pasti, luknje pa proti P-plasti.

Ti ločeni elektroni si obupno želijo nazaj k svojim luknjam, vendar jim notranje polje poti ne dopušta. Edina pot nazaj je skozi zunanji elektročni krog (tvoje porabnike ali baterijo).
- Ta neprekinjen tok elektronov v eno smer imenujemo enosmerni tok (DC)

Ena celica proizvede približno 0.5-0.6V. To je fizikalna omejitev silicija. Za polnjenje 12V akumulatorja bi potreboval vsaj 36 celic vezanih zaporedno.
Tok je odvisen predvsem od velikosti celice in intenzivnosti svetlobe. Za večji tok celice vežemi vzporedno.
  
Sončna celica je osnovni gradnik in proizvede 0.5V. 
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
  - Vzbujanje elektronov: Ko se silicij segreje, elektroni že zaradi toplote postanejo "nemirni": To zmanjša razliko v energijskih nivojih med p-n spojem.
  - Notranje upornosti: Povišana temperatura poveča vibracije atomov v kristalni mreži silicija, kar otežuje potovanje elektronov (poveča se upornost)
  - Rezultat: Najbolj trpi napetost odprtih sponk (Voc). Medtem ko se električni tok(Isc) ob vročini malenkostno celo poveča, je pa padec napetosti tako silovit, da skuphna izhodna moč pade. (P = UI)
  - Višja temperatura → nižja napetost (≈ −0.3%/°C za Voc) - pomeni da za vsako stopinjo nad referenčno temperaturo (25 stopinj) modul izgubi 0.3% svoje napetosti.

Nevarnost pozimi (Mraz = Visoka napetost) - To je kritična točka za vsakega projektanta. Inverterji imajo strogo določeno maksimalno vhodno napetost. Če sistem načrtuješ poleti pri 30 stopinjah, bo napetost nizka. Ko pride jasen zimski dan, in temperature padejo pa napetost panelov naraste, ker je koeficient negativen. 
Posledica: Če nisi pustil dovolj rezerve, lahko napetostni sunek ob mrzlem jutru trajno skuri inverter.
Pravilo: Pri izračunu števila panelov v nizu se vedno uporabi najnižja zgodovinska temperatura na tisti lokaciji.


V tehničnih listih opaziš dve meritvi: STC in NOCT. 
STC - Standard Test Conditions - Laboratorijski pogoji (25 stopinj, 1000 W/m2). Ti pogoji so v praksi skoraj nemogoči, saj se črn panel na soncu takoj segreje čez 25 stopinj.
NOCT – Nominal Operating Cell Temperature (tipično 45°C) - Pove nam, na kakšno temperaturo se bo celica segrela v realnih pogojih.
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
Vloga: Proizvodnja surove električne energije. Več panelov se veže zaporedno v "string", da dobimo dovolj visoko napetost za učinkovito delo inverterja. 

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

2. Charge Controller (Polnilni regulator) je ključna komponenta, ki je pri grid-tied sistemu sploh ne poznamo. Njegova naloga je, da energijo iz panelov varno in učinkovito "stisne" v baterijo.
Poznamo dva tipa:
- PWM (Pulse Width Modulation): Starejša, cenejša tehnologija. Deluje kot stiskalo, ki se hitro vklaplja in izklaplja. Je manj učinkovito, saj napetost panelov "povozi" na napetost baterije (izgubljaš energijo).
- MPPT (Maximum Power Point Tracking):  Sodobna in pametna izbira. Elektronsko pretvori višjo napetost panelov v nižjo napetost za polnjenje baterije, pri tem pa poveča tok. Je do 30% bolj učinkovita kot PWNM še posebej v hladnem vremenu.
  
3. Baterija je srce in hkrati najdražji del off-grid sistema. Baterija shranjuje energijo za čas, ko ni sonca.
  - Svinčeno-kislinske /AGM / Gel: Cenejše ob nakupu, a krajša življenska doba in občutljivost na globoko praznenje. ( Ne smeš izprazniti pod 50% )
  - LiFePO4 (Litij - Železo - fosfat) - Danes standard - lahko izprazniš do 90%, zdržijo 10x več ciklov in so varnejše.

4. Inverter (Otočni razsmernik)

V off-grid sistemu ima inverter drugačno vlogo kot v omrežnem:
  - Ustvarjanje lastne mreže: Sam določa frekvenco (50 Hz) in napetost (230 V), saj nima omrežja, po katerem bi se zgledoval.
  - Visoki zagonski tokovi: Ker napaja naprave direktno, mora biti sposoben prenesti kratkotrajne sunke (npr. ko se vklopi hladilnik ali vodna črpalka), ki so lahko 2-3x večji od njegove nazivne moči.
  - Vgrajen polnilnik (opcijsko): Veliko off-grid inverterjev ima tudi vhod za generator(agregat), da lahko napolniš baterije, če je sonca premalo več dni zapored.

5. Porabniki

- DC porabniki: Nekatere naprave lahko priklopimo direktno na regulator ali baterijo. S tem se izgonemo izgubam, ki nastanejo pri pretvorbi v 230V.
- AC porabniki: Standardne naprave na 230V.

Lastnost,Grid-tied (Omrežni),Off-grid (Otočni)
Baterija,Opcijska (za večjo avtonomijo),Nujna
Izpad omrežja,Elektrarna neha delovati,Deluje nemoteno
Načrtovanje,Glede na letno porabo,Glede na največjo dnevno porabo
Viški,Oddajaš v omrežje,Ostanejo neizkoriščeni (ko je baterija polna)

Pomemben nasvet: Pri off-grid sistemih je kritičen podatek "Days of Autonomy" (dnevi avtonomije). Pove nam, koliko dni lahko hiša živi samo iz baterij, če je zunaj popolna tema (npr. sneg na panelih). Običajno se projektira za 2–3 dni.
### Hibridni
```
Moduli → Hibridni inverter ←→ Baterija
              ↕
           Omrežje / Porabniki
```

Hibridni sistem je "najbolše iz obeh svetov". Združuje zanesljivost omrežne povezave s neodvisnostjo otočnega sistema. Danes je to "zlati standard" za stanovanjske hiše, saj omogoča maksimalno samooskrbo.

1. Hibridni inverter (Vse v enem) - To ni le navaden razsmernik, ampak kompleksna naprava, ki upravlja s tremi viri energije hkrati: Soncem, baterijo in omrežjem. V njem se najahajo:

  - MPPT regulator za panele
  - Baterijski polnilnik (dvosmerni: polni baterijo iz sonca/omrežja in prazni baterijo za hišo).
  - EMS (Energy management system): Možgani, ki se vsako sekundo odločajo, kam bo šla energija.

2. Baterija (visokonapetostna shramba) - Pri hibridnih sistemih se pogosto uporablja visokonapetostne baterije (150-450V) kar poveča ikoristek pretvorbe, saj je napetost bližje tisti v omrežju.
  - Vloga: shranjuje viške čez dan za porabo zvečer in ponoči.
  - Rezerva: Hibridni sistemi omogočajo nastavitev "rezervne kapacitete", ki se je nikoli ne dotakneš, razen če zmanjka elektrike v omrežju.

3. Načini delovanja (Logika sistema): Hibridni sistem deluje v treh glavnih načinih:

   - Samooskrba - sonce napaja hišo - viški polnijo baterijo - ko je baterija polna gredo viški v omrežje.
   - Backup mode(EPS/UPS): Ob izpadu omrežja se inverter v milisekundah fizično loči od zunanjega omrežja( da ne pošilja toka ven) in ustvari lastno "otočno" mrežo za nujne porabnike v hiši
3. Time of use (Tarifno delovanje) - Če imaš poceni in drago tarifo, lahko inverterju ukažeš, naj polni baterijo iz omrežja ponoči, ko je poceni in jo prazno podnevi, ko je draga.

Zakaj izbrati hibridni sistem? 

Prednost,Opis
Varnost,"Hiša ima elektriko tudi, ko sosedje ostanejo v temi (Blackout zaščita)."
Donosnost,Maksimiziraš porabo lastne energije (ki je brezplačna) in minimaliziraš nakup iz omrežja.
Fleksibilnost,"Baterije lahko dodaš naknadno, ko se potrebe povečajo."

Ključna razlika v shemi (Smart Meter)
V hibridni shemi je nujen še en element, ki ga nisi narisal: Pametni števec (Smart Meter), ki je nameščen tik ob glavnih varovalkah hiše.
Hibridni inverter mora vedeti, ali tvoja hiša trenutno "uvaža" ali "izvaža" elektriko. Brez tega podatka ne bi vedel, kdaj mora začeti prazniti baterijo, da ustavi uvoz iz omrežja.

## 6. Inverterji
- **String inverter** – 1 MPPT na string; en shadow → vse prizadeto
- **Central inverter** – za velike elektrarne (>100 kW); centraliziran
- **Micro inverter** – 1/modul; dražji, boljši pri senci
- **Power optimizer** – modul-level DC/DC; centralni inverter ostane

"Ali optimizirati na nivoju modula ali nivoju niza?

1. String Inverter (Nizni razsmernik)
To je klasična in najbolj razširjena tehnologija. Več panelov povežemo zaporedno v eno dolgo "verigo" (niz), ki se konča v inverterju na steni.
Problem sence: Ker so paneli vezani zaporedno, delujejo kot stare novoletne lučke. Če en panel prekrije senca dimnika, se upor v njem poveča, kar upočasni pretok elektronov skozi celoten niz.
Prednosti: Najcenejša rešitev, visoka zanesljivost (manj elektronike na vroči strehi), enostavno vzdrževanje.
Idealno za: Strehe brez senc, kjer so vsi paneli obrnjeni v isto smer.

2. Central inverter (Centralni razsmernik)

To so "veliki bratje" string inverterjev. Niso namenjeni hišam, ampak ogromnim poljem panelov.
Zasnova: Namesto da bi imeli 50 malih inverterjev, imamo eno ogromno omaro (velikosti kontejnerja), kamor se stekajo vsi nizi.
Moč: Običajno od 100kW pa vse do več MW.
Prednosti: Nižji stroški na vat moči pri velikih projektih, lažje upravljanje za elektroenergetski sistem.

3. Micro Inverter (mikro razsmernik)
Tukaj vsak panel dobi svoj mali inverter, nameščen neposredno pod njim. Iz strehe ne pride DC tok, ampak že pripravljen AC (230V).

Individualni MPPT: Vsak panel dela neodvisno. Če na enega pade senca, ostalih 19 dela s 100% močjo.
Prednosti: Najboljši izkoristek pri kompleksnih strehah (več smeri, dosti dimnikov/kukerlov), večja varnost (ni visoke DC napetosti na strehi).
Slabost: Visoka cena in dejstvo, da imaš občutljivo elektroniko izpostavljeno vročini neposredno pod paneli.

4. Power Optimizer (Močnostni optimizatorji)
To je hibridna rešitev (npr. SolarEdge). Pod vsak panel damo DC/DC pretvornik (optimizator), na steni pa še vedno ostane en osrednji inverter.
Kako deluje: Optimizator prilagodi napetost in tok posameznega panela tako, da ta ne ovira niza, tudi če je v senci.
MLPE (Module-Level Power Electronics): Omogoča spremljanje delovanja vsakega posameznega panela preko aplikacije.
Prednosti: Cenejši od mikro-inverterjev, a rešujejo problem sence skoraj enako dobro.

Hitra primerjava za odločitev:

Tehnologija,Cena,Izkoristek v senci,Lokacija elektronike
String,Nizka,Slab,V hiši/Garaži
Micro,Visoka,Odličen,Na strehi (pod paneli)
Optimizer,Srednja,Odličen,Oboje (streha + stena)

Zanimivost: Večina sodobnih string inverterjev ima danes že 2 ali 3 MPPT vhode. To pomeni, da lahko npr. 10 panelov na južni strani povežeš na en vhod, 10 na vzhodni pa na drugega, in bosta delovala neodvisno brez uporabe dragih optimizatorjev.

### MPPT – Maximum Power Point Tracking
Brez MPPT bi bili solarni sistemi le dragi in neučinkoviti grelniki silicija. Ker sonce ni konstanten vir energije, MPPT deluje kot dinamični vmesnik, ki "lovi" fizikalne ekstreme.

Sončna celica ima specifično I-V karakteristiko (razmerje med tokom in napetostjo). Če s panela črpaš preveč toka, napetost strmoglavo pade. Če je napetost previsoka, tok pade.
Točka maksimalne moči (MPP) je tisto "koleno" na krivulji, kjer je zmnožek P=UI največji. Ta točka se nenehno premika glede na osvetljenost in temperaturo.

Algoritmi:
- P&O(Perturb & Observe/ Poskusi & opazuj) je najpogostejši algoritem zaradi svoje preprostosti.
1. Perturb (Sprememba): Regulator malenkost spremeni (zviša ali zniža) delovno napetost panela.
2. Observe(Opazuj): Izmeri moč. Če je moč večja kot prej, nadaljuje v isti smeri. Če je moč padla, spremeni smer.
Slabost: Okoli točke MPP vedno malce "oscilira", namesto da bi se popolnoma ustavil. Ob hitrih spremembah vremena se lahko za trenutek "izgubi".

-Incremental Conductance(InCond): Bolj napreden algoritem, ki temelji na matematiki odvoda (dP/dV).
Algoritem meri inkrementalno prevodnost in neposredno ve, ali je dosegel vrh krivulje.
Prednosti: Ko doseže MPP, se tam ustali in ne niha. Hitreje se odziva na spremembe vremena, a zahteva več procesorske moči.

MPPT vhodni razpon vs. Voc (ključ za načrtovanje)
To je točka, kjer se najpogosteje delajo napake pri DIY projektih ali hitrem dimenzioniranju.

MPPT Voltage Range (Operativno območje)
To je območje napetosti (npr. 150-800V), v katerem je inverter sposoben izvajati MPPT algoritem.
- Če je napetost niza pod spodnjo mejo, se inverter sploh ne bo vklopil.
- Če je napetost nad zgornjo mejo, bo inverter še vedno deloval, vendar ne bo mogel izvleči maksimalne moči(začel bo omejevati moč).

Max DC Input Voltage (Vmax ali Voc meja)
To je absolutna varnostna meja, ki je ne smeš preseči niti za milivolt.  Pozimi pri nizkih temperaturah napetost niza Voc naraste. Če niz panelov v teoriji daje 950V pri 25 stopinjih, bo pozimi pri mrazu zlahka presegel 1000V in uničil vhodno stopnjo inverterja.

Težava: Več vrhov (Globalni vs. Lokalni MPP)

V primeru delnega zasenčenja se I-V krivulja popači in dobi več "grbin". 
- Lokalni MPP: "Lažni" vrh, kjer se enostaven P&O algoritem lahko ustavi, misleč da je na vrhu.
- Globalni MPP: Dejanska točka največje moči celotnega niza.
- Sodobni inverterji imajo funkcijo "Global Scan" ali "Shade Fix", ki vsakih nekaj minut preveri celotno krivuljo, da se prepriča, ali ni kje drugje še višji vrh.

Pri načrtovanju vedno poskrbi, da je napetost niza v vročem poletju (najnižja napetost) še vedno znotraj MPPT razpona, hkrati pa, da napetost v najhladnejši zimi ne preseže Max DC napetosti inverterja.

## 7. Stringing – dimenzioniranje
To so tri ključne enačbe, ki ločijo varno in učinkovito napravo od tiste, ki se bo bodisi pokvarila (previsoka napetost), ali pa se poleti sploh ne bo vklopila (prenizka napetost).
  - **Max string V** = Voc (STC) × koef. temp. (min. temp.) × N modulov < Vmax inverterja
  To je varnostna meja. Ta izračun preprečuje uničenje inverterja v mrzlih zimskih jutrih.
  - Temperaturni koeficient - Običajno je nehativen (npr -0.28%/stop. C). Pri izračunu ga upoštevamo tako, da se napetost z znižanjem temperature povečuje.
  - Tmin: Ne uporabi povprečne zimske temperature, ampak zgodovinski minimum na lokaciji (npr. -15 ali -20 stopinj v Sloveniji)
  - Pravilo: Ta vrednost mora biti vedno pod Max DC Input Voltage v tehničnem listu inverterja.

- **Min string V** = Vmp × koef. temp. (max. temp.) × N > Vmin MPPT - Operativna meja
Ta izračun zagotavlja, da bo inverter deloval tudi v najhujši vročini, ko se paneli segrejejo na 60 stopinj ali več
  - Tmax: To je temperatura celice. V vročem poletjue celice dosežejo tudi okoli 70 stopinj.
  - Vloga: Če ta napetost pade pod Vmin MPPT (spodnji prag delovnega območja), bo inverter izgubil točko maksimalne moči ali pa se bo celo izklopil, čeprav sonce močno sije.
  - Nasvet: vedno ciljaj na sredino MPPT območja za optimalen izkoristek.

- **Število vzporednih stringov** = Imax inverterja / Isc stringa - Tokovna omejitev (vzporedno vezanje)
Pri večjih sistemih pogosto vežemo dva ali več stringov vzporedno na isti MPPT vhod.
  -Napetost ostane ista, tok se sešteva: Itotal = Nstrings*Isc
  -Omejitev: Ta seštevek mora biti nižji od Max Input CUrrent (Idc,max) na posameznem MPPT vhodu inverterja.
  -Pozor na "Isc PV": Nekateri inverterji imajo navedeno tudi kratkostično tokovno mejo, ki je ne smeš preseči, da ob morebitni napaki ne pride do poškodb vezja,

Praktičen primer:
Panel z Voc = 40V, in inverter z Vmax = 1000V.
Teoretični max: 1000/40 = 25 panelov
Zimski popravek: Zaradi mraza napetost zraste za cca 15-20%
Varna meja: 25 * 0.85 = 21 panelov ->to je realna zgornja meja

Povzetek: 
Parameter,Kateri podatek gledaš?,Kdaj je kritično?,Cilj načrtovanja
Max Napetost,Voc​ (Open Circuit),Pozimi (mraz),Ne skuri inverterja!
Min Napetost,Vmp​ (Max Power),Poleti (vročina),Ostani v MPPT območju!
Max Tok,Isc​ (Short Circuit),Ob polnem obsevanju,Ne pregrevaj vhodov!

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

