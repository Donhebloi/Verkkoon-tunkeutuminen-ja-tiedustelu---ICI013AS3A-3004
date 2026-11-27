# h6 Wifi

## a) Wifi challenge lab harjoitukset

Tehtävät suorittiin **WiFiChallenge Lab v2.5.1** virtuaalikoneella. Virtuaalikoneen sai ladattua opettajan antamista materiaaleista, jonka jälkeen importtasin sen **Oracle VirtualBox Manageriin**.
VirtualBoxin vasemmasta yläreunasta **File** -> **Import Virtual Appliance** ja avautuvasta valikosta virtuaalikoneen tiedosto.  

<img width="519" height="466" alt="image" src="https://github.com/user-attachments/assets/57568214-06ff-483d-aae5-aa3ce2ea3ce7" />  

En ole aikaisemmin käyttänyt kyseistä virtuaalikonetta ja sen sisältämiä työkaluja, enkä ole tehnyt näitä tehtäviä ennestään, joten valitsin tehtäväksi ihan vaan neljä ensimmäistä "Recon" haastetta ja pidin WiFiChallenge Lab:in Walkthrough:n taustalla auki.  

**01. What is the channel that the wifi-global Access Point is currently using?**

Aloitin tekemällä oman wifi hakemiston, **mkdir ~/wifi**

<img width="568" height="39" alt="image" src="https://github.com/user-attachments/assets/ae7fa4bc-0940-4bc7-8364-941120c63cbb" />  

Tämän jälkeen ajoin **airmon-ng** ja **airodump-ng** komennot:  
````
sudo airmon-ng start wlan0
sudo airodump-ng wlan0mon -w ~/wifi/scan --manufacturer --wps --band abg
````
Googlasin vielä, että mitä kyseiset komennot tekevät.  
**Airmon-ng** komentoa käytetään langattomien verkkokorttien monitorointitilan käyttöönottoon. Komennolla voi myös lopettaa verkonhallintasovelluksia ja palata takaisin hallintatilaan monitorointitilasta.  
**airodump-ng** komentoa käytetään pakettien sieppaamiseen ja raakojen 802.11-kehysten tallentamiseen.  

**sudo airmon-ng start wlan0**:
<img width="1177" height="699" alt="image" src="https://github.com/user-attachments/assets/e9235f36-8905-4efd-9ca4-3734869650e3" />  

**sudo airodump-ng wlan0mon -w ~/wifi/scan --manufacturer --wps --band abg**:
<img width="1468" height="735" alt="image" src="https://github.com/user-attachments/assets/bf4bb78d-2b59-40be-b435-ca124d766241" />  

Tehtävässä piti selvittää mitä kanavaa **wifi-global** käyttää. Sen näkee taulukon toiselta riviltä, **CH** sarakkeelta.  

<img width="1463" height="102" alt="image" src="https://github.com/user-attachments/assets/eb3aea92-cdef-4ef5-9fac-fb48ae07b929" />  

**Wifi-global** käyttää kanavaa 44.  

Varmistin tämän vielä palauttamalla vastauksen WiFiChallenge Lab sivustolle.  

<img width="396" height="815" alt="image" src="https://github.com/user-attachments/assets/053f08da-a563-4f72-a71d-9c9924193410" />  

**02. What is the MAC of the wifi-IT client?**  

Tässä tehtävässä selvitetään **wifi-IT** client:in MAC osoite.  
  
Aloitin ajamalla komennon **sudo airodump-ng wlan0mon -w ~/wifi/scan --manufacturer --wps --band abg**, jolla selvitettiin mitä kanavaa **wifi-IT** käyttää:  

<img width="1166" height="25" alt="image" src="https://github.com/user-attachments/assets/9ff31162-022a-4bce-ac7f-5ad6d8230c76" />  

**Wifi-IT** käyttää kanavaa 11.  

Sitten **sudo airodump-ng wlan0mon -w ~/wifi/scanc11 --manufacturer --wps -c11** komento, jossa **-c11** parametri on **wifi-it**:n kanava.   
Tästä avautuu taulukko, josta MAC osoite selviää **BSSID**:n avulla:  

<img width="1357" height="438" alt="mac" src="https://github.com/user-attachments/assets/f2d45b8d-84eb-4419-baa0-12a770836b52" />  

Kuvan ylimmästä rivistä näkee **wifi-IT**:n BBSID:n, jonka avulla löytyi tarvittava MAC osoite kuvan alimmalta riviltä.  
MAC-osoite: **10:F9:6F:AC:53:52**  

Varmistus palauttamalla osoite sivustolle:  
<img width="405" height="475" alt="image" src="https://github.com/user-attachments/assets/91b7c8e6-6b66-464a-9609-96019d688599" />   


**03. What is the probe of 78:C1:A7:BF:72:46?**

Mulla oli edelleen edellisen tehtävän taulukko auki, josta tuo probe selvisi:  

<img width="1256" height="276" alt="probe" src="https://github.com/user-attachments/assets/de0dbd83-6dab-4363-9dde-097bf0c1a45c" />  

Probe on **wifi-offices**  

<img width="403" height="495" alt="image" src="https://github.com/user-attachments/assets/4dc8229a-fe28-4a3f-aece-30076b46a5f9" />  

Ekana kokeilin palauttaa sivustolle **wifi-offices,Jason**, mikä ei toiminut. Tämän jälkeen kokeilin palauttaa vaan **wifi-offices** ja se meni läpi.  


**04. What is the ESSID of the hidden AP (mac F0:9F:C2:6A:88:26)?**  

Tässä pitää selvittää F0:9F:C2:6A:88:26 MAC-osoitteen piilotettu **ESSID**.   
Aloitin ajamalla taas **sudo airodump-ng wlan0mon -w ~/wifi/scan --manufacturer --wps --band abg** komennon ja etsimällä rivin missä kyseinen MAC-osoite on.  

<img width="1413" height="457" alt="essid" src="https://github.com/user-attachments/assets/ec258789-6518-4622-9015-b1a076aeb7eb" />  

Kuvan ihan viimeisellä rivillä on kyseinen MAC-osoite ja **ESSID** sarakkeesta näkee että se on ainoa jossa ei lue selkeästi mikä se on.  

Tästä sitten ohjeita seuraamalla ajoin **cat ~/rockyou-top100000.txt | awk '{print "wifi-" $1}' > ~/wifi-rockyou.txt** komennon, mutta se ei toiminut, koska **rockyou-top100000.txt** oli root hakemistossa, eikä user hakemistossa missä itse olin.  
Kopioin sitten **sudo cp /root/rockyou-top100000.txt ~/rockyou-top100000.txt** komennolla tiedoston user kansioon.   

<img width="1114" height="31" alt="image" src="https://github.com/user-attachments/assets/d117829b-0b36-49a4-8244-b84178f1115c" />  

<img width="886" height="84" alt="image" src="https://github.com/user-attachments/assets/f57900a2-08a6-4bb6-afb4-82d5814d67f1" />  

Tästä sitten ajoin uudestaan **cat ~/rockyou-top100000.txt | awk '{print "wifi-" $1}' > ~/wifi-rockyou.txt** komennon ja pääsin etenemään.  
Ajoin sitten seuraavat komennot:  
````
sudo airmon-ng start wlan0
sudo iwconfig wlan0mon channel 11
mkd4 wlan0mon p -t F0:9F:C2:6A:88:26 -f ~/wifi-rockyou.txt
````

<img width="1300" height="811" alt="ESSID2" src="https://github.com/user-attachments/assets/40b50c77-3219-448c-bbbb-0b141d9ffdaa" />  

Tästä selvisi piilotettu ESSID, "wifi-free"

<img width="419" height="559" alt="image" src="https://github.com/user-attachments/assets/01110303-2534-498c-aac8-8e4d1874de31" />  

## b) Mitä opit ja mitkä asia yllättivät sinut?

Tehtävistä opin enemmän wifin toiminnasta ja työkaluista joita käytetään wifin tutkimiseen.  
En ole aikaisemmin käyttänyt **airmon-ng**, **airodump-ng** ja **mkd4** työkaluja, joten niiden käyttötarkoitukset ja toiminta tulivat tutummaksi tehtävien aikana.  
Yllätyin eniten siitä, että miten helposti muutamalla työkalulla ja komennolla voi selvittää tietoja wifistä ja siihen yhdistetyistä laitteista, ilman että verkkoon edes muodostaisi yhteyttä.  
Tukiasemien kanavat, MAC-osoitteet ja verkkoon yhdistettyjen asiakkaiden tietoja sai selville monitorointitilassa ihan pelkän verkkoliikenteen tarkkailulla.  
Jopa piilotetun WLAN verkon nimen sai aika helposti esille, muokkaamalla valmiiksi luotua sanalistaa ja käyttämällä **mkd4** työkalua.  
Tietenkin tässä helpotti todella paljon sivuston oma walkthrough, mutta on silti yllättävää miten helposti näitä tietoja sai esille.  
Tehtävät siis auttoivat ymmärtämään paremmin, millaista tietoa wifi verkoista saa selville muutamalla työkalulla ja komennolla sekä miten niitä käytetään.  
Vaikka raporttia varten tein vaan neljä ensimmäistä tehtävää, niin ne olivat sen verta mielenkiintoisia, että varmasti jatkan niiden tekemistä vapaa-ajalla.  

## c) Miten suhtautumisesi WLANin turvallisuuteen muuttui sen jälkeen kun teit harjoitukset?

Alan suhtautumaan WLAN verkkojen turvallisuuteen nyt aikaisempaa vakavammin. 
En ole oikeastaan aikaisemmin edes ajatellut kunnolla, että miten helposti kaikkia tietoja saa selville, ihan vaan muutamalla työkalulla.  
Jos pelkällä verkon tarkkailulla saa jo tän verran tietoa selville, niin mitä kaikkea sitten voisi saada aikaan jos tunkeutuisi vielä syvemmälle verkkoon.   
Pidän nyt myös sen mielessä, että langattoman verkon turvallisuudessa pitää muistaa huomioida muutakin kuin itse tukiasema, sillä verkkoon yhdistetyt laitteet ja niiden tiedot voi paljastaa tietoja verkon käyttäjistä.  


### Lähteet

Challenges - https://lab.wifichallenge.com/challenges  
Walkthrough WiFiChallenge Lab v2.0 - https://r4ulcl.com/posts/walkthrough-wifichallenge-lab-2.0/#01-what-is-the-channel-that-the-wifi-global-access-point-ap-is-currently-using  
Airmon-ng - https://www.aircrack-ng.org/doku.php?id=airmon-ng  
Airodump-ng - https://www.aircrack-ng.org/doku.php?id=airodump-ng  

