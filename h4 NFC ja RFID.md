# h4 NFC ja RFID

## a) Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Lähdin tutkimaan omia tuotteita, jotka voisivat sisältää RFID ominaisuuksia ja löysin ainakin nämä:  
````
Työpaikan HID-kulkulätkä
Maksukortti
Passi
ILOQ avain
Apple Watch
Iphone 15 Pro
RFID Safe lompakko
````
Googlasin näiden tuotteiden RFID ominaisuudet. HID käyttää RFID teknologiaa, mutta en löytänyt työpaikkani käyttämää lätkää HID:in sivuilta. Mutta todennököisesti työpaikkani HID-kulkulätkä hyödyntää RFID:tä.  
Suomen passeissa on RFID siru, joka sisältää henkilötiedot, kasvokuvan ja sormenjäljet.  
RFID safe lompakko, minkä pitäisi suojata maksukorttiani.  
Sitten maksukorttini, puhelimeni, kelloni ja kotiavaimeni. Nämä käyttävät NFC-teknologiaa, joka on RFID:n alamuoto. Esim. Maksukortin, puhelimen ja kellon lähimaksuominaisuus käyttää NFC:tä ja ILOQ-avain pystyy kommunikoimaan langattomasti ulko-oven lukijan kanssa NFC:n takia.  
Maksukorttini osalta olen suojautunut kohtuullisen hyvin RFID-urkinnalta lompakkoni ansiosta, mutta en tosiaan tiedä kuinka hyvä suoja siinä oikeasti on.  
Passi, puhelimeni, kelloni ja avaimeni hyödyntävät niiden omia suojausominaisuuksia.  
Passi käyttää PACE-protokollaa, joka suojaa passin sirua ja lukulaitteen välistä NFC-tiedonsiirtoa salakuuntelulta ja luvattomalta lukemiselta.  
Applen tuotteet käyttävät "Secure Element" toimintoa, mikä on suojattu ympäristö, joka pitää sisällään kaikki arkaluontoiset tiedot. Maksutapahtumat myös yleensä vaativat biometrisen tunnistautumisen.  
iLOQ avain käyttää AES256-salausta, kaksisuuntaisa todennusta ja jokaisella avaimella on yksilöllinen tunniste. Avaimesta voidaan myös poistaa kulkuoikeudet, jos se katoaa tai päätyy vääriin käsiin.  
Työpaikan kulkukortin suojasta ei ole mitään tietoa, kun en löytänyt kyseistä lätkää valmistajan sivuilta.  
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

