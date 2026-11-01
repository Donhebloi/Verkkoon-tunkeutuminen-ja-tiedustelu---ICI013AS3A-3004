# H2 Nuuh

## x) Lue ja tiivistä

Karvinen 2025: Wireshark - Getting Started  
- Wireshark on johtava tietoliikenne analysaattori  
- Suurinosa webbisurffaamisesta on suojattu TLS-salauksella  
- Wiresharkissa pystyy filtteröimään pakettilistaa eri protokollien avulla

Karvinen 2025: Network Interface Names on Linux  
- Verkkoliitäntä on melkein kuin verkkokortti, mutta se ei välttämättä ole fyysinen.
- Yleisiä verkkoliitäntöjä ovat esim. wlp4s0, joka on WiFi-kortti ja enp1s0, joka on langallinen Ethernet-kortti
- Eth0 ja wlan0 ovat vanhoja verkkoliitännän nimiä, joita uusimmat järjestelmät eivät enään käytä.  

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

Nyt wiresharkilla pääsee tutkimaan liikennettä.  

## d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista.

Aloitin suodattamalla wiresharkin pakettilistan **DNS** haulla ja valitsin listan ensimmäisen DNS-paketin. Wiresharkissa, sinisen evän alapuolella on hakukenttä, minkä avulla pystyy suodattamaan haluamia paketteja.  

<img width="1250" height="96" alt="image" src="https://github.com/user-attachments/assets/1aa494e9-d79d-46f1-b83c-73151b2b76f3" />  

Kun valitsin paketin, niin pakettilistan alapuolelle ilmestyi näkymä, mistä näkee paketin tarkemmat tiedot ja TCP/IP-mallin neljä kerrosta.  

<img width="946" height="104" alt="ipmallit" src="https://github.com/user-attachments/assets/db01394d-a387-4bf7-a257-f86ca1f4ab66" />  

Kerrokset ylhäältä alaspain:  
````
Linkkikerros: TCP/IP-mallin alin kerros. Ethernet ja wifi toimivat tässä kerroksessa. Linkkikerros huolehtii tiedonsiirrosta paikallisessa verkossa.
Internet-kerros: Toinen kerros. Huolehtii IP-osoitteista ja pakettien välittämisestä verkkojen välillä.
Siirtokerros: Kolmas kerros. Huolehtii tiedonsiirrosta laitteiden välillä. Käyttää porttinumeroita ohjatakseen datan oikealle ohjelmalle.
Sovelluskerros: Neljäs ja ylin kerros. Tarjoaa protokollat, joita ohjelmat käyttävät, kuten DNS-protokollan. 
````
Kerroksien selitykseen käytin **CoddyKit** sivuston materiaaleja.  
<sup>Linkki lähteissä</sup>

## e) Mitäs tuli surffattua?

Tiedoston lataamisen jälkeen, drag and droppasin tiedoston Kaliin ja avasin sen wiresharkissa, File -> Open.  
Ekana valitsin wiresharkin ylävalikosta Statistics -> Capture File Properties, josta näki kaappauksen tietoja.  

<img width="1191" height="642" alt="image" src="https://github.com/user-attachments/assets/eafbe7ab-57aa-4abb-b527-7a24febd83a7" />  

Tästä näkee mm.
````
Pakettien lukumäärän: 283
Kaappauksen koko: 122445 tavua
kaappauksen kesto: 7.536 sekunttia
````

Sitten lähdin tutkimaan protokollia. Valitsin ylävalikosta Statistics -> Protocol Hierarchy  

<img width="1164" height="210" alt="image" src="https://github.com/user-attachments/assets/092099e3-445b-4f36-84d7-c37f24271c50" />  

Tästä näkee protokollat, uudestaan pakettien määrän ja kuinka suuren osan paketeista kukin protokolla vie.  
````
Ethernet: Kaikki 283 pakettia kulki Ethernet-verkossa.
IPv4: 281 pakettia.
UDP: 44 pakettia, josta QUIC 14 pakettia ja DNS 30 pakettia.
TCP: 237 pakettia, josta TLS 99 pakettia.
ARP: 2 pakettia.
````

Sitten katsoin vielä kaappauksen päätepisteet, ylävalikosta Statistics -> Endpoints.  

<img width="971" height="121" alt="Näyttökuva 2026-11-01 173953" src="https://github.com/user-attachments/assets/f75c860b-9f82-41df-91b2-4129134aaee9" />  

<img width="1089" height="192" alt="Näyttökuva 2026-11-01 174006" src="https://github.com/user-attachments/assets/321f4fa6-1bbf-4a4a-98e5-76c17b4eaa53" />  

Kaappauksessa näkyy kaksi Ethernet-päätepistettä ja seitsemän IPv4-päätepistettä. 


## f) Vapaaehtoinen

Vapaaehtoinen jää nyt tekemättä.


## g) Minkä merkkinen verkkokortti käyttäjällä on?

Lähdin selvittämään verkkokortin merkkiä MACLookup sivuston kautta. Syötin wiresharkin endpoints sivulta löydetyn "52:54:00:2f:e1:e5" MAC osoitteen sivustolle, mutta vastaan tuli ongelma.  

<img width="1151" height="494" alt="image" src="https://github.com/user-attachments/assets/30e3b353-410b-4f54-91fe-078797b131af" />  

Mitään merkkiä ei löytynyt. MAC osoite on "Locally Administered Address" eli paikallisesti määritetty. Verkkokortti on todennäköisesti virtuaalinen, eikä kenenkään fyysisen valmistajan.


## h) Millä weppipalvelimella käyttäjä on surffaillut?

Aloitin menemällä pakettilistaukseen ja suodattamalla **http**, mutta tulokseksi sain tyhjän listauksen.  
Tehtävänannossa on mainittu, että yhteys on suojattu TLS-salauksella, joten tämän jälkeen kokeilin suodattaa pakettilistan **tls** haulla.  

<img width="1660" height="340" alt="image" src="https://github.com/user-attachments/assets/5396f487-8cdc-49ee-b9c0-8980271badcf" />  

Sieltä tuli hyvää tietoa näkyviin. Info sarakkeissa joissa on "Client Hello" niin lukee myös millä verkkosivulla on käyty.  
````
(SNI=terokarvinen.com)
(SNI=gc.zgo.at)
(SNI=terokarvinen.goatcounter.com)
````
Mutta tästä ei nyt kuitenkaan webbipalvelinta selvinnyt. Valitsin ensimmäisen sarakkeen missä lukee "terokarvinen.com" ja lähdin availemaan TLS:ssän tietoja.  

<img width="950" height="393" alt="image" src="https://github.com/user-attachments/assets/1440c76a-f7f9-4af4-a670-67753400d255" />  

Päädyin osioon "Server Name Indication extension" josta ajattelin löytäväni mikä webbipalvelin on kyseessä. No mutta enpä löytänyt, sielläkin luki vain "terokarvinen.com"  
Päätin tämän jälkeen hyökätä komentorivin kimppuun ja kokeilla **curl** komentoa.  
````
curl -I https://terokarvinen.com
````
Lisäsin komentoon -I option jotta komentoriville tulostuisi vain HTTP headerin tiedot, eikä ihan kaikki sivun tiedot.  

<img width="589" height="311" alt="image" src="https://github.com/user-attachments/assets/1ca32797-246f-48fb-b7de-40eb8aef9867" />  

Ja tästä selvisi Apache webbipalvelin.  
Tein saman myös terokarvinen.goatcounter.com ja gc.zgo.at osoitteille.  

<img width="503" height="183" alt="image" src="https://github.com/user-attachments/assets/c85e48f2-c0af-4fd3-941d-b72dd7b2ceea" />  

gc.zgo.at osoitteelle serveriksi ilmeni BunnyCDN, mikä nopeuttaa verkkosivujen ja niiden sisällön lataamista.  
terokarvinen.goatcounter.com ei paljastanut serveriä curl komennolla.  
En tosiaan tiedä, oliko tämä oikea tapa selvittää nämä asiat, mutta ainakin näin sai jotain selville.  

## i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi.

Aloitin taas valitsemalla **eth0** verkkoliitännän, pistin wiresharkin pyörimään, avasin selaimen ja kävin adidaksen sekä hotels.com sivuilla.  
Sivustot oli muutaman sekunnin auki ja wireshark sai kaapattua 1990 pakettia.  
Valitsin analysoitavaksi yhden DNS ja TCP paketin.  
DNS:  

<img width="1102" height="15" alt="image" src="https://github.com/user-attachments/assets/34651f0b-d835-4267-a514-535032e64a56" />  

<img width="948" height="297" alt="image" src="https://github.com/user-attachments/assets/94d954d1-a8c7-4c95-89b9-06a6242f1c9c" />  

Tutkin pakettia numero 364, joka sisältää DNS-kyselyn. Paketin koko on 73 tavua, joka lähtee virtuaalikoneeltani IP-osoitteesta 10.0.2.15 ja sen kohdeosoite on 192.168.50.1. DNS-kysely käyttää UDP-protokollaa, sen lähdeportti on 52080 ja kohdeportti on 53.  
Tietokone kysyy tässä DNS-palvelimelta osoitetta www.adidas.fi ja HTTPS-tietueita. Kyselyn tyyppi on HTTPS (65), jonka avulla selaimet ja verkkoyhteydet saavat tiedot verkkosivustoon yhdistämisestä DNS-kyselyn aikana.  

TCP:  

<img width="1507" height="19" alt="image" src="https://github.com/user-attachments/assets/602a8abe-b0f1-4de4-a1f5-4bb129979306" />  

<img width="947" height="398" alt="image" src="https://github.com/user-attachments/assets/39d538aa-2139-4ffd-855d-a37b0ac4fa60" />  

Tässä tutkin pakettia numero 5, joka sisältää SYN-paketin, mikä liittyy TCP-yhteyden muodostamiseen. Paketin koko on 74 tavua, paketti lähtee liikkeelle virtuaalikoneestani IP-osoitteesta 10.0.2.15 palvelimen IP-osoitteeseen 34.149.226.178.  
Paketin lähdeportti on 53156 ja kohdeportti on 443. Portti 443 on standardi portti HTTPS liikennettä varten. TCP-flags kohdassa näkyy aikaisemmin mainittu SYN, eli tietokone yrittää aloittaa TCP-yhteyden palvelimeen.  
TCP Segment Lenght on 0 tavua, eli paketissa ei ole varsinaista dataa.  
TCP-yhteyden muodostaminen alkaa ns. Kolmivaiheisella kättelyllä. Eli asiakas lähettää SYN-paketin, palvelin vastaa SYN-ACK-paketilla ja sitten asiakas kuittaa ACK-paketilla. 

### Lähteet

Karvinen - https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/  
Karvinen, Wireshark - Getting Started - https://terokarvinen.com/wireshark-getting-started/  
Karvinen, Network Interface Names on Linux - https://terokarvinen.com/network-interface-linux/#examples-of-common-network-interface-names  
CoddyKit, TCP/IP:n neljän kerroksen yleiskatsaus - https://www.coddykit.com/fi/courses/networking_fundamentals/the-four-tcp-ip-layers-overview-10134730  
MACLookup, MAC Address Lookup - https://maclookup.app/  
HTTPS checker, What Is the DNS HTTPS Record (Type 65) and How Does It Work? - https://httpsornot.com/blog/what-is-dns-https-record  
geeksforgeeks, TCP flags - https://www.geeksforgeeks.org/computer-networks/tcp-flags/
geeksforgeeks, TCP 3-Way Handshake Process - https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/
paloalto networks, What Is a TLS/SSL Port? - https://www.paloaltonetworks.com/cyberpedia/what-is-tls-ssl-port
Wireshark Q&A, Why are 0 length TCP packets returned on some HTTP / TCP sessions? - https://osqa-ask.wireshark.org/questions/52702/why-are-0-length-tcp-packets-returned-on-some-http-tcp-sessions/

