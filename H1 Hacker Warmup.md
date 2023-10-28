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
