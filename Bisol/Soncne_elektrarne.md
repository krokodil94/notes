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