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


