# h6 Wifi

## a) Wifi challenge lab harjoitukset

Tehtävät suorittiin **WiFiChallenge Lab v2.5.1** virtuaalikoneella. Virtuaalikoneen sai ladattua opettajan antamista materiaaleista, jonka jälkeen importtasin sen **Oracle VirtualBox Manageriin**.
VirtualBoxin vasemmasta yläreunasta **File** -> **Import Virtual Appliance** ja avautuvasta valikosta virtuaalikoneen tiedosto.  

<img width="519" height="466" alt="image" src="https://github.com/user-attachments/assets/57568214-06ff-483d-aae5-aa3ce2ea3ce7" />  

En ole aikaisemmin käyttänyt kyseistä virtuaalikonetta ja sen sisältämiä työkaluja, enkä ole tehnyt näitä tehtäviä ennestään, joten valitsin tehtäväksi ihan vaan kolme ensimmäistä haastetta ja pidin WiFiChallenge Lab:in Walkthrough:n taustalla auki.  

01. What is the channel that the wifi-global Access Point is currently using?

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

Tehtävässä piti selvittää mitä kanavaa **wifi-global** käyttää ja sen näkee taulukon toiselta riviltä, **CH** sarakkeelta.  

<img width="1463" height="102" alt="image" src="https://github.com/user-attachments/assets/eb3aea92-cdef-4ef5-9fac-fb48ae07b929" />  

**Wifi-global** käyttää kanavaa 44.  

Varmistin tämän vielä palauttamalla vastauksen WiFiChallenge Lab sivustolle.  

<img width="396" height="815" alt="image" src="https://github.com/user-attachments/assets/053f08da-a563-4f72-a71d-9c9924193410" />  


