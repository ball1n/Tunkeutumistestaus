# h6 Attaaack

## x) Lue/katso/kuuntele ja tiivistä

- € Yehoshua and Kosayev 2021:[Antivirus Bypass Techniques](https://www.oreilly.com/library/view/antivirus-bypass-techniques/9781801079747/), luku:
  - [Chapter 1: Introduction to the Security Landscape](https://www.oreilly.com/library/view/antivirus-bypass-techniques/9781801079747/B17257_01_Epub_AM.xhtml#_idParaDest-18)

    - Nykymaailmassa antivirus ohjelmat ovat tärkeässä roolissa päätelaitteiden tietoturvassa. Artikkelissa kerrotaan mitä AV tyyppejä on ja miten ne toimivat. Kopioin suoraan tekstistä itseäni kiinnostavimmat            kohdat ja liitin kuvankaappaukset, missä selitettiin miten tietyt AV-ohjelmat toimivat.

      ## Malware tyypit:
      - Virus: A malware type that replicates itself in the system.
      - Worm: A type of malware whose purpose is to spread throughout a network and infect endpoints connected to that network in order to carry out some future malicious action. A worm can be integrated as a                     component of various types of malware.
      - Rootkit: A type of malware that is found in lower levels of the operating system that tend to be highly privileged. Many times, its purpose is to hide other malicious files.
      - Downloader: A type of malware whose function is to download and run from the internet some other malicious file whose purpose is to harm the user.
      - Ransomware: A type of malware whose purpose is to encrypt the endpoint and demand financial ransom from the user before they can access their files.
      - Botnet: Botnet malware causes the user to be a small part of a large network of infected computers. Botnet victims receive the same commands simultaneously from the attacker's server and may even be part               of some future attack.
      - Backdoor: A type of malware whose purpose is – as the name suggests – to leave open a "back door", providing the attacker with ongoing access to the user's endpoint.
      - PUP: An acronym that stands for potentially unwanted program, a name that includes malware whose purpose is to present undesirable content to the user, for instance, ads.
      - Dropper: A type of malware whose purpose is to "drop" a component of itself into the hard drive.
      - Scareware: A type of malware that presents false data about the endpoint it is installed on, so as to frighten the user into performing actions that could be malicious, such as installing fake antivirus                        software or even paying money for it.
      - Trojan: A type of malware that performs as if it were a legitimate, innocent application within the operating system (for example, antivirus, free games, or Windows/Office activation) and contains                         malicious functionality.
      - Spyware: A type of malware whose purpose is to spy on the user and steal their information to sell it for financial gain.
    
      ## Suojausjärjestelmät:
    
     - EDR: The purpose of EDR systems is to protect the business user from malware attacks through real-time response to any type of event defined as malicious.
            For example, a security engineer from a particular company can define within the company's EDR that if a file attempts to perform a change to the SQLServer.exe process, it will send an alert to the               EDR's dashboard.

    - Firewall: A system for monitoring, blocking, and identification of network-based threats, based on a pre-defined policy.
    - IDS/IPS: IDS and IPS provide network-level security, based on generic signatures, which inspects network packets and searches for malicious patterns or malicious flow.
    - DLP: DLP's sole purpose is to stop and report on sensitive data exfiltrated from the organization, whether on portable media (thumb drive/disk on key), email, uploading to a file server, or more.


## Halonen, Rajala ja Ollikainen 2023: [PhishSticks Youtube Channel](https://www.youtube.com/@phishsticks_pentest/videos)

- Videoilla demonstroidaan kuinka Reverse Shell, Ransomware, Keylogger toimivivat ilman ja USB kanssa.

## Halonen, Rajala ja Ollikainen 2023: [PhishSticks Git Repository](https://github.com/therealhalonen/PhishSticks/)

- README.md on dokumentoitu projektin aikajana ja viikottain lisätty päivitys. 
- Viikko 38: Työ alkoi ja Github perustettu projektille
- Vikko 39: Eri lähteiden kautta haettiin tietoa payloadeihin
- Viikko 39: GUI tehtiin ransulle, Digisparkin saapui ja Arduinon sekä Digisparkin testaukset alkoivat
- Viikko 40: USB prototyyppi tehty Digisparkille, Digisparkin VID/PID formaatin vaihtamiselle tehty pythonilla automaatio 
- Viikko 41: Payloadit muokattu yksi rivisiksi, jotta suorittavat nopeammin
- Viikko 43: Keyloggerin payloadin muokkaamista ja tehostamista. Mietitty miten tuoda data, HTTPS POST vai sähköposti?
- Viikko 44: Keylogger valmis ja demovideo siitä
- Viikko 45: Mitigaatiot valmis payloadeille
- Viikko 46: Presis Helsecissä ja Penauskurssilla


## [MITRE Att&ck Frequently Asked Questions](https://attack.mitre.org/resources/faq/): Part 1. General.

- TTP = tactics, techniques and procedures.
- Tactics: Vastustajan taktinen tavoite eli syy suorittaa toiminta.
- Techniques: Kuinka vastustaja saavuttaa taktisen tavoitteen suorittamalla toiminnon.
- Sub-techniques: Alitekniikat on tarkempia kuvauksia vastustajan käyttämästä toimintatavasta.
- Procedures: Tarkat toteutukset, joita vastustaja käyttää tekniikoiden tai alitekniikoiden suorittamiseen. 


## [MITRE Att&ck Enterprise Matrix](https://attack.mitre.org/)

- Forced Authentication = Pakotettu todennus:
  - Vastustaja voi kerätä tunnistemateriaalia joko kutsumalla tai pakottamalla automaattisesti antamaan autentikaatio tietoja mekanismin kautta, josta voi sitten kaapata ne. SMB/WebDAV-autentikoinnin avulla          vastustajat voivat käyttää saadakseen pääsyn käyttäjätilille. Yleinen vastustajan tapa on lähettää spearphising emailin, jossa on linkki vastustajan hallitsemalle palvelimelle. 


## a) The OS pwns you

- Lähteenä toimii: Halonen, Rajala ja Ollikainen 2023: [Installing Windows 10 on a virtual machine](https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md)
- Aloitan lataamalla .iso filun [linkistä](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise) ja lataan ISO – Enterprise LTSC downloads 64-bit
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6f8fdf17-dd9f-422f-8eb1-1486be6901c6)
- Annan koneelle nimen, vaihdan verison Windows 10 ja lisään muistia. Loput vaiheet menen default vaihtoehdoilla. Vaihdetaan vielä prossujen määrä 1 -> 4
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8dd08095-b7aa-44e1-ad36-b8e7cb1fd523)
- Käynnistän winukka koneeni ja aloitettaessa kone kysyy asennustiedostoa, johon valitsen lataamani .iso filun -> Start
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8f21832b-5192-4ce4-b729-5d447e1262ca)
- Seuraan [Installing Windows 10 on a virtual machine](https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md) vaiheita Windows 10 asennuksissa ja tadaa, asennettu.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/cfab1751-b38e-41a3-806a-9856e0ba8f88)
- Seuraavaksi laitan winukan samaan verkkoon hyökkäyskoneeni Kalin kanssa. Koneen settings -> Network ja sieltä vaihdetaan yhteys Host-only Adapteri ja valitaan sama adapteri kuin hyökkäyskoneessa. Tämän jälkeen käynnistetään winukka kone uudestaan ja kokeillaan pingailla.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/7296e06f-0e74-48fb-8af4-fb559c78c6d4)
- tsekataan että winukalla ei pääse nettiin 
```
ping 8.8.8.8
```
- katotaan molempien koneiden IP-osoitteet ja pingailaan ristiin. Molemmilla koneilla sai yhteydet toisiinsa.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/d18fd2cd-38aa-4c90-a580-51c89e3045a6)

## b) Trustme.lnk. Kokeile PhishSticksin revshell vihamielistä tiedostoa, joka avaa käänteisen shellin hyökkääjän koneelle. Selitä, mitä tapahtuu ja miksi. Testaa, että pysyt antamaan kohdekoneelle komentoja reverse shellin kautta.

- Lataan [nc64.exe](https://github.com/therealhalonen/PhishSticks/blob/master/payloads/revshell_demo/.payload/nc64.exe) tiedoston "lasti" kansioon, jonka teen hyökkäyskoneelle. Teen myös tekstitiedoston, johon kirjoitan vain random sisältöä. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4575b95c-8e89-469e-90e2-3ab50eb425db)
- Seuraavaksi teen winukka koneelleni kansion johon tuon [linkistä](https://github.com/therealhalonen/PhishSticks/blob/master/payloads/revshell/README.md) haetun revshell koodin ja vaihdan iippariksi oman Kalin IP-osoitteen.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/d6c93faf-7a49-4ac6-ba25-a0e215709fbe)
- Otan molemmat koneet pois internetistä ja aloitan kokeilun. Aloitan hyökkäyskoneeltani kuuntelemaan porttia 9001 ja hostaamaan http serveriä portti 80:lla.
```
python3 -m http.server 80
```
```
nc -lvnp 9001
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/eb40f11f-9b8b-49a9-bbed-d1992a0e6b8e)
- ei toiminut. Löysin, että phistickin projektissa Ollikaisella oli ollut sama ongelma [linkki](https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/notes.md#week-47) ja yritän pistää Kalistani palomuurin pois. 

```
sudo ufw disable
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f3657285-6619-4188-8433-27921aaaa133)
- Kokeillaan aikaisemmat stepit uudelleen. Ei toiminut sama virheilmoitus mutta sitten tajusin, en ollut pistänyt IP-osoitetta jokaiseen tarvittavaan paikkaan. Kun avasin vbs tiedoston sain yhteyden winukkaan kalilta.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e855f4bc-15ee-4f5f-822d-c98278dafa7d)
- En saa toimimaan, jatkan eteenpäin. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/9f55a986-db33-4e9a-bbd1-7344dad677ba)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/77a8f437-236d-4b4a-9599-01ee324da248)
- Mutta ideana olisi, että kun usb syötetään tai tiedosto avataan niin revshell koodi avaa hyökkääjän tekstitiedoston ja lataa nc64.exen ja suorittaa sen, jolloin yhteys saavuitetaan. 


## d) PageRank. Laita linkki raporttiisi kurssisivun kommentiksi.

## c) Attaaack! MITRE Attack Enterprise Matrix: Demonstroi viisi tekniikkaa viidestä eri taktiikasta.

## Gather Victim Host Information:
 - T1592.001	Hardware 
   T1592.002	Software
   T1592.003	Firmware

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/5ad1a07d-2931-4ecc-b8be-e0adf94f8115)

- Nmappaan winukan ip-osoitetta, jotta saisin tietää mahdollisimman paljon -sA komennossa jotta saisin tietää version ja OS, mikä kohdekoneella on. Ainut hyödyllinen tieto itselleni on MAC address, joka kertoo, että on ORacle VB NIC.

## Phishing for Information

- T1598.002	Spearphishing Attachment

- Voisin koristellä hienon sähköpostin esimerkiksi Terolle, jossa olisi linkki minkä Tero tietenkin avaisi. Kyseisestä linkistä latautuisi Terolle [aikaisemman tehtävän](https://github.com/therealhalonen/PhishSticks/blob/master/payloads/revshell/README.md) reveshell koodi ja minä valkohattu hakkerinä sulkisin juuri avatun yhteyden Teron koneelle.


## Acquire Access

- Koska en ole loistava hakkeri vielä, menisin sieltä mistä aita on matalin ja ostaisin käyttäjätunnukset "BIG COMPANYN" työntekijältä. Tämä on erittäin tehokas taktiikka, koska tästä ei nouse ns. "hälytystä" ja ympäristössä pyörii tuttu henkilö ellei sitten ala korottelemaan äänekkäästi oikeuksiaan tai kopioimaan suuria määriä tietoja ja täten seurantarajat ylittyy. LAPSUS$ on tunnettu käyttävän tämmöisiä alkeellisia taktiikoita mutta ne valitettavasti toimivat erittäin hyvin. Mitä korkeammat käyttöoikeudet tai isommassa roolissa oleva työntekijä, sitä suuremmat vahingot. En muista nyt tarkalleen lukua mutta about yli 70% tietoturvariskeistä tai hyökkäyksistä ovat käyttäjien virheiden aiheuttamia. 

## Brute Force

- T1110.001	Password Guessing

- En lähde nyt demonstroimaan mutta etsin [lähteen](https://www.youtube.com/watch?v=Ia9ZcB9CEYw), jossa käydään läpi miten saadaan tehtyä helppo bruteforce ohjelma. Itselläni on heikko koodaustausta mutta uskon, että ajan kanssa saisin toimivan bf koodin.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/503fcad4-5dc9-43eb-a727-528fab69228b)

- Kyseinen koodi on aivan alussa mutta se periaatteessa tuo 3 random kirjainta/numeroa. Eli sillä voisi bruteforcata 3 merkin salasanan? Charlengthiä muuttamalla koodi lisää merkkejä.


## Lähteet



- https://attack.mitre.org/
- https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h6-attaaack
- https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise
- https://attack.mitre.org/resources/faq/#faq-0-0-header
- https://github.com/therealhalonen/PhishSticks
- https://www.youtube.com/@phishsticks_pentest/videos
- https://learning.oreilly.com/library/view/antivirus-bypass-techniques/9781801079747/B17257_01_Epub_AM.xhtml#_idParaDest-22
- https://ftp.kh.edu.tw/Linux/Redhat/en_6.2/doc/gsg/s1-managing-working-with-files.htm
- https://unix.stackexchange.com/questions/421808/shortest-way-to-download-from-github
- https://security.stackexchange.com/questions/118603/how-can-i-detect-the-remote-operating-system
- https://www.mygreatlearning.com/blog/nmap-commands/
- https://www.youtube.com/watch?v=Ia9ZcB9CEYw
