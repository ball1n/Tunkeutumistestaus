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





















