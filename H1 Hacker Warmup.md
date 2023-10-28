# H1 Hacker Warmup

x) The Art of Hacking (Video Collection) 
- Opetuskohta 4 käydään läpi kuinka aktiivista tiedustelua aloitetaan suorittamaan ja mitä työkaluja siihen käytetään.
- Aktiivinen tiedustelu aloitetaan portti skannauksella työkalu tähän Nmap mieluiten, koska on kaikista monipuolisin.
- Käydään läpi kuinka EyeWitness:in avulla voi käydä monta verkkosivua nopeasti läpi, joka voi skannaa nettisivun nopeasti ja löytää haavoittuvuuksia.
- Haavoittuvuusskannaus: Tietoverkon tai  verkon skannaamista jos sieltä löytyisi haavoittuvuuksia. 

x) https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf
- Artikkelissä käydään läpi kuinka ja miten Lockheed Martinin Cyber Kill Chain on saanut alkunsa. 
- Cyber Kill Chain on omassa työssäni tullut tutuksi ja sitä sovelletaan tietoturva-analyysejä tehtäessä. Toimenpiteet riippuu missä vaiheessa hyökkäys on, useimmiten vasta tiedustelussa. 

a) Ratkaise Over The Wire: Bandit kolme ensimmäistä tasoa (0-2).

Tehtävä 0
- SSH yhteys tietyllä käyttäjällä, osoitteeseen ja halutusta portista

![sss](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/08d61ade-2681-4723-a623-cf3aa0370a73)

Tehtävä 1
- Salasanan sai readme filusta aikaisemmasta ssh yhteydestä bandit0:aan
- Kirjauduin samanlailla mutta vain muutoksena nyt **bandit1**. 
- ls ja siellä on -filename, cat ./- näyttää mitä sielä lukee ja siinä on seuraava salasana.

![1111](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e310e8cb-8cf7-4405-8e3c-b4754bbafbee)

Tehtävä 2
- Aivan sama homma, nyt vain lopussa cat (filename)

![22222](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/d3879a07-4c88-4a66-bcc8-4ebb6b42644c)

b) Ratkaise Challenge.fi:stä yksi tehtävä, esim. Challenge.fi 2021 Where was this picture taken, Encoding basics. Tai joku Challenge.fi 2022. (Nimi vaihtui sattuneesta syystä, se on nykyisin Next Gen Hack Challenge)

- Valitsin tehtäväksi kuvan sijainnin selvittämisen.

![tetet](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e3ccf0b0-c3d7-46df-a2b4-016faed45c92)

Tämän voi ratkaista aika helposti, painamalla alt+enteriä, jonka jälkeen näet kuvan paikan. 

![blac](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/a66a23c5-a863-4438-8f29-542129f0e080)

c) Ratkaise PortSwigger Labs: Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data. (Edellyttää ilmaista rekisteröitymistä. Tehtävän voi ratkaista pelkästään selaimen osoitekenttää muokkaamalla.)

- Hyppäsin tehtävän yli

d) Asenna Linux virtuaalikoneeseen. Suosittelen joko Kali (viimeisin versio) tai Debian 12-Bookworm.

- Latasin Kalin täältä https://www.kali.org/get-kali/#kali-virtual-machines ja purin tiedoston, jonka jälkeen kone oli asennettu VMBoxiin.

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/71b95b84-1a70-4de1-8563-5d40790aba93)

e) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi (localhost). Analysoi tulokset.

- Ensiksi selvitän koneeni IP osoitteen jota lähden skannailemaan.
- Komennolla ifconfig tai ip addr saan selville koneeni IP osoitteen ja wlan yhteyteni IP-osoitteen.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/7d789227-0f9a-4b0e-8c53-fdeb6e0a3295)

komennolla nmpa -p1-1000 localhost scannaa halutun määrän portteja.
En ole aivan varma mutta blokkaako palomuuri asetukseni handshaket vai miksi ei ole edes 443 auki tjsp?
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/9c50f849-1e99-4e6a-aa47-789636aec37b)

f) Porttiskannaa kaikki koneesi (localhost) tcp-portit. Analysoi tulokset. (Edellisissä kohdissa mainittuja analyyseja ei tarvitse toistaa, voit vain viitata niihin ja keskittyä eroihin).

- Vaihtamalla komentoon -p- nmap skannaa kaikki portit. Analyysi ei muutu kun portit ei suostu juttelemaan.

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/71482487-f9bb-4df9-b664-ec82ac4a0325)

g) Tee laaja porttiskanaus (nmap -A) omalle koneellesi (localhost), kaikki portit. Selitä, mitä -A tekee. Analysoi tulokset. (Edellisissä kohdissa mainittuja analyyseja ei tarvitse toistaa, voit vain viitata niihin ja keskittyä eroihin.).

- Itselläni ei onnistu omasta mielestäni nyt tämä portti skannailu oikein. 
  - A komennossa auttaa havaitsemaan OS:n ja version. (enable OS detection and version scanning)

h) Asenna ja käynnistä jokin palvelin (apache, ssh...) koneellesi. Vertaile, miten porttiskannauksen tulos eroaa.

- ei onnistu porttiskannaus toivotulla tavalla ja aika loppuu itselläni tehtävien tekemiseen. Sirryyn eteenpäin. 

i) Kokeile ja esittele jokin avointen lähteiden tiedusteluun sopiva weppisivu tai työkalu. Hyviä esimerkkejä löytyy Bazzel: IntelTechniques: Tools ja Bellingcat: Resources, voit myös käyttää muuta itse valitsemaasi työkalua. Työkalua pitää siis myös kokeilla, pelkkä nimen mainitseminen ei riitä. Pidä esimerkit harmittomina, älä julkaise kenenkään henkilökohtaisia salaisuuksia raportissasi.

- Itse valitsen Virustotalin ja haen "kela.fi" 

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/41bb80fd-64fa-49a2-998d-d4252d1c2d76)

Sieltä "relations" kohdasta voi etsiä PDF tai Word tiedostoja, joita on ajettu automaattisesti VT:hen ja ladata omalle koneelle tai tutkia. 

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f55734c5-aa87-4b97-811a-16cc2e0ef3ca)

- Yksi toinen mielenkiintoinen on https://urlscan.io/ , jossa käyttäjät skannailee URL:eja. Sieltä voi löytää jotain jännää mitä ihmiset skannaa tajuamatta sitä, että on julkista dataa sen jälkeen.

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/32736e62-88cf-4c94-9360-04600018a471)

## Palaan porttiskannaus tehtäviin jos ehdin vielä

## Lähteet:

https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h1-hacker-warmup

https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_05_00/

https://www.codecademy.com/learn/getting-started-with-nmap/modules/basic-nmap-scans-configurations/cheatsheet

https://www.linux.fi/wiki/Nmap

https://www.kali.org/docs/virtualization/install-virtualbox-guest-vm/

https://overthewire.org/wargames/bandit/bandit3.html

https://2021.challenge.fi/challenges

https://medium.com/@theGirlWhoEncrypts/overthewire-bandit-level-1-level-2-9da2e3f51fb
