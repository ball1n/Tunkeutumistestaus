## x) Lue/katso ja tiivistä.
OWASP 2021: OWASP Top 10:2021
- A01:2021 – Broken Access Control (IDOR ja path traversal ovat osa tätä)
  - OWASP Top 1 haavoittuvuus
  - Broken Access Control on haavoittuvuuden tyyppi, joka mahdollistaa luvattomien käyttäjien pääsyn tietoihin tai järjestelmiin. 
  - Yleisiä haavoittuvuuksia on vähimmäisoikeuksien periaatteen rikkominen, pääsyvalvonnan tarkistuksen kiertäminen ja CORS-määritysvirheet
  - Ennaltaehkäisy on työlästä ja vaatii asetusten muokkaamista mahdollisimman turvalliseksi, riippuen organisaation tarpeista tietenkin.

- A10:2021 – Server-Side Request Forgery (SSRF)
  - Server-Side Request Forgery (SSRF) on serverin puolella tapahtuvan pyynnön väärentämishyökkäys. Hyökkääjä väärinkäyttää palvelimen toiminnallisuuttaa saadakseen pääsyn tai muokatakseen resursseja. Hyökkäys     
    kohdistuu sovellukseen, joka tukee tietojen tuontia URL-osoitteista tai sallii niiden lukemisen URL-osoitteista. 
  - SSRF hyökkäyksen ehkäisemiseksi tarvitsee muokata "Network layer" ja "Application Layer". 

PortSwigget Academy:
- Access control vulnerabilities and privilege escalation (IDOR on osa tätä)
  - Vertical privilege escalation, jos ei-admin käyttäjä saaa oikeuden admin sivulle mistä voi esim. poistaa käyttäjiä
  - Unprotected functionality, käyttäjä voi saada admin oikeudet menemällä suojattomaan URL-osoitteeseen
  - Parameter-based access control methods, sovellus antaa korkeammat oikeudet tietyn arvon kautta URL-osoitteesta
  - Broken access control resulting from platform misconfiguration, väärin konfiguroitu alusta, jossa HTTP headerilla voi saada vääriä oikeuksia
  - Broken access control resulting from URL-matching discrepancies, polkujen arvot eivät ole tarkkoja ja syöttämällä ns. sinnepäin voi johtaa pääsyjä vääriin paikkoihin
  - Horizontal privilege escalation, oikeus toisen käyttäjän tiedostoihin, esim. muokkaamalla URL:n ID parametria
  - Horizontal to vertical privilege escalation, jos pääsee käsiksi admin käyttäjään ja suorittaa sillä toimenpiteitä

- Server-side template injection
  - Server-side malli injektio tarkoittaa tilannetta, jossa hyökkääjä pystyy käyttämään alkuperäistä mallin syntaksia upottaakseen haitallisen kuorman malliin, jonka jälkeen se suoritetaan palvelinpuolella.
  - Paras tapa estää palvelinpuolen mallin injektiota on olla sallimatta käyttäjien muokata tai lähettää uusia malleja. Tämä ei kuitenkaan aina ole mahdollista liiketoimintavaatimusten vuoksi.
- Server-side request forgery (SSRF)
  - Tyypillisessä SSRF-hyökkäyksessä hyökkääjä saattaa aiheuttaa palvelimen tekemään yhteyden organisaation infrastruktuurissa oleviin vain sisäisiin palveluihin. Toisissa tapauksissa he voivat pakottaa   
    palvelimen yhteyteen mielivaltaisiin ulkoisiin järjestelmiin. Tämä voisi johtaa arkaluontoisten tietojen vuotamiseen, kuten käyttöoikeuksien todennustietoihin.
  - Tavallisia SSRF hyökkäysmethodeja:
    - SSRF attacks against the server
    - SSRF attacks against other back-end systems
    - SSRF with blacklist-based input filters
    - SSRF with whitelist-based input filters
    - Bypassing SSRF filters via open redirection
- Cross-site scripting
  - Cross-site scripting (XSS) on verkkohaavoittuvuus, joka mahdollistaa hyökkääjän kompromisoida vuorovaikutukset, joita käyttäjillä on haavoittuvan sovelluksen kanssa.
  - Cross-site scripting toimii manipuloimalla haavoittuvaa verkkosivustoa siten, että se palauttaa käyttäjille haitallista JavaScriptiä. Kun haitallinen koodi suoritetaan uhrin selaimessa, hyökkääjä voi täysin 
    kompromoida heidän vuorovaikutuksensa sovelluksen kanssa.

Karvinen 2020: Using New Webgoat 2023.4 to Try Web Hacking
  - Tero käy läpi miten Webgoatin avulla voi suorittaa WEB tunkeutumistestausta

## a) Totally Legit Sertificate. Asenna OWASP ZAP, generoi CA-sertifikaatti ja asenna se selaimeesi. Laita ZAP proxyksi selaimeesi. Osoita, että hakupyynnöt ilmestyvät ZAP:n käyttöliittymään.

- Aloitan päivittämällä Kalin ja asentamalla Javan. "sudo apt-get update" ja "sudo apt-get install openjdk-17-jre"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1bfc7ba1-afd4-4c62-92e2-3fb415b30c1a)
- Tämän jälkeen asennan palomuurin ja pistän sen päälle. "sudo apt-get install ufw" ja "sudo ufw enable"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/41f7052d-5c98-42de-a0ff-4ec7d98b0302)

- Käyn lataamassa ZAP:n https://www.zaproxy.org/download/
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/75160576-0369-4edd-a1a4-279b0e13b194)

- Siirryn "cd Downloads" kansioon ja unzippaan tiedoston "unzip ZAP_2.14.0_Crossplatform.zip". "ls" komennolla näen, että tiedosto on purettu.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/38d1812e-be6c-43f6-bf1e-14cd4862fa14)
- Siirryn tiedostoon "./ZAP_2.14.0/" ja avaan sen "./zap.sh"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/561c6392-b729-435e-ba41-afefe26c2d19)
- Uuden CA-sertifikoinnin luominen onnistuu Tools-> Options-> Dynamic SSL Certificates
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f12f2f28-1ead-4ee7-9066-ebb9c432c4e0)
- Painamalla "save" se tallentuu ja komentokehotteessa näkyy myös polku minne tallentunut
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/fe80acdb-bdd6-49e8-8adf-1bb5ae6e4974)
- Siirryn Firefoxiin, sieltä Application Menu -> Settings -> Privacy & Security -> View Certificates -> Import. Etsin tallennetun zap_root_ca.cer tiedoston ja valitsen sen. Valitsen, että luotan siihen myös.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/aedbdd63-23fd-4782-a733-7c0827a0a9e0)
- ZAP:ssa ei näy vielä mitään. Käyn muuttamassa portin 8080 -> 8081 ZAP:ssa 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/a027c184-2d3e-44db-8c07-8abe75c347e8)
- Sekä Firefoxissa network Managerista. HTTP Proxy "localhost" ja Port "8081". Täppään "Also use this proxy for HTTPS" tämä siksi, että toimii myös HTTPS sivuille?
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/06ebeebd-9d93-4cae-81d2-03deaf25485f)
- Nyt tulee ZAP:iin dataa
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/a0084902-af7a-49e0-80ab-406e026a6e48)

## b) Kettumaista. Asenna FoxyProxy Standard Firefox Addon, ja lisää ZAP proxyksi siihen.

- 































