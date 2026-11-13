# h4 NFC ja RFID

## a) Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Lähdin tutkimaan omia tuotteita, jotka voisivat sisältää RFID ominaisuuksia ja löysin ainakin nämä:  
````
Työpaikan HID-kulkulätkä
Maksukortti
Passi
iLOQ avain
Apple Watch
Iphone 15 Pro
RFID Safe lompakko
````
Googlasin näiden tuotteiden RFID ominaisuuksia. HID käyttää RFID teknologiaa, mutta en löytänyt työpaikkani käyttämää lätkää HID:in sivuilta. Mutta todennököisesti työpaikkani HID-kulkulätkä hyödyntää RFID:tä.  
Suomen passeissa on RFID siru, joka sisältää henkilötiedot, kasvokuvan ja sormenjäljet.  
RFID safe lompakko, minkä pitäisi suojata maksukorttiani.  
Sitten maksukorttini, puhelimeni, kelloni ja kotiavaimeni. Nämä käyttävät NFC-teknologiaa, joka on RFID:n alamuoto. Esim. Maksukortin, puhelimen ja kellon lähimaksuominaisuus käyttää NFC:tä ja iLOQ-avain pystyy kommunikoimaan langattomasti ulko-oven lukijan kanssa NFC:n takia.  
Maksukorttini osalta olen suojautunut kohtuullisen hyvin RFID-urkinnalta lompakkoni ansiosta, mutta en tosiaan tiedä kuinka hyvä suoja siinä oikeasti on.  
Passi, puhelimeni, kelloni ja avaimeni hyödyntävät niiden omia suojausominaisuuksia.  
Passi käyttää PACE-protokollaa, joka suojaa passin sirua ja lukulaitteen välistä NFC-tiedonsiirtoa salakuuntelulta ja luvattomalta lukemiselta.  
Applen tuotteet käyttävät "Secure Element" toimintoa, mikä on suojattu ympäristö, joka pitää sisällään maksamiseen liittyvät arkaluontoiset tiedot. Maksutapahtumat myös yleensä vaativat biometrisen tunnistautumisen.  
iLOQ avain käyttää AES256-salausta, kaksisuuntaista todennusta ja jokaisella avaimella on yksilöllinen tunniste. Avaimesta voidaan myös poistaa kulkuoikeudet, jos se katoaa tai päätyy vääriin käsiin.  
Työpaikan kulkukortin suojasta ei ole mitään tietoa, kun en löytänyt kyseistä lätkää valmistajan sivuilta.  
Tässä oli nyt aika tiivistetysti tuotteiden joitakin omia suojausominaisuuksia, niitä löytyy vielä lisää.  
Eli sanoisin, että ihan kohtuullisen hyvin olen suojatunut RFID-urkinnalta, jos vaan lompakon ja muiden laitteiden suojat pitävät oikeasti paikkaansa.  


## b) Tutustu APDU komentojen rakenteeseen

APDU komentojen rakenteen tutustumiseen käytin tekoälyä ChatGPT.  
Application Protocol Data Unit, APDU on komentorakenne, jota käytetään älykorttien ja niitä lukevien laitteiden välisessä tiedonsiirrossa.  
APDU-komentoja käytetää esim. Maksukorteissa, passeissa, SIM-korteissa ja NFC-korteissa. APDU-komentojen avulla lukijalaite voi lähettää kortille komentoja ja pyytää siltä tietoja.  
APDU-komento koostuu useista kentistä. Komennon perusrakenne sisältää neljä pakollista kenttää:  
````
CLA, INS, P1 ja P2
````
Näiden lisäksi komennossa voi olla datan pituuden ilmoittava Lc-kenttä, varsinainen Data-kenttä sekä vastauksen odotettua pituutta kuvaava Le-kenttä.  
````
CLA - Määrittelee komennon luokan.
INS - Määrittelee suoritettavan toiminnon.
P1 - Ensimmäinen komentoon liittyvä parametri.
P2 - Toinen komentoon liittyvä parametri.
Lc - Ilmoittaa lähetettävän datan pituuden tavuina.
Data - Sisältää komennon mukana lähetettävän tiedon.
Le - Ilmoittaa, kuinka paljon dataa odotetaan kortilta vastaukseksi.
````
APDU-komentojen rakenne riippuu siitä, mitä komentoa ollaan suorittamassa. Sen takia kaikki kentät eivät ole jokaisessa APDU-komennossa mukana.  
Kun älykortti vastaanottaa APDU-komennon, se käsittelee sen ja lähettää lukijalaitteelle **vastaus-APDU**:n.  
Vastaus sisältää mahdollisesti kortin palauttamaa dataa sekä kaksi tilakoodia, **SW1** ja **SW2**.  
Näiden tilakoodien avulla lukijalaite saa tiedon siitä, onnistuiko komennon suorittaminen vai tapahtuiko jokin virhe.  
Esim. Tilakoodi **90 00** tarkoittaa, että komento suoritettiin onnistuneesti ja tilakoodi **6A 82** tarkoittaa, että pyydettyä tiedostoa tai kohdetta ei löytynyt.  
**SELECT**-komento on yksi esimerkki APDU-komennosta. **SELECT**-komennolla lukijalaite voi valita älykortilta tietyn sovelluksen tai tiedoston. Tämän komennon avulla lukijalaite voi esim. Aloittaa kommunikoinnin tietyn korttisovelluksen kanssa.  
Eli APDU-komennoilla älykortit ja eri laitteet pystyvät kommunikoimaan keskenään yhdenmukaisella tavalla.  


## c) Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutiset löysit. 

Löysin **The Hacker News** -sivustolta vuonna 2018 julkaistun uutisen, jossa kerrottiin F-Securen tietoturvatutkijoiden **Tomi Tuomisen** ja **Timo Hirvosen** löytämästä haavoittuvuudesta hotellien sähköisissä lukitusjärjestelmissä.  
Haavoittuvuus koski **Assa Abloyn** valmistamaa **Vision By VingCard** lukitusjärjestelmää, jota käytettiin yli 42000 kiinteistössä, 166 eri maassa.  
**Tuominen** ja **Hirvonen** onnistuivat rakentamaan "Master Key":n, jolla pystyi avaamaan kaikki hotellihuoneet jotka käyttivät kyseistä järjestelmää.  
Master Key:n luomiseen tarvitaan vain yksi järjestelmään kuuluva sähköinen avainkortti, oli se sitten uusi, vanha tai kokonaan poistettu käytöstä.  
Avainkortin tiedot luetaan etää RFID-lukijalla tai saamalla kortti fyysisesti käsiinsä ja kortin tietoja muokataan erillisellä ohjelmointilaitteella, millä saadaan se Master Key tehtyä minuuteissa.  
Hyökkäyksestä ei edes jää mitään jälkeä lukitusjärjestelmän lokitietoihin.  
Tutkijat käyttivät omaa kustomoitua softaa, minkä avulla he onnistuivat hakkeroinnissa. Ilmiselvistä syistä he eivät ole julkistanut kyseistä softaa.  
Tutkijat ilmoittivat haavoittuvuudesta **Abloy**:lle huhtikuussa 2017. **Abloy** teki yhteistyötä tutkijoiden kanssa ja julkaisi haavoittuvuuden korjaavat ohjelmistopäivitykset helmikuussa 2018.  
Lähteissä on linkki videoon missä näytetään miten haavoittuvuus toimii.  


### Lähteet  

RFID Tags, Readers & Modules  - https://www.hidglobal.com/categories/rfid-tags-readers-modules  
iLOQ S5 - https://www.iloq.com/fi/katalogi/k5s-6/  
RFID ja NFC – mikä on niiden välinen ero ja miten tunnistat kortin teknologian? - https://checkpointsystems.com/fi/blog/rfid-nfc-kortit-lahimaksaminen-ero/  
Apple-alustojen tietoturva - https://support.apple.com/fi-fi/guide/security/sec2561eb018/web  
Supplemental access control - https://en.wikipedia.org/wiki/Supplemental_access_control  
Näin käytät passia - https://poliisi.fi/nain-kaytat-passia#nain-kaytat-passia  
Hackers build a 'Master Key' that unlocks millions of Hotel rooms - https://thehackernews.com/2018/04/hacking-hotel-master-key.html  
One Key That Can Hack Them All - https://www.youtube.com/watch?v=1PSwH8ldw5M&t=37s  
Smart Card APDU Commands: A Practical Developer Reference - https://ambimat.com/smart-card-selected-apdu-commands/  
ChatGPT käytetty ARDP-komentojen rakenteen tutustumiseen  




