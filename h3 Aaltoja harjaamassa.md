# h3 Aaltoja harjaamassa

## b) rtl_433. Asenna rtl_433 automaattista analyysia varten.

Katsoin asennusohjeet githubista -  https://github.com/merbanan/rtl_433  
Asennus onnistui ihan vaan **sudo apt-get install rtl-433** komennolla.  

<img width="437" height="133" alt="image" src="https://github.com/user-attachments/assets/53312bec-ca74-4092-b8b6-4ad156460fe3" />  

Kokeilin sitten ajaa ohjelman.  

<img width="939" height="96" alt="image" src="https://github.com/user-attachments/assets/b6dc3e5c-1978-4e78-ab17-61cdec878c7e" />  

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
Kaikilla on sama id tai house code "8785315", joten voisin olettaa että kaikki signaalit lähtevät samasta paikasta. Jokaisella on myös sama **Unit** numero "3", mikä voisi tarkoittaa että laitteet on konfiguroitu yhdeksi yksiköksi. Ryhmätunnus, **Group 0** on kaikilla sama myös.     
**Proove-Security** ja **Nexa-Security** ovat näytteessä aina kytkimen jälkeen joten luulen että ne reagoivat siihen kun kytkintä painetaan ja tässä tapauksessa sitä on painettu neljä kertaa.  
Aikavälit näillä on 0.083284 - 0.383568 mikä voisi olla signaalin vastaanoton aika.  
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




