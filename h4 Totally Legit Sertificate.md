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

- latasin foxyproxyn Googlen kautta ja avasin sen extension osasta.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/0a7723c8-89dc-4901-a429-423dea4d3088)
- Menemällä "Add" avautui uusi ikkuna, johon syötin oman proxyni tiedot. -> "Save"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/528ce74c-4d53-49c8-9c69-a7eada8c3474)
- Avasin Googlen ja nyt näkyi enemmän sivuja
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/9c9e0998-814b-4f40-ab99-53e4c97fa512)
- Itselle jäi vähän epäselväksi tämä tehtävä ja sen suorittaminen. Mikä idea tässä on? ZAP seuraa web liikennettä ja sen avulla voi löytää heikkouksia tai korjata niitä. Miten Foxyproxy liittyy tai auttaa? Tuoko se     
  lisää infoa ZAP:in päälle vai onko vain sovellus jolla pystyy vaihtamaan proxy asetuksia? Ihan mielenkiinnosta heräsi, tuntuu, että en itse sisäistänyt tätä vaihetta aivan kokonaan. 

## PortSwigger Labs. Ratkaise tehtävät. Selitä ratkaisusi: mitä palvelimella tapahtuu, mitä eri osat tekevät, miten hyökkäys löytyi, mistä vika johtuu. (Voi käyttää ZAPia, vaikka malliratkaisut käyttävät harjoitusten tekijän maksullista ohjelmaa)

## c) Insecure direct object references
 - Tehtävässä käyttäjien keskustelut tallentuu palvelimen systeemille ja hakee ne käyttämällä staattista URL-sosoitetta.
 - Avaan ZAP:in ja aloitan tehtävän. Seuraan tehtävän ohjeita -> Live chat -> Aloitan keskustelun ja seuraan mitä tapahtuu ZAP:ssa -> ei oikein mitään -> lataan view transcript ja huomaan, että keskustelu on 
      tallentunut. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/2578c941-524c-4494-8a05-5a0a81b91851)
 - Miten tätä voi hyödyntää? Liitin URL osoitteeseen "https://0a190050038eda72805635d300ac00b1.web-security-academy.net/download-transcript**/1.txt**" Jolloin transcriptin lataus alkoi ja Carloksen salasana tuli 
      esille.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4336239c-7fdb-4b72-af54-97b18284c8dd)
 - Kirjaudun sisään carloksen salasanalla.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/3209c0af-a2aa-4688-ac58-cac44a25b0a3)

## d) File path traversal, simple case
- Harjoituksessa on haavoittuvuus kuvien näyttämisessä. Joten availen tuotteita missä on kuvia. ZAP:ssa GET hhtps headeri näyttää tältä ja ohjeiden mukaan sitä pitäisi jatkaa "../../../etc/passwd"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/3da9c1b6-0ddb-41b5-bb72-036e5fa24049)
- Kopion "https://0a5d000104c343ef806fa841003400e2.web-security-academy.net/image?filename=" ja lisään perään "../../../etc/passwd" eli "https://0a5d000104c343ef806fa841003400e2.web-security-academy.net/image?filename=../../../etc/passwd HTTP/1.1" kokeilen ilman HTTP/1.1 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/821d8d85-1d59-417b-81e3-dfaaf4b187e1)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/ea631101-20ca-4339-a5d5-3ace65e8e223)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/63f2c83d-86ef-47d1-ad99-18f8219f0892)
- Harjoitus sanoo, että olen suorittanut sen. en löydä sitä etc/password kansiota itse ainakaan ZAP:sta :D Siirryn seuraavaan, kulutin liikaa aikaa jo tässä.

## e) File path traversal, traversal sequences blocked with absolute path bypass
- hyvin samanlainen tehtävä kuin aikaisempi. Pitää taas lisätä filename kohdalle "/etc/passwd"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/378b37e8-a542-40e9-9d05-e7d91ba15c0a)
- Itselläni oli vaikeuksia löytää miten saan noita pyyntöjä muokattua helposti mutta täältä löytyi hyvä esimerkki: https://kulonpaa.com/?p=338
- Tämän jälkeen kun pyyntö oli lähetetty sain etc kansion tiedot
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/cfc113f0-07d3-4198-81dd-29fdd27cc590)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8e9ed531-c6ab-4633-ba43-2c68f0f0936f)

## f) File path traversal, traversal sequences stripped non-recursively
- Sama idea kuin aikaisemmissa tehtävissä, nyt vain pitää tehdä hausta kai jatkuva? "....//....//....//etc/passwd"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/08064f36-a31a-4061-915f-999ae6f5e3c9)
- Avaan tuolta muokkauksen ja vaihdan GET pyyntöä. "https://0a1900e4046767898032df98002000dd.web-security-academy.net/image?filename=....//....//....//etc/passwd HTTP/1.1"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/3d89ca24-ceb7-45e7-9f54-4b81f90ce5f1)
- Tähän pitäisi tulla /etc/passwd sisältö mutta ei ole nyt 5min sisällä antanut mitään. Labra näyttää siltä, että olen raktaissut sen. Siirryn eteenpäin. Oman käsitykseni mukaan se tekee pyyntöjä tai etsii kansiota niin kauan, ennenkuin se löytyy?

# Server Side Template Injection (SSTI)

## g) Server-side template injection with information disclosure via user-supplied objects (Tämä on merkitty hieman vaikeammaksi, jätä viimeiseksi jos näyttää hankalalta)
- Teron pelottelu onnistui, jätän viimeiseksi.

# Server Side Request Forgery (SSRF)

## h) Basic SSRF against the local server
- Aloitin tehtävän menemällä tuotteen sivulle ja painamalla "check stock". ZAP liikenne näytti tältä, seuraavaksi muokkaan stockApi komentoa
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f4074ddc-de6b-4bb8-9e86-2e7a370bad7d)
- Liitän stockApi kohdalle URL:n 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f3bfeb0b-c196-4a4f-8fa0-3b833f0bfa42)
- Olen onnistuneesti poistanut käyttäjä "carloksen"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4eee5587-c8d3-444d-8084-a9b0102973c3)

# Cross Site Scripting (XSS)

## i) Reflected XSS into HTML context with nothing encoded

- Haku kentässä on XXS haavoittuvuus. Solve kentästä saa haun millä etsiä "alert" funkiota. "<script>alert(1)</script>"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/54226e65-9384-4468-aa1d-638892d1ff15)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/512843f3-e261-4048-ad8a-cdb4a5deed6b)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/70b78fa4-e8f0-45a9-8e84-51def2afac31)
- Yllättävän helppo, kun vastaus annetaan valmiiksi

## j) Stored XSS into HTML context with nothing encoded

- Aika sama kuin ylempi mutta säilytetty haavoittovuus, kommentti funktiossa. Samalla "<script>alert(1)</script>" mennään
- Jätän kommentin
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/542b921e-f7ab-482f-98c9-a983ab0f778b)
- "back to blog" jälkeen
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b553bccb-416d-40bd-96d7-72dbdbf722d3)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/009d9ed4-4b34-42e6-b939-25ad3cd065b1)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/70d9dffc-b6a9-4199-8831-e0d9e4445748)

## k) Asenna Webgoat 2023.4. (Uusi versio, jossa on eri tehtäviä kuin vanhemmissa)

- Seuraan Teron ohjeita. https://terokarvinen.com/2023/webgoat-2023-4-ethical-web-hacking/
- Itse olen jo asentanut Javan ja palomuurin
- Asennan WebGoatin komennolla "wget https://github.com/WebGoat/WebGoat/releases/download/v2023.4/webgoat-2023.4.jar" 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8ac69fd9-3e6f-4064-aea5-7fba80f99631)
- Seuraavaksi muutan portin toiseksi kuin mikä minulla on OWASP ZAP:ssa "java -Dfile.encoding=UTF-8 -Dwebgoat.port=8888 -Dwebwolf.port=9090 -jar webgoat-2023.4.jar"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/eb4585f6-7e2d-44f8-9a0a-1f9cc7f855ce)
- Luon käyttäjän Webgoattiin, ehkä nimeltä "carlos"

# Ratkaise WebGoat 2023.4

## m) Hijack a session (1)

- Oli vaikeuksia saada liikennettä ZAP:iin mutta kun pistin Foxyproxyn päälle niin liikenne tuli esille.
- Aloitan syöttämällä keskittyjä käyttäjiä ja salasanoja, sen jälkeen analysoin ZAP:ssa tuloksia
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4b3090dd-4f37-47f2-8777-0315bb692b2a)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/9aaad2bd-5a86-4676-8aad-9323395165a9)
- hijack cookie pysyy samana. 

- Palaan tehtäviin varmaan myöhemmin. Tämä ensimmäinen vaikutti jo todella vaikealta ja aika loppui kesken



Lähteet: 
- https://terokarvinen.com/2023/webgoat-2023-4-ethical-web-hacking/
- https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h4-totally-legit-sertificate
- https://www.youtube.com/watch?v=YO8rsCMVUyY
- https://portswigger.net/web-security/cross-site-scripting
- https://portswigger.net/web-security/ssrf
- https://portswigger.net/web-security/server-side-template-injection
- https://portswigger.net/web-security/access-control
- https://github.com/Jiikiam/PenTestingCourse/blob/main/H4TotallyLegitSertificate/h4.md
- https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/
- https://owasp.org/Top10/A01_2021-Broken_Access_Control/
- https://www.google.com/search?q=how+to+solve+Lab%3A+Basic+SSRF+against+the+local+server&sca_esv=583584307&sxsrf=AM9HkKm2YPY9CNfnvTtYhBk0yZhVbnlwDg%3A1700301153413&ei=YYlYZc3nGOLPwPAPo-OyoAs&ved=0ahUKEwiNnIqyo82CAxXiJxAIHaOxDLQQ4dUDCBA&uact=5&oq=how+to+solve+Lab%3A+Basic+SSRF+against+the+local+server&gs_lp=Egxnd3Mtd2l6LXNlcnAiNWhvdyB0byBzb2x2ZSBMYWI6IEJhc2ljIFNTUkYgYWdhaW5zdCB0aGUgbG9jYWwgc2VydmVyMgUQIRigAUj4G1DPBVjqFnABeAGQAQCYAaYBoAHYB6oBBDEyLjK4AQPIAQD4AQH4AQKoAgrCAgcQIxjqAhgnwgIEECMYJ8ICCxAAGIAEGLEDGIMBwgIREC4YgAQYsQMYgwEYxwEY0QPCAg4QLhiABBiKBRixAxiDAcICDhAuGIAEGLEDGMcBGNEDwgILEC4YgAQYsQMYgwHCAgUQLhiABMICBRAAGIAEwgIIEAAYgAQYsQPCAggQLhiABBjUAsICBBAAGAPCAgoQIxiABBiKBRgnwgIKEAAYgAQYigUYQ-IDBBgAIEGIBgE&sclient=gws-wiz-serp#fpstate=ive&vld=cid:10213f4e,vid:yblAc0upHC4,st:0
- Myös käytetty ChatGPT suomennoksiin




























