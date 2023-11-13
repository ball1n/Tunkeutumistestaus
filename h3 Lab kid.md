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


## c) Tee koneille virtuaaliverkko, jossa
Kali saa yhteyden Internettiin, mutta sen voi laittaa pois päältä
Kalin ja Metasploitablen välillä on host-only network, niin että porttiskannatessa ym. koneet on eristetty intenetistä, mutta ne saavat yhteyden toisiinsa
Osoita eri komennoilla, että Internet-yhteys katkeaa: 'ping 1.1.1.1', 'ping www.google.com', 'curl www.google.com'

- Teen host-only networkin Kalin ja Metan välille
- oracle VM Managerista -> File -> Host Network Manager ja create -> Jolloin luodaan uusi host adapteri
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f98dc85a-41ba-4d9e-8c20-06570a21a06d)

- Avaan VM koneen Kali asetukset -> Network
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8dbdc04d-2ebb-4814-aef7-6b87dc9cb27c)
- Valitsen Adapter 2 ja juuri luodun uuden hostin
- Kalin saa pois internetistä kun ruksii "cable connected" adapter 1 kohdalla, tein niin.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/5787027d-fde0-4c0c-8645-7a05265161e6)


- Metasploitin VM koneesta avaan myös Network asetukset ja valitsen Adapter 1 kohtaan Host-only ja valitsen host 2
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/01191d5c-7c80-4e3b-93fc-6bab2ca8d84b)

- Käynnistän koneet uudelleen

- Meta koneesta komennolla ifconfig selvitän koneen ip-osoitteen ja pingaan google 8.8.8.8 varmistakseen, ettei kone ole internetissä
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/c7bf7ae6-79b8-45d1-92a2-2b4f06d1c2fc)
- Jostain syystä en saa Ip osoitetta.
- Ongelma selvitetty, Host Netwrok Managerista ei ollut DHCP päällä
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/7091bc7a-37c5-4abe-ac64-df8e4b97353c)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/86f81fcd-e6f3-41e2-931c-28a2c12da2f8)
- Kokeillaan uudelleen pingailuja
- Kalin IP 192.168.88.4, ei ole avoin internettiin ja pingaus onnistuu meta Vm konetta päin.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/ddc13017-957e-4436-8139-024192367e14)

- Meta VM:n IP 192.168.88.3
- Meta ei ole avoin internettiin ja pingaus onnistuu Kali VM konetta päin
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/711c2bcc-2938-4429-a96c-85fe39799af2)

## d) Etsi Metasploitable porttiskannaamalla (db_nmap -sn). Tarkista selaimella, että löysit oikean IP:n - Metasploitablen weppipalvelimen etusivulla lukee Metasploitable. Katso, ettei skannauspaketteja vuoda Internetiin
- Ennen kuin aloitan varmistan, että Kali on pois internetistä pingaamalla Googlea 8.8.8.8
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/ebb996a2-7fd9-4e3d-b538-739ebf715db9)
- Käynnistän Metasploit frameworkin komennolla msfconsole, etsin hosts komennolla metsploit koneen IP-osoitetta mutta en löydä mitään. Kokeilen db_nmap -sn 192.168.88.3 (Varmistan vielä omalla koneella missä internet toimii, että IP varmasti on Metasploitin.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/5e6816e7-94c6-4974-ab82-5938d567fbaa)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b33d0a0b-6499-46f9-a9c0-dba2a9fbd4bf)
- Taisin vain tehdä väärässä järjestyksessä.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4b6386bd-6a75-4841-8972-d192e6fb96fc)

## e) Porttiskannaa Metasploitable huolellisesti (db_nmap -A -p0-). Analysoi tulos. Kerro myös ammatillinen mielipiteesi (uusi, vanha, tavallinen, erikoinen), jos jokin herättää ajatuksia.
- Porttiskannaan laajemmalla haulla metasploitable IP:n db_nmap -A -p0- 192.168.88.3. -A hakee laiteversioita, -p- skannaa kaikki portit
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/18396774-3934-41ee-aebc-05f1a05936b4)
- nmap löysi 30 avointa porttia
- Portti 21 FTP on yhteys minun Kaliin.
- Portti 22 SSH antaa paljon dataa, hostkey, versio
- Yleisesti haku antaa paljon infoa porttien järjestelmistä, versioista ja lisäinfoa (en osaa selittää tarkalleen, enkä ehdi googletella jokaista)

## f) Murtaudu Metasploitablen VsFtpd-palveluun Metasploitilla (search vsftpd, use 0, set RHOSTS - varmista osoite huolella, exploit, id)
- Etsin Metasploitablesta VsFtpd-palvelua haulla search vsftpd
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/76ebe52a-6094-4457-8861-9290893f81f0)
- Valitse vaihtoehto 1, koska rankki on parempi ja komennolla "use 1" se tulee komentokehoitteeseen.
- "show options" komennolla saan muokattua defaultti vaihtoehdoista haluamakseni. ja "set rhosts 192.168.88.3" annan exploitille kohteen IP-osoitteen
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4acc2b35-d9e2-4496-a3e3-0be8d9e188f8)
- "exploit" komennolla msf suorittaa hyökkäyksen
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/0531ce33-acd3-41a7-af07-d9af1a964b93)
- kuten kuvassa näkyy olen päässyt sisälle ja käyttäjänä on root

## g) Parempi sessio. Tee vsftpd-hyökkäyksestä saadusta sessiosta parempi. 
- Tämä tehtävä oli itselle vaikea ja tein sen apua käyttäen. Linkkinä:  (https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/full-ttys)  & (https://github.com/Jiikiam/PenTestingCourse/blob/main/H3LabKid/h3LabKid.md)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e8e18fcb-80b3-4527-8b9c-fcf319e8b672)
- tallennan session CTRL+Z ja etsin shell_to_meterpreter
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1e3d372e-1cd8-4e32-ab63-74adba5de094)
- Valitsen komennolla "use 0" ja katson "show options" komennolla mitä tehdään. 
- otan tallennetun "set session 1" komennolla mukaan ja "run" komennolla ajan hyökkäyksen.
- Komennolla "sessions -l" listaa tehdyt sessiot
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/401341c1-8216-45dd-acca-e5c85ae5a8b3)

- valitaan session 2 komennolla "sessions -i 2"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/39cbbfad-7bf5-4c4e-9618-7046c493dae8)
- Sessio on muutettu meterpreteriksi.

## h) Etsi, tutki ja kuvaile jokin hyökkäys ExploitDB:sta.
- Valitsin heti ensimmäisen "Splunk 9.0.5 - admin account take over", koska olen Splunkilla vähän leikkinyt ja kiinnostus heräsi. 
- Kyseisessä hyökkäyksessä low-privilege käyttäjä, jolla on "edit_user" rooli annettuna pystyy eskaloimaan oikeuksia admin rooliin asti antamalla tarkoin tehtyjä web pyyntöjä.
- Linkki hyökkäykseen: https://www.exploit-db.com/exploits/51747

## i) Etsi, tutki ja kuvaile hyökkäys 'searchsploit' -komennolla. Muista päivittää.
- Päivitetään ensimmäisenä "searchsploit -u", jonka jälkeen haen "searchsploit -t azure". Otin "Azure Apache Ambari 2302250400 - Spoofing" ja googletin sen, jos löytyisi ExploitDB:stä. Sieltähän se löytyi: https://www.exploit-db.com/exploits/51546
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/16583ff8-ccd9-43b3-9045-85c63cd2bc9a)
- Hyökkäyksen infot: 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/256fc11c-8b8d-498e-8b27-a74137e9c6a4)
- Hyökkääjän pitää lähettää uhrille spooffattu URL, jonka uhrin pitää executea.
- Tämän haavoittuvuuden onnistunut hyväksikäyttö edellyttää, että hyökkääjällä tai kohteena olevalla käyttäjällä on erityiset korkeammat käyttöoikeudet. Vain käyttäjät, joilla on roolit "Cluster Admin" ja "Cluster Operator", voivat käyttää tätä.

## j) Kokeile vapaavalintaista haavoittuvuusskanneria johonkin Metasploitablen palveluun
- Kokeilen Niktoa komennolla "nikto -h 192.168.88.3"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/c4782d53-8495-465a-8ebb-5453b46737be)
- Haavoittuvuusskanneri kertoo esim. Apache on vanha ja mitä haavoittuvuuksia sieltä löytyy, mitä kansioita löytyy ja on "avoimena", "/#wp-config.php#: #wp-config.php# file found. This file contains the credentials.
" poppasi pahimpana silmään, koska sieltä löytyy mahdollisesti tunnuksia.

## k) Kokeile jotain itsellesi uutta työkalua, joka mainittiin x-kohdan läpikävelyohjeessa
- Aloitan hakemalla komennolla "services" ja valitsen UnrealIRCd, jota käsiteltiin x) kohdan artikkelissa: https://learning.oreilly.com/library/view/mastering-kali-linux/9781801819770/Text/Chapter_10.xhtml#_idParaDest-249
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/c11e66a2-61ea-4b00-904e-e611cb9fd7e6)
- Ja kuten aikaisemmin "use 0" valitsee haluaman vaihtoehdon, "show options" näyttää infot, "set rhosts 192.168.88.3"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/dcef0cd3-86c4-4e60-a00b-f3800a771d20)
- Tämä hyökkäys tarvitsi tarkemmat tiedot, lshotin, payloadin ja toisen portin, jonka katsoin nmap tuloksista.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/33801287-a9e6-4a12-a5dd-15f4f4b3fa5c)


## Lähteet:
- https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h3-lab-kid
- https://github.com/Jiikiam/PenTestingCourse/blob/main/H3LabKid/h3LabKid.md
- https://msrc.microsoft.com/update-guide/vulnerability/CVE-2023-23408
- https://rikumannonen935063021.wordpress.com/2022/04/09/h2-turbo-boosted/
- https://sourceforge.net/projects/metasploitable/
- https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/full-ttys
- https://learning.oreilly.com/library/view/mastering-kali-linux/9781801819770/Text/Chapter_10.xhtml#_idParaDest-250
- https://0xdf.gitlab.io/about
- https://myllys.wordpress.com/tunkeutumistestaus-2021-syksy-harjoitus-2/
- https://www.exploit-db.com/exploits/51747
- https://www.exploit-db.com/exploits/51546






 







