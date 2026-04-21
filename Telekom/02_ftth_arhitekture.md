# FTTx Arhitekture

## 1. FTTx — Fiber to the X

"X" pove, do kod sega optika:

| Kratica | Polno ime | Optika sega do | Zadnja milja |
|---|---|---|---|
| **FTTH** | Fiber to the Home | Stanovanja/hiše | Optika do ONT |
| **FTTB** | Fiber to the Building | Kleti/tehničnih prostorov | Ethernet/VDSL v stavbi |
| **FTTC** | Fiber to the Curb | Omarice ob cesti (~300m) | VDSL2/G.fast do 300m |
| **FTTN** | Fiber to the Node | Vozliščne omarice (~1km) | VDSL2 do 1 km |
| **FTTdp** | Fiber to the Distribution Point | Rozdelilna točka (~10m) | G.fast ali kratka baker |
| **FTTCO** | Fiber to the Central Office | Centralna lokacija | Klasična xDSL |

### Razlika za stranko:
- **FTTH**: gigabitne hitrosti, simetrično, brez bakra
- **FTTB**: dobre hitrosti v bloku, odvisno od notranje instalacije
- **FTTC**: 100–300 Mbps, asimetrično, baker omeji hitrost in razdaljo

> **United Fiber gradi FTTH** — optika direktno do vsake enote.

---

## 2. P2P vs P2MP (PON)

### P2P — Point-to-Point
```
CO ────── vlakno 1 ────── Stranka 1
CO ────── vlakno 2 ────── Stranka 2
CO ────── vlakno 3 ────── Stranka 3
```
- Vsaka stranka ima **dedicirano vlakno** do CO
- Prednosti: enostavno, polna kapaciteta, zasebnost
- Slabosti: **ogromno vlaken** v CO, drag ODF, draga gradnja
- Tipična uporaba: poslovni odjemalci, datacenter povezave

### P2MP — Point-to-Multipoint (PON)
```
CO ─── 1 vlakno ─── Splitter 1:32 ─┬─ Stranka 1
                                    ├─ Stranka 2
                                    ├─ ...
                                    └─ Stranka 32
```
- **Eno vlakno od CO deli 32–128 strank**
- Prednosti: bistveno manj vlaken v trasi, cenejša infrastruktura
- Slabosti: deljeno medij (bandwidth se deli), latenca DBA
- Standard za FTTH masovni rollout

---

## 3. Aktivno vs Pasivno optično omrežje

### AON — Active Optical Network
- Med CO in strankami so **aktivni Ethernet stikali** v terenu
- Vsak node potrebuje napajanje, vzdrževanje
- Primer: Ethernet P2P z aktivnimi ojačevalniki

### PON — Passive Optical Network
- Med OLT in ONT so **samo pasivne komponente** (vlakno + splitter)
- Brez napajanja v terenu
- Prednosti: nižji OPEX, manj vzdrževanja, zanesljivost
- **Standard za modernen FTTH rollout**

---

## 4. 3-nivojska segmentacija FTTH omrežja

```
┌─────────────────────────────────────────────────────────┐
│                    CO / POP                              │
│   OLT ──── ODF ──── Patch panel                         │
└─────────────────────────┬───────────────────────────────┘
                          │
              FEEDER segment
         (1 ali več vlaken do FDH)
                          │
┌─────────────────────────▼───────────────────────────────┐
│              FDH (Fiber Distribution Hub)                │
│         Splitter 1. nivo (npr. 1:4)                      │
└──────┬──────────────┬──────────────┬────────────────────┘
       │              │              │
   DISTRIBUTION segment (do ODP/JB)
       │              │              │
┌──────▼──┐      ┌────▼────┐    ┌───▼─────┐
│  ODP 1  │      │  ODP 2  │    │  ODP 3  │
│Splitter │      │Splitter │    │Splitter │
│2. nivo  │      │2. nivo  │    │2. nivo  │
└──┬──┬───┘      └─┬──┬────┘    └─┬──┬────┘
   │  │            │  │           │  │
DROP segment (drop kabel do ONT)
   │  │
┌──▼─┐ ┌▼──┐
│ONT│ │ONT│
└────┘ └────┘
```

### Feeder segment
- Od CO/POP do FDH (ali prvega splitterja)
- Tipično 1–10 km
- Kabel: 48–288 vlaken, G.652.D, v mikrokanalu ali direktno
- **Eno ali več vlaken na en OLT port**

### Distribution segment
- Od FDH/splitterja do ODP (zunanjih razdelilnih točk)
- Tipično 200 m – 2 km
- Kabel: 12–48 vlaken
- Konča se pri ODP — zunanja omara/muffa s splitterjem

### Drop segment
- Od ODP/JB do ONT pri stranki
- Tipično 10–200 m (max ~500 m za link budget)
- Kabel: 1–4 vlakna, G.657.A2, drop kabel
- Zadnji meter = patch kabel znotraj stanovanja

---

## 5. Ključni elementi omrežja

### CO (Central Office) / POP (Point of Presence)
- Lokacija aktivne opreme (OLT, routerji, BNG)
- ODF (Optical Distribution Frame) — zaključevanje feeder kablov
- Klimatizacija, UPS, nadzor
- Pokriva tipično 2000–10000 strank (odvisno od OLT kapacitete)

### ODF — Optical Distribution Frame
- Pasivni regal s patch paneli
- Zaključevanje kablov in konektorji
- Patchanje OLT portov na feeder kable
- Tipično SC/APC konektorji

### FDH — Fiber Distribution Hub
- Zunanja omara (IP55/IP65) ali notranja
- Vsebuje: splice enclosure, splitterji 1. nivo, patch paneli
- Lokacija: tehnični prostori blokov, ulični kabineti
- Kapaciteta: tipično 32–576 vlaken

### ODC — Outdoor Cabinet
- Zunanja omarica na drogu ali steni
- Manjša od FDH, tipično 1–4 splitterji

### ODP — Optical Distribution Point
- Najmanjša zunanjo razdelilna točka
- Lokacija: fasada stavbe, jašek, ulica
- Vsebuje zadnji splitter in zaključke drop kablov
- Tipično 1:8 ali 1:16 splitter
- Konektorji SC/APC za priključitev drop kablov

### ONT — Optical Network Terminal
- Aktivna oprema pri stranki
- Pretvori optični signal v Ethernet/WiFi/VoIP/TV
- Tipično: 1× GE WAN, 4× GE LAN, 2× FXS (VoIP), WiFi
- Napajanje iz električne vtičnice stranke

---

## 6. Tipična topologija za slovensko FTTH omrežje

### Mestno okolje (bloki):
```
POP (1 na 10.000 strank)
    └── FDH v kleti bloka (per 200–500 strank)
            └── ODP na vsakem nadstropju (per 8–16 strank)
                    └── Drop do vsakega stanovanja
```
Split: 1:4 v FDH × 1:16 v ODP = **1:64 skupaj**

### Primestno (individualne hiše):
```
CO / POP
    └── FDH ob cesti (per 100–200 hiš)
            └── ODP na drogu ali v jašku (per 8–16 hiš)
                    └── Drop kabel po drogu ali pod zemljo do hiše
```
Split: 1:4 × 1:8 = **1:32 skupaj**

### Podeželje (redka poselitev):
```
Remote POP (v kontejnerju)
    └── ODP pri vsaki skupini hiš (2–4 km feeder)
            └── 1:8 splitter, kratki dropi
```
Nižji split ratio (1:16 ali 1:32) ker je manj strank in daljše razdalje.

---

## 7. Hitri povzetek — kar morate znati na razgovoru

1. FTTH = optika do stanovanja, FTTB = do kleti bloka
2. PON = pasivno (samo splitterji v terenu), brez napajanja v terenu
3. 3 segmenti: feeder → distribution → drop
4. CO/POP → OLT + ODF → feeder → FDH (splitter 1) → distribution → ODP (splitter 2) → drop → ONT
5. Tipični split: 1:32 za redkejšo poselitev, 1:64 za gosto mestno okolje
6. FDH = večja omara s splitterji, ODP = mala zunanja razdelilna točka
7. Drop kabel = G.657.A2, max 200–500 m
