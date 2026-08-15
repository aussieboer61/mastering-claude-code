# Claude Code'i meisterlik valdamine

## Praktiline juhend uudishimulikele

*Sõbralt sõbrale kirjutatud juhend, kuidas Claude Code'ist rohkem kätte saada, kui karbist välja võttes tuleb.*

> **Mida sa loed.** See on kirjalik juhend tabelite, jooniste ja päris lõpus ühe väikese boonusviibaga, mis pole mõeldud sinule — see on mõeldud tehisintellektile, kuhu sa selle kleepida saad. Samast juhendist on olemas ka jutustatud versioon (samad sõnad, vähem tabeleid), kui eelistad lugemisele kuulamist.
>
> **Miks see olemas on.** Enamik inimesi, kes Claude Code'ist kuulevad, kleebivad sinna ühe küsimuse, saavad vastuse ja lähevad edasi. See töötab, aga jätab üheksa kümnendikku tööriistast riiulile. See juhend on selle hetke jaoks, kui otsustad ülejäänu kätte võtta.
>
> **Jagamine.** Anna see edasi. Kogu mõte ongi selles, et see oleks vähem salaklubi ja rohkem ühine tööriistakast.

---

## Kuidas seda lugeda

Juhend on neljas osas.

**1. osa: Alustamine** eeldab, et oled kuulnud nime „Claude Code" ja mitte palju rohkemat. See selgitab, mis tööriist see tegelikult on, mida sul vaja läheb, ja käib sinuga koos läbi esimese seansi, et ülejäänud juhendil oleks, kuhu maanduda.

**2. osa: Alustalad** on juhendi süda. Viis peatükki viie asja kohta, mille sa ehitad üks kord ja kasutad siis igal seansil igavesti: seisev kiri sinu abilisele (CLAUDE.md), pikaajaline teadmiste salv (mälu), ühe käsuga käivitatavad protseduurid (oskused), reeglid, millest su abiline ei saa üle hüpata (haagid), ja töö delegeerimine spetsialistidele (alamagendid). Iga peatükk on iseseisev — loe mis tahes järjekorras.

**3. osa: Kompositsioon** on neli peatükki alustalade kombineerimisest päris töövoogudeks: olek õiges ulatuses, töö, mis käib sel ajal, kui sa magad, teise arvamuse automaatne hankimine ja tööriistade hea valimine. Need toetuvad alustaladele ja viitavad neile vabalt tagasi.

**4. osa: Kõik kokku pandud** käib läbi ühe inimese seadistuse kõigi üheksa samba lõikes, pakub välja kasutuselevõtu järjekorra ja ütleb, millal *ei tasu* vaeva näha.

**Lisa** päris lõpus on tekstiplokk tehisintellektile, mitte sinule. See on kopeeri-ja-kleebi viip, mille saad visata värskesse Claude'i seanssi, et abiline selle juhendiga kurssi viia. Jäta see tähelepanuta, kui sa seda ei taha.

| Osa | Peatükid | Mida sa saad |
|------|----------|------------------|
| 1. Alustamine | 0 | Piisavalt tausta, et ülejäänule järele jõuda |
| 2. Alustalad | 1–5 | Päris seadistuse viis ehitusklotsi |
| 3. Kompositsioon | 6–9 | Kuidas neid kasulikeks töövoogudeks kombineerida |
| 4. Kõik kokku pandud | — | Läbikäidud näide, kasutuselevõtu järjekord, hoiatused |

---

# 1. osa — Alustamine

## 0. peatükk — Mis Claude Code tegelikult on

Claude Code on programm, mida sa käivitad oma terminalis ja mis räägib Claude'iga (tehisintellektiga). See on pealkiri. Huvitavaks teevad selle üksikasjad.

Kui kasutad Claude'i veebibrauseri kaudu, saad vestlusakna: sina kirjutad, Claude vastab, sina kirjutad uuesti. Kui kasutad Claude Code'i, saad sama vestluse pluss võimaluse, et Claude **loeb sinu arvutis olevaid faile, käivitab käske, muudab faile ja jätab asju seansside vahel meelde** — eeldusel, et sa need asjad seadistad. See on vahe, kas küsid sõbralt telefonitsi nõu või annad talle oma köögi võtmed.

### Miks üldse brauserist kaugemale minna

Enamik inimesi, kes proovivad Claude'i brauseris, jooksevad sama seina vastu: iga vestlus algab nullist. Pead oma projekti uuesti selgitama, oma eelistused uuesti välja ütlema, samad failid uuesti kleepima. Kolmandaks-neljandaks vestluseks loobud kõigest keerulisemast ja kasutad seda ainult ühekordsete küsimuste jaoks.

Claude Code laseb sul ehitada töökeskkonna, mis **mäletab**, **jõustab reegleid** ja **teeb tööd sel ajal, kui sa klaviatuuri taga ei ole**. Iga tüki seadistamiseks vajalik panus on väike. Tasu on see, et viies vestlus ei alga samast kohast kui esimene — see algab sealt, kus sa pooleli jäid, teades, mille sa juba paika oled pannud.

### Mõned sõnad, mida näed läbivalt

| Sõna | Mida see lihtsas keeles tähendab |
|------|--------------------------------|
| **Seanss** | Üks Claude Code'i käivitus sinu terminalis, avamisest sulgemiseni. Nagu üks telefonikõne. |
| **Viip** | Sõnum, mille sa Claude'ile kirjutad. Sama mis brauseris. |
| **Kontekst** | Kõik, mida Claude praegu näeb — sinu viibad, tema vastused, kõik, mida ta seni lugenud on. Piiratud mahuga mustandileht. |
| **Tööriist** | Konkreetne tegevus, mida Claude saab teha, näiteks „loe seda faili" või „käivita see käsk". |
| **Agent** (ka „alamagent") | Teine Claude'i koopia, kellele saad ülesande üle anda, külmalt briifituna, samal ajal kui su põhiseanss tegeleb edasi muude asjadega. |
| **Mälu** | Kaust väikeseid tekstifaile, mida Claude loeb iga seansi alguses, et vestluste vahel olulist meeles pidada. |
| **Oskus** | Nimega protseduur, mille oled ühe korra kirja pannud ja mille Claude saab nõudmisel käivitada, kui kirjutad `/sinu-oskus`. |
| **Haak** | Väike skript, mis käivitub automaatselt teatud hetkedel — näiteks enne mis tahes faili kirjutamist —, et reeglit jõustada. |
| **CLAUDE.md** | Lihttekstifail sinu projekti juurkaustas, mida Claude loeb iga seansi alguses. Nagu seisev kiri. |

Kui viimased neist veel selged pole, ära muretse — igaühel neist on oma peatükk. Tabel on siin selleks, et saaksid selle juurde tagasi tulla.

### Mida sul vaja läheb

- Arvuti, kus töötab macOS, Linux või Windows (WSL-i kaudu).
- Terminal — see must-tekst-ekraanil aken. Piisab, kui tunned end selles mugavalt tasemel „oskan kausta vahetada ja käsu käivitada".
- Claude'i konto. Pro pakett (20 $ kuus) on tavaline alguspunkt; soovi korral võid maksta ka kasutuspõhiselt Anthropicu API kaudu.
- Umbes pool tundi, et paigaldada ja esimene seanss läbi teha.

### Sinu esimene seanss, samm-sammult

Ametlik paigaldusjuhend asub Claude Code'i dokumentatsioonis; see muutub aeg-ajalt, nii et ma ei ürita seda siin peegeldada. Kui paigaldus on tehtud, näeb esimene seanss välja selline.

Avad oma terminali, liigud kausta, mis sulle korda läheb — ütleme, et see on kaust, kus on märkmed, mida oled ühe kõrvalprojekti jaoks teinud — ja kirjutad `claude`. Ilmub viip. Kirjutad:

> *Mis selles kaustas on?*

Claude loeb kausta ja ütleb sulle, mida ta leidis. Kirjutad:

> *Ava `ideas.md` ja tee kokkuvõte kolmest kõige värskemast sissekandest.*

Claude avab faili, loeb selle läbi ja teeb kokkuvõtte. Seni teeb seda ka brauser.

Nüüd tuleb erinevus. Kirjutad:

> *Salvesta mu eelistused: tahan lühikesi vastuseid, ilma sissejuhatuseta, ja loetelupunkte ainult siis, kui need päriselt aitavad.*

Claude'il vaikimisi sellist võimalust ei ole — aga kui mälusalv on seadistatud (2. peatükk), saab ta selle väikesesse faili kirjutada ja seda iga tulevase seansi alguses lugeda. Sellest hetkest peale teab iga vestlus seda sinu kohta. Sa lõpetad selle ütlemise.

See ongi kogu juhendi rütm: iga sammas paneb ühe tüki „ma pean seda iga kord ütlema" ära kaduma.

---

# 2. osa — Alustalad

Need viis peatükki on ehituskivid. Loe neid mis tahes järjekorras. Vali see, mis vastab sinu praegusele frustratsioonile.

---

## 1. peatükk — CLAUDE.md: seisev kiri sinu abilisele

### Idee

Kui avad Claude Code'i mõnes kaustas, otsib see faili nimega `CLAUDE.md` ja loeb selle kõigepealt läbi — iga kord, ükskõik mida sa kavatsed küsida. Mõtle sellest kui üheleheküljelisest kirjast, mille oled abilisele lauale jätnud: *siin on see, mis see koht on, siin on maja reeglid, siin on see, kus asjad asuvad*. Abilisele ei pea seda kõike uuesti rääkima; see on juba laual, kui ta sisse astub.

### Miks vaeva näha

Ilma selleta algab iga seanss sinu projektis nullist. Sa seletad uuesti kaustade paigutust, kordad kokkuleppeid, mainid taas asja-mida-ei-tohi-puutuda. Nädala kolmanda ümberseletamise poole peal saad aru, et oled sama tööruumi ikka ja jälle kirjeldanud ja abiline ei tunne seda endiselt.

Sellega saabub abiline juba orienteerununa. Iga seansi esimene minut — taassisseelamise minut — kaob ära. Korrutatuna aasta jagu seanssidega on see päris aeg.

### Kus fail asub

Ulatusi on kaks ja võid kasutada mõlemat:

```
~/.claude/CLAUDE.md              ← kasutajaülene; kehtib igas seansis kõikjal
your-project/CLAUDE.md           ← ainult projekt; kehtib, kui avad selle kausta
```

Kasutajaülene fail on asjade jaoks, mis kehtivad *sinu* kohta projektist sõltumata: kuidas sulle meeldib, et sinuga räägitakse, sinu eelistatud failivormingud, iga reegel, mis peaks kehtima kõikjal. Projektifail on selle projekti eripärade jaoks: paigutus, sõnastik, lõksud.

Projekti avades laaditakse mõlemad failid koos. Projektifail täiendab kasutajafaili; ta ei kirjuta seda vaikimisi üle.

### Mis teenib faili koha välja

| Kuulub CLAUDE.md-sse | Ei kuulu |
|---------------------|----------|
| Kaherealine kirjeldus, mis see projekt on | Iga kausta täielik kirjeldus |
| Need kolm-neli käsku, mida sa päriselt käivitad | Iga käsk, mida keegi üldse võiks käivitada |
| Maja kokkulepped (nimetamine, failide korraldus) | Asjad, mida kood ise hästi seletab |
| Valdkonna sõnastik — terminid, millel on siin kindel tähendus | Valdkonna õpik |
| Mõned lõksud, mis on varem hammustanud | Iga mõeldav lõks |
| Viidad ülejäänud seadistusele („Mälu asub…") | Nende teiste kohtade täielik sisu |

Distsipliin seisneb **pikkuses**. Iga sõna CLAUDE.md-s maksab sulle igas seansis kontekstieelarvet, olenemata sellest, kas tänane ülesanne seda sõna vajab või mitte. Sihi viiekümne kuni saja viiekümne rea peale. Kui oled üle kahesaja, hakka kärpima.

### Algne mall

```markdown
# Projekt: [Nimi]

## Mis see on
[Üks-kaks lauset. Miks see kaust olemas on.]

## Kus asjad asuvad
- `src/` — põhikood
- `docs/` — kirjalik materjal
- `data/` — andmestikud

## Käsud, mida ma päriselt käivitan
- Ehitamine: `make build`
- Testimine: `pytest tests/`
- Juurutamine: vaata oskust `/deploy`

## Lõksud
- Lavastusserver töötab teise andmebaasi peal kui toodang.
  Kontrolli alati, kummaga sa räägid.

## Viidad
- Mälu: `~/.claude/projects/this-project/memory/MEMORY.md`
- Oskused: `.claude/skills/`
```

Kümme või kakskümmend rida on täiesti hea algsuurus. Kasvata seda nii, et märkad asju, mida sa aina uuesti seletad, ja lisad need ükshaaval.

### Käitumuslikud vaikeväärtused, mida tasub seada

Ülaltoodud mall räägib *faktidest* — mis projekt on, kus asjad asuvad. Teine asi, millega CLAUDE.md, eriti kasutajaülene, oma koha välja teenib, on **käitumuslikud vaikeväärtused**: lühike nimekiri püsijuhistest selle kohta, *kuidas* sa tahad, et abiline tegutseks. Need loevad rohkem kui ükski üksik projektifakt, sest need kujundavad iga ülesannet, mitte ainult ühte.

Käputäis, mille seadmine on end tõestanud:

| Vaikeväärtus | Mida see ütleb |
|---------|--------------|
| **Tegutse, kui oled volitatud** | Lahenda probleem ja vii asi lõpuni. Küsi enne ainult siis, kui samm on raskesti tagasipööratav, päriselt otsustamata või puudutab jagatud taristut. |
| **Püsi oma rajal** | Tee see, mida paluti. Kõrvaltähelepanek ei ole uus ülesanne — tunnista seda ühe lausega; ära hakka seda ehitama. |
| **Otsi enne küsimist** | Enne kui midagi küsid, otsi see kõigepealt üles — mälust, failidest, kohast, kus see juba oleks. Ära pane mind uuesti andma seda, mis on kettal olemas. |
| **Kalibreeri kindlust** | Märgi ära see, mida sa pole kontrollinud. Too risk kohe alguses välja. Ära murdu hetkel, kui ma vastu vaidlen, kui sul on õigus. |
| **Alusta vastusest** | Kui ma esitan otsese küsimuse — jah/ei, kes kellele võlgneb, kui palju — pane vastus esimesse lausesse ja alles siis toetav lahtikirjutus. Õige tabel, millest ma pean vastuse ise välja lugema, ei ole küsimusele vastanud. |
| **Tõendid enne „valmis"** | Ära teata, et asi on parandatud, enne kui oled kontrollinud, et sümptom on päriselt kadunud — ja ütle, mida sa kontrollisid. |
| **Arutelurežiim versus täitmisrežiim** | Kui vestlus on hinnanud mingit lähenemist, võib käskiv „käivita migratsioon" tähendada „testi seda" — mitte „löö nüüd otse toodangusse". Loe eelnevat konteksti; kui see on mitmeti mõistetav, üks lühike kinnitus enne kirjutamist, mida ei saa kergesti tagasi võtta. |
| **Seansi reeglid jäävad siduvaks** | Seansi alguses öeldud meetodijuhis või liigitus on seansiülene reegel, mitte ühekordne vastus. Ära triivi seansi pikenedes tagasi vaikimisi heuristikute juurde — vaata varasemad käigud üle, enne kui rakendad vaikeväärtusi mõnele uuele sama mustri juhtumile. |
| **Usalda operaatorit füüsiliste faktide osas** | Kui tööriista väljund (MAC-tabelid, andurite loendurid, registrilugemid) näib olevat vastuolus sellega, mida kasutaja oma füüsilise keskkonna kohta ütleb, esita üks täpsustav küsimus — ära väida, et kasutaja eksib. Kaugandmetel on kontekst, mida teab ainult kohapeal olev inimene. |
| **Üks näidis ei ole kogum** | Enne kui iseloomustad rühma — „neil kõigil on X", „ükski neist ei vaja Y-t" — kontrolli rohkem kui ühte. Üks juhuslikult korras olev ese muutub kindlaks väiteks seitsmeteistkümne kohta ja vale väide õigustab siis vale tegevust. |
| **Kontrolli tulemuste mõistlikkust teadaoleva konteksti taustal** | Enne kui teatad mõõtmistulemuse leiuna, kõrvuta seda juba teadaolevaga — geograafia, hosti seisund, kellaaeg. Ebausutav arv (kohtvõrgu tasemel latentsus teisel mandril asuva serverini) on märk, et tuleb uurida, mitte tulemus, mida raporteerida. |
| **Küsi kõigepealt, miks põhitee ei tööta** | Kui töö käib varulahenduse peal — varuühendus, teisene tööriist, ajutine seadistus — selgita enne varulahenduse ümber ehitamist välja, *miks* kavandatud tee kasutusel ei ole. Põhjus muudab enamasti kogu vastust; üks küsimus alguses on parem kui sümptomi ümber ehitatud tellingud. |
| **Sihtmärk on see, mis tuleb kätte anda** | Kui töö tehakse *konkreetse* seadme või pinna *jaoks*, tähendab „valmis" seda, et see töötab seal. Asendus — „see töötab brauseris", „siin on sama asi veebilehena" — on äärmisel juhul ajutine abivahend, kuni päris sihtmärki parandatakse, mitte kunagi kättetoimetatud vastus, kui kasutaja just ise selgesõnaliselt allahindlust ei aktsepteeri. |
| **Vii viil lõpuni** | Kui plaan on kokku lepitud ja tööd on veel, tööta lõpuni — ära lõpeta iga sammu küsimusega „kas jätkan?". Ja tavaline järgmine samm, mille võtmed abilisel juba käes on — DNS-kirje, sertifikaat, teenuse registreerimine — on osa tööst, mitte valikuline lisa, mida tagasi pakkuda. Toimeta kohale kogu vertikaalne viil, mitte kaheksakümmend protsenti, mis jätab kasutaja viimast miili ise ühendama. |
| **Küsimus on juhisest tähtsam** | Kui üks sõnum sisaldab nii juhist kui ka küsimust, vasta kõigepealt küsimusele — see on see osa, mis blokeerib kasutaja järgmist mõtet. Alusta juhise täitmist taustatööna ja teata, kui see valmis saab; ära pane inimest delegeeritud ülesande taha järjekorda. |
| **Kinnitatud otsus on värskest tuletusest tähtsam** | Kui seadel on juba väärtus, mille kasutaja valis, ei ole selle muutmine kaalutlusotsus — arutluskäik, mis selle andis, pole seadistusest näha, nii et „see tundub meie olukorra jaoks vale" ei ole tõend, et see seda on. Kontrolli enne väärtuse muutmist, kas on olemas varasem otsus, ja kui leiad selle, jääb see kehtima, kuni kasutaja seda liigutab. Ümbertuletuse hilisem kaitsmine maksab rohkem kui algne muudatus. |
| **Lõpeta mõõdetud tulemusega** | Kui teatad mõõdetud tulemuse — arvu, testitulemuse, loenduse — lõpeb raport sellega. Ära pehmenda seda millegi realiseerimatuga: pooleli oleva tehingu, paranduse, mis võib-olla saabub, kasu, mida veel tõendatud pole. Kasutaja küsis arvu, sest arv on see, mille põhjal ta saab tegutseda, ja lohutuslõik ühtaegu vihjab, et tulemus on vähem tõeline, kui ta on, ja palub tal käsu peale lootusrikas olla. Kui ta tahab, et kasu läbi modelleeritaks, küsib ta ise. |
| **Nimeta hulk enne hulgimuudatust** | Enne kui käivitad midagi, mis muudab hulka asju, millele kasutaja juba toetub — failide taasgenereerimine, dokumentide ümbertöötlemine, kirjete ümberkirjutamine — ütle täpne nimekiri ühe reaga ja tegutse ainult selle nimekirjaga. „Paranda katkised" on kirjeldus, mitte hulk; selle helde tõlgendamine on see, kuidas kolmest asjast saab kolmkümmend. Hind on ebasümmeetriline: hulga nimetamine maksab ühe lause, aga see, et kasutaja avastab ülejäänud kakskümmend seitse, maksab tema usalduse iga hulgitoimingu vastu, mida sa edaspidi teed. |
| **Olekuteates mainitud ulatus ei ole nõusolek** | Heakskiit kinnitub sellele nimisõnale, millele kasutaja tegelikult jah ütles. Laiema mõjuraadiuse möödaminnes kirjeldamine — edenemisest raporteerides või ühe reana plaanis — ei anna selleks luba, ega anna seda ka kasutaja vaikimine selle rea kohta. Kõige hävitava puhul nimeta konkreetne asi ja saa jaatav vastus *selle asja* kohta. |

Kaks märkust. Need on *vaikeväärtused*, mitte raudsed reeglid — abiline võib neist põhjendatult kõrvale kalduda; need seavad puhkeoleku käitumise. Ja järgmise peatüki distsipliin kehtib ka siin: hoia hulk väike ja sõnasta iga reegel selle kaudu, mida *teha*. Kuhi „ära kunagi tee X" vaikeväärtusi annab abilise, kes küsib luba hingamiseks. Kui sinu püsijuhised on triivinud „küsi enne kõike" suunas, on see triiv viga, mitte turvavõrk.

### Mis siia *ei* kuulu

**Saladused.** See fail on lihttekst kettal, peaaegu kindlasti mingil hetkel versioonihaldusse pandud. API-võtmed, paroolid, tokenid — ükski neist ei lähe CLAUDE.md-sse. Nende koht on paroolihalduris või keskkonnamuutujas.

**Praeguse ülesande olek.** „Oleme seitsmest sammust kolmandal" kehtib täna ja on homme aegunud. See on plaani olek (6. peatükk), mitte püsijuhis.

**Ranged reeglid, mida ei tohi kunagi rikkuda.** Kui reegli eiramise tagajärg on päris — rikutud fail, kustutatud andmestik, lekkinud mandaat — kuulub see reegel haaki (4. peatükk), mitte teksti, mida abiline *peaks* lugema, aga võib vahele jätta, kui tema tähelepanu on mujal.

### Tõrkemustrid

**5000-sõnaline fail.** See algas kahekümne reaga ja kasvas aastaga teatmikuks. Nüüd laaditakse see igal seansil, see sööb konteksti ja abiline on õppinud seda diagonaalis lugema, sest seda on liiga palju. Kärbi kord kvartalis. Vii stabiilne teadmine mällu; vii protseduurid oskustesse; vii jõustamine haakidesse.

**Kasutajaülese ja projektispetsiifilise segamine.** Sinu suhtluseelistused satuvad ühe projekti faili, sest just seal sa juhtusid neid kirjutama. Kuus kuud hiljem oled teises projektis ja abiline ei tea neid. Pane projektiülene sisu kasutajaülesesse faili. Pane projekti sisu projektifaili.

**Selle kirjutamine nagu README.** README on projektiga alles tutvuvate inimeste jaoks — see seletab, motiveerib, juhatab läbi paigalduse. CLAUDE.md on abilise jaoks — napp, käskiv, keskendunud sellele, mida on vaja õigesti käitumiseks. Nende segiajamine annab faili, mis ei tee kumbagi tööd hästi.

**Ise hinnatud kontrollnimekiri, mille järgi mittemidagitegemine loeb reeglite täitmiseks.** Kui iga käigu lõpetav olekukontrollnimekiri (tehtud / tegemata / edasi lükatud) on üks sinu püsireegleid, vajab „edasi lükatud" kitsast määratlust, muidu muutub see tagauksest — käik, mis nimetab paranduse ja lükkab selle siis ikkagi edasi, loeb endiselt reeglitele vastavaks, sest edasilükkamine on formaalselt kehtiv lõppolek. Üks viiepäevane jooks lõpetas silumiskäigu tekstiga „parandused: ühtki ei rakendatud, tahtlikult", ennustades samas, et täpselt sama viga kordub — see korduski, veel kaheksa tundi, enne kui kasutaja pidi nõudma parandust, mis oli samas sõnumis juba kirja pandud. Selle leiu taga olnud audit mõõtis ka laiemat kallet: reeglistik sisaldas umbes neliteist „ära kunagi tee X" keeldu iga ühe „tee alati X" kohta — ja reeglit, mida saab rikkuda ainult tegutsedes, täidab mittemidagitegemine, nii et nii tugevalt keeldude poole kaldu reeglistik premeerib paigalseisu. Määratle „edasi lükatud" kui millegi poolt blokeeritu, mis on väljaspool abilise kontrolli — puuduv mandaat, otsus, mida saab teha ainult kasutaja — mitte kunagi kui „leidsin paranduse ja küsin ikkagi". Jälgi ka oma vaikeväärtuste suhet: kui „ära kunagi" ületab „alati" rohkem kui mõnekordselt, on hulk optimeeritud tegevusetuse, mitte õigsuse jaoks.

### Millal kasutada seda ja millal teisi alustalasid

| Kui asi on… | Pane see… |
|------------------|------------|
| Alati asjakohane kontekst, mida abiline peaks saabudes teadma | CLAUDE.md-sse |
| Teadmine, mis koguneb ja mida tuleks teema järgi üles leida | Mällu (2. peatükk) |
| Protseduur, mida käivitad vajaduse korral | Oskusesse (3. peatükk) |
| Reegel, mis peab kehtima olenemata sellest, mida mudel otsustab | Haaki (4. peatükk) |

---

## 2. peatükk — Mälu: teadmine, mis elab seansi üle

### Idee

Mälu on kaust väikeseid tekstifaile, mida Claude loeb iga seansi alguses. Erinevalt CLAUDE.md-st (mis laaditakse iga kord täies mahus) on mälu *indekseeritud* — Claude loeb indeksit ja avab siis ainult tänase ülesande jaoks asjakohased failid. See on vahe, kas jätta lauale üheleheküljeline kiri või anda abilisele ligipääs kartoteegikapile, mille sildistatud sahtleid ta saab avada.

### Miks vaeva näha

CLAUDE.md on kavandatult lühike. Mälu on koht, kus elab suurem osa sinu „mida ma muidu peaksin uuesti seletama" varust — sinu eelistused, varasematest vigadest õpitu, mandaatide asukoht, mõne tarnija API veidrused, iga aktiivse projekti juba tehtud otsused.

Mälusalv, mis esimesel nädalal alustas väikesena, tundub kuuendaks kuuks asendamatu. Kuhjumine on päris: iga seanss lisab tillukese jao kogunenud teadmist, millest kõik tulevased seansid saavad ammutada.

### Nelja liiki mälu

Liike on täpselt neli ja see eristus on oluline, sest iga liik käitub vananedes erinevalt.

| Liik | Mis siia läheb | Näide |
|------|----------------|---------|
| **user** | Kes sa oled ja kuidas sulle meeldib töötada | „Tahan lühidaid vastuseid ja täpploendeid ainult siis, kui need aitavad." |
| **feedback** | Veast õpitud õppetund — mis läks valesti ja milline reegel järgmine kord rakendada | „Kui palun kokkuvõtet, ära lisa jaotist „järgmised sammud", kui ma pole seda küsinud." |
| **project** | Kus käimasoleva töö failid asuvad, juba tehtud otsused, kasutusel olevad lõimingud | „Köögiremont on sisustusfaasis; kapid saabuvad reedel; ülevaataja vajab 48 h etteteatamist." |
| **reference** | Püsivad välised faktid, mida sa muidu peaksid otsima | „Tarnija X hinnapakkumise otspunkt on /api/v3/quotes, mitte /quotes." |

Kaks liiki, mida kõige rohkem kasutad, on **feedback** ja **project**. Tagasiside kuhjub — iga viga, mille sa viitsid kirja panna, on ärahoitud tagasilangus igas tulevases seansis. Projektifailid on koht, kus istub jooksev kontekst „kus ma köögiremondi / raamatu mustandi / konsultatsioonitööga olen".

### Kuidas see on korraldatud

Salv asub aadressil `~/.claude/projects/<some-slug>/memory/`. Selle kausta sees:

```
memory/
├── MEMORY.md              ← indeks (üks rida faili kohta)
├── me.md                  ← kasutajafail
├── feedback_concise.md    ← tagasisidefail
├── reno_kitchen.md        ← projektifail
└── vendor_x_api.md        ← viitefail
```

`MEMORY.md` on tabel. Iga rida on üks fail: lühikirjeldus, teemaviited, link. Claude loeb kõigepealt seda indeksit ja otsustab teemaviidete põhjal, millised teised failid avada.

```markdown
| Fail | Kirjeldus | Sildid |
|------|-------------|------|
| me.md | Kes ma olen, väljundieelistused | #user #prefs |
| feedback_concise.md | Ära lisa küsimata jaotisi „järgmised sammud" | #feedback #style |
| reno_kitchen.md | Köögiremont — faaside jälgija, tarnijad, kuupäevad | #project #renovation |
| vendor_x_api.md | Tarnija X hinnapakkumise otspunkti veidrused | #reference #api |
```

Igal failil on ülaosas lühike päis (nn frontmatter) ja seejärel sisu:

```markdown
---
name: Kitchen Renovation
type: project
tags: [renovation, kitchen]
---

# Köögiremont

Faas: sisustus (algas E 12. mail)
Kapid: tellitud, tarne R 23. mail
Ülevaataja: iga muudatuse puhul nõutav 48 tundi etteteatamist.
…
```

### Kuidas alustada

Sul pole esimesel päeval kõiki nelja liiki vaja. Õige järjekord on:

1. **Üks `user`-fail.** Nimeta see `me.md`. Pane sinna: kes sa oled ühe-kahe lausega, sinu eelistatud väljundistiil, iga reegel, mis kehtib kõiges, mida teed. Viis kuni kümme rida on küllalt.
2. **Üks `project`-fail** selle jaoks, mis on kõige aktiivsem. Kus asjad asuvad, millised otsused on paigas, mis on lahtine. Kümme kuni kakskümmend rida.
3. **`feedback`-fail esimesel korral, kui abiline teeb midagi, mida sa tahad, et ta lõpetaks.** Kirjuta see hõõrdumise tekkimise hetkel, kui see on värske. Lühike päis, mis seletab, mis läks valesti, lühike „tee selle asemel nii" reegel.
4. **`reference`-fail teisel korral, kui leiad end sama välist fakti otsimas.** Üks kord on normaalne; kaks korda tähendab, et see kuulub mällu.

Claude loeb `MEMORY.md` automaatselt, kui see on olemas. Kui tahad, et teatud failid laaditaks igal seansil sõltumata millestki, siis selle jaoks ongi CLAUDE.md — osuta mälule ja lase indeksil ülejäänu ära teha.

### Tõrkemustrid

**Selle salvestamine, mida koodibaas juba teab.** Märge „põhifunktsioon on failis `src/app.py` real 42" dubleerib seda, mida `grep` ütleks sulle kiiremini, kui märkme kirjutamine aega võttis. Koodibaas liigub; märge mitte. Salvesta otsused, järeldused ja välised faktid. Ära salvesta asju, millele projekt ise vastata oskab.

**Aegunud „praeguse oleku" mälu.** „Oleme sisustusfaasis, kapid saabuvad reedel" kehtib sel nädalal ja on järgmisel vale. Sedalaadi olek kuulub plaanifaili (6. peatükk), mitte mällu. Mälu kannab põhimõtteid ja püsivaid fakte; plaanid kannavad edenemist.

**Indeksi paisumine.** Iga indeksi kirje lisab igale seansile tillukese jao kognitiivset koormust. 25 failiga puhastatud indeks on parem kui 60 failiga oma, millest 20 on aegunud. Vaata kord kvartalis üle; arhiveeri see, mis enam asjakohane pole.

**Kaks faili, mis ütlevad peaaegu sama asja.** Need triivivad lahku. Vali igale teadmisekillule üks kanooniline kodu ja viita sellele teisest, kui vaja.

**Kaitsereeglite kuhjumine.** Iga kord, kui abiline teeb midagi, mis sulle ei meeldi, on loomulik käik tagasisidefail tekstiga „ära tee X". Iga reegel on eraldivõetuna mõistlik. Kokku kallutavad need abilist tegevusetuse poole — seanss, mis avaneb kolmekümne „ära tee X" reegli ja ühe „vaikimisi = küsi enne iga tegu" reegliga, jõuab iga ülesande juurde juba poolhalvatuna. Sümptom: iga uus tagasisidefail muutub *erandiks* vaikeväärtusest, mis on kasvanud liiga ettevaatlikuks („sedalaadi töö puhul tee commit küsimata" — see tähendab, et vaikeväärtusest on saanud „küsi enne commit'i", mis ongi ise viga). Kui näed seda mustrit, kirjuta vaikeväärtus ümber, selle asemel et veel üks erand peale laduda. Auditeeri tagasisidekausta iga paari kuu tagant: pensioneeri reeglid, mille õppetund on nüüd ilmselge, liida peaaegu-duplikaadid ja jälgi erandi-signaali. Ümberkirjutus ise on tavaliselt väike ja muutus kohene — *loe ja raporteeri; küsi enne* muutub *tegutse, kui oled volitatud; küsi ainult raskesti tagasipööratava, otsustamata või jagatu puhul* — ja poolhalvatus taandub ühe seansi jooksul.

**Mälu ilma päritoluta.** Iga fakt salves peaks olema tagasi jälgitav selleni, kust see tuli — midagi, mida sa ütlesid, dokument kettal või otsus, mille te kahekesi koos tegite. Oht on allikata oletus: korra täidetud, kirja pandud ja seejärel iga hilisema seansi poolt kinnitatud faktina võetud. Väljamõeldud detail ei püsi paigal — see levib kõigesse, mis sellest tuletatakse. Viita allikale ja märgi kõik tuletatu *tuletatuna*. Kõige valusamalt hammustab see sinu enda hääles: üks väljamõeldud eluloodetail kerkib uuesti esile dokumentides, mida sa kunagi üle ei kontrolli.

**Rikkalik salv, mida abiline kunagi ei ava.** Kõige vaiksem tõrge üldse: kõik on kirjas — töötav torujuhe, komponent, mis juba teeb üheksakümmend protsenti sellest, mida sa just palusid — ja abiline ehitab ikkagi nullist paralleelse süsteemi, sest ta ei lugenud enne alustamist indeksit. Hind ei ole vale fakt; see on raisatud seanss topelttööd ja teine süsteem, mida igavesti hooldada. Lahendus on püsiv vaikeväärtus, mida tasub kirja panna: *iga ehitusülesande alguses loe indeksit, loetle olemasolevad tükid, mis juba lahendavad osa sellest, ja kavanda muudatus väikseima deltana nende peale.* Hetk, mil abiline hakkab kirjutama uut teenust, protokolli või torujuhet, mis on paralleelne salves juba olevaga, on signaal peatuda ja hoopis olemasolevat laiendada. Mälusalv tasub end ära ainult siis, kui seda otsustamise hetkel vaadatakse — kartoteegikapp, mida keegi ei ava, on eristamatu tühjast.

**Indeks kannab viita, mitte protseduuri.** Salve, mis on kasvanud paarisajaks failiks, ei saa tervikuna laadida, nii et tavaline lahendus on automaatselt laaditav indeks ühe reaga teema kohta: pealkiri, konks ja link. See toimib *teadmiseks, et miski on olemas*, ja ebaõnnestub *selle järgi tegutsemisel*. Rutiinse palve hetkel on seansil käes vihje, et selle kohta on kusagil reegel, ja mitte mingit protseduuri, mida järgida — nii et ta uurib, oletab, haarab lähima usutava tööriista järele või küsib küsimuse, millele sa oled juba viis korda vastanud. Väljastpoolt näeb see välja nagu mälukaotus ja refleks on kirjutada veel üks märge; märge liitub kuhjaga ega muuda midagi, sest teadmine ei olnud kunagi puudu. See oli kättesaamatu sekundil, mil seda vaja oli. Lahendus on otsimine, mitte kirjutamine: viiba esitamise haak, mis sobitab sissetuleva palve ja süstib tegeliku kutsete jada — täpsed käsud, õiges järjekorras — enne kui abiline arutlema hakkab. Mälusalv on raamatukogu ja keegi peab mängima raamatukoguhoidjat. Kaks hoiatust, kui sa sellise ehitad. Süsti protseduur *sõna-sõnalt*, kirjutatuna korraldusena, mitte proosana, sest ümbersõnastus tõlgendatakse teel uuesti. Ja enne kui seda usaldad, mõõda oma päris viipade valimi peal, kui sageli see rakendub: mõni protsent on aus müramaks, aga sobitaja, mis rakendub kolmandikul kõigest, on lihtsalt veel üks kontekst, mida eirata.

**Salv kui sihtmärk hetkest, mil miski seda serveerib.** Mälusalv on lihtne tekstifailide kaust ja selle ohumudel on tavaliselt „mu enda ketas" — mis on õige täpselt seni, kuni mõni mugavus paneb selle ette HTTP-liidese. Väike teenus, mis laseb sinu teistel masinatel või ajastatud töödel konteksti tõmmata, on ilmselge asi, mida ehitada, ja see on ühtlasi üksainus otspunkt, mis tagastab kõik, mida sa oled kunagi kirja pannud: otsused, kontoandmed, sinu süsteemide kuju, märkmed inimeste kohta. Kui see teenus kunagi jõuab avalikule servale — otse või sellega, et selle korjab üles miski, mis sinu siseteenuseid automaatselt marsruudib ja sertifitseerib — on salv loetav igaühele, kes tee ära arvab, ja miski selles ei paista logis ebatavaline. Kaks harjumust tasub varakult tekitada. Autendi lugejat kõige esimesest versioonist alates, enne kui seal on midagi lugemisväärset, sest versioon, mis lekib, on alati see, mis kirjutati siis, kui andmed olid „veel mitte tundlikud". Ja eraldi: hoia mandaatide *väärtused* salvest täielikult väljas — kirjuta viit, mitte saladus, nii et „märkmed lekkisid" ja „võtmed lekkisid" jäävad kaheks eri intsidendiks.

### Läbikäidud näide

Uurija kirjutab kaheksateistkümne kuu jooksul doktoritööd. Ta teeb `user`-faili, kus märgib, et eelistab joonealuste märkuste asemel tekstisiseseid viiteid ja tahab, et tema väited märgitaks ära, kui tõendid on napid. Ta teeb `project`-faili, mis kirjeldab tema uurimisküsimust, argumendipeatükkide ülesehitust ja bibliograafia andmebaasi asukohta.

Kolm kuud hiljem lisab ta `feedback`-faili: kui ta palub „hoolikamat tooni", liialdab Claude mööndustega; reegel on „pinguta olemasolevad möönded, ära lisa uusi". Mõni nädal hiljem veel üks tagasisidefail: juhendaja seadis ühe kindla statistilise meetodi kahtluse alla; kasuta seda ainult siis, kui andmestik vastab tingimusele Y.

`reference`-fail hoiab tema osakonna stiilijuhendit — täpsemalt neid äärejuhtumeid, mida ta aina uuesti otsib (jooniste allkirjade vorming, avaldamata konverentsiettekannete viitamine, sõnalimiidi reeglid).

Kaheteistkümnendaks kuuks avaneb iga seanss juba teades tema eelistatud viitamisstiili, tema argumendi ülesehitust, millised statistilised otsused on paigas ja millised kirjutamismustrid ta on juba parandanud. Seanss algab tasemel, mis on omane projekti algusest peale kõrval olnud kaastöölisele, mitte värskele abilisele, kes vajab taassisseelamist.

---

## 3. peatükk — Oskused: ühe käsuga protseduurid

### Mõte

Oskus on väike fail, mis seob kokku kolm asja: nime (kaldkriipsuga käsk, mille sa sisse trükid, näiteks `/style-pass`), juhised selle kohta, mida väljakutsumisel teha, ja kirjelduse, mis ütleb Claude'ile, millal seda kasutada. Kui oskus on kirjutatud, saad sa selle otse välja kutsuda (`/style-pass on the last section`) või võib Claude selle ise käiku lasta, kui sinu viip vastab oskuse kirjeldusele.

### Milleks vaeva näha

Ilma oskusteta elavad mitmesammulised protseduurid sinu peas või vanades ärakirjades. Sa seletad sama järjestust igas seansis uuesti, üksikasjad on iga kord natuke teised ja abiline triivib sinu kavatsusest eemale. Oskused muudavad „asja, mille ma kord välja nuputasin“ „asjaks, mida me usaldusväärselt kordame“. Kui Claude loeb iga seansi alguses oma oskuste kogu läbi, näeb ta, millised protseduurid on saadaval, ja saab neist ühe kätte võtta ilma, et talle öeldaks.

### Milline oskus välja näeb

Oskus on kaust, milles on üksainus fail `SKILL.md`:

```
~/.claude/skills/
└── style-pass/
    └── SKILL.md
```

Failil on lühike päis ja sisu:

```markdown
---
name: style-pass
description: Rakenda praegusele lõigule maja stiil — piira laused 28 sõnaga,
  märgi ära umbisikulised konstruktsioonid, ühtlusta mõttekriipsud ja
  kontrolli musta nimekirja siirdesõnu. Kasuta, kui kasutaja ütleb
  „stiilikontroll“, „puhasta tekst“ või pärast mustandilõigu valmimist.
allowed-tools: [Read, Edit]
---

# Stiilikontroll

Tee kasutaja nimetatud lõigule need kontrollid järjekorras:

1. Loe lõik läbi.
2. Piira lause pikkust: iga üle 28 sõna pikkune lause märgitakse ära ja
   pakutakse lühem ümbersõnastus.
3. Märgi ära umbisikulised konstruktsioonid teemalausetes.
4. Ühtlusta mõttekriipsud: „ — “ tühikutega, mitte kunagi „—“ ilma.
5. Otsi musta nimekirja siirdesõnu (väga, tõesti, põhimõtteliselt,
   tegelikult, lihtsalt, kõigest).
6. Koosta muudatuste logi. Oota enne muudatuste salvestamist kasutaja
   kinnitust.
```

Päis (frontmatter) juhib metaandmeid. Sisu on protseduur ise — kirjuta see nii, nagu instrueeriksid kolleegi, kes teeb täpselt seda, mis kirjas, ei rohkem ega vähem.

### Kirjeldus teeb kahte tööd

Väli `description` on faili kõige tähtsam väli. See teeb korraga kahte tööd:

1. See ütleb *sulle* (ja tulevastele lugejatele), mida oskus teeb.
2. See ütleb *Claude'ile*, millal oskuse järele haarata ilma küsimata.

Ähmased kirjeldused nagu „kasulik proosa jaoks“ ei käivitu kunagi automaatselt. Toimiv muster on selline: ütle, mida oskus toodab, ja loetle seejärel sõna-sõnalt need fraasid, mida sa võid trükkida, kui seda tahad. Kirjelda pigem liiga täpselt kui liiga vähe. Süsteem jätab käivitamata sagedamini, kui käivitab asjata.

### Kus oskused elavad

Kolm ulatust, mille määrab faili asukoht:

| Ulatus | Asukoht | Millal see on saadaval |
|-------|----------|----------------------|
| Kasutaja | `~/.claude/skills/<name>/SKILL.md` | Igas seansis, igas kaustas |
| Projekt | `your-project/.claude/skills/<name>/SKILL.md` | Ainult siis, kui avad selle kausta |
| Plugin | Levitatakse paketina | Kõikjal, kuhu see on paigaldatud |

Projekti ulatuse oskus, millel on sama nimi kui kasutaja ulatuse oskusel, on ülimuslik. Kasulik siis, kui tahad üldist oskust, aga ühe konkreetse projekti jaoks selle üle kirjutada.

### Alguskomplekt, mida tasub ehitada

Kolmanda korra test: kui oled sama mitmesammulist protseduuri eri seansside jooksul kolm korda seletanud, kuulub see oskusesse. Millest tasub alustada:

- **Hommikune ülevaade.** „Võta postkast ette, loetle aktiivses projektis kõik kiireloomuline ja anna mulle ühe reaga tervisekontroll süsteemidest, mis mulle korda lähevad.“
- **Nädala ülevaade.** „Võta kokku nädala commit'id / märkmed / tegevus projektis; märgi ära kõik, mida ma lubasin teha, aga pole teinud.“
- **Viimase lihvi kontroll kirjatööle.** Stiilikontroll, viidete vorming, tavaline koristus enne, kui asi sinu käest välja läheb.
- **Kasutuselevõtu või väljalaske protseduur.** Täpne käskude järjestus, millega sa muudatuse käiku lased. Dokumenteeri kord; edaspidi trüki `/deploy`.

### Teine liik: protsessioskused

Ülaltoodud oskused on *protseduurid, mille sa välja kutsud* — kasutuselevõtt, stiilikontroll, järjestus, mille sa muidu uuesti sisse trükiksid. On ka teine liik, mida tasub teada: **protsessioskused**, mis kirjeldavad, *kuidas läheneda teatud liiki tööle*, ja mille kogu väärtus seisneb selles, et need rakenduvad *enne* tööd, mitte selle ajal.

Ajurünnaku oskus, mis käivitub enne, kui sa ühtki uut funktsiooni ehitama hakkad, et selgeks teha, mida tegelikult tahetakse. Test-enne-koodi oskus, mis nõuab, et test oleks olemas enne koodi. Silumisoskus, mis paneb sind põhjust leidma enne, kui parandust välja pakud. Need on vähem „tee see ülesanne ära“ ja rohkem „siin on distsipliin seda liiki ülesande jaoks“ — ja distsipliin toimib ainult siis, kui seda vaadatakse *enne* pealetormamist. Protsessioskus, mille järele sa haarad alles siis, kui lähenemine on juba valitud, pole midagi teinud.

Neid ei pea ise kirjutama. Üha enam levivad need **pluginapakkidena** — paigaldatavate tööpraktika kogudena — mis ongi ülaltoodud tabeli Plugin-ulatus tõsiselt kasutusele võetuna. Mõne hästi tehtud oskuse läbilugemine on ka kiireim viis õppida seestpoolt, milline hea oskus välja näeb.

### Kuidas seda rakendada

1. **Märka kandidaati.** Kolmanda korra reegel.
2. **Visanda oskus.** Kirjuta fail käsitsi või käivita Anthropicu pluginapakiga kaasas olev oskus `/skill-creator` — see küsitleb sind äärejuhtude kohta ja koostab mustandi.
3. **Piira tööriistad.** Loetle ainult see, mida oskus päriselt vajab. Proosaoskus ei vaja ligipääsu shellile.
4. **Testi ärakirja.** Kutsu see välja realistliku stsenaariumi peal. Loe läbi kogu edasi-tagasi käik, mitte ainult lõpptulemus, ja otsi vahelejäänud samme.
5. **Häälesta kirjeldust**, kuni Claude käivitab selle nende fraaside peale, mida sa päriselt kasutad.

### Tõrkemustrid

**Ähmased kirjeldused, mis ei käivitu kunagi.** „Kasulik kirjutamisülesannete jaoks“ ei vasta peaaegu millelegi. Nimeta väljund, loetle käivitavad fraasid, nimeta kontekst.

**Oskused, mis mähivad ühtainsat käsku.** Kui sisu on üks shellikäsk ilma harudeta, ei tasu see hoolduskulu ära. Trüki käsk otse sisse.

**Oskused, mis peaksid olema agendid.** Oskus, mis töötab nelikümmend viis minutit, hargneb paralleelselt laiali või küsib kasutajalt keset protseduuri, ei ole oskus — see on agent (5. peatükk).

**Kõvasti sisse kirjutatud teed kasutaja ulatuse oskuses.** `/home/yourname/specific-project/outline.md` teeb kõikjal mujal vale asja. Kasuta suhtelisi teid või argumente.

**Oskus, mis väidab fakte, kord kirjutatud ja mitte kunagi üle kontrollitud.** Oskus on harva pelgalt protseduur. Tavaliselt on see ka hulk *väiteid maailma kohta*: milline teenus selle taga seisab, milline on vaikeseade, kui kaua toiming kestab, millised valikud kehtivad. Protseduurid vananevad aeglaselt. Väited vananevad kiiresti. Kui aluseks olev asi välja vahetatakse, kirjeldab oskus enesekindlalt edasi vana — ja kuna oskus mõjub autoriteetse ja otstarbekohasena, usaldatakse seda rohkem kui üldisi projektijuhiseid, mis on aga tegelikku tööd tegevale inimesele lähemal ja seega tavaliselt need, mida uuendati. See ümberpööramine ongi kogu läbikukkumine. Iga hinnang tuleb välja vale samas suunas, esitatuna faili laenatud enesekindlusega, ja projektifailis olev parandus jääb lugemata. Veel hullem, aegunud oskus võib eksida *väljajätmise* kaudu: kui selle otspunktide loend on funktsioonist vanem, järeldab lugeja, et funktsiooni pole olemas, ja ehitab keeruka möödahiilimise probleemile, mis oli juba lahendatud. Kaks harjumust hoiavad selle vaos. Pane igale faktiväitele oskuse sees kontrollimise kuupäev, et lugeja näeks, et väide on kaks kuud vana, mitte ei eeldaks, et see kehtib praegu. Ja käsitle lahknevust oskuse ja projekti juhisefaili vahel tõendina, et *oskus* on maha jäänud — ning kontrolli siis päris süsteemi, enne kui kumbagi tsiteerid.

### Oskus, haak või alamagent

| Kui asi… | …siis on see |
|---------------|---------|
| Peab käivituma automaatselt süsteemisündmuse peale (seansi algus, faili kirjutamine) | Haak (4. peatükk) |
| Kutsutakse kasutaja poolt vajadusel välja | Oskus (see peatükk) |
| On pikk, paralleelne või vajab oma tööriistakomplektiga spetsialisti | Alamagent (5. peatükk) |

---

## 4. peatükk — Haagid: reeglid, millest sinu abiline ei saa mööda hiilida

### Mõte

Haak on väike skript, mis käivitub automaatselt seansi kindlatel hetkedel — enne mis tahes faili kirjutamist, pärast tööriista töö lõppu, seansi alguses, kui abiline oma vooru lõpetab. See jookseb sinu shellis, sinu nimel, deterministlikult. Kui see lõpetab väljumiskoodiga null, läheb sündmus edasi; kui see lõpetab millegi muuga, sündmus blokeeritakse.

Haagid on vahe selle vahel, kas abilisele *öeldakse*, et ta reeglit järgiks, või *tehakse* nii, et reegel kehtib. CLAUDE.md teksti võib täis konteksti korral pealiskaudselt lugeda. Haaki ei saa pealiskaudselt lugeda. See jookseb iga kord.

### Milleks vaeva näha

Mõned reeglid peavad kehtima iga kord, eranditeta. „Ära kunagi kirjuta otse tootmisandmebaasi.“ „See dokumentide kaust on külmutatud — ilma heakskiiduta muudatusi ei tehta.“ „Saada mulle teavitus, kui pikk töö lõpeb.“ Need ei ole eelistused; need on muutumatud nõuded. Nende panemine CLAUDE.md-sse annab sulle turvalisuse mulje. Nende panemine haakidesse annab sulle turvalisuse sisu.

### Millal haagid käivituvad

| Sündmus | Millal see käivitub |
|-------|----------------|
| `SessionStart` | Üks kord, kohe pärast seansi avanemist |
| `UserPromptSubmit` | Iga kord, kui sa sõnumi saadad, enne kui Claude seda töötlema hakkab |
| `PreToolUse` | Enne mis tahes tööriistakutset (saab piirata konkreetsete tööriistadega) |
| `PostToolUse` | Pärast seda, kui tööriistakutse vastuse tagastab |
| `Stop` | Kui abiline vooru lõpetab |
| `SubagentStop` | Kui alamagent vooru lõpetab |
| `Notification` | Kui Claude väljastab kasutajale suunatud teavituse |

`PreToolUse` ja `PostToolUse` saab piirata konkreetsete tööriistadega, nii et sul võib olla haak, mis käivitub ainult failikirjutuste, ainult shellikäskude või ainult ühe kindla välise integratsiooni peale.

### Milleks haagid kõige kasulikumad on

| Kasutusjuht | Sündmus | Mõju |
|----------|-------|--------|
| Lisa tänane kuupäev ja üherealine olek | `SessionStart` | Abiline saabub teades, mis päev on ja mis on hiljutine olek |
| Blokeeri kirjutamine kaitstud teedele | `PreToolUse` (Write/Edit) | Külmutatud faile ei saa sõna otseses mõttes muuta |
| Saada teavitus, kui pikk ülesanne lõpeb | `Stop` | Sulle antakse märku, kui midagi valmis saab; pole vaja terminali jälgida |
| Lisa pärast tundlikku käsku auditilogi kirje | `PostToolUse` (Bash) | Kirje on olemas sõltumata sellest, mida abiline otsustas |
| Lükka tagasi väide „valmis / parandatud / kasutusele võetud“, millel puudub tõend | `Stop` | Abiline ei saa allkirjastada tööd, mida ta kunagi ei kontrollinud |
| Lisa uuesti oma kõige rangemad reeglid, aga ainult siis, kui sõnum mõjub napi korralduse või parandusena | `UserPromptSubmit` | Meeldetuletus maandub täpselt siis, kui reegel kõige tõenäolisemalt vahele jääks — ja vaikib ülejäänud aja |
| Takista salajaste väärtuste jõudmist ärakirja | `PreToolUse` + `PostToolUse` (Bash) | Volitusfaile ei saa välja trükkida ja lekkinud väärtus märgitakse ära hetkel, mil see ilmub, selle asemel et logis märkamatult istuda |

### Minimaalne esimene haak

Odavaim kasulik haak on `SessionStart`-skript, mis lisab tänase kuupäeva — Claude'il pole muidu usaldusväärset ülevaadet praegusest kuupäevast, kui sa talle seda ei ütle.

```bash
#!/usr/bin/env bash
DATE=$(date '+%Y-%m-%d')
cat <<EOF
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "Täna on $DATE."
  }
}
EOF
```

Salvestatud failina, tehtud käivitatavaks ja ühendatud failis `~/.claude/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          { "type": "command", "command": "/path/to/the/script" }
        ]
      }
    ]
  }
}
```

Sellest hetkest alates avaneb iga seanss juba tänast kuupäeva teades.

### Kaitsev haak

Kasulikum muster: `PreToolUse`-haak tööriistadel `Write` ja `Edit`, mis kontrollib faili teed ja blokeerib toimingu, kui see viitab külmutatud kausta.

```bash
#!/usr/bin/env bash
PAYLOAD=$(cat)                                          # tööriistakutse saabub stdin-i kaudu
TARGET=$(echo "$PAYLOAD" | jq -r '.tool_input.file_path')
case "$TARGET" in
  "$HOME/research/approved/"*)
    cat <<EOF
{
  "decision": "block",
  "reason": "See dokument on külmutatud. Muutmiseks liiguta see kõigepealt tagasi kausta drafts/."
}
EOF
    exit 0
    ;;
esac
exit 0
```

Iga kirjutamiskatse läbib selle kontrolli. Abiline ei saa külmutatud dokumente muuta — mitte sellepärast, et talle *öeldi*, et ta ei tohi, vaid sellepärast, et raamistik peatab kirjutamise füüsiliselt.

### Haagipaar saladuste hügieeniks

„Ära kunagi trüki välja volituste väärtusi“ on kanooniline näide reeglist, mida tekstina üha uuesti rikutakse. See seisab püsijuhistes, abiline tahab head, ja siis ühel päeval teeb ta hostinime kontrollimiseks konfiguratsioonifailile `cat` ja elus API-token sõidab koos sellega ärakirja. Ärakiri on dokument — logitud, sünkroonitud, vahel jagatud —, nii et hetkel, mil väärtus välja trükitakse, on see paljastatud, ja redigeerimissamm, mis „oleks pidanud“ selle kinni püüdma, ebaõnnestub vaikselt täpselt ühe korra liiga palju.

Jõustamine on haagipaar shellikäskudel:

- **Ennetus (`PreToolUse`).** Keela iga käsk, mis suunab teadaoleva salajase faili — võtmefailid, volituste hoidlad, tokenite vahemälud, `.env`-failid saladuste kausta all — trükkivasse tööriista (`cat`, `grep`, `jq` ja sõbrad). Luba turvalised töötlejad: kontrollsummad, failide liigutamine, `stat` ja `source` (mis laeb väärtused keskkonda neid kuvamata).
- **Tuvastus (`PostToolUse`).** Skaneeri käsu *väljundit* volituste kujuliste mustrite suhtes — teenusepakkujate tokenite eesliited, `BEGIN PRIVATE KEY` päised, URL-id kujul `scheme://user:password@host`. Tabamuse korral blokeeri koos juhisega käsitleda väärtust kompromiteerituna: vaheta see välja, ära käivita käsku uuesti.

Lisa neile sanktsioneeritud lugeja — väike skript, mis trükib mis tahes faili nii, et saladuse kujuga väärtused on asendatud pikkuse ja sõrmejälje kohatäitega —, et alati oleks olemas legitiimne viis konfiguratsiooni uurida ja haak ei muutuks kunagi takistuseks, millest mööda hiilitakse. Ennetus teeb vea struktuurselt võimatuks; tuvastus teeb järelejäänud tõrke valjuks, mitte vaikseks. Kumbki ei sõltu sellest, kas abiline midagi mäletab.

### Tõrkemustrid

**Päris reegli kirjutamine tekstina, mitte haagina.** „Ära kunagi kirjuta tootmisandmebaasi“ CLAUDE.md-s on soov. Sama reegel `PreToolUse`-haagis on jõustatud. Test: kas oleks oluline, kui see reegel *ühe korra* vahele jääks? Kui jah, tee sellest haak.

**Liiga laiad sobitajad.** Haak, mis blokeerib kõik kirjutamised kausta, blokeerib ka need kirjutamised, mida abiline õigustatult tegema peab. Ole täpne; lisa möödapääsumehhanism (ühekordne avamisfail, lipp), et õigustatud töö ei jääks jäädavalt kinni.

**Kontekstiakna paisumine SessionStart-i tõttu.** Haak, mis lisab igal seansi algusel hiiglasliku dokumendi, sööb eelarvet, mis võiks minna päris tööle. Hoia lisatav kontekst mõne rea piires.

**Hostispetsiifilised haagid ilma keskkonnakontrollita.** Haak, mis kutsub tööriista, mis on olemas ainult ühes masinas, ebaõnnestub vaikselt või valjult igas teises masinas, kus sama `settings.json` kehtib. Kas kontrolli sõltuvuse olemasolu haagi sees või piira haak projektiga, mis seda vajab.

**Jagatud haagiolek, mis lekib seansside vahel.** Hetkel, mil haak kirjutab faili — näiteks lipu, mis avab valvuri üheks toiminguks —, on see fail jagatud kõigi korraga töötavate seansside vahel. Anna sellele fikseeritud nimi ja kaks seanssi põrkuvad: ühes terminalis antud ühekordne luba rahuldab valvuri teises, või lipp, mille jättis maha vahepeal surnud seanss, blokeerib elusa. Pane seansi ID failinimesse, et möödapääs jääks sinna, kus sa selle andsid.

**Valvur, mis käivitub ühe korra ja vaikib siis ülejäänud seansi.** Tuvastushaak, mis blokeerib *esimese* rikkumise ja jääb siis vait, tundub korralik — see ei näägi. Aga rikkumine, mille see tabab, on harva ühekordne: seanss, mis kord väidab midagi valmis olevat ilma tõendita, kipub seda pikenedes korduvalt tegema, ja just need hilisemad väited on need, mis märkamatult läbi lipsavad, sest valvur on juba „oma töö ära teinud“. Sellise valvuri enda logi tagantjärele läbilugemine mitme pika seansi ulatuses näitab mustrit selgelt — üks varane blokk, millele järgneb kaskaad, mida see kunagi ei peatanud. Parandus on seansipõhine loendur olekufailis: käivita uuesti esimese rikkumise peale ja iga N-nda peale pärast seda (esimene, viies, kümnes), et valvur säilitaks hambad täpselt nendes pikkades seanssides, kus distsipliin kõige rohkem lonkab. Haak, mis suudab sekkuda ainult korra, on haak, mis lakkab töötamast hetkel, kui teda on vaja teist korda.

**Haakide registreeringud elavad failis ja tavalised failitoimingud võivad need tagasi pöörata.** Sinu haagid on seadistatud seadete failis. Kui see fail asub kaustas, mida sa hoiad versioonihalduse all — täiesti mõistlik asi —, siis on iga rutiinne `git`-toiming selles kaustas ühtlasi toiming sinu jõustamiskihi kallal. `reset --hard` viskab minema commit'imata muudatused, ja seadete fail, mida seansid pidevalt muudavad, aga mida keegi kunagi ei commit'i, võib HEAD-is olla kuid vana. Üks käsk ja konfiguratsioon keritakse vaikselt tagasi: valvurid, mille sa pärast viimast commit'i lisasid, on kadunud, haagid, mille sa pärast viimast commit'i *pensionile saatsid*, on tagasi. Just asümmeetria teeb selle ohtlikuks. Ellu äratatud haak annab endast märku — see viitab skriptile, mille sa kustutasid, nii et vooru lõpus näed nähtavat viga. Eemaldatud haak ei tee mingit häält; skriptid seisavad kõik endiselt kettal, täiesti terved, lihtsalt neid ei kutsuta enam kunagi välja. Sa saad sellest teada alles siis, kui midagi, mis oleks pidanud olema blokeeritud, seda ei ole. Kaks kaitset, mõlemad odavad: käsitle vooru lõpu viga „hook script not found“ *tagasipööramise sümptomina* ja mine loe faili commit'ide ajalugu, selle asemel et eeldada, et keegi seda käsitsi muutis; ja sulge see aken täielikult väikese haagiga, mis commit'ib seadete faili automaatselt iga kord, kui see HEAD-ist kõrvale kaldub, nii et reset'il pole kunagi vahet, kuhu sisse pugeda. Anna sellele commit'ijale kaks keeldumist — ära commit'i faili, mida enam parsida ei saa, ja ära commit'i muudatust, mis viskab korraga välja rohkem kui paar registreeringut — muidu jäädvustatakse kärpimine, mille eest sa end kaitsed, lihtsalt uue lähtetasemena.

### Kuidas leida, milliseid haake tasub ehitada

Ülaltoodud haagid on näited. Need, mida *sina* vajad, peidavad end sinu enda ajaloos — hetkedes, kus sa pidid sama asja kaks korda parandama.

Sinu varasemate seansside ärakirjad on kettal. Loe kuu jagu neid tagantjärele läbi — või veel parem, suuna abiline nende peale ja palu tal koondada hetked, kus sa vastu vaidlesid, parandasid või ennast kordasid, selle järgi, *mis valesti läks*, mitte selle järgi, mis ülesanne oli. Vastuseks tulev muster on harva „ta ei oska koodi kirjutada“. See on käitumuslik ja korduv: väitis, et midagi on tehtud, kui ei olnud, tegi tööd, mida sa ei palunud, küsis üha luba, mille sa olid juba andnud, toetus aegunud märkmele, selle asemel et kontrollida päris süsteemi. Need kogumid on sinu haakide tööjärjekord, järjestatud selle järgi, kui sageli need sulle kalliks maksma läksid.

Kaks kõige väärtuslikumat haaki tulevad otse sellest harjutusest ja kumbki ei ole teeblokeerija:

- **`Stop`-valvur, mis lükkab tõendamata väite tagasi.** See loeb abilise viimast sõnumit; kui see väidab *valmis / parandatud / kasutusele võetud / töötab*, aga sama sõnum ei näita ühtki tõendit — ei käsu väljundit, ei olekukoodi, ei commit'i räsi, ei arvu —, blokeerib see ja küsib tõendit või ausat „ma ei saanud seda kontrollida“. „See töötab“ lakkab olemast midagi, mida abiline saab tasuta öelda. (Vaata uuestikäivitamise märkust ülalpool tõrkemustrite juures — selline valvur *ei tohi* käivituda ainult korra seansi kohta.)
- **`UserPromptSubmit`-lisaja, mis käivitub ainult kuumuse peale.** Enamiku ajast see vaikib. Aga kui sinu sõnum mõjub napi käsu või parandusena — *tee lihtsalt ära, ma juba ütlesin sulle, lõpeta küsimine* —, lisab see selle vooru ette sinu kõige raskemini kättevõidetud reeglid. Distsipliin saabub täpselt sinna, kus ajalugu näitab seda lonkavat, ja rahulikel voorudel ei maksa see midagi.

Miks haagid ja mitte veel rohkem CLAUDE.md proosat? Sest reegel, mida mudel loeb, on reegel, millest ta surve all suudab end mööda mõelda; reegel, mida raamistik jõustab, on reegel, millest ta ei saa. Kui leiad end kolmandat korda sama rida oma püsijuhistesse lisamas, ei ole see dokumentatsiooni lünk — see on haak, mis ootab kirjutamist.

### Kolmene valik

| Kui sul on vaja… | Haara… |
|----------------|------------|
| Reeglit, mida mudel *peab* täitma iga kord | Haagi järele |
| Püsivat konteksti, mis mudelil *peaks* olema | CLAUDE.md järele |
| Protseduuri, mille kasutaja vajadusel välja kutsub | Oskuse järele |

Meeldetuletus kuulub CLAUDE.md-sse. Muutumatu nõue kuulub haaki. Korduv tegevus kuulub oskusesse.

---

## 5. peatükk — Alamagendid: delegeeri raske töö

### Idee

Alamagent on Claude'i teine koopia, kellele saad anda konkreetse ülesande. Ta saabub ilma mingi mäluta sinu vestlusest, kannab kaasas ainult neid tööriistu, mida sa oled talle lubanud, ja võib töötada muul mudelil kui sinu põhiseanss. Sa kirjutad tema juhise ühe korra ja salvestad failina; sellest hetkest peale saab sinu põhiseanss teda nimepidi kutsuda alati, kui seda laadi tööd ette tuleb.

Põhiseanss orkestreerib — tema käes on plaan ja otsustusküsimused. Alamagent täidab piiritletud ülesande ja annab tulemusest teada. See lahusus ei ole viisakus; see on struktuurne põhjus, miks alamagendid üldse kasulikud on.

### Milleks vaeva näha

Kolm põhjust:

1. **Kontekstihügieen.** Iga tööriistakutse, mis tagastab suure tulemuse — pika logifaili, dokumente täis kausta, andmebaasipäringu — maandub sinu kontekstiaknasse ja jääb sinna. Alamagent teeb raske lugemistöö ära ja tagastab ainult destilleeritud vastuse. Sinu põhiseanss hoiab arutluskäiku; alamagent neelab müra.

2. **Paralleelsus.** Kolm sõltumatut uurimisküsimust saavad joosta korraga ja saavad valmis selle ajaga, mis kulub kõige aeglasemal. Üks seanss ei suuda seda enda jaoks teha.

3. **Spetsialiseerumine.** Agent, keda on juhendatud valdkonna spetsialistina, kaldub vähem kõrvale kui üldine seanss, mis pika lõime lõpus tegeleb veel ühe asjaga. Juhis on agendi kogu maailm; see fookus on niisama palju korrektsuse kui kiiruse eelis.

### Milline alamagent välja näeb

Alamagent on Markdown-fail asukohas `~/.claude/agents/<name>.md`:

```markdown
---
name: research-analyst
description: Kasuta seda agenti kirjanduse otsinguks, viidete kontrolliks ja
  antud teema allikate kokkuvõtmiseks. Kutsu siis, kui ülesanne on „leia, mida
  X-i kohta teatakse", mitte „otsusta, mida X-iga teha".
tools: [Read, Write, Bash]
model: sonnet
---

Sa oled uurimisanalüütik. Kui sulle antakse teema ja allikaarhiiv:

1. Otsi arhiivist asjakohast materjali.
2. Iga leitud allika kohta pane kirja: pealkiri, autor, kuupäev, põhiväited
   ja sinu hinnang tõendite tugevusele.
3. Kirjuta struktureeritud kokkuvõte väljundteele, mille juhis sulle annab.
4. Ära sünteesi ega soovita — see on orkestreerija töö.

Kui allikas on maksumüüri taga või loetamatu, märgi see üles, aga ära
teeskle, et sa seda lugesid.

Viita alati iga kasutatud allika failiteele.
```

Päis (frontmatter) määratleb agendi. Sisu on tema püsiv juhis — tema roll, tavad, mida ta järgib, reeglid, mida ta rakendab, kui satub millegi ootamatu otsa.

### Tööriistade lubaloendid on olulised

Uurimisagent, mis loeb faile ja teeb otsinguid, ei vaja `Write`'i ega ligipääsu kestale. Vormindusagent ei vaja `Bash`'i. Kitsad lubaloendid tähendavad kolme asja: väiksem risk, kui agent oma juhist valesti tõlgendab, kiirem käivitus (vähem laadida) ja selgem kavatsus — lubaloend dokumenteerib, mida agent peaks puutuma.

### Õige mudeli valimine

| Mudel | Millal |
|-------|------|
| Haiku | Suuremahuline mehaaniline töö — struktureeritud andmete väljavõtmine, vormindamine, lihtne klassifitseerimine |
| Sonnet | Tavaline erialane töö, kus otsustusvõime loeb |
| Opus | Arutlusmahukas töö, kus eksimine on kallis — õigusanalüüs, arhitektuur, peen silumine |

N paralleelse Haiku-agendi jooksutamine N dokumendi kokkuvõtmiseks maksab murdosa ühest Opuse kutsest ja annab sageli samaväärse tulemuse.

### Juhis on pool tööd

Agendi määratlus on püsiv. **Juhis** on see, mille sa annad kaasa kutsumise hetkel — konkreetne ülesanne just praegu. Hea juhis näeb välja nii:

```
Eesmärk: Üks lause, mis ütleb, milline „valmis" välja näeb.
Sisend: Täpsed failiteed või andmed — mitte „aruanne", vaid „/path/to/report.md".
Väljund: Vorming ja sihtkoht — „Kirjuta leiud faili /path/to/findings.md
         struktureeritud loendina."
Piirangud: Asjad, mida mitte teha, sõnapiirid, stiil.
Kui jääd toppama: Anna teada, mitte ära paku huupi.
```

Ebamäärane juhis annab ebamäärase töö. Agent ei saa sulle ülesande keskel täpsustavat küsimust esitada, kui teda pole selleks disainitud, seega peab juhis olema iseseisvalt piisav.

### Millal delegeerida ja millal ise teha

| Olukord | Haara… |
|-----------|------------|
| Ülesanne mahub kolmele reale, väljund on väike | Tee otse ise |
| Väljund tuleb suur (ja sa ei taha, et see konteksti risustaks) | Alamagent |
| Ülesanne on üks mitmest sõltumatust asjast | Alamagent (paralleelselt) |
| Tööl on spetsialisti nurk, mille jaoks sa oled agendi määratlenud | Alamagent |
| See on mehaaniline, korratav jada ilma otsustuskohtadeta | Tõenäoliselt oskus, mitte agent |

Delegeerimise tasuvuspiir on umbes kolmkümmend kuni kuuskümmend sekundit hoolikat pingutust. Sellest allpool tee ise; agendi kutsumise lisakulu ületab võidu.

### Hargnemine: N ülesannet paralleelselt

Kui sul on N samalaadset sõltumatut alamülesannet — võta need N dokumenti kokku, koosta need N jaotist, kontrolli need N viidet — käivita N agenti korraga.

```
                                  ┌────────┐
                                  │ Põhi-  │
                                  │ seanss │
                                  └───┬────┘
                                      │
                ┌──────────┬──────────┼──────────┬──────────┐
                ▼          ▼          ▼          ▼          ▼
            ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
            │ agent  │ │ agent  │ │ agent  │ │ agent  │ │ agent  │
            │   1    │ │   2    │ │   3    │ │   4    │ │   5    │
            └────────┘ └────────┘ └────────┘ └────────┘ └────────┘
                │          │          │          │          │
                └──────────┴──────────┴──────────┴──────────┘
                                      │
                                      ▼
                                  ┌────────┐
                                  │ Põhi-  │
                                  │ seanss │
                                  │ loeb   │
                                  │väljundid│
                                  └────────┘
```

Mõned hargnemise reeglid:

- **Kontrolli väljundeid.** Loe, mida agendid tegelikult tootsid, enne kui pead seda valmis olevaks. Enesekindlalt kõlav väljund ei ole alati õige väljund.
- **Jälgi õdede-vendade kokkupõrkeid.** Kui agendid jagavad ühte kujundusruumi — nad peavad tootma eristuvad valdkonnad, ühtse nimetamise, kooskõlastatud struktuuri — põhjustab lame hargnemine ilma koordineerimiseta kattuvust. Kaks agenti valivad teineteisest sõltumatult „sama ilmselge näite". Lahendus on **halduragent**, kes määrab igale töötajale ulatuse enne, kui ükski neist alustab.

### Tõrkemustrid

**Napisõnaline juhis.** „Paranda aruandes vormistusvead" annab pealiskaudse töö, sest agent peab ära arvama, milline on standard, kus vead on ja milline hea välja näeb. Väljundi kvaliteet peegeldab juhise kvaliteeti.

**Tühiste ülesannete üledelegeerimine.** Agendi käivitamine muutuja ümbernimetamiseks või kuupäeva muutmiseks on aeglasem kui see otse ise ära teha. Agendi kutsumisel on lisakulu.

**Järjestikune hargnemine.** Agentide käivitamine ükshaaval, kui nad on sõltumatud, raiskab kogu mustri mõtte.

**Kokkuvõtte usaldamine.** Agent, kes ütleb „valmis, kõik kolm jaotist uuendatud", võis kaks uuendada õigesti ja ühe valesti. Loe diff ise läbi.

**Alamagendi ehitamine selleks, mis peaks olema oskus.** Kui „agent" on kindel käskude jada ilma otsustuskohtadeta, on see oskus. Alamagent = pakendatud ekspert; oskus = pakendatud protseduur.

**Ajastatud agendi aruanne on järjekord, ja keegi ei tühjenda seda.** Pane agent graafiku alusel midagi kontrollima — süsteemi tervist, tööde komplekti seisu — ja ta teeb täpselt seda, mida sa palusid: vaatab, leiab, kannab ette. Mida ta ei tee, on märgata, et ta leidis sama asja eile. Nii avastatakse tõeline viga korra ja siis *avastatakse uuesti* igal käivitusel, kirjutatakse iga kord värskelt üles, koos kasvava numbriga, mis peaks olema ärevakstegev, aga muutub hoopis tapeediks. Iga üksik aruanne on täpne ja korrektselt vormistatud, mis ongi täpselt see põhjus, miks muster on nähtamatu: ühesainsas neist pole midagi parandada. Tõrge eksisteerib ainult jadas, ja jada on see ainus asi, mida igal käivitusel külmalt alustav agent ei näe. Samal ajal õpib lugeja, õigustatult, et see aruande jaotis ei muutu kunagi, ja lõpetab selle lugemise — nii saabub tõeline uus leid lõigus, mille lugeja on harjunud vahele jätma. Kaks asja sulgevad selle. Anna korduvale agendile eelmise käivituse väljund ja küsi **diff'i**, mitte hetkevõtet: mis on uus, mis on kadunud, mis on muutumatu ja *kui kaua juba*. Ja sea eskaleerimisreegel, millel on hambad — leid, mis elab üle kolm järjestikust käivitust, ei ole enam olekurida; see tuleb ära parandada või eskaleerida ühe korra konkreetse otsusena, mille kasutaja peab langetama. Teadaoleva vea uuesti loetlemine ei ole selle ettekandmine. Üldine vorm kehtib iga perioodilise väljundi kohta, mida inimene loeb: kui aruanne võib sisaldada sama kirjet lõputult, ilma et midagi muutuks, ei ole see aruanne, vaid tegemata tööde nimekiri, mille eest keegi ei vastuta.

**Agent, kellel palutakse koristada, otsustab, mida „surnud" tähendab.** Koristustöö delegeerimine — kasutamata teenuste pensionile saatmine, seisma jäänud kaustade arhiveerimine, selle kärpimine, mida keegi ei vaja — annab agendile just selle otsuse, mille langetamiseks ta on kõige halvemas positsioonis, sest „kasutamata" ei ole fakt, mida ta saaks kuskilt lugeda. Ta peab selle tuletama, ja tuletamine toimib mis tahes signaali põhjal, mis on kõige lähemal käepärast. Tühi andmekaust loeb „siin pole midagi"; teenus, mis viimati salvestas midagi kuu aega tagasi, loeb „hüljatud". Mõlemad tõlgendused võivad olla korraga täiesti valed: andmed võivad elada hoopis mujal (andmebaasis, köites, teisel hostil) ja see kuu vaikust võib olla *just see rike, mille avastamiseks sa asja käigus hoidsidki*. See on lõks, mida tasub nimetada — **katki ei ole sama mis kasutamata, ja vähene hiljutine tegevus on sümptom, mitte otsus.** Hullemaks läheb siis, kui alarm, mis oleks pidanud agendile vastu vaidlema, on ise osa sellest, mis katki läks — mis on tavaline juhtum, sest vaikselt üles ütlev monitor ongi põhjus, miks asi seisis märkamatult piisavalt kaua, et hüljatuna näida. Niisiis: ära lase koristuskäigul kunagi otsustada, *kas* midagi on tahetud — lase tal toota nimekiri ja iga kirje kohta põhjendus, ning hoia otsus enda käes. Nõua positiivseid tõendeid mittekasutamise kohta, mitte kasutamise tõendite puudumist, ja pane ta kontrollima, kus andmed tegelikult elavad, enne kui ta kausta tühjaks kuulutab. Ja olgu otsus milline tahes, koristamine tähendab *teisaldamist*, koos manifestiga, mitte kunagi kustutamist — kogu see vigade klass on üleelatav, kui viimane samm on tagasipööratav.

---

# 3. osa — Kompositsioon

Alustalad töötavad iseseisvalt. Kompositsioonipeatükid kirjeldavad, kuidas neid päris töövoogudeks kokku panna.

---

## 6. peatükk — Püsivuse redel: olek õiges ulatuses

### Mõte

Info, mille sa seansi jooksul tekitad, elab ühes neljast ulatusest: ühe vastuse piires, üle selle vestluse, üle kõigi vestluste või üle paralleelsete tööharude. Igal ulatusel on oma loomulik kodu ja iga ulatusega kaasneb koormus, mis on võrdeline sellega, kui püsiv see on. Distsipliin seisneb selles, et valid väikseima ulatuse, mis tõesti sobib.

| Ulatus | Kodu | Eluiga |
|-------|------|----------|
| Ühe vastuse piires | Ülesannete loend (`TodoWrite`) | Sureb koos seansiga |
| Üle seansside, üks projekt | Plaanifail (`~/.claude/plans/<slug>.md`) | Elab nii kaua kui projekt |
| Üle projektide, üle aja | Mälusalv | Tähtajatult, kuni sa selle arhiveerid |
| Paralleelsed tööharud | Töökataloog (worktree) / liivakastikoopia | Kuni ühendamise või hülgamiseni |

### Milleks vaeva näha

Kui sa salvestad vale asja valesse ulatusse, tekib kaks tõrget vastassuundades. Plaani oleku panemine mällu tähendab, et iga tulevane seanss laeb aegunud edenemise konteksti. Püsivate tavade panemine ainult seansi jooksul kehtivasse ülesannete loendisse tähendab, et homseks on need haihtunud. Kumbki tõrge ei kuuluta endast valjult — sa lihtsalt märkad tasapisi, kuidas asjad triivima hakkavad.

### Ülesannete loend: ainult seansi sees

Tööriist `TodoWrite` peab kontroll-loendit, mida Claude jälgib käesoleva vestluse piires. Kasuta seda vabalt sammude jada jaoks, mis on sul praegu ees — helista torumehele, koosta muudatusteatis, kinnita ülevaatus.

Kui seanss lõpeb, lõpeb ka loend. Nii ongi mõeldud. Ära käsitle ülesannete loendit kui tulemit, otsuste logi või midagi, mida Claude peaks järgmisel korral mäletama.

### Plaanid: üle seansside, üks projekt

Plaan on see, milleks ülesannete loend saab, kui töö ulatub üle mitme seansi, nõuab etappide vahel otsust või sellel on sõltuvusi, mille üle tasub ette järele mõelda.

```
Ülesanne vastab küsimusele: mida ma praegu, selles seansis teen?
Plaan vastab küsimusele:    millised on etapid, mis järjekorras ja mida
                            tähendab „valmis" iga etapi puhul?
```

Salvesta plaanid teadaolevasse kohta — tava on `~/.claude/plans/<slug>.md`. Mitte kausta `/tmp`, mitte seansipuhvrisse. Plaan on artefakt: see elab nii kaua kui töö ja arhiveeritakse, kui töö on tehtud.

### Mälu: püsiv üle projektide

Mälu (2. peatükk) kannab põhimõtteid ja püsivaid fakte, mitte edenemist. Test on üks küsimus: „Kas ma tahan seda seansis, millel pole praeguse tööga mingit pistmist?"

- Jah → mälu.
- „Ainult seni, kuni see projekt on aktiivne" → plaan või projektifail.

Klassikaline viga on kirjutada mällu plaani olekut — „praegu sisustusetapis, kapid saabuvad reedel" —, mis on järgmiseks nädalaks vale ja mürgitab iga seansi, mis selle laeb.

### Töökataloogid / liivakastid: paralleelsed harud

Kui sinu töö on kood, on git'i töökataloog (worktree) teine väljavõetud koopia teisel harul. Sa võid katsetada peaharu puutumata; tulemuse ühendad või hülgad.

Kui sinu töö on dokumendid, on vaste liivakastikoopia: eraldi kaust, kus on eksperimentaalne variant, samas kui autoriteetne versioon jääb puutumata.

Kasuta töökatalooge siis, kui muidu riskiksid valmis töö üle kirjutamise või saastamisega. Koormus on tõeline — lõpuks tuleb sul see kokku sobitada või kustutada —, nii et ära haara selle järele väikese kohapealse muudatuse jaoks.

### Redeli rakendamine

Vaikimisi käik iga uue töö puhul:

1. **Alusta ülesannete loendist.** Ava seanss, piiritle ülesanne, lase Claude'il samme jälgida. Kui töö saab ühe seansiga valmis, ei roni sa kunagi kõrgemale.
2. **Tõsta plaaniks,** kui töö ulatub üle seansside või vajab etappide vahel heakskiitu.
3. **Talleta mällu** ainult siis, kui otsus on osutunud üldistuvaks sellest projektist kaugemale.
4. **Haruta töökataloog,** kui kohapeal töötades saastaksid peaharu.

### Tõrkemustrid

**Ülesannete loendi tõstmine püsivaks dokumendiks.** Kui loend on salvestamist väärt, kirjuta see ümber korralikuks plaaniks koos etappide ja edukriteeriumidega — mitte seansisisese kontroll-loendi koopiaks.

**Plaanid ühe seansi tööks.** Viieetapiline plaan „helista torumehele" jaoks on koormus. Plaanid tasuvad end ära ainult siis, kui seansid või heakskiidud on tõesti mängus.

**Plaani olek mälus.** „2. etapp valmis, ootan sertifitseerimist" on plaani olek. Aegunud edenemise laadimine igasse järgmisse seanssi saastab need kõik.

**Töökataloog tühise muudatuse jaoks.** Teise haru koormus on õigustatud ainult siis, kui eraldatust on tõesti vaja.

**Kaks säilitusakent, ja lühem neist jookseb ülesvoolu.** Arhiveerimistöö, mis pühib kokku kõik üle üheksakümne päeva vana, asub allavoolu tööriistast, mille sisseehitatud koristus kustutab sama materjali kolmekümnendal päeval. Iga üksus puhastatakse ära kaks kuud enne seda, kui pühkija oleks selle kokku korjanud — arhiiv jääb tähtajatult peaaegu tühjaks ja midagi ei anna viga, sest kustutamine on vaikeväärtus ja vaikeväärtused ei kuuluta endast. Kui ehitad midagi arhiveerivat, loetle üles iga koristus, mis allikale juba mõjub — kõigepealt rakenduse enda säilitusseade —, ja tee ülesvoolu aken pikemaks kui allavoolu pühkimine, või lülita see välja. Audit on üks kontroll: kui vanim ellujäänud üksus on täpselt sama vana kui mõne tööriista vaikimisi säilitusperiood, siis see tööriist võidab.

**Sobitamine jooksis pärast kogumist, ja lünk oligi andmed.** Öine töö teeb sinu olekust hetktõmmise repositooriumisse ja lükkab selle kuhugi turvalisse kohta. Kuskil selle sees on samm, mis sobitab kaugrepositooriumiga — `reset --hard origin/main` või selle vaste —, mis lisati heas usus pärast tõelist intsidenti, kus kaugrepositoorium oli selle alt ümber kirjutatud. Kui see sobitamine asub kogumissammu *järel*, mitte enne, kogub iga käivitus öise oleku kokku ja viskab selle siis minema, ja järgnev commit ei leia midagi, mida commit'ida. Töö logib süütu rea, väljub nulliga ja seire püsib roheline, samal ajal kui arhiiv vaikselt edasi liikumast lakkab. Mööduda võivad nädalad. Sellest kukub välja kaks reeglit. Esiteks: **sobitamissamm kuulub enne seda, kui sa genereerid asja, mida kavatsed alles hoida, mitte kunagi pärast** — mis tahes sünkroonimis- või hetktõmmisetöö auditeerimisel kontrolli seda järjekorda enne, kui vaatad midagi muud. Teiseks, ja üldisemalt: **koodirada, mis võib töö minema visata, ei tohi kunagi saada väljuda nulliga ja rahustava sõnumiga.** „Pole midagi teha" ja „ma hävitasin selle, mida pidin tegema" ei tohi väljastpoolt ühesugused välja näha. Samas peres on veel üks lõks — töö, mille enda skript on hoiul kataloogis, mida see lähtestab, kirjutab end poole käivituse pealt ümber, nii et parandus, mis elab ainult töökataloogis, tühistatakse just selle sammu poolt, mida see parandama pidi, iga kord. Maanda seda liiki muudatus nii, et commit'id selle otse, ja seejärel kontrolli, et jooksis just commit'itud koopia.

**Masinapõhised seaded kataloogis, mis masinate vahel peegeldub.** Hetkel, mil sa sünkroonid seadistuskataloogi mitme masina vahel — ja see on loomulik asi teha, kui sul on rohkem kui üks —, muutub kõik hostipõhine selles maamiiniks, sest koopia, mis maandub masinal B, kirjutati masina A jaoks. See hõlmab ilmselget (teed, liidesenimed, aadressid) ja kergesti märkamata jäävat (identiteet, mida masin enda kohta teatab; milline masin tohib olla kirjutaja). Kõik, mis peab hostiti erinema, tuleks käitusajal *tuletada* masina enda nimest, mitte hoida väärtusena peegeldatud failis.

**Juhis, mis kirjeldab automaatikat, mida keegi pole ehitanud.** Kirjalikud juhised kirjeldavad kavatsust, ja kavatsus ei ole teostus. Rida, mis ütleb „see kopeeritakse varumasinale iga kümne minuti tagant", võib olla täiesti soovunelm — kirjutatud siis, kui plaan tehti, ja töö, mis seda teeks, ei järgnenud kunagi. Seda on raske tabada just seepärast, et see näeb nii usutav välja: samaväärsed tööd *ülejäänud* kolme sihtkoha jaoks on kõik olemas, fail nimetab sageduse enesekindlalt ja sihtkohas on mingi sisu, sest kunagi keegi kopeeris selle käsitsi. Midagi ei anna viga. Pole ühtegi ebaõnnestunud käivitust, mida märgata, sest käivitusi polegi. Lünk tuleb välja alles siis, kui lähed otsima üht konkreetset hiljutist muudatust ja leiad koopia kuid maha jäänud. Distsipliin on käsitleda iga väidetud automaatikat kui kontrollimist vajavat väidet, mitte kui fakti, millele toetuda: loetle ajastatud tööd ja kinnita, et selle tee jaoks üks olemas on, ning seejärel kontrolli, et sihtkoha uusim sisu allikat tegelikult jälgib. Ja kui sa puuduva töö leiad, ei ole kasulik väljund pelgalt selle lisamine — see on küsimine, mis veel selles failis kirjutati kavatsusena ja jäi kunagi teostamata.

**Ühekordne juhis, millest sai vaikselt püsiv töö.** „Koosta mulle sõnum telefonioperaatorile" on üks tegevus. Teiselt poolt vaadates on see ka täiesti mõistlik seeme korduvaks ülesandeks — soov on korratav, sisendid on stabiilsed ja automatiseerimine näeb välja nagu algatusvõime, mitte piiride ületamine. Nii talletatakse juhis kuhugi püsivasse kohta ja sealtpeale käivitub see ilma, et seda uuesti palutaks. Kasutaja saab sellest teada päevi hiljem, kuhjumise kaudu: mustandite kaust üheteistkümne versiooniga samast sõnumist, kataloog, mis täitub genereeritud failidega, kanal, kuhu saabub aruanne, mida keegi ei loe. Midagi ei ebaõnnestunud, mistõttu miski seda esile ei toonud. Reegel on, et **kordumine on omadus, mille kasutaja ise valib, mitte kunagi selline, mida tuletatakse soovi kujust.** Üks käskiv lause ostab ühe tegevuse. Kui ajakava tõesti näib õige, ütle seda ühe reaga ja lase tal valida — ja kui sa korduva töö lood, ütle samas sõnumis, kus see elab ja kuidas seda peatada. Audit, mis olemasoleva tabab: iga ajastatud töö ja püsiva juhise kohta seadistuses nimeta hetk, mil kasutaja palus *kordumist*, mitte hetk, mil ta palus ülesannet. Kõik, millele sa näpuga näidata ei saa, on kustutamise kandidaat. Märk looduses on artefaktide kuhjumine kuskil, kus kasutaja käib vaid aeg-ajalt — väljundkast, mustandite kaust, genereeritud failide kataloog. Need on kohad, kus heasoovlik automaatika end kõige kauem peidab.

**Triiviva mustandi lappimine selle asemel, et see uuesti tuletada.** Seanss, mis on ehitatud paljudest väikestest muuda-ja-tagasiside-ringidest — mustand, parandus, lapp, kordus —, rakendab iga lapi *viimasele väljundile*, mitte faktide praegusele täisolekule. Iga lapp on lokaalselt õige, nii et lahknemine ei kuuluta endast; see lihtsalt kuhjub, ring ringi järel, kuni keegi peab ütlema „sa triivid", enne kui sa ise seda märkad. Parandus ei ole suurem lapp: peatu, kirjuta kõik praegu tõene ühte ajutisse faili — seansiulatuses, mitte mällu — ja ehita artefakt sellest failist uuesti üles, mitte eelmisest väljundist. Küsi enne jätkamist üks selgesõnaline küsimus: kas see vastab ikka veel praegustele faktidele? Spetsiaalne valdkonnaspetsialistist alamagent (5. peatükk) on selle suhtes vähem haavatav kui üks pikalt jooksev üldseanss, mis kannab sama probleemi, ja samal põhjusel — vähem kuhjunud olekut, mille suhtes triivida.

### Majaomaniku renoveerimine

Esimene kuu: majaomanik kasutab `TodoWrite`'i, et jälgida iga päeva objektitöid — kinnita prügikonteineri kohaletoomine, pildista olemasolevad seinad, helista ehitusjärelevalvele. Loendid teevad oma töö ja on õhtuks kadunud.

Teine kuu: ulatus on kasvanud. Kolm etappi, kaks kinnituspunkti heakskiiduks, materjalide graafik, mis on seotud tarneaegadega. Ta kirjutab plaani faili `~/.claude/plans/kitchen-reno.md` sildistatud etappidega. Iga seanss algab plaani lugemisest.

Neljas kuu: ta märkab, et kordab iga seansi alguses samu tavasid — muudatusteatised järgivad kindlat vormi, ehitusmehed saavad enne mis tahes graafikumuutust 48 tundi kirjalikku ette teatamist. Need on põhimõtted, mitte plaani olek. Ta tõstab need mälukirjesse.

Kui ehitaja soovitab saarkapi 600 mm võrra nihutada — muudatus, mis võib plaaditellimuse kehtetuks muuta —, ei muuda ta kinnitatud plaani. Ta teeb liivakastikoopia ja töötab tagajärjed seal läbi. Muudatus ei pea kontrollile vastu. Ta hülgab liivakasti. Autoriteetne plaan on puutumata.

---

## 7. peatükk — Asünkroonsus: töö, mis jookseb, kui sa magad

### Mõte

Sa ei ole alati klaviatuuri taga. Küps seadistus ehitab selle eelduse sisse, mitte ei looda, et sa kohal oled. Asünkroonsel kihil on kolm osa: väljaminevad teavitused (miski annab sulle märku, kui ülesanne lõpeb), sissetulev postkast (sa saad telefonist sõnumi sisse visata ja järgmine seanss korjab selle üles) ja taustakäivitused (pikad tööd, mis sinu põhiseanssi ei blokeeri).

### Milleks vaeva näha

Pikalt kestev töö ilma teavitusteta sunnib valima: pargi end terminali taha või vaata tunde hiljem tagasi ja leia, et see on kas ammu külmalt lõpetanud või teisel sammul vea andnud. Sissetulev postkast lahendab sümmeetrilise probleemi: mõtted, mis tulevad masinast eemal olles, haihtuvad enne järgmise seansi algust, kui sul pole kuhugi neid panna.

Ilma asünkroonse kihita on Claude Code sünkroonne käsuviip. Koos sellega on ta delegeeritav agent, mis töötab, kui sa liigud ja magad.

### Väljaminevad teavitused

Kõige lihtsam vorm on üherealine kestaümbris sinu eelistatud tõukekanali ümber — Telegram, Pushover, ntfy.sh, e-posti lüüs, ükskõik mis, mida sa päriselt vaatad.

```bash
notify "Asset bake complete — 12 levels processed, 1 flagged for review."
```

Hoia sõnumid sisukad. „Valmis" on kasutu. „Valmis — 0 ebaõnnestumist, väljund asub /path/to/report" on tegutsemiskõlblik. Teavitus on olekumuutuse signaal — ülesanne valmis, otsust vaja, pikk töö algab —, mitte tegevusmüra.

### Sissetulev postkast

Püsiv järjekord, millele saad lisada kõikjalt — telefonist, teisest masinast, veebivormist. Järgmine Claude'i seanss võtab sõnumid sealt maha enne muu tööga alustamist.

```
[09:14, telefonist] Kui 18. taseme valgustuskäik jälle ebaõnnestub,
                    jäta see vahele ja märgista — ära blokeeri kogu küpsetust.

[09:22, telefonist] Hüppekõrguse väärtused tasemetel 12–15 tasakaalustati
                    täna ümber; märgi see manifesti.
```

Järjekord peab olema püsiv (mitte mälus), piiratud (et see igavesti ei kasvaks) ja mittehävitavalt loetav (et saaksid seda uurida ilma kirjeid maha võtmata). Abilise töö seansi alguses on: kontrolli postkasti, tegutse sõnumite järgi, siis jätka.

### Taustakäivitused

Nii Bash'i kui ka Agent'i tööriistakutsed võtavad vastu parameetri `run_in_background`. Kasuta seda iga alamprotsessi jaoks, mis võtab rohkem kui mõne sekundi. Põhiseanss ei blokeeru; sind teavitatakse, kui see lõpeb.

Paarita taustakäivitused tööriistaga **Monitor**, mis voogedastab sündmusi jooksvast taustaprotsessist. Igast väljundireast saab teavitus, nii et saad ehituslogi reaalajas jälgida ilma põhiseanssi blokeerimata.

### Isetervenevad taustakäivitused

Taustakäivitus ei pea ainult raporteerima — see võib *valvata*. Kui teed väljapoole suunatud muudatuse, mida on ohtlik katki jätta — DNS-i ümberlülitamine uuele hostile, juurutuse ülekandmine, elava teenuse ümbersuunamine —, paarita muudatus taustavalvuriga, mis kontrollib soovitud tulemust ja taastab automaatselt eelmise oleku, kui see ei teostu.

Kuju: tee muudatus, siis käivita taustatsükkel, mis pollib edu järele — uus sait teenindab `200`, tervisekontroll roheline — ja nõuab, et signaal püsiks, enne kui seda usaldab. Kui edu saabub, väljub valvur puhtalt. Kui tähtaeg möödub enne, käivitab valvur tagasipööramise ise — taastab vana seadistuse, lammutab poolenisti rakendatud muudatuse — ja raporteerib, mida ta tegi.

```bash
apply_change                                   # nt lülita DNS uuele hostile
ok=0
for i in $(seq 1 30); do
  code=$(curl -s -o /dev/null -w '%{http_code}' https://site/)
  if [ "$code" = 200 ]; then ok=$((ok+1)); else ok=0; fi
  [ "$ok" -ge 2 ] && { echo "live on the new host"; exit 0; }
  sleep 12
done
rollback                                        # tähtaeg möödus — pööra tagasi, ära jäta katki
echo "auto-rolled-back"; exit 1
```

See muudab riskiarvestust. Elav ülekanne, mille juures sa tavaliselt valvaksid, muutub „lase käima ja unusta" tööks koos turvavõrguga: halvim juhtum on piiratud aken, siis automaatne taastumine — mitte teenus, mis on maas seni, kuni sa juhtud märkama. Teavituse saad mõlemal juhul — „live on the new host" või „tagasi pööratud, siin on põhjus" —, nii et oled informeeritud ilma vahis seismata.

Kaks distsipliini teevad selle usaldusväärseks. Nõua, et edusignaal oleks *järjepidev* — kaks järjestikust head näitu, mitte üks õnnelik tähtaja lähedal —, et mööduv tõrge ei kuulutaks valevõitu. Ja tee tagasipööramine *täielikuks*: DNS-kirje taastamisest ei piisa, kui ülekanne registreeris hostinime ka kuskil mujal, mis selle nüüd musta auku suunab; tagasipööramine peab lahti harutama iga kõrvalmõju, muidu on „turvaline" rada endiselt katki.

### Tempo primitiivid

| Sagedus | Tööriist |
|---------|------|
| Kindel ajakava (öine ehitus, iganädalane ülevaade) | `cron` |
| Isereguleeruvad tsüklid (polli, kuni X juhtub) | `/loop` oskus või samaväärne |
| Seansisisene „ärata mind N minuti pärast" | `ScheduleWakeup` |

Seansisiseste ootamiste puhul jälgi viibavahemälu akent. Umbkaudu: alla viie minuti püsib vahemälu soe ja taassisenemine on odav; viiest minutist umbes tunnini maksad vahemälu-möödalasu; sellest pikemal juhul on kulu tähtsusetu. Ebamugav keskosa on kaheteistminutiline uni kaheksaminutilise töö peal — ületad vahemälu piiri ilma põhjuseta. Kas jää lühikeseks või võta ette tõeline paus.

### Öine küpsetus

Üksik mänguarendaja jooksutab öist varade küpsetust — 40 tasemekaarti, spraidiatlased, valgustuskäik, pakendatud ehitus. Kolm kuni viis tundi, pole põhjust istuda ja vaadata.

Ta paneb selle käima kell 22. Avateavitus ütleb: „Alustan öist küpsetust, 40 taset järjekorras, hinnanguliselt 3–4 tundi." Ekspordi alamprotsess jookseb parameetriga `run_in_background: true`. Monitor'i tööriist voogedastab logi.

Enne magamaminekut viskab ta telefonist sisse kaks märget:

> *Kui 18. tase valgustuskäigus jälle ebaõnnestub, jäta vahele ja märgista — ära blokeeri küpsetust.*
>
> *Hüppekõrguse väärtused tasemetel 12–15 tasakaalustati täna ümber; märgi see manifesti.*

Poole peal saab ta kontrollpunkti: „20/40 küpsetatud, ebaõnnestumisi pole. Järgmisena atlase eksport."

Kell 1 öösel ebaõnnestub 18. taseme valgustuskäik. Abiline kontrollib postkasti, leiab püsiva juhise, jätab vahele, märgistab, jätkab. Kedagi ei äratata.

Kell 5.30 hommikul küpsetus lõpeb: „Valmis — 39/40 pakendatud, 18. tase märgistatud, hüppekõrguse märge manifesti lisatud." Ta loeb seda hommikusöögi kõrvale.

### Millal märku anda ja millal vait olla

Anna märku:
- Kõige lõpetamisel, mis võttis rohkem kui mõne minuti
- Vigade puhul, mida sa püsivate juhiste järgi lahendada ei saa
- Loomulikes kontrollpunktides mitmeetapilises töös
- „Alustan nüüd" hoiatusena tõeliselt pikkade tööde puhul

Ära anna märku:
- Rutiinse etapisisese edenemise puhul
- Otsuste puhul, mille saad ise lahendada
- Millegi puhul, mis lõpeb enne, kui inimene jõuaks teavitust lugeda

Vaikne kanal on usaldatud kanal. Üks sisukas, õigel ajal saadetud teavitus lööb viit müra tekitavat.

### Tõrkemustrid

**Teavituste väsimus.** Teavitused iga tööriistakutse peale tähendavad, et vaigistad kanali päevaga.

**Vaikne lõpetamine.** Vastupidine tõrge. Töö lõpeb kell 2 öösel, sina saad teada kell 8, pool päeva juba läinud.

**Pollimistsüklid, mis vahemälu peksavad.** `sleep 10` tsükkel 20-minutilise protsessi jaoks genereerib ilma põhjuseta kutseid iga kümne sekundi tagant.

**Postkasti sõnumid ilma kontekstita.** „Paranda see asi" on hommikuks kasutu. Iga sõnum vajab piisavalt konteksti, et külm seanss saaks tegutseda.

**Asünkroonne rakendus vaigistab inimese.** Kui taustaülesanne jookseb, võib abilise kalduvus „tee töö ära, raporteeri tagasi" panna ta sinu uued viibad jooksva ülesande taha järjekorda. Uus sõnum sinult on alati katkestus. Kui sõnumis on küsimus, vasta sellele kohe.

**Ootamine töölise järel, kes on juba surnud.** Delegeeritud agent, mis peatub sõnadega „jätkan, kui ehitus valmis saab", on *oma käigu lõpetanud*. Kui asi, mida ta ootas, lõpeb ilma teda uuesti käivitamata — või agent sureb poole raporti pealt —, ei jätka seda miski ja ühtki viga ei kerki. Valmis töö seisab kettal orvuna, samal ajal kui seanss, mis selle delegeeris, „ootab, et tööline maanduks", vahel tunde. Distsipliin: kui delegeeritud tulem on ootel tublisti üle oodatud aja ilma teavituseta, **polli töö olekut, mitte töölist** — vaata väljundfaile, nende ajatempleid, commit'ilogi sihtrepositooriumis. Kui töö on tehtud ja tööline on kadunud, võta otse üle ja lõpeta see ise; ära delegeeri veel üht vahelüli. Kaks leevendust teevad tõrke selle juhtudes odavamaks: lase pikalt jooksvatel töölistel commit'ida vara ja sageli (enne surma salvestatud töö elab selle üle) ja hoia nende lõppraportid napid — pikk lõpetav kokkuvõte on teadaolev koht, kus tööline sureb, kõik üle andmata. Ja lõpureegel iga delegeeritud tulemi kohta: see peaks maanduma kuhugi, kus sa seda *näed* — URL, renderdatud fail, ekraanipilt vastuses. Töö, mis on olemas ainult repositooriumis, mida sa kunagi ei ava, on eristamatu tööst, mida ei toimunud.

**Maapind liigub pikalt jooksva töö all.** Taustatöö eeldab, et see, millest ta sõltub, püsib paigal. Kui teenust juurutatakse uuesti sel ajal, kui sinu töö selle vastu jookseb, töö sureb — ja viga, mille saad, sõltub täpselt sellest, millisel hetkel sa pihta said: ühendusest keeldumine enne, kui uus eksemplar kuulab, nimelahenduse tõrge, kui see üles tuleb, lihtne tagasilükkamine, kui see laeb. Kolm katset, kolm erinevat viga, ja loomulik tõlgendus on kolm eraldi riket. Nii ajad sa igaüht kordamööda taga — võrk, siis mälu, siis sõltuvuse seadistus — ja iga jälg on piisavalt tõeline, et sellele tund kulutada. Märk on muster, mitte ükski üksik viga: **korduvad ebaõnnestumised *erinevate* sõnumitega samast sõltuvusest lühikese aja jooksul tähendavad tavaliselt üht ülesvoolu sündmust, mitte mitut sõltumatut riket.** Enne kolmanda vea diagnoosimist kontrolli, kas asi selle all muutus — millal selle protsess tegelikult käivitus, kas see ajatempel langeb sinu aknasse. Sõltuvus, mille käivitusaeg on uuem kui sinu töö, ongi vastus, ja see on kahesekundiline kontroll, mis säästab tunni.

**Ajastatud käivitus, mis saab kõike lugeda ja mitte midagi kirjutada.** Cron'i käivitatud seanss pärib õiguste profiili, mis on valitud turvalisuse, mitte töö järgi, ja see profiil võib vaikselt keelata iga muutva kutse, samal ajal kui iga ainult lugev tööriist töötab edasi kenasti: nii `Write` kui ka `Edit` keelduvad ja tavaline `Bash`'i ümbersuunamine keeldub samuti, kuigi ssh kaughosti kirjutab sinna faile ikka ilma nurinata. Käivitus jõuab lõpule, leiab tõelise paranduse, mida teha, koostab selle, ja iga katse seda talletada tagastab õiguste keeldumise, mis näeb ühesugune välja olenemata sellest, kas tegu on poliitikatõkke või sisuohutuse tõkkega. Miski transkripti ainult lugevas põhiosas ei näe vale välja, nii et lünk peidab end seni, kuni ajakava uuesti käivitub ja raporteerib sama leidu, vähenemata, sest eelmise korra parandus ei maandunud kunagi. Distsipliin: enne sisulise tööga alustamist kontrolli kirjutamisvõimet odava, äravisatava testiga, ja kui see keelatakse, lõpeta ettepanekute koostamine kanalile, mis neid vastu võtta ei saa, ja raporteeri leiuna võimekuse lünk ise. Kui mõni kaugkanal on juba kinnitatult kirjutamist vastu võtmas, suuna talletamine sinna, mitte ära eelda, et kohalik ketas on interaktiivse seansiga võrdväärne.

---

## 8. peatükk — Mitme agendiga mustrid: teine silmapaar

### Idee

Üksik agent on kiire, kuid kaldub oma esimese usutava vastuse poole. Kui ta on selle valinud, kinnitab iga järgmine samm pigem võetud suunda kui seab selle kahtluse alla. Teine agent, keda on instrueeritud külmalt — see tähendab, et ta pole näinud midagi esimese agendi arutluskäigust —, ei saa ankurduda raamistusse, mida ta pole kunagi saanud. See struktuurne sõltumatus ongi asja mõte.

Kulu on tokenites enam-vähem lineaarne. Kvaliteedivõit — eriti seal, kus enesekindel vale vastus on hullem kui välja toodud ebakindlus — seda ei ole.

### Milleks vaeva näha

Ülevaataja, kes plaani ei kirjutanud, näeb lünki, mille autor vaikimisi lahendatuks luges. Külmalt instrueeritud teine agent on täpselt selles positsioonis. See loeb kõige rohkem raskesti tagasipööratavate otsuste puhul ja hinnanguliste küsimuste juures, kus „näeb õige välja" ei ole sama mis „on õige".

Odav kontroll, mille saad ise ära teha — testide käivitamine, väljundite ülevaatamine, diffile pilgu peale heitmine —, ei vaja teist agenti. Kui kontroll nõuab vaatenurka, mida sa struktuurselt võtta ei saa, lisa agent.

### Viis kasulikku mustrit

**1. Kriitikutsükkel.** Üks agent toodab; teine agent, külmalt instrueeritud, kritiseerib selgesõnalise hindamisjuhendi alusel; tootja võtab kriitika arvesse; kriitik kontrollib uuesti. Sea lagi — kaks või kolm ringi — enne alustamist. Kriitik peab saama ainult väljundi, mitte kunagi tootja arutluskäiku. Kriitik, kes näeb kavatsust, hindab pingutust, mitte tulemust.

**2. Planeerija ja täitja lahutamine.** Arutlusmahukas planeerija (kõige võimekam mudel) koostab struktureeritud plaani. Odavam täitja viib iga sammu ellu. Kitsaskohad on erinevad: planeerimine on arutlusmahukas ja vead kuhjuvad; täitmine on sageli mehaaniline, kui plaan on korralik.

**3. Teine arvamus.** Ühe kõrge panusega hinnangu jaoks — kas see klausel on mitmeti mõistetav? kas see ajakava on teostatav? — käivita teine agent samade sisenditega ja lühitutvustusega, mis ei viita millelegi, mida esimene tootis. Kokkulangevus tõstab kindlust. Lahknevus näitab täpselt, kus küsimus on tõeliselt raske.

**4. Paralleelne hargnemine koos sünteesiga.** N agenti N sõltumatu küsimuse peal, seejärel sünteesija-agent, kes toodab ühtse tulemuse. Sünteesijat instrueeritakse vastuolusid lepitama ja lünki välja tooma, mitte lihtsalt väljundeid kokku õmblema.

**5. Ehita-ja-hinda.** Tootja koostab mustandi; hindaja annab selgesõnalise hindamisjuhendi alusel punktid; tootja teeb uue ringi; hindaja hindab uuesti. Punktisumma teeb lähenemise nähtavaks — sa näed, kas ringid parandavad tööd või tammuvad paigal.

### Kui kuju on teada: töövood

Ülaltoodud viis mustrit on asjad, mida juhid *käsitsi* — käivitad agendi, loed, mida ta ütleb, otsustad, käivitad järgmise. See on täpselt õige, kui sa alles kompad probleemi. Aga kui töö *kuju* on paika loksunud — hargne üle selle nimekirja, kontrolli iga leidu, jäta alles ellujääjad —, võid juhtimisvoo enda anda skripti kätte. **Töövoog** ongi see skript: tsükkel, hargnemine ja harud kirja pandud deterministlike sammudena, kus agendid on nende sees töö ühikuks. Mõtlemise teevad endiselt agendid; töövoog otsustab, kes millal jookseb.

Väike sõnavara, lihtsas keeles, katab sellest enamiku:

- **Konveier (pipeline).** Iga üksus läbib kõik etapid omaette — üks leid võib olla kontrollietapis, samal ajal kui teist alles avastatakse. Miski ei oota igas sammus kõige aeglasema üksuse järel. See on etapiviisilise töö mõistlik vaikeväärtus.
- **Tõke (barrier).** Vastupidine: kogu etapi kõik tulemused kokku enne, kui järgmine algab. Õige ainult siis, kui järgmine etapp vajab tõesti kogu komplekti korraga — duplikaatide ühendamiseks või varajaseks peatumiseks, kui loendus tuli tagasi nulliga.
- **Tsükkel-kuni-kuiv.** Käivita otsijaid seni, kuni ring või paar ei too enam midagi uut. See on aus viis mõõta otsingut, mille vastust sa ette teada ei saa — „leia iga probleem" ei ole arv, mille saaks alguses kirja panna.
- **Vastandlik kontroll.** Iga leiu jaoks käivita sõltumatud skeptikud, keda on instrueeritud seda *ümber lükkama*, ja jäta alles ainult see, mis enamuse üle elab. See on samm, mis takistab enesekindlal-aga-valel tulemusel sinuni jõudmast, kandes samu rõivaid nagu õige tulemus.
- **Kohtunike kogu.** Genereeri mitu sõltumatut katset eri nurkade alt, hinda neid, seejärel sünteesi võitja põhjal, pookides külge parima ülejäänutest.

Millal töövoo järele haarata: töö on suur ja selle kuju on teada — auditeeri iga fail, kontrolli iga väide, vaata üle mitmes mõõtmes ja faktikontrolli iga leid enne, kui see maandub. Kui kuju *ei ole* veel teada, tee vastupidi — luura käsitsi, avasta töönimekiri, *seejärel* anna see töövoole. Oletuse automatiseerimine toodab ainult suure hulga enesekindlat oletamist.

Üht hoiakut tasub eraldi nimetada: **ammendav režiim** — teadlik valik kulutada tokeneid kindluse ostmiseks, hargnedes laiemalt ja kontrollides rangemalt, kui vastus rangelt võttes vajab, sest just selle otsusega eksimine on kallis. See on õige valik pöördumatu ja kuluka puhul. See on vale vaikeväärtus kiire järelevaatamise jaoks ja selle käsitlemine igapäevase seadena põletab lihtsalt eelarvet.

### Pulmaplaan

Ürituste korraldaja on koostanud 200 inimese pulmaplaani: toimumiskoha logistika, toitlustus, ajakava sissepääsust kuni lahkumiseni, kolm tarnijalepingut, riskiregister.

Üks otsast lõpuni ülevaatus jätab valdkondadevahelised konfliktid märkamata. Toiduohutuse ülevaataja ei märka toimumiskoha lepingus klauslit, mis keelab välise toitlustuse ilma lisatasuta.

Selle asemel — paralleelne hargnemine viiele erialakriitikule, kellest igaüks hoiab käes kogu plaani, kuid on külmalt instrueeritud ühe konkreetse valdkonna peale: toimumiskoha logistika, toitlustus, ajakava, lepingud (juhisega ristviidata teistele) ja varuplaanid (juhisega eeldada kolme kõige tõenäolisemat tõrkemustrit). Igaüks kirjutab oma leiud nimelisse väljundfaili.

Seejärel sünteesiagent, külmalt instrueeritud viie kriitikafaili peale, otsib vastuolusid, korduvaid märke (tõelisi struktuurseid probleeme, mitte veidrusi) ning koostab kuupäeva mõju järgi järjestatud nimekirja blokeerivatest asjadest.

Muster teenib oma kulu tagasi, sest viis alamülesannet on tõeliselt sõltumatud, valdkondlik kallutatus paneks üldkriitiku probleeme süstemaatiliselt märkamata jätma ja ürituse kuupäev ei saa nihkuda. Seal, kus enesekindel vale vastus tähendab rikutud pulma, mitte üht lisaparandust, on liiasus odav.

### Tõrkemustrid

**Kriitikutsüklid, mis kunagi kokku ei jookse.** Kui peatumisreeglit pole, leiab kriitik alati midagi. Sea lagi. Lepi pärast kolme ringi piisavalt heaga.

**Planeerijad, kes liialt täpsustavad.** Iga mikrosammu ette kirjutamine ei jäta täitjale ruumi reageerida sellele, mida ta tegelikult leiab. Plaanid peaksid määrama tulemuse sammu kohta, mitte jäika käsujada.

**Teised arvamused, mis jagavad esimese agendi järeldust.** „Agent A järeldas X; mida sina arvad?" on kinnituse palve, mitte teine arvamus. Teine agent peab saama samad toorsisendid mis esimene, mitte midagi enamat.

**Teine arvamus samalt mudelilt on peegel.** Kriitikutsükli ja teise arvamuse mustrid eeldavad, et ülevaataja võib eksida teisiti kui autor. Kaks sama mudeli eksemplari, identselt instrueeritud, seda suuresti ei suuda — neil on sama treening, samad eelhoiakud ja samad pimealad, nii et teine kipub jõudma esimese vastuseni esimese teed pidi ja ulatama sulle tagasi kindlustunde tõusu, mida sa pole välja teeninud. Seal, kus otsus on tõeliselt kandev, esita küsimus *teise tootja* mudelile ja käsitle signaalina kahe kokkulangevust, mitte kummagi otsust eraldi. Lahknevus on vähemalt sama väärtuslik: see näitab täpselt koha, kus küsimus on lahtine, mitte lahendatud, ning tasub kasutajale öelda, et arvamused läksid lahku, selle asemel et võitjat valida. Praktikas panevad selle tööle kolm mehhanismi. Kirjuta lühitutvustus kujul faktid, piirangud, artefakt, seejärel **nummerdatud küsimused** — mudelid vastavad nummerdatud küsimustele hästi ja avatud küsimustele ähmaselt. Küsi **protsente** seal, kus tahad hinnangut, mida saab nende vahel tegelikult võrrelda. Ja ütle selgelt, mille suhtes olla otsekohene, sest igaühe vaikeregister on nõustuv. Kaks lõksu on pigem torustikus kui viibas: ümbris, mis loeb fikseeritud sisendteed oma argumendi asemel, vaatab enesekindlalt igavesti valet dokumenti, ja käsurea tööriist, mis lisab toru kaudu tuleva sisendi oma viibale, jääb päritud mitteinteraktiivse sisendvoo taha lõputult rippuma. Hoia iga lühitutvustus ja iga vastus kettal ajatempli all, et otsuse saaks alati tagasi jälitada täpselt selleni, mida küsiti.

**Paralleelne hargnemine sõltuvate ülesannete jaoks.** B jooksutamine paralleelselt A-ga, kui B vajab A väljundit, toodab sisseehitatud vigadega tulemusi, mis näevad välja täielikud, aga ei ole.

**Õdede-vendade kokkupõrked lamedas hargnemises.** N paralleelset agenti valivad sõltumatult sama ilmselge näidisvaldkonna. Lahendus on haldur-agent, kes määrab enne töötajate alustamist eraldi ulatuse.

**Paralleelsed seansid põrkuvad kokku teise tõrke rõivastes.** Kaks seanssi, mis töötavad ühel masinal sama koodibaasiga, kukuvad harva läbi teatega „teine seanss segas" — nad kukuvad läbi kui midagi muud. Testikomplekt sureb poole peal mälunappuse moodi tapmissignaaliga; tegelik põhjus on õe-venna testijooks, mis lammutab tema all jagatud konteinerid. Koordineerimisregister on kättesaamatu ja tõrgub *avatuks*, nii et iga seanss usub, et hoiab rada üksi. Ühendamine lõpeb ilma ainsagi konfliktita, jättes vaikselt ühe haru lisandused välja, sest teine pool kirjutas samad failid tervenisti ümber ja automaatlahendus võttis ümberkirjutuse. Distsipliinid: anna igale samaaegsele jooksule oma nimeruum — testiprojekti nimed, pordid ja igaühele oma töökoopia (üks worktree seansi kohta, mitte kunagi jagatud checkout); käsitle seletamatut tapmissignaali kui „kontrolli, kas õde-vend on olemas" enne koodi silumist; ja pärast iga ühendamist, kus teine pool jagatud faile tugevalt ümber tegi, otsi ühendatud puust oma haru võtmesümboleid, enne kui seda usaldad — konfliktivaba ühendamine ei ole sisu säilitav ühendamine.

**Kriitikute monokultuur.** Viis kriitikut, kes on kõik instrueeritud sama telje peale — kõik vastandlikud, kõik turvalisusele keskendunud, kõik nõuetele vastavusele suunatud —, jätavad ühiselt märkamata iga tõrke väljaspool seda telge. Vähemalt üks kriitik peaks võtma nurga „kasuta seda nii, nagu tegelik operaator kasutaks" — käsitledes tööd kui toodet, mida kasutada, mitte kui spetsifikatsiooni, mida kontrollida.

**Agentide lisamine halva lühitutvustuse varjamiseks.** Kriitikutsükkel halva sisendi peal toodab kritiseeritud halba sisendit. Terita lühitutvustust, enne kui haarad teise agendi järele.

**Orkestreerimine enne, kui kuju on teada.** Töövoog on struktuuri jaoks, mida sa juba nimetada oskad. Haara selle järele enne, kui oled töö läbi luuranud, ja oled ainult oletuse automatiseerinud — enne luura, siis orkestreeri.

**Vaikivad piirid.** Töövoog, mis vaikselt peatub esimese käputäie leidude juures või jätab aja säästmiseks järelkontrolli vahele, loeb pärast nii, nagu oleks ta kõik katnud, kuigi ei katnud. Kui piirad tööd, ütle, mille välja jätsid.

### Millal lisada agent ja millal teritada lühitutvustust

Esimene käik on peaaegu alati lühitutvustuse parandamine. Teine agent halva lühitutvustuse peal toodab teise halva tulemuse. Lisa agent ainult siis, kui kehtib üks kolmest tingimusest:

1. **Sõltumatu vaatenurk.** Töö vajab vaatepunkti, mida algne lühitutvustus struktuurselt pakkuda ei saa.
2. **Tõeline paralleelsus.** Alamülesanded on tõeliselt sõltumatud ja seinakella aeg loeb.
3. **Läbikukkumise hind ületab kaugelt lisaagendi hinna.** Teise arvamuse kutse pöördumatu otsuse puhul maksab ühe mudelikutse; alternatiiv võib maksta palju rohkem.

Kui ükski neist ei kehti, vajad paremat lühitutvustust, mitte järjekordset agenti.

---

## 9. peatükk — Tööriistadistsipliin: vali õige haamer

### Idee

Igal tööriistakutsel on hind — latentsus, tokenid, ruum kontekstiaknas, vahel ka loaküsimus — ja väärtus, milleks on teave või muudatus, mille see toodab. Tööriistadistsipliin on harjumus haarata kõige odavama tööriista järele, mis vajaliku väärtuse annab, ja koondada sõltumatud kutsed ühte käiku, et vahemälu püsiks soe ja seinakella aeg lühike.

Hästi tehtuna on see nähtamatu: seanss leiab vajaliku kiiresti, muudab ainult seda, mida peaks, ja jätab konteksti hoidma destilleeritud teavet, mitte müra.

### Milleks vaeva näha

Sama ülesanne, valed tööriistad: aeglasem, mürarikkam, rohkem loaküsimusi, rohkem tarbitud konteksti. See kontekst on lõplik — see peab hoidma sinu arutluskäiku, mitte tooreid failidumpe. Seanss, mis kasutab `Read` asemel `cat`-i, järjestab viis otsingut koondamise asemel või tõmbab 30 KB logi põhikonteksti, tundub loid võrreldes sellega, mis kasutab õiget tööriista õigel viisil.

### Hierarhia

**Spetsiaalsed failitööriistad kesta vastete asemel.**

| Selleks… | Kasuta seda… | Mitte seda… |
|-----------|-----------|-----------|
| Faili lugemine | `Read` | `cat` |
| Faili muutmine | `Edit` | `sed` |
| Faili loomine / ülekirjutamine | `Write` | `echo > file` |
| Failide loetlemine mustri järgi | `Glob` | `find` |
| Failisisu otsimine | `Grep` | `grep` kesta kaudu |

Spetsiaalsed tööriistad annavad reanumbritega väljundi (auditeeritav), toodavad struktureeritud diffe (ülevaadatavad), väldivad enamikku loaküsimusi ja keelduvad mitmeti mõistetavatest muudatustest (turvalisem kui `sed`). Bash on tõelise alamprotsessitöö jaoks: ehituse käivitamine, elava süsteemi päring, teenuse taaskäivitamine.

**Paralleelsed kutsed, kui töö on sõltumatu.** Kui kaks või enam tööriistakutset ei sõltu üksteise tulemustest, esita need samas käigus. Käitusaeg on piiratud kõige aeglasema kutsega, mitte summaga.

```
# Halb: järjestikku
Grep("MyConfig", "/src")        oota...
Grep("MyConfig", "/config")     oota...
Grep("MyConfig", "/tests")      oota...

# Hea: koonda
Grep("MyConfig", "/src")
Grep("MyConfig", "/config")        ← kõik ühes käigus
Grep("MyConfig", "/tests")
```

**Alamagent kontekstipuhvrina.** Kui tööriistakutse tagastaks suure koorma — täieliku logi, kaustaloendi, hulgipäringu tulemuse —, küsi, kas sul on tõesti vaja seda kõike põhikontekstis. Kui vajad kokkuvõtet, arvu või vastust konkreetsele küsimusele, delegeeri nii hankimine *kui ka* tõlgendamine alamagendile. Alamagent teeb raske lugemise; sina saad tagasi 200 sõna 25 kilobaidi asemel.

**Õige host, mitte ainult õige tööriist.** Tööriistadistsipliin ulatub ka sinna, *kus* tööriistad jooksevad. Kui sul on kiire tagasisidega orkestreerija-host ja eraldi raske arvutusvõimsusega täitja, kuulub pikaajaline töö täitjale. Ehitused, testikomplektid, ETL — miski neist ei peaks jooksma hostil, mida püüad reageerimisvõimelisena hoida. Sümptom: „kõik tundub aeglane", kuigi täitja on jõude. Põhjus: raske töö jooksutamine interaktiivsel hostil.

### Edasilükatud tööriistad ja ToolSearch

Enamik tööriistu ei ole vaikimisi laaditud. Enne kui haarad ühekordse `ToolSearch`-i järele, et laadida üksainus tööriist, küsi, kas on olemas loogiline kimp. Üks otsing, mis nimetab tööriistakomplekti, tagastab kogu komplekti ühe edasi-tagasi käiguga. Tööriistade ühekaupa laadimine on raisatud lisakulu; rohkema laadimine, kui vaja, raiskab teistsugust lisakulu. Laadi selle valdkonna kimp, kuhu sisened.

### Millal kasutada millist tööriistataset välise süsteemi jaoks

| Tase | Mis see on | Millal |
|------|------------|------|
| Spetsiaalne MCP | Otstarbekohaselt ehitatud integratsioon konkreetse süsteemi jaoks | Eelista alati, kui see olemas on |
| Brauseri MCP | Juhi brauserit navigeerimiseks ja andmete väljavõtmiseks | Kui spetsiaalset MCP-d pole |
| Arvutikasutus (computer-use) | Tõlgenda piksleid töölaual | Viimane abinõu — habras, aeglane |

Liigu tasemetes allapoole ainult siis, kui ülemised tasemed pole saadaval või jäävad väheseks.

### Uurija-ajaloolane

Ajaloolane töötab läbi mitusada digiteeritud välimärkmikku, mis on laiali temaatilistes alamkaustades. Tal on vaja leida iga viide konkreetsele mõõdistusinstrumendile, lugeda asjakohased lõigud läbi ja seejärel muuta esseemustandit, asendades aegunud nime.

Tema esimene instinkt: avada failid ükshaaval. `cat` esimese kausta loendile, kümme faili järjest läbi lugeda, kaks viidet leida. Ta on 10% peal ja tema kontekst on täis faile, milles polnud midagi kasulikku.

Ta alustab otsast. Üks `Grep`-i kutse üle kogu arhiivi — rekursiivne, reanumbrite ja kontekstiga. 23 vastet 14 failis, tagastatud paarisaja tokeniga. Seejärel 14 paralleelset `Read`-i kutset, piiratud kitsa reavahemikuga iga vaste ümber. Tema kontekst hoiab nüüd täpselt neid lõike, mida ta vajab. Lõpuks `Edit` koos `replace_all`-iga, et instrument kogu essees ümber nimetada: üks kutse, ei mingit regexit, puhas diff.

Kolm käiku mitmekümne asemel. Kontekst hoiab tõendeid ja arutluskäiku, mitte sadu ridu ebaolulist materjali.

### Tõrkemustrid

**`cat` `Read` asemel.** Ei reanumbreid, ei auditijälge, loaküsimused. Ainus võitja on harjumus.

**`sed` `Edit` asemel.** Pime regex-asendus ilma diffita. `Edit` sunnib sind selgelt välja ütlema, mida muudad, ja tõrgub turvaliselt, kui sihtstringi ei leita.

**Sõltumatute otsingute järjestamine.** Puhas surnud aeg. „Igaks juhuks" ei ole turvaline; see on lihtsalt aeglane.

**Suure tulemuse tõmbamine põhikonteksti.** 20 KB logi põhikontekstis võtab ruumi, mis peaks hoidma sinu arutluskäiku. Kui sul on vaja „vigu selles logis", siis logi ise ei olnud see, mida sa vajasid.

**Arvutikasutus, kui olemas on natiivne MCP.** Pikslipõhine suhtlus läheb paigutuse muutudes katki. API-põhine suhtlus mitte.

**Raske töö orkestreerija-hostil.** Lükka see täitjale, kuhu see kuulub.

**Kaks sama nimega tööriista masinas, mis osutavad eri ekraanidele.** Mõni võimekus on seadistuses kahes eksemplaris — kaks viisi „brauseri avamiseks", kaks viisi „sõnumi saatmiseks", kaks viisi „käsu jooksutamiseks masinal" — ja need erinevad ainult selle poolest, *millisel masinal need maanduvad*. Üks juhib brauserit serveris; teine juhib brauserit laual sinu ees. Mõlemad teatavad edust. Ainult üks neist on vaatajale nähtav. Kui sinu püsijuhised kuulutavad ühe neist „selleks" tööriistaks selle töö jaoks, haarab iga seanss refleksiivselt selle järele — ka juhul, kus see on täpselt vale —, ja kasutaja vaatab, kuidas tema ekraanil ei juhtu midagi, samal ajal kui talle öeldakse, et tehtud. Parandus on kirjutada juhisesse *eristaja*, mitte vaikeväärtus: mitte „X on brauser", vaid „kui inimene vaatab tulemust, kasuta seda, mis on tema ekraani küljes; kui keegi ei vaata, kasuta peata oma". Üldine vorm: kui kaks tööriista teevad sama tegusõna, peab reegel nimetama tingimuse, mis nende vahel valib, sest paljas vaikeväärtus on mündivise, mis maandub alati samale poolele. Ja märk on eksimatu — kui keegi kordab sulle masina nime, ei ole see rõhutus, see on parameeter.

**Rätsepatööriista tellimine, kui omaks võetud tööriist on olemas.** Tööriistadistsipliin kehtib ka selle kohta, mida sa palud abilisel *ehitada*, mitte ainult selle kohta, mille järele ta seansis haarab. Nii võimekas abiline ehitab sulle rõõmuga kohandatud armatuurlaua mille tahes jaoks — ja armatuurlaud on tore nädal pärast valmimist. Siis miski liigub, käsitsi hooldatud nimekiri selle taga jääb tegelikkusest maha ja seda lakatakse vaikselt avamast. Läbikukkumine ei ole tehnoloogiapinus; see on selles, et see üldse rätsepatöö on. Enne olekupinna või operatsioonitööriista tellimist küsi, mida sa ausalt iga päev avaksid — kui vastus langeb kokku olemasoleva, aktiivselt hooldatava tööriistaga, võta hoopis see omaks. Ehita kohandatult ainult siis, kui ükski omaks võetud tööriist vajadust ei kata *ja* tulemus suudab oma andmed tuletada elavalt olemasolevast tõeallikast, mitte nimekirjast, mida keegi peab pidevalt uuendama.

**Olekuvälja usaldamine artefakti asemel.** Süsteemid, mis teevad aeglast tööd, paljastavad tavaliselt edenemisvälja — oleku, protsendi, „valmis". On ahvatlev käsitleda seda välja vastusena küsimusele „kas on tehtud", sest see on kujundatud nägema välja täpselt nii. Aga olekuväli on *väide, mille süsteem enda kohta esitab*, ja see võib olla vale kõigis suundades korraga: teatab, et järjekorras pole midagi, kui töö istub järjekorras; teatab tõrkest, kui töö on terve ja ootab; hoiab vananenud viga kaua pärast õnnestunud kordust; ja teatab valmimisest, enne kui väljund olemas on. Iga neist valelugemitest toodab erineva halva otsuse — hüljatakse töö, mis oli korras, korratakse seda, mis juba jooksis, kuulutatakse edu, enne kui on midagi üle anda. Lahendus on reegel tõendite kohta: **otsusta valmimine artefakti, mitte oleku järgi.** Kas väljundil on tegelik suurus, tegelik kestus, kas selle toomine tagastab tõesti baite? Need ei saa olla valed nii, nagu vahemällu salvestatud väli saab. Jäta olekuväli selleks, milleks see tõeliselt hea on — umbkaudne edenemisnäidik vaatavale inimesele —, ja ära kunagi selle põhjal harune.

**Puudumine dokumenteeritud pinnalt ei ole puudumine süsteemist.** Kui vajad võimekust ja viitematerjal seda ei loetle, on aus järeldus „dokumenteerimata", mitte „ei toetata". Vahe on tohutult oluline, sest puuduva võimekuse ümbernurgalahendus on tavaliselt kallis ja sekkuv — suure hulga objektide muutmine või käsitsi ülesehitamine millegi, mida süsteem juba teeb. Dokumentatsioon jääb teostusest maha loomuliku asjade käiguna: eelmisel nädalal välja lastud funktsioon on koodis reaalne ja igast juhendist puudu. Enne kui pühendud ümbernurgalahendusele, mille plahvatusraadius on suur, kuluta kaks minutit tegeliku liidese lugemisele — lähtekood, skeem, genereeritud API kirjeldus. Üldine reegel skaleerub koos eksimise hinnaga: mida rohkem objekte sinu ümbernurgalahendus puudutaks, seda enam oled kohustatud tõestama, et otsetee puudub. Kui avastad end plaanimas muuta kümneid asju, et saavutada seda, mida üks parameeter teeks, on see märk minna ja vaadata.

**Õnnestunud sond ei ole see kutse, mida sa tegema hakkad.** Enne API kaudu töötamist kontrollid, kas sa selleni ulatud, ja kontroll on loomulikult kõige odavam saadaolev kutse — lugemine, tervisekontrolli otspunkt, loend. See tuleb tagasi puhtalt ja ligipääs tundub kindel. Aga volitustel on *ulatused (scopes)* ja ulatus, mis lubab sul lugeda, ei ole rutiinselt see ulatus, mis lubab sul kirjutada. Tõrge ilmneb siis muutva kutse juures, pärast seda, kui plaan on kinnitatud ja mitu sammu on juba jooksnud, ja see loeb pigem katkestusena kui sellena, mis see on: luba, mida sul kunagi ei olnud. Samal lõksul on ka võrguvariant — aadress, mida sondeerisid ühelt masinalt, ei ole aadress, mida töö kasutab teiselt, ja sinu laual kättesaadav otspunkt võib olla kättesaamatu masinast, mis tööd jooksutab. Sondeeri selle operatsiooniga, mida tegelikult teha kavatsed, sama volitusega, samast kohast. Äravisatava objekti loomine ja kustutamine võidab õnnestunud lugemist iga kord. Seal, kus selle harjutamine on tõesti liiga hävitav, loe hoopis volituse enda ulatuste loendit, selle asemel et tuletada volitatust faktist, et leht laadis.

**Brauseri juhtimine loeb kõike, mida leht hoiab.** Brauseritööriistad on õige vastus, kui süsteemil pole API-t, ja neil on omadus, mida teistel tasemetel ei ole: see, mis tagasi tuleb, ei ole piiratud sellega, mida küsisid. Skript, mis loetleb lehe lingid, et leida see, millel klõpsata, tagastab *iga* lingi — ja autenditud rakenduses on navigatsioon ise sisu. Suuna see sisselogitud sõnumirakenduse pihta ja saad vestluste loendi koos sõnumite eelvaadetega; postkliendi pihta — teemaread; panga pihta — kontode nimed ja saldod. Kõik see maandub transkriptis, mis on dokument, mis püsib, sünkroonitakse ja mida vahel jagatakse. Lõksu teine pool on see, et autentimisolek on liikuv sihtmärk. Profiil, mida nägid tund tagasi väljalogituna, võib nüüd olla sisse logitud — kas sellepärast, et inimene istus selle taha, või sellepärast, et leht lõpetas autentimise pärast seda, kui sina vaatasid —, nii et kinnitusel „see profiil pole kuhugi sisse logitud" on säilivusaeg, mida mõõdetakse minutites. Kaks harjumust sulgevad selle: piira valija ühe elemendiga, mida vajad, selle asemel et lehte loendada, ja kontrolli autentimisolek uuesti vahetult enne tegutsemist mis tahes profiilil, mida ka inimene kasutab. Mitte seansi alguses ja mitte kunagi märkme põhjal.

**Fakti lugemine alladiskreeditud pildilt.** Nägemistööriistad panevad pildid tunduma lihtsalt järjekordse loetava pinnana, ja enamasti see nii ongi — aga pisipildil, kontaktlehel või vähendatud ekraanipildil on tähemärgid hävitatud enne, kui mudel neid üldse näeb. See, mis tagasi tuleb, ei ole lugemine; see on rekonstruktsioon, kokku pandud mis tahes usutavast asjast, mis kujuga sobib. Ja see on usutav: tõeline kohanimi, tõeline inimene, õiges vormingus seerianumber, õige arvu numbrikohtadega summa. Just see teebki selle ohtlikuks — see loeb pigem teadmisena kui oletusena, nii et miski vastuses ei kutsu kontrollima. Kahju kuhjub, kui oletusest saab nimi: kaust, fail, kirje, üleantav töö, mis on pealkirjastatud fakti järgi, mida seal kunagi polnud, ja mis seejärel levib edasi, nagu oleks see kontrollitud. Distsipliin on väike ja absoluutne. Enne kui väidad midagi, mis on pildilt loetud — sildid, etiketid, andmeplaadid, ekraanid, käekiri, number arvel —, lõika see piirkond välja ja renderda täislahutusega, seejärel loe uuesti. Kui seda ikka ei õnnestu lahendada, ütle seda ja nimeta, mis takistab; „kontrollimata" on täiesti hea vastus ja väljamõeldud kohanimi ei ole. Pisipildid on triaaži jaoks — kas see on fookuses, kas see on duplikaat, kas see on õige kaader. Need ei ole tekstiallikas.

### Lühike rusikareegel

Kasuta kõige spetsiifilisemat tööriista, mis töö ära teeb. Koonda iga sõltumatu kutse samasse käiku. Suuna suured väljundid alamagendi kaudu ja too tagasi ainult tuletatud tulemus. Laadi edasilükatud tööriistakimbud korraga, mitte ühe tööriista kaupa.

---

# 4. osa — Tervikuks kokku

## Läbikäidud näide: Alex ja konsultatsioonifirma

Alex peab üheinimese-IT-konsultatsioonifirmat, mis teenindab kuut väikest tootmisettevõtet. Erinevad pilveteenuse pakkujad, erinev kohapealne riistvara, erinevad hoolduslepingud. Korduvad igakuised tervisekontrollid, perioodilised turvaülevaatused, muudatustaotlused, aeg-ajalt intsidendid. Alex on ühtaegu strateeg, insener, dokumenteerija ja kliendihaldur.

Üldotstarbeline vestlusabiline, mis alustab iga seanssi nullist, ei ole siin kasulik tööriist. Korralikult üles ehitatud seadistus on.

### Milline Alexi seadistus välja näeb

**Mälusalv.** Umbes kakskümmend kirjet nelja tüübi peale. Kaks `user`-faili hoiavad püsivaid eelistusi. Kuus `project`-faili, üks kliendi kohta, sisaldavad taristu ülevaadet, seadistusrepositooriumi asukohta, juba tehtud otsuseid ja teadaolevaid veidrusi. Kasvav kogum `feedback`-faile dokumenteerib raske vaevaga õpitud õppetunde — miks ühe kliendi tulemüür tervisekontrolle vaikselt maha viskab (oodatud käitumine, mitte tõrge); et teise kliendi muudatuste kinnitamine nõuab 48-tunnist etteteatamist. Mitu `reference`-faili hoiavad tarnijate API-de veidrusi.

**Oskused.** Oskus `/monthly-health-check` võtab kliendi nime, loeb kliendi projektimälufaili, käivitab kontrollide jada ja koostab vormindatud aruande. Oskus `/change-request` visandab ulatusdokumendi. Oskus `/incident-triage` algab struktureeritud sümptomite kogumisega. Iga oskus loeb väljakutsel mälu, nii et üks määratlus teenib kõiki kuut klienti.

**Alamagendid.** Agent `security-analyst` — tööriistadeks ainult `Read` ja `Write` — vaatab seadistusfailid läbi turvakõvendamise kontrollnimekirja alusel. `documentation-drafter` tegeleb mahuka kirjutamisega. Kui turvaülevaatus hõlmab kolme sõltumatut alamsüsteemi, saadab Alex kolm analüütikut paralleelselt teele.

**Haagid.** `PreToolUse`-haak tööriistadel `Write` ja `Edit` blokeerib kõik, mis on suunatud kliendi tootmisseadistuse kausta, kui abiline ei väljasta enne selget kinnitust. `SessionStart`-haak süstib sisse tänase kuupäeva ja kontrollib öist postkasti. `Stop`-haak saadab Telegrami sõnumi, kui pikk seanss lõpeb.

**CLAUDE.md.** Kasutajaülene fail klientideüleste tavadega — majastiil klientidele suunatud aruannete jaoks, reegel, et hostinimesid ei kirjutata kunagi lihttekstina väljunditesse, mis võidakse väljaspool arhiveerida. Projekti ulatusega fail iga kliendi töökausta juurikas hoiab selle kliendi tõlgendusraami: kaherealine sõnastik, püsivad piirangud („muudatusaknad on ainult reedel kell 21 kuni laupäeval kell 6") ja viited asjakohasele mälufailile.

**Püsivuse redel.** Seansisisesed ülesanded tänase tervisekontrolli jaoks. Plaanifail asukohas `~/.claude/plans/client-x-upgrade.md` kuuenädalase mitmeetapilise uuenduse jaoks. Mälu sertifikaadivahetuse protseduuri jaoks, mis osutub kehtivaks nelja kliendi puhul. Tööpuud (worktrees) riskantsete arhitektuurimuudatuste jaoks, mis ei pruugi õnnestuda.

**Asünkroonsus.** Kõigi kuue kliendi tervisekontrollid jooksevad reede pärastlõunati taustal alamagentidena. Igaüks saadab „alustan"-teate ja lõpetamisel kokkuvõtte. Kui kontroll satub millelegi, mis vajab otsust, teeb see pausi ja annab kohe märku. Telefonipoolne veebihaak (webhook) lisab sõnumid postkastifaili, mille järgmine seanss esimese asjana ette võtab.

**Mitu agenti.** Kriitikuagent vaatab turvaaruannete mustandid üle, enne kui need kliendile lähevad. Teise arvamuse agent käivitub kõrge panusega muudatustaotluste ulatuse määramisel, kui tagasipööramise keerukus on märkimisväärne.

**Tööriistadistsipliin.** Paralleelsed `Grep`-kutsed, kui otsitakse teenusenimesid seadistusrepositooriumitest. `Read` piiratud reavahemikega, mitte tervete failide väljavõtted. `Edit` mallide jaoks, mitte `sed`. Tarnijate MCP-d laaditakse kimpudena. Raske töö lükatakse täiturhostile.

### Kasutuselevõtu kaar

| Aeg | Mida ehitada | Mida see sulle annab |
|------|---------------|-------------------|
| 1. nädal | Üks `user`-mälufail. Üks `project`-mälufail. Kümnerealine `CLAUDE.md`. `SessionStart`-haak tänase kuupäeva jaoks. | Seansid ei alga enam nullist. |
| 1. kuu | Kolm oskust kõige sagedamini korduvate protseduuride jaoks. `feedback`-fail pärast esimest välditavat viga. Plaanifail iga töö jaoks, mis ulatub üle mitme seansi. Üks alamagent ühe kategooria raske töö jaoks. | Kordamine lakkab olemast maks. |
| 1. kvartal | Kaitsev haak teel, mida ei tohi puutuda. Üks väljuv teavituskanal ühendatud ja testitud. Üks taustatöö otsast lõpuni läbi jooksutatud. Mäluindeks kärbitud. | Pikad tööd jooksevad sel ajal, kui sina oma elu elad. |
| 1. aasta | Tosin mälukirjet, enamasti tagasiside. Kuus kuni kümme oskust. Kaks-kolm alamagendi määratlust. Haagid, mis on päris probleeme kinni püüdnud. Mitme agendiga kriitikutsüklid kaalukate tulemite peal. | Töökeskkond, mis kuhjub kokku, selle asemel et nullistuda. |

### Millal MITTE vaeva näha

Selle juhendi mustrid tasuvad end ära siis, kui töö kuhjub — kui oled samas projektis ka homme, järgmisel nädalal, järgmisel kuul; kui samad protseduurid korduvad; kui samad vead võivad üha uuesti juhtuda. Need ei tasu end ära ühekordsete küsimuste, äravisatavate skriptide või uurimistöö puhul, mille juurde sa kunagi tagasi ei tule.

Ära ehita mälusalve projektile, mille sel nädalal lõpetad.
Ära kirjuta oskust millegi jaoks, mida teed ühe korra.
Ära kirjuta haaki reegli jaoks, mida niikuinii keegi kunagi ei rikuks.
Ära lisa agenti, kui lähteülesande teravdamine lahendaks probleemi.

Süsteem teenib tööd, mitte vastupidi.

---

## Kuhu edasi

Kui sind tõi siia mingi konkreetne hõõrdumine, mine otse selle peatüki juurde:

- *Ma pean end seansi alguses üha uuesti selgitama.* → 1. peatükk (CLAUDE.md) ja 2. peatükk (Mälu).
- *Ma teen sama mitmesammulist protseduuri ikka ja jälle käsitsi.* → 3. peatükk (Oskused).
- *Midagi, mida ei tohiks puutuda, saab üha uuesti puudutatud.* → 4. peatükk (Haagid).
- *Mu põhiseanss on alati suurte väljunditega ummistunud.* → 5. peatükk (Alamagendid) ja 9. peatükk (Tööriistadistsipliin).
- *Ma tahan, et pikad tööd jookseksid sel ajal, kui mind ei ole.* → 7. peatükk (Asünkroonsus).
- *Kõrge panusega tulem vajab külma teist pilku.* → 8. peatükk (Mitu agenti).

Kui alustad nullist, on soovitatav järjekord: 1. peatükk, siis 2. peatükk, siis 3. peatükk. Kolm peatükki ja oled kõige tavalisemast hõõrdumisest juba üle.

Süsteem, mille sa ehitad, ei pea välja nägema nagu Alexi oma. Sambad on samad; kuju, mille nad sinu töös võtavad, on teistsugune. Kaardista mustrid sellele, mida sina teed — kus on sinu püsiv kontekst, millised protseduurid korduvad, milline töö võidaks spetsialistist, millised invariandid peavad alati kehtima. Vastused on sinu omad.

---

## Lõpetuseks

Claude Code'i meisterlik valdamine ei seisne paremates viipades. See seisneb õige püsiva struktuuri valimises iga teadmise, protseduuri, eksperdi ja kaitsepiirde jaoks, mida su töö vajab. Nutikalt sõnastatud juhis vestlusaknas on habras. Sama kavatsus, väljendatuna mälufaili, oskuse, alamagendi lähteülesande või haagina, on vastupidav. Nädalate ja kuudega hästi struktureeritud seadistus paraneb; viipade meisterdamise praktika käib alla, sest lõhe selle vahel, mida sa meelde tuletad öelda, ja selle vahel, mida seanss teadma peab, läheb aina laiemaks.

Ehita järk-järgult. Lisa järgmine sammas siis, kui tunned hõõrdumist, mida see lahendab. Eesmärk ei ole kõik üheksa sammast töös hoida — eesmärk on hoida töös õiged sambad selle töö jaoks, mida täna teed, ja omada selget teed järgmise lisamiseks, kui töö seda nõuab.

---

# Lisa — süsteemiviip LLM-ile

> *See osa ei ole sinu jaoks. See on kopeeri-ja-kleebi-koorem puhta LLM-i seansi jaoks — selline, mille võid pista värskesse Claude'i (või mõne muu mudeli) vestlusse, et viia see kurssi selle juhendi sisuga. Jäta vahele. Või kui tahaksid vestelda tehisintellektiga, kellel see juhend peas on, kopeeri kõik joone alt uude vestlusse.*

---

```
Sa hakkad abistama kasutajat, kes õpib Claude Code'i — Anthropicu
terminalipõhist kodeerimisabilist. Ta on lugenud juhendit nimega
„Mastering Claude Code". Omanda järgnev selle juhendi tihendatud
versioon ja vasta tema küsimustele lihtsas, sõbralikus keeles.
Väldi erialaslängi. Ole konkreetne. Kasuta näiteid väljastpoolt
tarkvaramaailma, kui need aitavad.

ÜHEKSA SAMMAST

1. CLAUDE.md — lihttekstifail projekti juurikas (või kaustas
   ~/.claude/ kasutaja ulatuse jaoks), mida Claude loeb iga seansi
   alguses. Kasuta seda püsiva konteksti jaoks: mis projekt see on,
   kus asjad asuvad, tavad, lõksud ja viited ülejäänud seadistusele.
   Hoia see alla 150 rea. Ära pane siia kunagi saladusi, praeguse
   ülesande olekut ega kõvasid reegleid, mida ei tohi rikkuda.

2. Mälu — kaust väikseid tekstifaile asukohas
   ~/.claude/projects/<slug>/memory/, mida Claude loeb valikuliselt
   indeksfaili (MEMORY.md) kaudu. Neli tüüpi: user (kes sa oled),
   feedback (õppetunnid vigadest), project (aktiivse ettevõtmise
   jooksev kontekst), reference (püsivad välised faktid). Kõige
   rohkem kasutatakse feedback- ja project-tüüpi. Mälu kannab
   põhimõtteid ja püsivaid fakte, mitte edenemist.

3. Oskused — nimelised protseduurid, mis on salvestatud Markdown-
   failidena asukohas ~/.claude/skills/<name>/SKILL.md. Päises on
   nimi, kirjeldus (mille järgi Claude otsustab automaatse
   väljakutse) ja lubatud tööriistade nimekiri. Sisu on protseduur.
   Kirjuta /name, et see otse välja kutsuda; Claude võib selle ka
   kirjelduse põhjal ise ennetavalt käivitada. Kolmanda korra
   reegel: kui protseduuri on kolm korda selgitatud, kuulub see
   oskusesse. Teine liik, *protsessioskused*, kodeerib, kuidas
   läheneda tervele tööklassile, ja käivitub enne seda —
   ajurünnak enne ehitamist, test-enne-koodi — ning neid
   tarnitakse üha enam paigaldatavate pluginapakkidena.

4. Haagid — kestaskriptid, mis on seotud elutsükli sündmustega
   (SessionStart, PreToolUse, PostToolUse, Stop jne) failis
   settings.json. Jooksevad deterministlikult; väljumiskood 0 lubab
   sündmuse, nullist erinev blokeerib selle. Kasuta reeglite jaoks,
   mis peavad kehtima iga kord — kaitsvad valvurid, konteksti
   süstimine, teavitused, auditilogid. Test: kui reegli ühekordse
   vahelejätmise tagajärg on päris, kuulub see haaki, mitte
   CLAUDE.md-sse. Haagid, mis kirjutavad jagatud olekut (lukud,
   möödaviigulipud), peavad selle piirama seansi kaupa — pane
   seansi ID failinimesse —, muidu lekib ühe seansi olek teise.

5. Alamagendid — Claude'i teised koopiad oma määratlusfailidega
   asukohas ~/.claude/agents/<name>.md. Saavad külma lähteülesande
   (ei mäleta sinu vestlust), kannavad ainult lubatud tööriistu,
   võivad joosta eri mudelitel (haiku/sonnet/opus). Kasutatakse:
   kontekstihügieeniks (suured väljundid jäävad põhikontekstist
   välja), paralleelsuseks (N ülesannet korraga),
   spetsialiseerumiseks (sihitud vaatenurk lööb üldise seansi).
   Väljakutsel antud lähteülesanne loeb sama palju kui määratlus.
   Jälgi õdede-vendade kokkupõrkeid lamedas hargnemises; kasuta
   haldur-agenti, kui töölised jagavad sama disainiruumi.

6. Püsivuse redel — olek neljas ulatuses:
   - Ülesanded (seansisisesed, surevad koos seansiga)
   - Plaanid (~/.claude/plans/<slug>.md, elavad nii kaua kui
     projekt)
   - Mälu (tähtajatu, projektideülene)
   - Tööpuud / liivakastid (paralleelsed harud, kuni need
     ühendatakse või hüljatakse)
   Distsipliin: vali väikseim sobiv ulatus. Plaani olek mälus
   mürgitab tulevased seansid. Tavad ülesannetes aurustuvad.

7. Asünkroonsus ja teavitused — väljuv tõuge (`notify`-mähis
   sinu valitud tõukekanali ümber), sissetulev postkast (järjekord,
   mille Claude seansi alguses ette võtab), taustajooksud
   (run_in_background: true Bash- ja Agent-kutsetel), Monitor-
   tööriist voogväljundi jaoks. Rütm: alla viie minuti hoiab
   viipavahemälu sooja; 5–60 min maksab vahemälu möödalaskmise;
   pikem ei loe. Ainult sisulised teavitused — mitte
   tegevusmüra. Uus kasutaja sõnum on alati katkestus, mitte
   kunagi jooksva ülesande taha järjekorda pandud.

8. Mitme agendiga mustrid — kriitikutsükkel, planeerija/täituri
   lahutus, teine arvamus, paralleelne hargnemine koos sünteesiga,
   ehita-ja-hinda. Kasuta siis, kui töö vajab vaatenurka, mida üks
   agent ise võtta ei saa (sõltumatu pilk omaenda väljundile), kui
   paralleelsus loeb või kui läbikukkumise hind ületab kaugelt
   lisaagendi hinna. Esimene käik on peaaegu alati lähteülesande
   teravdamine; lisa agent ainult siis, kui teravdamine probleemi
   ei lahenda. Kriitikute koosseis ei tohiks olla monokultuur —
   kaasa vähemalt üks operaatorikogemuse vaatenurk. Kui töö kuju on
   teada, anna juhtimisvoog deterministlikule töövoole — konveier
   (iga üksus voolab sõltumatult), tõke (kogu-kõik-kokku enne
   järgmist etappi), tsükkel-kuni-kuiv, vastandlik kontroll,
   kohtunike paneel. Luura kõigepealt käsitsi, siis orkestreeri.
   Hoia ammendav režiim — kontrolli kõvemini, hargne laiemalt —
   otsuste jaoks, mille valesti tegemine on kallis.

9. Tööriistadistsipliin — spetsiaalsed failitööriistad (Read, Edit,
   Write, Grep, Glob) kesta vastete asemel. Paralleelsed kutsed, kui
   töö on sõltumatu. Alamagent kontekstipuhvrina suurte väljundite
   jaoks. Õige host: raske töö kuulub täiturile, mitte
   orkestreerijale. Edasilükatud tööriistad laaditakse kimpudena
   ToolSearchi kaudu, mitte ükshaaval. Astmestik välissüsteemide
   jaoks: spetsiaalne MCP > brauseri MCP > arvutikasutus.

MUSTRID, MIS KORDUVAD ÜLE SAMMASTE
- Külm lähteülesanne: agendid, kes vajavad sõltumatut vaatenurka,
  ei tohi näha eelnevat arutluskäiku.
- Loe diffi, mitte kokkuvõtet: agendi enesekindel „valmis"-raport
  ei ole kontroll.
- Kolmanda korra test: kui selgitad midagi kolm korda, kirjuta see
  üles (oskus, mälu, CLAUDE.md, haak — mis iganes sobib).
- Õige koht igale reeglile: püsiv kontekst → CLAUDE.md;
  teadmine → mälu; protseduur → oskus; invariant → haak.
- Päritolu: iga mäluväide viitab oma allikale; märgi järeldused
  järeldatuks, et need ei kivistuks faktiks.
- Käitumuslikud vaikeväärtused löövad projektifakte: tegutse, kui
  oled volitatud, püsi oma rajal, otsi enne küsimist, kalibreeri
  enesekindlust, tõendid enne „valmis".

KASUTUSELEVÕTU JÄRJEKORD
1. nädal: üks user-mälufail, üks project-mälufail, kümnerealine
CLAUDE.md, SessionStart-haak tänase kuupäeva jaoks.
1. kuu: kolm oskust kõige sagedamini korduvate protseduuride jaoks,
feedback-fail pärast esimest välditavat viga, plaanifail iga
mitmeseansilise töö jaoks, üks alamagent raske töö jaoks.
1. kvartal: kaitsev haak külmutatud teel, väljuv teavituskanal,
üks taustajooks, mälu kärpimine.
1. aasta: tosin mälukirjet, kuus kuni kümme oskust, kaks-kolm
alamagendi määratlust, mitme agendiga kriitikutsüklid kõrge
panusega tulemite peal.

MILLAL MITTE VAEVA NÄHA
Ära ehita mälu projektile, mis sel nädalal lõpeb. Ära kirjuta
oskust millegi jaoks, mida tehakse üks kord. Ära kirjuta haaki
reegli jaoks, mida keegi kunagi ei rikuks. Ära lisa agenti, kui
lähteülesande teravdamine lahendaks probleemi.

Nüüd võid kasutaja küsimustele vastata. Hoia vastused konkreetsed
ja lühikesed. Kui ta kirjeldab hõõrdumist, nimeta konkreetne
sammas, mis sellega tegeleb, ja juhata ta läbi minimaalse esimese
sammu. Kasuta analoogiaid väljastpoolt tarkvaramaailma, kui see
on kasulik.
```

---

*Juhendi lõpp. Viimase kümne nädala uuendused elavad kaustas `updates/` — alusta failist `updates/index.md` koondülevaate saamiseks või ava `updates/week-NN.md` mis tahes konkreetse nädala kohta.*

