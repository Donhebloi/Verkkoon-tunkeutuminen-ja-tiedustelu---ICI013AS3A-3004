# H2 Nuuh

## x) Lue ja tiivistä


## a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen

Poikkeuksellisesti tätä kohtaa ei tarvitse raportoida, jos ei ollut mitään ongelmia.  
Kali virtuaalikone löytyy jo ennestään millä olen suorittanut muitten kurssien tehtäviä.   

<img width="436" height="72" alt="image" src="https://github.com/user-attachments/assets/f6798f58-519e-417a-9bbc-2851a16c91dc" /> <img width="1055" height="587" alt="image" src="https://github.com/user-attachments/assets/a83b18e0-e113-4198-a235-189b7a7a42de" />  


## b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.

Kalin oikeassa ylänurkassa, äänenvoimakkuuden vieressä on Ethernet kuvake, mistä netin saa pois ja takaisin päälle:  

<img width="251" height="168" alt="image" src="https://github.com/user-attachments/assets/c54c3117-ac01-4770-970b-1842cc1deba7" />  

Tuosta kun painaa "Disconnect" niin netti katkeaa. Siitä tulee myös ilmoitus että netti on nyt katkaistu. 

<img width="411" height="152" alt="image" src="https://github.com/user-attachments/assets/311269de-c45b-438f-9084-b494cce31b29" />  

Kokeilin että netti on oikeasti pois päältä, hakemalla "Steam" selaimesta.  

<img width="1113" height="693" alt="image" src="https://github.com/user-attachments/assets/a2e8a904-2ba7-46d4-b2ff-7fbe4cc8deff" />  

Netin saa takaisin päälle samasta kuvakkeesta Kalin oikeasta yläkulmasta ja minun tilanteessa valitsemalla "Wired connection 1".  

<img width="216" height="167" alt="image" src="https://github.com/user-attachments/assets/d08d52b4-54b4-4da1-b8fe-086655fee1e4" />  

Kokeilin onko netti päällä, samalla "Steam" haulla.  

<img width="1122" height="736" alt="image" src="https://github.com/user-attachments/assets/4c7c570e-a101-4d40-8703-b6ff81be7791" />  

Nyt on taas netti päällä.  


## c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla.

Minulla oli jo ennestään Wireshark ladattuna.  

<img width="252" height="146" alt="image" src="https://github.com/user-attachments/assets/ba354b80-dbf7-4f1a-93b0-81c8528a3348" />  

Mutta jos sitä ei ole ja sen haluaa ladata, niin kalissa se onnistuu näin:  
````
sudo apt-get update
sudo apt-get install wireshark
````
Alotin sieppaamisen avaamalla wiresharkin ja valitsemalla oikean verkkoliitännän, joka on "eth0".  

<img width="435" height="380" alt="image" src="https://github.com/user-attachments/assets/fd3de507-1306-4ccd-bae0-f9c3ad87fda4" />  

Sitten klikkaamalla sinistä evä kuvaketta wiresharkin vasemmassa yläkulmassa pääsee sieppaamaan liikennettä.  

<img width="407" height="181" alt="image" src="https://github.com/user-attachments/assets/a9d6603d-7487-491a-b779-b09a91304eb2" />  

Avasin hakukoneen ja Youtuben taustalle, jotta wiresharkkiin ilmestyisi paketteja.  

<img width="1662" height="574" alt="image" src="https://github.com/user-attachments/assets/63879d41-fec5-48c8-aac9-591175570d4f" />  


