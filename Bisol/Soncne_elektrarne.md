# Soncne_elektrarne

# Solarni PV sistemi – Osnove


## 1. Fotonapetostni efekt

Čisti silicij je slab prevodnik. Da postane uporaben za fotonapetostni efekt, ga moramo namenoma "onesnažiti". (proces imenovan doping)
- N-tip (negativni): Siliciju dodamo fosfor, ki ima en elektron več. To ustvari presežek prostih elektronov.
- P-tip (pozitivni): Siliciju dodamo boron, ki ima en elektron manj. To ustvari "vtičnice" ali luknje, ki čakajo na elektrone

Ko ti dve plasti staknemo skupaj, se na stičišču zgodi:
- Elektroni z N-strani skočijo v luknje na P-strani. To ustvari siromašno območje, kjer nastane močno notranje električno polje.
- To polje deluje kot "enosmerni ventil": dovoli pretok v eno smer, ne pa nazaj.

Ko foton(delec svetlobe) zadane sončno celico, svojo energijo preda elektronu v siliciju.
Če je energija fotona dovolj visoka (večja od t.i energijske reže), elektron "odskoči" iz svoje vezi. Nastane par elektron-luknja.
Zaradi prej omenjenega električnega polja v p-n spoju so ti prosti elektroni prisiljeni potovati proti N-pasti, luknje pa proti P-plasti.
Ti ločeni elektroni si obupno želijo nazaj k svojim luknjam, vendar jim notranje polje poti ne dopušta. Edina pot nazaj je skozi zunanji elektročni krog (tvoje porabnike ali baterijo). Ta neprekinjen tok elektronov v eno smer imenujemo enosmerni tok (DC)
Ena celica proizvede približno 0.5-0.6V. To je fizikalna omejitev silicija. Za polnjenje 12V akumulatorja bi potreboval vsaj 36 celic vezanih zaporedno.
Tok je odvisen predvsem od velikosti celice in intenzivnosti svetlobe. Za večji tok celice vežemi vzporedno.
Fotovoltaični modul je skupina 60-72 celic v enem okvirju in proizvede 30-45V. PV niz je več modulov povezanih na strehi in proizvede 300-800V.


---


## 2. Tipi solarnih modulov

| Tip | Izkoristek | Opomba |
|------------------|--------|---------------------------------|
| Monokristalni Si | 20–23% | Najboljši izkoristek, najdražji |
| Polikristalni Si | 16–19% | Kompromis cena/izkoristek       |
| Tankoplastni     | 10–14% | Slabši izkoristek, fleksibilni  |
| Bifacial         | +5–25% | Spredaj + zadaj                 |


---

## 3. Električne karakteristike modula

- **Voc** – napetost odprtega tokokroga (no-load)
- **Isc** – kratkostični tok
- **Vmp / Imp** – napetost/tok pri max. moči
- **Pmax = Vmp × Imp**
- **Fill Factor (FF)** = Pmax / (Voc × Isc); idealno > 0.75
- **STC** – Standard Test Conditions: 1000 W/m², 25°C, AM 1.5
  

---

## 4. Temperaturni koeficienti
Pri fotonapetostnih sistemih je temperatura paradoksalen faktor: Čeprav potrebujemo sonce(toploto), je vročina dejansko sovražnik učinkovitosti.

- Vzbujanje elektronov: Ko se silicij segreje, elektroni že zaradi toplote postanejo "nemirni": To zmanjša razliko v energijskih nivojih med p-n spojem.
  - Notranje upornosti: Povišana temperatura poveča vibracije atomov v kristalni mreži silicija, kar otežuje potovanje elektronov (poveča se upornost)
  - Rezultat: Najbolj trpi napetost odprtih sponk (Voc). Medtem ko se električni tok(Isc) ob vročini malenkostno celo poveča, je pa padec napetosti tako silovit, da skupna izhodna moč pade. (P = UI)
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


---

## 5. Komponente sistema

### Grid-tied (omrežni)

```
Moduli → String kabel → DC Combiner Box → Inverter → AC panel → Omrežje
                                              ↑
                                         MPPT regulator (v inverterju)
```

1. Moduli (sončni paneli)

To so generatorji energije. Proizvajajo sončno sevanje v enosmerni električni tok. Več panelov se veže zaporedno v "string", da dobimo dovolj visoko napetost za učinkovito delo inverterja.

2, String kabel (solarni kabel)

- UV odporni
- Temperaturno vzdržljivi
- Dvojno izolirani: Zaradi varnosti, saj prenašajo visoke napetosti (tudi do 1000 V).

3. DC Combiner box

Če imaš na strehi več nizov se ti kabli srečajo tukaj. Vsebuje varovalke za vsak niz posebej in prenapetostno zaščito (SPD), ki ščiti inverter pred udarom strele. Običajno vsebuje glavno DC ločilno stikalo, ki omogoča, da varno izklopiš panele od ostalega sistema.

4. MPPT Regulator (Maximum Power Point Tracking)

To so "možgani" sistema. ki so danes skoraj vedno integrirani neposredno v inverterju. 
Vloga: Sonce se čez dan spreminja (oblaki, kot sevanja). MPPT nenehno(večkrat na sekundo) prilagaja razmerje med napetostjo in tokom tako, da iz panelov iztisne maksimalno moč.

5. Inverter (Razsmernik)

Srce sistema. Njegova glavna naloga je pretvorba DC(enosmernega toka) iz panelov v AC(izmenični tok, 230V/400V), ki ga uporabljajo gospodinjski aparati.
Sinhronizacija: Inverter mora svojo frekvenco (50 Hz) in fazo popolnoma uskladiti z javnim omrežjem. 
Varnost: Če v javnem omrežju zmanjka elektrike, se mora omrežni inverter takoj izklopiti. To preprečuje, da bi elektrarna pošiljala elektriko v žice, na katerih morda ravno takrad delajo monterji elektro podjetja.

6. AC panel (Elektro omarica z varovalkami)

Tukaj se poti srečajo. Izmenični tok iz inverterja vstopi v tvojo hišno inštalacijo.
Prednostna poraba: Energija iz sonca najprej napaja tvoje trenutne porabnike
Dvosmerno merjenje: Tukaj je nameščen pametni števec, ki beleži koliko energije iz omrežja si vzel in koliko viškov si vanjo oddal.

7. Omrežje

V grid tied sistemu deluje kot tvoj stabilizator.
Podnevi: Viški energije odtekajo v omrežje sosedom.
Ponoči/pozimi: Ko sonca ni, energijo črpaš nazaj iz omrežja.


---

### Off-grid

Moduli → Charge Controller (MPPT/PWM) → Baterija → Inverter → Porabniki

Tukaj ni varnostne mreže javnega omrežja, zato mora biti sistem popolnoma samostojen in sposoben preživeti energetsko sušo.

1. Moduli

Pri off-grid sistemih je kjučno pre-dimenzioniranje. Ker ne moreš uvažati energije iz omrežja, morajo paneli tudi ob slabem vremenu proizvesti dovolj, da pokrijejo porabo in hkrati napolnijo baterije.

2. Charge controller (Polnilni regulator) je ključna komponenta, ki je pri grid-tied sistemu sploh ne poznamo. Njegova naloga je, da energijo iz panelov varno in učinkovito "stisne" v baterijo.

Poznamo dva tipa:
- PWM (Pulse Width Modulation): Starejša, cenejša tehnologija. Deluje kot stiskalo, ki se hitro vklaplja in izklaplja. Je manj učinkovito, saj napetost panelov "povozi" na napetost baterije. ( Izgubljaš energijo).
- MPPT: Sodobna in pametna izbira. Elektronsko pretvori višjo napetost panelov v nižjo napetost za polnjenje baterije, pri tem pa poveča tok. Je do 30% bolj učinkovita kot PWM še posebej v hladnem vrmeenu.

3. Baterija je srce in hkrati najdražji del off-grid sistema. Shranjuje energijo za čas, ko ni sonca.
  - LiFePO4 (Litij - Železo - fosfat) - Danes standard - lahko izprazniš do 90%, zdržijo 10x več ciklov in so varnejše.
    
4. Inverter

V off-grid sistemu ima inverter drugačno vlogo kot v omrežnem:
- Ustvarjanje lastne mreže: Sam določa frekvenco(50Hz) in napetosti (230V), saj nima omrežja, po katerem bi se zgledoval.
- Visoki zagonski tokovi: Ker napaja naprave direktno, mora biti sposoben prenestki kratkotrajne sunke(npr. ko se vklopi hladilnik ali vodna črpalka), ki so lahko 2-3x večji od njegove nazivne moči.
- Vgrajen polnilnik (opcijsko): Veliko off-grid inverterjev ima tudi vhod za generator(agregat), da lahko napolniš baterije, če je sonca premalo več dni zapored.

5. Porabniki

- DC porabniki: Nekatere naprave lahko priklopimo direktno na reuglator ali baterijo, in se s tem izognemo izgubam, ki nastanejo pri pretvorbi v 230V.

Lastnost,Grid-tied (Omrežni),Off-grid (Otočni)
Baterija,Opcijska (za večjo avtonomijo),Nujna
Izpad omrežja,Elektrarna neha delovati,Deluje nemoteno
Načrtovanje,Glede na letno porabo,Glede na največjo dnevno porabo
Viški,Oddajaš v omrežje,Ostanejo neizkoriščeni (ko je baterija polna)

Pomemben nasvet: Pri off-grid sistemih je kritičen podatek "Days of Autonomy" (dnevi avtonomije). Pove nam, koliko dni lahko hiša živi samo iz baterij, če je zunaj popolna tema (npr. sneg na panelih). Običajno se projektira za 2–3 dni.


---



### Hibridni
```
Moduli → Hibridni inverter ←→ Baterija
              ↕
           Omrežje / Porabniki
```

Hibridni sistem je "najbolše iz obeh svetov". Združuje zanesljivost omrežne povezave z neodvisnostjo otočnega sistema. Danes je to "zlati standard" za družinske hiše, saj omogoča maksimalno oskrbo.

1. Hibridni inverter - ni le navaden razsmernik, ampak kompleksna naprava, ki upravlja s tremi viri energije hkrati: Soncem, baterijo in omrežjem. V njem se nahajajo:

- MPPT regulator za panele
- Baterijski pomnilnik (dvosmerni: polni baterijo iz sonca, in prazni baterijo za hišo).
- EMS (Energy management system): Možgani, ki se vsako sekundo odločajo, kam bo šla energija.









