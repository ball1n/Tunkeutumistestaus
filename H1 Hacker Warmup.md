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
