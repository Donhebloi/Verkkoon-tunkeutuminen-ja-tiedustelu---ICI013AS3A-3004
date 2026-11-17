# h5 Labratakki

## a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.

Aloitin seuraamalla ohjeita, jotka löytyivät kurssin luento materiaaleista.  
Eli avasin Mininet koneen ja suoritin komennon:  
````
ryu-manager ryu.app.simple_switch_13
````
<img width="518" height="94" alt="image" src="https://github.com/user-attachments/assets/528676e2-18e4-4eba-ac99-e247adfd9fc6" />  

Tämän jälkeen avasin toisen terminaali ikkunan painamalla **oikea ctrl**+**f2** ja ajoin komennon:  
````
sudo mn --topo single,3 --mac --switch ovsk --controller remote
````
<img width="695" height="296" alt="image" src="https://github.com/user-attachments/assets/5b9a0787-d4d4-4954-b862-3ed5e5321eea" />  
  
Sitten kokeilin **pingall** komennolla, pystyvätkö **h1**, **h2** ja **h3** koneet kommunikoimaan keskenään:  

<img width="307" height="117" alt="image" src="https://github.com/user-attachments/assets/3e00015d-2f59-4d35-867a-47c92066776d" />  

Yritin sitten yhdistää h1 koneeseen **xterm h1** komennolla, mutta se ei onnistunut ja sain seuraavanlaisen virheilmoituksen:  

<img width="263" height="37" alt="image" src="https://github.com/user-attachments/assets/f3879b1e-e469-48d1-a80c-845407fdc1a8" />  

Tästä sitten avasin taas uuden terminaali ikkunan ja seurasin opettajan antamia ohjeita **xterm** ongelmien ratkomiseen.  
Uudessa ikkunassa ajoin komennon **./get_xauth.sh**:  
Tulostui **mininet-vm/unix:11  MIT-MAGIC-COOKIE-1  c709c63c5aeaf55c525e6f0e19492417**  
Niin tästä sitten ohjeiden mukaan ajoin **sudo -s xauth add mininet-vm/unix:11 MIT-MAGIC-COOKIE-1  c709c63c5aeaf55c525e6f0e19492417**  

<img width="1454" height="94" alt="image" src="https://github.com/user-attachments/assets/fa1adf6a-2210-48bc-9562-57db5daac911" />  

Tämän jälkeen ajoin uudestaan **sudo mn --topo single,3 --mac --switch ovsk --controller remote** komennon, kokeilin yhteyttä **pingall** komennolla ja yritin avata h1 terminaalin:  

<img width="1071" height="543" alt="image" src="https://github.com/user-attachments/assets/db35e8c7-ee80-4c5b-abae-de26d839dbba" />  

Nyt avautui h1 terminaali. Hyvin pienenä ja epäselvänä, mutta avautui kuitenkin.  


