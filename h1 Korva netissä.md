# H1 Korva netissä

## x) Spektrini

Tässä hyvin yksinkertainen ja taiteellinen sähkömagneettinen spektri:  

<img width="1269" height="636" alt="image" src="https://github.com/user-attachments/assets/efcd2de5-2f2e-4101-ba26-a9c83ca3f503" />




## a) WebSDR

Ekaksi siirryin WebSDR sivulle, **WebSDR.org** ja valitsin **University of Twente**:n radion. Valitsin tämän radion koska se oli heti listan ensimmäisenä, se on Alankomaissa joten tarpeeksi kaukana tehtävänannon mukaan ja sillä oli paljon käyttäjiä, noin 470 sillä hetkellä, joten ajattelin että tältä kanavalta voisi helpommin löytyä joku selkeästi kuultava radiolähetys.  
Aluksi vain kliksuttelin randomisti vähän kaikkia nappeja mitä näin ja liikuttelin taajuudensäädintä edestakas, toivoen että alkaisi kuulumaan jotain.  
En kummiskaan kauaa päättömästi kliksutellut kaikkea kun huomasin radion sivulla linkin **quick start guide** oppaaseen, minkä sitten avasin ja rupesin lukemaan läpi.  
<img width="535" height="20" alt="image" src="https://github.com/user-attachments/assets/e05ba7fa-1d5a-4cd1-a084-a57cc7944eb4" />  

Quick start guiden avulla sivuston käyttö selkeni.  
Valitsin modulaatioksi **AM** ja päätin **Quick start guiden** mukaan kokeilla taajuutta 7300 kHz. Sillä taajuudella ei ollut mitään, mutta taajuudella 7295 kHz oli selkeästi kuultava radiolähetys menossa. Tai ainakin melkein selkeä, välillä ääni sähisi ja rähisi, mutta siitä sai kokoajan selvää.    
Päädyin siis **CHN China Radio Int.** kanavalle, jossa oli englannin kielinen lähetys menossa. Vaikka lähetys olikin englanniksi, niin en ole ihan varma mistä siellä puhuttiin mutta se kuulosti joltain väittelyltä. En kauaa ehtinyt sitä kuuntelemaan kun alkoivat mainokset soimaan radiosta.  

<img width="1092" height="590" alt="image" src="https://github.com/user-attachments/assets/4c28b60d-3e6c-4476-af34-f6b30f652091" />  

Eli kuvassa minulla on:  
Taajuus 7295 kHz  
AM modulaatio  
Filter 9 kHz  

Zoomasin taajuudensäädintä isommaksi kuvasta näkyvän **waterfall zoom** avulla, jonka ansionsa näin radiokanavien nimet noissa oransseissa bokseissa.  
Aallonpituuden laskemiseen käytin **everythingRF** sivuston **Frequency to Wavelength Calculator**:ia. Syötin sinne tuon 7925 taajuuden ja vastaukseksi sain 37828.70132492 mm, eli aallonpituus on noin 37.8 metriä.  

<img width="692" height="252" alt="image" src="https://github.com/user-attachments/assets/a2be6d2a-8864-445e-b688-cea653e530d4" />  


## b) Moduwhat?

Tässä kohtaa pysyin edelleen **University of Twente**:n sivulla.  
Valitsin modulaatioksi **LSB** ja rupesin liikuttelemaan taajuudensäädintä 7050 - 7200 kHz taajuuksilla kunnes kuulin selkeää puhetta.  
Päädyin taajudelle 7190 kHz missä käytiin jotain keskustelua. Laitoin **autonoch**:in ja **noise reduction**:in päälle jotta puheen kuulisi vielä selkeämmin. En ole ihan varma millä kielellä he puhuivat, itse ymmärsin puheesta vain Aplha, Charlie ja Foxtrot:in.   

<img width="1123" height="597" alt="image" src="https://github.com/user-attachments/assets/3cedd6e6-e4f2-4877-b398-c291df529e57" />  

Kokeilin tällä taajuudella myös kaikkia muita modulaatioita mutta silloin puheesta ei saanut mitään selvää.  
Tähän käytin myös apuna sivulta löytyvää **Quick start guide**:a.  

## c) ADS-B

Siirryin **ADS-B Exchange** sivulle etsimään mieluista konetta.  
Sivuilta avautui kartta, mistä näki reaaliajassa todella monen koneen lennot.  
Vaikka vaihtoehtoja oli ihan huimasti, niin päädyin ihan meidän Finnairin koneeseen, joka oli raportin tekohetkellä Keski-Suomen kohdalla. 
Kartasta näki että lento on lähtenyt Japanista, Osakasta, Kansain kansainväliseltä lentoasemalta.  

<img width="526" height="473" alt="image" src="https://github.com/user-attachments/assets/d7a26eee-2fe8-4db3-8944-db504a7765ad" />  

Kuvassa näkyvä pinkki kone oli se minkä valitsin.  
Koneen tärkeimmät tiedot:  
````
Kutsutunnus: FIN70
Rekisteri: OH-LWO Finland
Lentoyhtiö: Finnair Oyj
Tyyppi: A359
Tyypinkuvaus: L2J
Malli: Airbus A-350-900
Pituus: 219.4 ft = 66.8 m
Korkeus: 56.3 ft = 17.1 m
Siipiväli: 212.4 ft = 64.7m
Polttoaineenkulutus: 2128.94 gal/h = 8058.9 l/h
````
Lentokoneen yksityiskohtaisemmat tiedot löytyivät vihreän **FULL DETAILS** napin takaa.  

<img width="183" height="34" alt="image" src="https://github.com/user-attachments/assets/679c1dbc-2d5e-42cb-a1c8-e749fbe32c24" />  

Sivustolta löytyy myös kuva lentokoneesta ja huimasti muutakin tietoa lennosta, kuten mistä lento on alkanut, nopeuden, korkeuden, lennon koordinaatit jne:  

<img width="188" height="1646" alt="image" src="https://github.com/user-attachments/assets/d7c8899c-56d7-4bc6-b195-9bda6f1822a2" />  



