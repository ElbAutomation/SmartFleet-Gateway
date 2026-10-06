# SmartFleet Gateway — Bauanleitung Trägerplatine V1.0

Ein Hutschienengerät mit 2 TE: XIAO ESP32S3 Plus und WIZ850io werden ohne
Sockel direkt auf eine Trägerplatine gelötet, die nur Durchsteckbauteile trägt.
Du lötest keine SMD-Teile.

**Stand:** Die Maße stammen aus den Datenblättern. Bevor du Platinen bestellst
oder ins Gehäuse schneidest, gehört eine Anprobe mit den echten Teilen dazu:
Passen RJ45-Stecker, Klemmenabdeckung, SMA-Buchse und USB-C-Stecker so, wie
hier beschrieben?

Lage auf der Platine: In dieser Anleitung liegt die Platine so vor dir, dass die
**Klemme unten links** und das **WIZ850io oben links** liegt; der Schriftzug
„SmartFleet Gateway V1.0“ steht unten rechts neben der Klemme.
„Links“ ist die Seite der Klemme.

## 1. Teile prüfen

Die Stückliste steht am Ende dieser Anleitung und als `stueckliste.csv`, je
Teil mit Reichelt-Link und, wo es eins gibt, einem Ersatzteil, falls das erste
nicht lieferbar ist. Leg die Teile nach
Bezeichner bereit (C1 … U2). Die Platine bestellst du mit
`traegerplatine_gerber.zip` bei einem Leiterplattenfertiger (2 Lagen, 1,6 mm,
HASL bleifrei).

Du brauchst: Lötkolben, Lötzinn, Seitenschneider, Multimeter, Labornetzteil oder
24-V-Netzteil, Bohrer 6,5 mm, kleine Feile oder Cuttermesser.

## 2. Löten — niedrige Teile zuerst

| Schritt | Teil | Worauf achten |
|---|---|---|
| 1 | D1, D2 (links, senkrecht) | **Ring nach oben.** D1 ist die 1N5819, D2 die dickere P6KE33A |
| 2 | D3 (über dem XIAO, links neben U1, waagerecht) | 1N5819, **Ring nach links** |
| 3 | F1 | PTC, beliebig herum |
| 4 | C2 (über D3) | **Liegend:** Plusbein links, Minusbein rechts, Beine 90° biegen, Körper flach nach **oben** auf die Platine legen |
| 5 | U2 (oben rechts, neben der RJ45) | MCP1702 im TO-92: die beiden **äußeren Beinchen auf 2,54 mm aufbiegen**. **Flache Seite nach unten**, wie die gerade Linie im Bestückungsdruck. Höchstens 8 mm hoch, er sitzt unter dem Schulterdach |
| 6 | C3 (oben rechts, über U2), C4 (rechts neben dem WIZ850io) | Keramik 1 µF, beliebig herum, stehend bis auf die Platine. Hat das Teil Raster 2,54 (KEMET C315), die Beinchen auf 5,08 mm aufbiegen |
| 7 | C1 (links) | Stehend, **Minusstreifen nach oben** |
| 8 | U1 (Mitte, über dem XIAO) | Traco TSR 1-2450. Der **Punkt am Wandler** (Pin 1) gehört zum **Punkt im Bestückungsdruck**; Pin 1 liegt links |
| 9 | J1 (unten links) | Klemme mit der **Leitereinführung zum unteren Platinenrand** |

Die beiden Module kommen erst nach der Prüfung in Abschnitt 3 dran.

## 3. Prüfung vor dem Einlöten der Module

Die Module sind noch **nicht** eingelötet. Gemessen wird an ihren Lötaugen.

1. 24 V an J1 anlegen (+ links, − rechts).
2. 5-V-Zweig messen: linke XIAO-Reihe, **unterstes Lötauge** (5V) gegen das
   darüber (GND). Erwartet: **4,6–5,0 V**.
3. 3,3-V-Zweig messen: rechte WIZ-Reihe, **zweites und drittes Lötauge von
   oben** (3V3) gegen das oberste (GND). Erwartet: **3,20–3,40 V**.
4. Verpolung probieren: 24 V vertauscht anlegen. Das Netzteil zeigt unter
   1 mA, nichts wird warm. Danach wieder richtig herum anschließen, die Werte
   aus 2 und 3 sind unverändert.

Stimmt ein Wert nicht, lötest du **kein** Modul ein, bevor der Fehler gefunden ist.

## 4. Module einlöten

Beide Module liegen **flach** auf: Der Kunststoffsteg ihrer Stiftleisten sitzt
auf der Trägerplatine.

- **XIAO:** **USB-C nach unten** zur Klemmenseite, wie im Bestückungsdruck
  „USB-C“. Kommt er ohne Stiftleisten: zwei 7-polige Stücke von der
  Stiftleiste 1 × 40 abtrennen, mit dem langen Ende in die Trägerplatine
  stecken, XIAO aufsetzen, erst oben am XIAO löten, dann unten.
- **WIZ850io:** **RJ45 nach oben**, Öffnung zur oberen Platinenkante, wie im
  Bestückungsdruck „RJ45“.

Beide Module passen mechanisch auch verdreht auf die Platine. Verdreht liegen
5 V bzw. 3,3 V an den falschen Pins, und eingelötet lässt sich das kaum noch
korrigieren. Prüf die Lage deshalb **vor dem ersten Lötpunkt** zweimal. Löte
zuerst je einen Eckpin, prüf, ob das Modul flach aufliegt, dann den Rest.

## 5. Gehäuse bearbeiten

1. `bohrschablone.pdf` mit **100 %** drucken. Den Prüfmaßstab nachmessen: 50 mm
   ± 0,5 mm.
2. **Obere Klemmenabdeckung:** links den Teil über der RJ45 nach Schablone 1
   abtrennen, über die ganze Tiefe. Die RJ45 steht dort etwas über das
   Schulterdach, der Stecker kommt von oben durch die Stirnseite.
3. **RP-SMA-Bohrung** 6,5 mm rechts in der oberen Stufe des Gehäuses (zwischen
   oberem Klemmenraum und Front) nach Schablone 2.
4. Einbaubuchse des Antennenkabels (Delock 88383) mit Mutter und Sicherungsring
   befestigen.

## 6. Antenne

Den MHF-I-Stecker des Kabels **senkrecht** auf die U.FL-Buchse des XIAO
drücken, bis er einrastet. Nicht schräg ansetzen, die Buchse ist klein.
Die Stabantenne (Delock 88460) wird direkt auf die RP-SMA-Buchse geschraubt
und zeigt nach oben, neben dem Netzwerkkabel. Sitzt darüber ein Kabelkanal,
legst du sie mit dem Kippgelenk zur Seite.

## 7. Firmware aufspielen (Erstflash)

Der XIAO ist eingelötet; seine USB-C-Buchse zeigt nach unten an die Stufe zum
unteren Klemmenraum. Rechts neben der Klemme ist der Weg frei: Ein gerader
USB-C-Stecker passt, solange die Platine noch nicht im Gehäuse liegt oder die
untere Klemmenabdeckung ab ist.

Das Firmware-Image und die Anleitung zum Aufspielen liegen im Ordner
`firmware/` des Repositories SmartFleet-Gateway.

**Über USB allein hat das WIZ850io keinen Strom.** LAN geht nur mit 24 V an J1.
USB und 24 V gleichzeitig sind erlaubt: D3 verhindert, dass Strom in den
USB-Anschluss des Rechners zurückfließt.

Spätere Updates kommen über das Netz.

## 8. Einbau und Anschluss

1. Platine in die untere Platinenebene des Gehäuses einlegen und an den beiden
   Befestigungsdomen festschrauben (Schraubengröße nach der Anprobe).
2. Deckel aufsetzen, Gehäuse auf die Hutschiene.
3. **24 V** (12–28 V) an die Klemme, **Netzwerkkabel** von oben in die RJ45.
4. Das Einrichtungs-WLAN `SmartFleet-XXXX` erscheint. Weiter mit der
   Einrichtung, siehe Handbuch zum SmartFleet Gateway.

## Prototyp auf dem Steckbrett

Zum Ausprobieren vor der Platine: `steckbrettplan.png` zeigt den kompletten
Aufbau auf einem Breadboard mit 830 Kontakten (63 Spalten, Reihen A–J). Die
Projektdatei `traegerplatine.fzz` enthält dieselbe Ansicht in Fritzing.

- **Schienen:** unten außen GND, unten innen VIN (nach der Verpoldiode), oben
  außen GND; oben innen bleibt frei.
- XIAO (USB-C links) und WIZ850io (RJ45 rechts) überbrücken jeweils den
  Mittelsteg.
- C1 steckt direkt zwischen den beiden unteren Schienen. U2 (MCP1702) sitzt
  mit C3 und C4 in den Spalten 27–30.
- **24 V am einfachsten mit zwei Drahtbrücken zuführen** (+ in Spalte 2,
  − in Spalte 4) statt über die Klemme J1. Ob deren Stifte in die Kontakte
  deines Steckbretts passen, hängt vom Brett ab.

## Stückliste

| Bez. | Anz. | Teil | Wert | Hersteller-Nr. | Bemerkung | Reichelt |
|---|---|---|---|---|---|---|
| J1 | 1 | Leiterplattenklemme 2-polig, Raster 5,08 mm | Höhe 10,1 mm | Degson DG127-5.08-02P-14-00A(H) | Bauhöhe höchstens 10,5 mm (Klemmenraum) – Phoenix MKDS 1,5/2-5,08 ist mit 17,3 mm zu hoch. Ersatz: RIA AKL 101-02 (10 mm) | [DG127-5.08-02P-14-00A(H)](https://www.reichelt.de/de/de/shop/produkt/leiterplattenklemme_2_polig_rm_5_08_mm-276156) · [31101102](https://www.reichelt.de/de/de/shop/produkt/anschlussklemme_2-pol_2_mm_rm_5_08-36605) |
| F1 | 1 | Rückstellende Sicherung (PTC), radial | 0,5 A Halten / 1 A Auslösen, 60 V | Littelfuse RXEF050 | Ersatz: Bourns MF-R050 (0,5 A, 60 V) | [RXEF050](https://www.reichelt.de/de/de/shop/produkt/rueckstellende_sicherungen_1_a-242422) · [MF-R050](https://www.reichelt.de/de/de/shop/produkt/ptc_widerstand_750_mw_770_mohm_60_v-240126) |
| D1 | 1 | Schottky-Diode, DO-41 | 40 V, 1 A | 1N5819 | Verpolschutz – Ring = Kathode. Ersatz: SB140 im DO-41 (nicht DO-15) | [1N5819](https://www.reichelt.de/de/de/shop/produkt/schottkydiode_40_v_1_a_do-41-41850) · [SB140](https://www.reichelt.de/de/de/shop/produkt/schottkydiode_40_v_1_a_do-41-16024) |
| D2 | 1 | TVS-Diode unidirektional, DO-15 | 33 V, 600 W | Littelfuse P6KE33A | Raster 10,16 mm – Ring = Kathode (an VIN). Ersatz: P6KE33A eines anderen Herstellers | [P6KE33A](https://www.reichelt.de/de/de/shop/produkt/tvs-diode_unidirectional_33_v_600_w_do-204ac_do-15-42013) |
| D3 | 1 | Schottky-Diode, DO-41 | 40 V, 1 A | 1N5819 | vor dem 5-V-Pin des XIAO – Ring = Kathode. Ersatz: SB140 im DO-41 | [1N5819](https://www.reichelt.de/de/de/shop/produkt/schottkydiode_40_v_1_a_do-41-41850) · [SB140](https://www.reichelt.de/de/de/shop/produkt/schottkydiode_40_v_1_a_do-41-16024) |
| C1 | 1 | Elko radial, Ø 5 × 11 mm, RM 2,0 | 22 µF, 50 V, 105 °C | Panasonic EEUFR1H220H | stehend – TSR-Datenblatt fordert ab 32 V Eingang 22 µF / 50 V. Ersatz: jeder Elko 22 µF / 50 V, 105 °C, Ø 5 mm, RM 2,0 (z. B. Panasonic FC) | [EEUFR1H220H](https://www.reichelt.de/de/de/shop/produkt/elko_radial_22_f_50v_105_c_low_esr-121288) · [EEUFC1H220H](https://www.reichelt.de/de/de/shop/produkt/elko_radial_22_uf_50_v_105_c_low_esr_aec-q200-84589) |
| C2 | 1 | Elko radial, Ø 5 × 11 mm, RM 2,0 | 47 µF, 16 V, 105 °C | Panasonic EEUFC1C470 | LIEGEND einbauen, Körper nach oben, links neben U1. Ersatz: jeder Elko 47 µF ab 16 V, 105 °C, Ø 5 × 11 mm, RM 2,0 (z. B. Panasonic NHG 47 µF / 25 V) | [EEUFC1C470](https://www.reichelt.de/de/de/shop/produkt/elko_radial_47_uf_16_v_105_c_low_esr_aec-q200-199902) · [ECA1EHG470](https://www.reichelt.de/de/de/shop/produkt/elko_radial_47_f_25_v_105_c_5_x_11_mm_rm_2_0-200353) |
| C3 | 1 | Keramikkondensator bedrahtet, Footprint RM 5,08 | 1 µF, 50 V, X7R | KEMET C315C105K5R5TA | Ausgang U2 – oben rechts unter dem Schulterdach, beliebig herum, höchstens 9,2 mm hoch. C315 hat Raster 2,54: Beinchen auf 5,08 mm aufbiegen. Ersatz: jeder 1 µF ab 25 V, X7R oder X5R (Datenblatt MCP1702: Keramik 1–22 µF). Nicht Z5U/Y5V: verliert bei Wärme mehr als die Hälfte | [C315C105K5R5TA](https://www.reichelt.de/de/de/shop/produkt/vielschicht-kerko_1uf_63v_125_c-393649) · [CK06BX105K](https://www.reichelt.de/de/de/shop/produkt/vielschicht-kerko_1_0_f_50v_125_c-206914) |
| C4 | 1 | Keramikkondensator bedrahtet, Footprint RM 5,08 | 1 µF, 50 V, X7R | KEMET C315C105K5R5TA | Eingang U2 – rechts neben dem WIZ850io, beliebig herum. Beinchen wie bei C3 auf 5,08 mm aufbiegen. Ersatz wie C3 | [C315C105K5R5TA](https://www.reichelt.de/de/de/shop/produkt/vielschicht-kerko_1uf_63v_125_c-393649) · [CK06BX105K](https://www.reichelt.de/de/de/shop/produkt/vielschicht-kerko_1_0_f_50v_125_c-206914) |
| U1 | 1 | DC/DC-Wandler SIP3 | 5 V, 1 A, 6,5–36 V ein | Traco TSR 1-2450 | Ersatz: Traco TSR 1-2450E (7–36 V ein) – passt in denselben Footprint: Pin 1 3,26 mm von der Kante, Pinreihe 5,45 mm von der Rückseite, 10,2 mm hoch (Datenblatt TSR 1E) | [TSR 1-2450](https://www.reichelt.de/de/de/shop/produkt/dc_dc-wandler_tsr-1_1_w_5_v_1000_ma_sil_to-220-116850) · [TSR 1-2450E](https://www.reichelt.de/de/de/shop/produkt/dc_dc_converter_tsr_1e_1_a_7-36_5_0_vdc_sip-3-288648) |
| U2 | 1 | LDO-Regler TO-92 | 3,3 V, 250 mA, bis 13,2 V ein | Microchip MCP1702-3302E/TO | hängt an den 5 V von U1 – sitzt oben rechts neben der RJ45 unter dem Schulterdach – äußere Beinchen auf 2,54 mm aufbiegen. Ersatz: MCP1700-3302E/TO, gleiche Pinfolge im TO-92, Eingang höchstens 6,0 V (reicht für 5 V) | [MCP1702-3302E/TO](https://www.reichelt.de/de/de/shop/produkt/ldo-regler_fest_3_3_v_to-92-90114) |
| M1 | 1 | Seeed Studio XIAO ESP32S3 Plus | 16 MB Flash, 8 MB PSRAM, U.FL | Seeed 102010671 | wird ohne Sockel direkt eingelötet. 102010671 kommt laut Seeed und DigiKey ohne angelötete Stiftleisten – dann 2 × 7 Stifte von der Stiftleiste 1 × 40 einlöten. BerryBase verkauft ihn als „pre-soldered“ (SE-102010671) | [102010671](https://www.reichelt.de/de/de/shop/produkt/xiao_esp32s3_plus_dual-core_wifi_bt5_0-395757) |
| M2 | 1 | WIZnet WIZ850io | W5500, RJ45 mit Übertrager | WIZnet WIZ850io | wird mit seinen Stiftleisten ohne Sockel flach eingelötet. Nicht bei Reichelt – auch im WIZnet-Shop: https://shop.wiznet.eu/en/wiz850io.html | — |
|  | 1 | Stiftleiste 1 × 40, gerade, RM 2,54 | — | Econ Connect SL40G1 | 2 × 7 Stifte für den XIAO, falls er ohne Leisten kommt | [SL40G1](https://www.reichelt.de/de/de/shop/produkt/stiftleiste_1_x_40_polig_gerade_rastermass_2_54_mm-404316) · [SL 1X40G 2,54](https://www.reichelt.de/de/de/shop/produkt/40pol_stiftleiste_gerade_rm_2_54-19506) |
|  | 1 | Hutschienengehäuse 2 TE, Bausatz | 36 × 90 × 58 mm | Camdenboss CNMB/2/KIT | Gehäuse, Deckel, Klemmenabdeckungen (perforiert), Sockel, Hutschienen- und Wandclip | [CNMB/2/KIT](https://www.reichelt.de/de/de/shop/produkt/leergehaeuse_58_x_36_x_90_mm_2_te-133936) |
|  | 1 | Antennenkabel RP-SMA-Einbaubuchse auf MHF I (U.FL-kompatibel) | 35 cm, Gewinde 10 mm | Delock 88383 | Bohrung 6,5 mm rechts in der oberen Stufe (Bohrschablone). RP-SMA, nicht SMA: die Antenne hat einen RP-SMA-Stecker | [88383](https://www.reichelt.de/de/de/shop/produkt/antennenkabel_rp-sma_buchse_mhf_i_stecker_einbau-349327) |
|  | 1 | WLAN-Stabantenne RP-SMA-Stecker mit Kippgelenk | 2,4/5 GHz, 2 dBi @ 2,4 GHz, 143 mm | Delock 88460 | direkt auf die RP-SMA-Buchse in der oberen Stufe, zeigt nach oben; mit dem Kippgelenk zur Seite legen, wenn darüber ein Kabelkanal sitzt. Ohne Kippgelenk: Delock 88394 (89 mm) | [88460](https://www.reichelt.de/de/de/shop/produkt/wlan_antenne_rp-sma-179738) · [88394](https://www.reichelt.de/de/de/shop/produkt/wlan_antenne_rp-sma-179727) |
|  | 1 | Leiterplatte 86,5 × 33 mm, 2 Lagen, 1,6 mm, HASL bleifrei | — | — | Fertiger nach Wahl (z. B. JLCPCB) mit traegerplatine_gerber.zip | — |
|  | 2 | Schraube für die Befestigungsdome des Gehäuses | — | — | Größe nach der Anprobe – Lochdurchmesser auf der Platine 3,2 mm | — |
