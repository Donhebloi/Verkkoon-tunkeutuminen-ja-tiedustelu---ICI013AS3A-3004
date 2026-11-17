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
Tästä sitten etenin taas ohjeiden mukaan ja ajoin h1 terminaalissa **arp -n** komennon:  

<img width="510" height="73" alt="image" src="https://github.com/user-attachments/assets/6224afc8-deb7-46c6-8163-e03e7636a523" />  

Sitten siirryin takaisin **mininet>** komentoriville, avasin h3 terminaalin **xterm h3** komennolla ja ajoin komennot:  
````
sysctl -w net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 22
tcpdump –i h3-eth0 –w arp-p.pcap &
````
<img width="621" height="36" alt="image" src="https://github.com/user-attachments/assets/abb266cb-8227-4b96-88ff-14c8a58d275e" />  

<img width="700" height="55" alt="image" src="https://github.com/user-attachments/assets/24facddc-2bbe-4538-b39c-8219a6013f85" />  

Tämän jälkeen avasin Wiresharkin, **wireshark &** komennolla ja avasin **h3-eth0** liitännän, mutta siinä ei ollut vielä mitään liikennettä:  

<img width="963" height="385" alt="image" src="https://github.com/user-attachments/assets/aa8ce961-5d23-442b-81ce-911f7303e20b" />  

Wiresharkin avaamisen jälkeen ajoin vielä **sshesame -port 22 -listen_address 0.0.0.0** komennon:  

<img width="1407" height="27" alt="image" src="https://github.com/user-attachments/assets/54c8d879-7068-45c5-9b34-3c546ff14a99" />  

Sitten avasin uuden h3 terminaali ikkunan ARP-hyökkäystä varten ja ajoin **python3 ./arp_poison.py** komennon ja siirryin takaisin h1 terminaaliin.  
Ajoin vielä kerran **arp -n** komennon, tarkistaakseni onko mac osoitteisiin tullu mitään muutoksia:  

<img width="501" height="52" alt="image" src="https://github.com/user-attachments/assets/0e80a1cc-4235-4a1f-9a63-f196c328e6ca" />  

Nyt osoitteen **10.0.0.2** mac osoite oli muuttunut. Alunperin se oli **00:00:00:00:00:02**, mutta nyt se oli **00:00:00:00:00:03**.  
  
Sitten h1 terminaalissa yritin yhdistää h2 terminaaliin ssh:lla:  

<img width="456" height="331" alt="image" src="https://github.com/user-attachments/assets/4c3a713f-a31a-4f0b-ad61-1be39fd0cb45" />  

"Possible DNS spoofing" varoitusilmoitus tuli näkyviin.  
Tämän jälkeen poistin vanhan avaimen, **ssh-keygen -R h2** komennolla ja yritin uudestaan yhdistää h2 terminaaliin ssh:lla:  

<img width="538" height="168" alt="image" src="https://github.com/user-attachments/assets/c4a58921-5797-4b7d-b97c-340b48269f3a" />  

Vastasin kumpaankin kysymykseen "yes" ja **root@h2** salasanaksi syötin "salasana", jonka jälkeen pääsin h2 sisään.  

Siirryin takaisin siihen h3 terminaaliin jossa ajoin **sshesame -port 22 -listen_address 0.0.0.0** komennon. Nyt terminaalissa näkyi loki, josta näki h2 kirjautumistiedot:  

<img width="963" height="129" alt="image" src="https://github.com/user-attachments/assets/4e35da1b-8904-4bdd-ae94-0cd88b66f117" />  

ARP-myrkytys siis toimi. Kun yritin muodostaa h1 koneelta SSH yhteyden h2 koneeseen, niin SSH yhteys ohjautui h3 koneella pyörivälle SSHeSame palvelimelle, jonka lokiin tallentui h2 koneen IP-osoite, käyttäjätunnus ja salasana.  
Näin hyökkääjä olisi voinut siepata kirjautumistiedot ARP-myrkytyksen avulla.  

Kävin vielä katsomassa wireshark liikenteen:  

<img width="960" height="504" alt="image" src="https://github.com/user-attachments/assets/6d2d47b3-e85a-402b-8a45-82ffbb634561" />  

Wiresharkista näkyi myös että myrkytys onnistui. Suodatin wiresharkin näyttämään vain ARP-paketit helpompaa havainnollistamista varten.  
H3 kone lähetti toistuvia ARP-vastauksia, jossa se väitti omaavansa sekä h1 että h2 koneiden IP-osoitteet. Tämän takia wiresharkissa lukee "10.0.0.1 is at 00:00:00:00:00:03" ja "10.0.0.2 is at 00:00:00:00:00:03", vaikka se ei pidä paikkaansa.  
Wireshark tunnisti tämän ja merkkasi paketit varoituksella "Duplicate IP address detected for 10.0.0.1 (00:00:00:00:00:03) also in use by 00:00:00:00:00:01" ja "Duplicate IP address detected for 10.0.0.2 (00:00:00:00:00:03) also in use by 00:00:00:00:00:02"  
Hyökkäys perustuu siis siihen, että verkkoon lähetetään väärennettyjä ARP-viestejä, joiden avulla kohdekoneelle saadaan virheellinen IP- ja MAC-osoiteen välinen vastaavuus. Kohdekone siten lähettää liikennettä hyökkääjän koneelle, oikean kohdekoneen sijasta.  


## b) ICMP Spoofing ja TCP Session Hijacking

Aloitin siirtymällä tehtävien hakemistoon, joka oli **/lab/01-Network-Security-Lab/scripts** 
Avasin tehtävien README:n osoitteesta **https://github.com/ssam246/Network-Security-Lab** ja lähdin seuraamaan ohjeita.  

Käynnistin mininet ympäristön **sudo python3 hub_topo.py** komennolla ja kokeilin toimiiko yhteys **pingall** komennolla:  

<img width="1074" height="477" alt="image" src="https://github.com/user-attachments/assets/b6743bb9-b77c-4927-93a8-58c094698ffc" />  

Avasin sitten h1 terminaalin, **xterm h1** ja siellä käynnistin **python3 sniff_icmp.py** skriptin.  

H2 terminaalissa ajoin **ping 10.0.0.1** komennon:  

H1: Vastaanottaa paketit 
<img width="807" height="219" alt="image" src="https://github.com/user-attachments/assets/81c7a6fb-5a02-4d72-bf82-5a8530e04fa9" />  

H2: Pingaa osoitteen "10.0.0.1"  
<img width="728" height="155" alt="image" src="https://github.com/user-attachments/assets/00030b03-35b1-4444-982f-339fcc002ab5" />  

Tämän jälkeen avasin vielä h3 terminaalin, jossa ajoin **python3 spoof_icmp.py** skriptin.  
Ajoin h1 **sniff** skriptin ja h2 terminaalissa **ping** komennon uudestaan.  

H3: Lähettää nyt yhden ylimääräisen, väärennetyn paketin  
<img width="802" height="184" alt="image" src="https://github.com/user-attachments/assets/28221077-c055-41a3-b538-b3459665cc46" />  

H1: H1 nyt vastaanottaa ylimääräisen paketin, jonka takia näkyy kaksi "10.0.0.1 > 10.0.0.2" riviä peräkkäin.    
<img width="813" height="114" alt="image" src="https://github.com/user-attachments/assets/a6127b0e-635f-4076-b710-e9b386d0194c" />  

H2: Pingaa edelleen samalla tavalla  
<img width="723" height="127" alt="image" src="https://github.com/user-attachments/assets/8f7d6a45-f7e3-4cb0-969f-133db502e3f1" />  

H1 **sniff_icmp.py** skriptin normaali request/reply vuorottelu muuttui, kun verkkoon tuli ylimääräinen paketti.  
H3 **spoof_icmp.py** skripti teki tämän ylimääräisen paketin jolla oli väärennetty lähdeosoite. Skripti sai näyttämään siltä, että paketti tulisi oikeasti "10.0.0.1" osoitteesta.  
ICMP ei siis sisällä mitään todennusmekanismia lähdeosoitteen tarkistamiseksi, minkä takia hyökkääjä voi lähettää väärennettyjä paketteja, jotka näyttävät siltä että ne tulevat oikeasta osoitteesta.  
Tällä tavalla hyökkääjä voisi häiritä kommunikaatiota tai käyttäää tätä tekniikkaa osana laajempaa Man in The Middle-hyökkäystä.  

Sitten **TCP Hijacking**  
Käynnistin kaikki kolme terminaalia uudelleen, jonka jälkeen ajoin skriptit tässä järjestyksessä:  
````
H1: python3 tcp_server.py - Taustalle kuuntelemaan
H3: python3 sniff_tcp_session.py - Taustalle sniffaamaan
H2: python3 tcp_client.py - Yhdistämään kohdekoneeseen
H3 uusiksi: python3 tcp_hijack.py - Kaappaamaan H2 ja H1 välisen liikenteen
````

H1: TCP serveri kuunteli ja sai yhteyden osoitteeseen "10.0.0.2" sekä "Hello" viestin.  
<img width="902" height="103" alt="image" src="https://github.com/user-attachments/assets/96d003eb-3322-4061-b9df-75660d221521" />  

H3: Sniffasi liikenteen, jonka jälkeen lähetti yhden väärennetyn paketin.  
<img width="966" height="471" alt="image" src="https://github.com/user-attachments/assets/1c8c4e62-3a92-493a-8bb4-70979670d695" />  

H2: Lähetti ja vastaanotti "Hello" viestin.  
<img width="916" height="96" alt="image" src="https://github.com/user-attachments/assets/7ec6ff1d-092e-4b1b-bb29-f2ed42a65df3" />  
  
Tämä ei nyt tainnut onnistua ihan niin kuin piti.  
**sniff_tcp_session.py** onnistui havaitsemaan käynnissä olevan TCP-session h1:n ja h2:n välillä sekä sai selville niiden SEQ ja ACK numerot.  
**tcp_hijack.py** yritti lähettää väärennetyn paketin samaan sessioon, mutta se ei nyt tainnut tulla perille, vaikka h3 väitti lähettäneensä sen.  
Tässä voi olla ongelmana se että **hijack** ei onnistunut väärentämään lähdeosoitetta ja kohdeporttia tai TCP-sessio oli niin lyhyt, että se ehti sulkeutua ennenkuin väärennetty paketti saapui perille.  
Hyvin todennäköisesti ongelma johtuu vain omista taidoista.  
Ainakin tämän avulla saan sellaisen käsityksen, että TCP-session kaappaaminen on vaikeampaa, kuin esim. Edellisen ICMP:n väärentäminen.  



