# h3 Aaltoja harjaamassa

## x) Lue ja tiivistä.

Hubacek 2019  
- Näytti miten signaali nauhotetaan URHilla.  
- Näytti miten URHilla analysoidaan signaalia.
- Kävi läpi bittejä ja demodulaatiota.
  
Cornelius 2022  
- Sääasema purettiin rtl_433 avulla.
- Sääaseman signaalia analysoitiin URHilla.
- Sääaseman signaali demoduloitiin URHilla.

## b) rtl_433. Asenna rtl_433 automaattista analyysia varten.

Katsoin asennusohjeet githubista -  https://github.com/merbanan/rtl_433  
Asennus onnistui ihan vaan **sudo apt-get install rtl-433** komennolla.  

<img width="437" height="133" alt="image" src="https://github.com/user-attachments/assets/53312bec-ca74-4092-b8b6-4ad156460fe3" />  

Kokeilin sitten ajaa ohjelman.  

<img width="939" height="96" alt="image" src="https://github.com/user-attachments/assets/b6dc3e5c-1978-4e78-ab17-61cdec878c7e" />  

Tulostui ohjelman versio, joten ohjelma toimii.  

## c) Automaattinen analyysi. 

Latasin tarvittavan näytteen Teron sivuilta **wget** komennolla  
````
wget https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/samples/Converted_433.92M_2000k.cs8
````
<img width="1832" height="272" alt="image" src="https://github.com/user-attachments/assets/acf60677-1a43-4b38-b794-31c27104c83d" />  

Sitten ajoin ohjelman **rtl_433 -r Converted_433.92M_2000k.cs8** komennolla. Pidin tässä **merbanan** githubia auki, missä oli eri ajo ohjeita, mistä nappasin tuon -r option. -r optio lukee datan suoraan syötetystä tiedostosta, eikä vastaanottajasta.  

<img width="1561" height="482" alt="image" src="https://github.com/user-attachments/assets/2480ac91-3da7-47fd-9788-935d5242fbcb" />  

Kuvassani näkyy 4 tulostetta, mutta niitä oli yhteensä 12.  
**KlikAanKlikUit-Switch**, **Proove-Security** ja **Nexa-Security** kaikki toistuivat kolme kertaa. Googlailin mikä KlikAanKlikUit-Switch voisi olla ja selvisi että se on jokin seinäkytkin tai älypistorasia. **Switch** loppuosan perusteella se on kytkin.   
Googlasin myös **Proove-Security** sekä **Nexa-Security** ja nekin osoittautuivat älykotilaitteiksi.    
Kaikilla on sama id tai house code "8785315", joten voisin olettaa että kaikki signaalit lähtevät samasta paikasta. **Proove-Security**llä ja **Nexa-Security**llä on sama **Unit** numero "3", mikä voisi tarkoittaa että laitteet on konfiguroitu yhdeksi yksiköksi. Ryhmätunnus, **Group 0** on kaikilla sama myös.     
**Proove-Security** ja **Nexa-Security** ovat näytteessä aina kytkimen jälkeen joten luulen että ne reagoivat siihen kun kytkintä painetaan ja tässä tapauksessa sitä on painettu neljä kertaa.  
Aikavälit näillä on 0.083284 - 0.383568s mikä voisi olla signaalin vastaanoton aika.  
Oletan että **Group call** on komento kytkimeltä muille laitteille mikä saa ne **State: Off** tilaan. Kytkimeltä luultavasti siis lähtee sammutuskomento.  


## d) Too compex 16?

Latasin URH-näytteen Teron sivuilta taas **wget** komennolla.  
````
wget https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/samples/Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s
````
<img width="1898" height="293" alt="image" src="https://github.com/user-attachments/assets/0718d68d-9868-4168-a73a-ddb664b512c6" />  

Tarkoituksena olisi vaihtaa tiedoston nimi oikeaan muotoon jotta se olisi rtl_433-yhteensopiva.  
Kokeilin kuitenkin muodon vuoksi ajaa ohjelman alkuperäisellä nimellä.  
````
rtl_433 -r Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s
````
<img width="1531" height="473" alt="image" src="https://github.com/user-attachments/assets/03227929-87d6-41c6-b5e5-6b4ffa4b4d4e" />  

Jaaha, se näyttäisi toimivan, mutta sisältö on täysin sama kuin edellisessä tehtävässä.  
Lähdin tästä sitten vaihtamaan tiedoston nimeä, tehtävänannon vinkkien perusteella.  
Vinkkien mukaan tiedostomuodon muuttaminen onnistuu kun muuttaa tiedoston nimen ja lisää siihen oikean taajuuden.  
Käytin nimen muuttamiseen **mv** komentoa. Ekana yritin vaihtaa nimeksi "foo_433.92M_2MSps_2000k.cs8".  

<img width="1283" height="61" alt="image" src="https://github.com/user-attachments/assets/6b51fb87-4d4e-4a38-9cbf-fcb1b4dc6215" />  

Sitten ohjelma ajoon **rtl_433 -r foo_433.92M_2MSps_2000k.cs8** komennolla.  

<img width="1545" height="478" alt="image" src="https://github.com/user-attachments/assets/2c02b05e-7c58-45d6-a355-c6993829e727" />  

Sekin näytti toimivan, mutta sisältö oli edelleen sama.  
Kokeilin sitten vielä kerran vaihtaa nimeä, ottamalla nyt nimestä osan "2MPsp" pois, sillä sitä ei ollut Teron antamissa esimerkeissä.  

<img width="745" height="52" alt="image" src="https://github.com/user-attachments/assets/8f154add-a595-42f9-adda-24d8b416bf5a" />  

Ja taas ajoon, **rtl_433 -r foo_433.92M_2000k.cs8**.  

<img width="1533" height="557" alt="image" src="https://github.com/user-attachments/assets/28a74e21-63f3-4b50-b2c7-e5af7a4075a0" />  

Sekin toimi, mutta sisältö oli edelleen sama. En ole varma, teinkö jotain väärin, vai onko sisältö oikeasti sama kuin edellisessä tehtävässä, mutta päätin tässä kohtaa siirtyä seuraavaan tehtävään.    


## e) Ultimate. Asenna URH, the Ultimate Radio Hacker.

Aloitin URH:n asentamisen seuraamalla Teron ohjeita tehtävänannosta.
````
sudo apt-get update
sudo apt-get -y install pipx
pipx install urh
pipx ensurepath
````
<img width="710" height="269" alt="image" src="https://github.com/user-attachments/assets/f70da7e4-2e09-4065-85c1-462452584159" />  

<img width="811" height="192" alt="image" src="https://github.com/user-attachments/assets/c5834f14-d954-4c10-8ed3-a52056d5f899" />  

Multa puuttui jotain setuptoolsseja, mistä sain warning ilmoituksen, mutta eikai se menoa haittaa. URH kuitenkin suostui latautumaan.  

<img width="1692" height="166" alt="image" src="https://github.com/user-attachments/assets/88d4f4b9-6d41-4852-931d-a1a1c35a4512" />  

**Pipx ensurepath** komennon jälkeen suljin ja avasin terminaalin uudelleen ja ajoin **urh** komennon.  

<img width="1904" height="576" alt="image" src="https://github.com/user-attachments/assets/33d163c5-16c0-43b5-b710-9f45ec5c557e" />  

Siitä sitten avautui URH:in käyttöliittymä.  


## f) Yleiskuva. Kuvaile näytettä yleisesti.

Taas latasin näytteen **wget** komennolla.  
````
wget https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/samples/1-on-on-on-HackRF-20250412_113805-433_912MHz-2MSps-2MHz.complex16s
````
<img width="1890" height="42" alt="image" src="https://github.com/user-attachments/assets/e31553a1-e987-4788-8b43-e5b9bebeb4e7" />  

Sitten avasin urh:in uudestaan, klikkasin vasemmasta yläreunasta File -> Open ja valitsin näytteen.  

<img width="1231" height="201" alt="image" src="https://github.com/user-attachments/assets/7b6e26ba-241d-4e36-b9d1-c05fa2961192" />  

Miltä näyte näyttää:  

<img width="1901" height="538" alt="image" src="https://github.com/user-attachments/assets/2175c396-c793-4eff-9578-55e888020ba8" />  
Janaa klikkaamalla siitä voi maalata haluamansa alueen. Valitsin koko janan jotta saisi yleiskuvan selville.  
Koko jana valittuna:  

<img width="1611" height="453" alt="image" src="https://github.com/user-attachments/assets/030ca8f1-931c-4b4b-9f8a-8a14bd2ea74d" />  

Tästä selvisi janan pituus, joka on 5.49 sekunttia.  
Janan vasemman yläreunan vieressä on sininen "i" nappi mistä näkee lisää tietoja janasta.  

<img width="765" height="207" alt="image" src="https://github.com/user-attachments/assets/16aa6694-5214-4a98-a3bd-0d7e9806aa8b" />  

Janan koko: 10.47MB  
Luonti päivämäärä: 4.11.2026  
Näytteet: 5491580  
Näytteenottotaajuus: 1.0M  
Näytteen pituus: 5.49 s  


## g) Bittistä. Demoduloi signaali niin, että saat raakabittejä.

Modulaatio oli valmiiksi **ASK**, joten pidin sen koska sillä näkyi janan alla bittejä.  
*Signal view**in pystyi myös vaihtamaan. Alunperin Signal view oli "analog", mutta vaihdoin sen "Demodulated" muotoon.  

<img width="1524" height="431" alt="image" src="https://github.com/user-attachments/assets/957ba266-c3b4-4bac-95e2-87752fc41e9f" />  

Tästä sitten valitsin rivistä ensimmäisen bitin, joka oli "1".  

<img width="1072" height="431" alt="image" src="https://github.com/user-attachments/assets/74912bb1-d34f-4ee0-84e0-0e053c294a46" />  

Tästä selvisi yhden raakabitin kesto ajassa, joka on **525µs** eli 0.525 millisekunttia.  
Valitsin vielä seuraavan bitin, joka oli "0".  

<img width="1039" height="437" alt="image" src="https://github.com/user-attachments/assets/9cc4b36d-9c51-468b-9976-d205477eeb8f" />  

Sen pituus ajassa on **518µs**, eli 0.518 millisekunttia. Hieman lyhyempi kuin ensimmäinen bitti.  
Löysin sivuston, missä pystyy muuntamaan näytön virkistystaajuuden millisekunneiksi. Vertailua varten valitsin oman näytön virkistystaajuuden joka on 144Hz.  
144Hz näytöllä menee 6.94 millisekunttia yhden ruudun näyttämiseen, joten tässä ajassa radiosignaali ehtii lähettämään noin 13 raakabittiä.  

## Lähteet  

Hubacek 2019, Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs - https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s.  
Cornelius 2022, Decode 433.92 MHz weather station data - https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html.  
Karvinen, tehtävänannon vinkit - https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/.  
Merbanan, rtl_433 - https://github.com/merbanan/rtl_433.  
PureUnits, Monitor Hz → ms Calculator - https://pureunits.com/tools/monitor-delay.  






