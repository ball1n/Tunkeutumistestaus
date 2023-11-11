# H3 Lab Kid

x) 
## € Velu 2022: Mastering Kali Linux for Advanced Penetration Testing 4ed: Chapter 10 - Exploitation: kappaleet "The Metasploit Framework", "The exploitation of targets using Metasploit" ja "Using public exploits". 
The Metasploit Framework
- MSF on avoimen lähteen työkalu, joka on suunnattu tunkeutumistestaajille. 
- Kirjoitettu Ruby ohjeilmointi kielellä.
- MSF voi jakaa kolmeen eri osaan:
1. Kirjastot 2. Moduulit 3. Käyttöliittymä
1. Kirjastot: 
- REX: Tämä kirjasto tarjoaa erilaisia luokkia, jotka ovat hyödyllisiä hyökkäyksen kehittämisessä. Nykyisessä MSF:ssä REX käsittelee kaikkia ydintoimintoja, kuten socket-yhteyksiä, raakoja funktioita ja muita 
       muotoilutehtäviä.
- Framework core: tarjoaa perussovellusohjelmointirajapinnan (API) kaikille uusille kirjoitettaville moduuleille.
- Framework base: tarjoaa hyvän ohjelmointirajapinnan (API) istunnoille.

2. Moduulit:
- Metasploit Framework koostuu moduuleista, jotka yhdistetään hyökkäyksen suorittamiseksi.
- Exploits, Payloads, Auxiliary moduulit, Post moduulit, encoders ja No operations. Näitä moduuleja käytetään yhdessä tiedusteluun ja hyökkäysten toteuttamiseen kohteita vastaan.


## Vapaavalintainen läpikävely 0xdf tai ippsec (Kannattaa valita helppo; esim "Base Points: Easy")

- Valitsin "HTB:Broker" https://0xdf.gitlab.io/2023/11/09/htb-broker.html
- "Broken" on HackTheBoxissa julkaistu ei-kilpailulliseen jonoon korostaakseen sen suurta tietoturvariskiä. 0xdf hyödyntää ActiveMQ:ta saadakseen jalansijan ja sitten ekaloi pääkäyttäjäoikeudet käyttämälää oikeutta suorittaa nginx roottina. 
- 0xdf pystyttää valepalvelimen tiedostonluku oikeuden saamiseksi ja sen jälkeen lisää PUT kyvykkyydet ja kirjoittaa SSH-avaimen rootille. 

## Nyrkkeilysäkki ei kuulu. Etsi hakukoneesta kotitehtäväraportti, jossa Kali ja Metasploitable on asennettu samaan verkkooon VirtualBoxiin; sekä testaamalla osoitettu, että koneet on saatu irti Internetistä. Tällaiset tehtävät ovat olleet jonain vuonna esimerkiksi nimillä "Nyrkkeilysäkki" ja "Ei kuulu". (Löytyy hakukoneista, esimerkiksi hakusanoilla "tero karvinen nyrkkeilysäkki". Raportit voivat olla pitkiä, vain nuo mainitut kohdat tarvitsee käsitellä)


- Valitsin Riku Mannosen tekemän kotitehtävän (https://rikumannonen935063021.wordpress.com/2022/04/09/h2-turbo-boosted/)
- Mannonen asentaa Metasploitable 2 samaan verkkoon Kalin kanssa ja tarkistaa, ettei haavoittuva Metasploitable 2 näy internettiin.

## a) Asenna Kali virtuaalikoneeseen
- Itselläni on jo Kali asennettuna virtuaalikoneeseen
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/947e31de-834d-48b4-9ae9-52e238f12242)

## b) Asenna Metasploitable 2 virtuaalikoneeseen
- Lataan Metasploitable 2 täältä https://sourceforge.net/projects/metasploitable/

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/84b14709-3fb9-4128-bb68-2eb152aa0252)
- Tein uuden koneen ladatulla Metasploitable tiedostolla


## ) Tee koneille virtuaaliverkko, jossa
Kali saa yhteyden Internettiin, mutta sen voi laittaa pois päältä
Kalin ja Metasploitablen välillä on host-only network, niin että porttiskannatessa ym. koneet on eristetty intenetistä, mutta ne saavat yhteyden toisiinsa
Osoita eri komennoilla, että Internet-yhteys katkeaa: 'ping 1.1.1.1', 'ping www.google.com', 'curl www.google.com'

- Teen host-only networkin Kalin ja Metan välille
- oracle VM Managerista -> File -> Host Network Manager ja create -> Jolloin luodaan uusi host adapteri
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f98dc85a-41ba-4d9e-8c20-06570a21a06d)

- Avaan VM koneen Kali asetukset -> Network
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8dbdc04d-2ebb-4814-aef7-6b87dc9cb27c)
Valitsen Adapter 2 ja juuri luodun uuden hostin
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/eb438b35-d030-464d-ae3a-5b9eeaaa8fc6)
Metasploitin VM koneesta avaan myös Network asetukset ja valitsen Adapter 1 kohtaan Host-only ja valitsen host 2
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/01191d5c-7c80-4e3b-93fc-6bab2ca8d84b)








