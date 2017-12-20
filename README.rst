Eksperimentinė gydytojo/paciento informacinė sistema
####################################################

Iš esmės šis projektas sprendžia https://github.com/Kodas100/pradzia/issues/5.

Projekto tikslai
================

- Išbandyti Kodas100 bendruomenės darbo organizavimo principus sutelkiant
  skirtingų technologijų specialistus darbui prie vieno projekto.

- Pademonstruoti, kaip galėtų būti kuriami valstybiniai projektai, naudojant
  atviro kodo principus.

- Praktiškai išbandyti visas e-sveikatos infrastruktūros grandis kuriant naują
  sistemą, tokiu būdu geriau suprantant jos silpnąsias vietas.

- Išsiaiškinti, kaip maksimaliai optimizuoti naudotojo aplinką pasirinktoms
  naudotojų grupės, išsiaiškint jų darbo su sistema specifiką. 

- Padaryti veikiantį gydytojo/paciento informacinės sistemos prototipą
  integruota su ESPBI IS.

- Jei padarytas prototipas pasiteisintų, tada padaryti lengvai diegiamą atviro
  kodo sistemą, kurią galėtų nemokamai įsitiegti visos įstaigos, taip pat
  mažoms įstaigos turėtų būti sudaryta SaaS principu veikiančios sistemos
  prijungimo galimybė.


Darbų etapai
============

Pirmas etapas: partnerių paieška
--------------------------------

- Surasti gydymo įstaigą, kuri sutiktų bendradarbiauti aiškinantis ko
  konkrečiai reikia pasirinktai gydytojo darbo vietai ir sutiktu išbandyti
  sukurtą prototipą.

- Susitarti su Registrų Centru dėl prieigos prie testinės ESPBI IS aplinkos.

- Išsiaiškinti apie galimybę prisijungti prie produkcinės aplinkos, tuo atveju,
  jei pavyktų sukurti veikiantį variantą.

Antras etapas: situacijos analizė
---------------------------------

- Išbandyti komunikaciją su ESPBI IS, padarant elementarias užklausas.

- Su gydymo įstaiga, kuri sutinka bendradarbiauti išsiaiškinti, kokias
  naudotojų roles norime dengti ir kokio funkcionalumo reikia pasirinktoms
  naudotojų rolėms.

- Peržiūrėti esamus atviro kodo sprendimus ir išsiaiškinti ar galima juos
  panaudoti.

Trečias etapas: darbo principai, priemonės ir architektūra
----------------------------------------------------------

- Apsispręsti, kaip tiksliai atskiri projekto komponentai, galimai įgyvendinti
  naudojant skirtingas technologijas, komunikuos tarpusavyje.

- Pasirinkti esminius darbo įrankius, tokius kaip API aprašymo karkasas,
  komunikacijos protokolas, priemonės komponentų apjungimui ir pan.

- Pasirinkti projektų valdymo metodologiją ir susitarti dėl esminių darbų
  valdymo procesų ir įrankių.

Ketvirtas etapas: įgyvendinimas
-------------------------------

- Pasiskirstyti į komandas ir imtis darbų.

- Glaudžiai bendradarbiauti su pasirinktomis gydymo įstaigomis ir pacientais,
  kurie naudos sistemą. Kiekviena sistemos funkcija turėtų būti aptarta
  dalyvaujant gydymo įstaigos atstovams, pacientams, dizaineriams, UX
  sprecialistams, programuotojams ir kitų susijusių sričių atstovams.

- Veikianti sistemos versija turėtų būti nuolat prieinama ir atnaujinama vos
  tik padarius naują funkciją.

- Kai tik sistemoje atsiranda nauja funkcija, ji turėtų būti testuojama
  gydytojų ir pacientų, kurie pateiktų atsiliepimus kas veikia, o kas neveikia.


Naudojamos technologijos
========================

Šis projektas yra neutralus technologijoms, tai reiškia, kad nepriklausomai nuo
to, kokia programavimo kalba programuoji, gali jungtis prie projekto.

Kadangi Kodas100 bendruomenė turi daug narių, kurie dirban su skirtingomis
technologijomis, susiskaldymas žymiai sumažintų žmonių skaičių, kurie dirba
prie projekto. Todėl vienas iš būdų tai išspręsti yra mikroservisų architektų,
kur atskiri sistemos komponentai gali būti daromi su bet kuria pasirinkta
technologija.

Toks architektūrinis pasirinkimas šiek tiek apsunkina darba, tačiau leidžia
didesniam ratui žmonių dirbti prie vieno projekto, kas turėtų atpirkti darbo su
mikroservisais sunkumus.

Darbo principas būtų toks:

- Apsikeitimas duomenimis vyktų per ESPBI ir pasirinktą duomenų bazės
  technologiją.

- Darbui su duomenų baze būtų naudojama vieninga duomenų schema, kurią naudotų
  visi komponentai.

- Vietos, kur būti atliekamas rašymas į duomenų bazę turėtų būti
  konkrolioujamos atskirų komponentų. Du skirtingi komponentai neturėtų rašyti
  į tas pačias duomenų bazės lenteles ar bent jau neturėtų mutuoti vienos
  srities loginių objektų. Kiti komponentai, kurie norėtų atlikti rašymo į
  duomenų bazę veiksmus, turėtų tai daryti per dedikuotus API.

- Skaitymą iš duomenų bazęs arba ESPBI visi komponentai galėtų daryti
  tiesiogiai, be tarpinikų. Arba per tarpinius komponentus, jei taip patogiau.

- Autorizacijai turėtų būti naudojamas SSO principas, kad naudotojų sesija
  vieningai veiktų tarp skirtingų komponentų.

- Naudotojo sąsajos gali būti daromos taip pat naudojant skirtingas
  technologijas, kur tai yra praktiška. Pavyzdžiui mobiliems įrenginimas, gali
  būti visiškai skirtingi ir nepriklausomi projektai, naudojantys bendrus API
  sudarytus iš migroservisų.

  Skirtingų naudotojų rolių naudotojo sąsajos, taip pat gali būti daromi, kaip
  atskiri projektai, naudojant pasirinktinas frontend technologijas.

- Tarp skirtingų frontend komponentų turėtų būti naudojamas vieningas stilių
  karkasas, kad atskirtų frontend dalių išvaizda atrodytų vienodai.

- Jei komanda dirbanti prie tam tikro komponento yra neproduktyvi, jos darbą
  galėtų perimti kita komanda, net gi dirbanti su visiškai kita technologija,
  tiesiog perdarydama komponento funkcionalumą naujai ir atsisakant senojo
  komponento, kuris nebėra vystomas.

Vadovaujantis tokiais principais, manau įmanoma organizuoti darbus taip, kad
prie projekto galėtų dirbti žmonės naudojantys skirtingas technologijas.


Klausimai/atsakymai
===================

**Yra sukurta bent 5 tokios sistemos, kam reikia dar vienos?**

Visos esamos sistemos yra uždaro kodo. Todėl tokiai visuomeninei iniciatyvai,
kaip Kodas100 nėra galimybės prisidėti prie sistemos tobulinimo ar klaidų
taisymo.


**Kas apsiims sistemos palaikymu?**

Kadangi Senu sistema yra atviro kodo, teikti palaikyma gali, bet kas, nėra
pririšimo prie vieno tiekėjo.

Kadangi Sanu sistema kuriama mikroservisų principu, kur gali būti naudojamos
kelios skirtingos technologijos, palaikymas tampa šiek tiek sudėtingesnis.
Reikia kelių palaikymo paslaugas teikiančių tiekėjų, vienas būgų atsakingas už
serverių ir bendrai sistemos veikimo priežiūrą ir papildomai, kiekvienai
technologijai, reikėtų atskiro tiekėjo, kuris dirba su ta technologija.
