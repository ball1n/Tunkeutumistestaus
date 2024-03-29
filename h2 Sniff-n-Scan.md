## h2 Sniff-n-Scan

# x) Lue/katso ja tiivistä. 
# Hoikkala "joohoi" 2020: Still Fuzzing Faster (U fool). In HelSec Virtual meetup #1. (about 1 hour)
- Hoikkala kertoo videossa mitä on fuzzing.
- Fuzzing työkalu etsii anomaleita, riippuen syöttämästä datasta.
- Syöttämällä eri haku kohtiin "FUZZ" sanan, ohjelmisto syöttää siihen valmiiksi määritettyjä dataa

- Mitä voi syöttää dataksi? 
  - salasanoja, käyttäjänimiä
  - Tunnettuja API polkuja
  - Tavallisia tiedostopolkuja, parameettereitä ja arvoja

- Tavallisia kohteita
  - GET parametrit: nimet, arvot ja molemmat
  - Headerit: Host, autentikoiminen, cookies, proxy headerit
  - POST data: form data, JSON, kansiot

- Mitä tarkkailla?
  - Vastaavat koodit
  - Sisältöä (regex)
  - Vastauksien koko (bitit, # sanoja)

- Hoikkala esittelee eri työkaluja fuzzaukseen, esim. Burp, OWASP ZAP, wfuzz.
- Hoikkala demoo kuinka fuffia käytetään, esim. miten brute forcettaa tai löytää piilossa olevia GET headereitä
  -  -w, Wordlist
  -  -u, URL
  -  -e, Extension
  -  -c, colorised output
  -  -v, verbose option
  -  -recoursion, fuzzaa löydetyt URL:t automaattisesti, ekan haun jälkeen
  -  -fs, size filter
  -  -od, output directory
  

# Lyon 2009: Nmap Network Scanning: Chapter 15. Nmap Reference Guide:
- Open: Sovellus vastaanottaa TCP, UDP tai SCTP liikennettä kyseisestä portista.
- Closed: Portti on saavutettavissa mutta ei vastaanota liikennettä miltään sovellukselta. 
- Filtered: Palomuuri, reititin tai käyttäjän sovellus estää liikenteen, jolloin nmap ei voi päätellä onko portti auki vai ei.
- sS: SYN scan, skannaa tuhansia portteja sekunnissa, eikä skannaa palomuurilla suojattuja. Ei suorita TCP yhteyttä, joten skannaaja pysyy salassa.
- sT: TCP yhteys skannaus
- sU: UDP skannaus


# a) Fuff. Ratkaise Teron ffuf-haastebinääri. Artikkelista Find Hidden Web Directories - Fuzz URLs with ffuf voi olla apua.

- Aloitin ihan alusta Teron ohjeista. Mitä enemmän toistoja sen parempi. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/506dad76-d561-43ff-a94c-a100d68b6e70)

- Seuraavaksi asennat fuff:in.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b425f811-3c6f-4547-806a-c3234ea3036e)

- lataan sanalista.

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/eaf34e64-1eee-4012-b182-2c9d8ddc9c47)

- haen kansion ensiksi, annan oikeudet ja katson mitä sielä sisällä on. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1d0a4b03-e1aa-451a-93f8-32fa29a0d8ba)
- Firefoxilla avatessa, sivu näyttää tältä. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b3bc162d-a722-4756-a86d-1f3729283bb0)

- katkaisen netin seuraavaksi ja aloitan fuzzauksen.
- En onnistu löytämään sanalistan avulla mitään, enkä keksi mitä tein väärin.
- Syntaxi: ./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -v -c

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/73ce8260-e9a7-4ae8-b7bb-7825fe79cc05)

# b) Fuffme. Asenna Ffufme harjoitusmaali paikallisesti omalle koneellesi. Ratkaise tehtävät (kaikki paitsi ei "Content Discovery - Pipes")
- Seuraan https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/ ohjeita.
- Sain kohde sivun asennettua
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6432e3b7-3a4e-4436-a792-637394ed4dec)

- lataan vielä sanalistat ohjeen mukaan.
- Suljen internetin ja aloitan fuzzauksen taas.

- Basic Content Discovery
![1](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/45f57943-fc42-4376-a379-0593aea6ee08)

- Content Discovery With Recursion
![2](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/9f700fb0-aa5d-43b1-b29b-b54881d23988)

- Content Discovery With File Extensions
![3](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1da7289b-67f9-404a-9dc3-11afe0cd100b)

- No 404 Status
![4](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1e6d1586-af5e-4a28-9c2a-8008fd2e5986)

- Param Mining
![5](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/aead47fc-714e-495d-b739-2ef6a105a833)

- Rate Limited (lopetin kesken, kesti ikuisuus haussa)
![7](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/dde0d199-5b8b-4e57-9f3e-7f1d8f9998ee)

- Subdomains - Virtual Host Enumeration
![reda](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/0d1faffa-a9ff-4a07-a834-bcccb6918a47)

# Porttiskannaa paikallinen kone (127.0.0.2 tms), sieppaa liikenne snifferillä, analysoi.
- c) nmap TCP connect scan -sT
- -sudo nmap localhost -sT 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1b4afa96-6e36-475a-b3b7-104799a77516)
- TCP liikennettä, jossa jutellaan edestakaisin.
- d) nmap TCP SYN "used to be stealth" scan, -sS (tätä käytetään skannatessa useimmin)
- sudo nmap localhost -sS
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/3f1fd46f-0923-4378-b2d6-8e0dfa686c77)
- eroaa edellisestä sen verran, että vastauksena lähtee vain saama viesti? En ole aivan varma
- e) nmap ping sweep -sn
- -sudo nmap localhost -sn
- Wireshark ei napannut mitään liikettä
- f) nmap don't ping -Pn
- -sudo nmap localhost -Pn
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/44b05cf6-e206-4036-ab71-4736cccc3cf8)
- Haun pitäisi estää hostin löytäminen
- g) nmap version detection -sV (esimerkki yhdestä palvelusta yhdessä portissa riittää)
- -sudo nmap 127.0.0.1 -sV (locahostilla ei onnistunut)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/71edb70f-250b-4d6b-935e-7f204fe0bbf7)
- löytää, että portti 80 on auki ja on liikennettä. Mikä on HTTP portti
- h) nmap output files -oA foo. Miltä tiedostot näyttävät? Mihin kukin tiedostotyyppi sopii?
- -sudo nmap localhost -oA foo
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/de49484d-468c-4968-bb7e-efb0f8b97b64)

- i) nmap ajonaikaiset toiminnot (man nmap: runtime interaction): verbosity v/V, help ?, packet tracing p/P, status s (ja moni muu nappi)
- j) Ninjojen tapaan. Piiloutuuko nmap-skannaus hyvin palvelimelta? Vinkkejä: Asenna Apache. Aja nmap-versioskannaus -sV tai -A omaan paikalliseen weppipalvelimeen. Etsi Apachen lokista tätä koskevat rivit. Wiresharkissa "http" on kätevä filtteri, se tulee siihen yläreunan "Apply a display filter..." -kenttään. Nmap-ajon aikana p laittaa packet tracing päälle. Vapaaehtoinen lisäkohta: jääkö Apachen lokiin jokin todiste nmap-versioskannauksesta?
- k) UDP-skannaus. UDP-skannaa paikkalinen kone (-sU). "Mulla olis vitsi UDP:sta, mutta en tiedä menisikö se perille":
- -sudo nmap localhost -sU
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/bf3f1739-5623-4f2a-9608-116f6dfc7dbe)
- Etsii UDP portteja. Port unreachable, mikä tarkoittaa, että ei ole päällä.

# l) Miksi UDP-skannaus on hankalaa ja epäluotettavaa? Miksi UDP-skannauksen kanssa kannattaa käyttää --reason flagia ja snifferiä? (tässä alakohdassa vain vastaus viitteineen, ei tarvita testiä tietokoneella)

- Ei vaadi vastausviestejä, tosin kuin TCP. Tila voi olla piilossa, vaikea määrittää onko portti avoin vai suljettu. Vaikea tulkita porttinumeroita, koska ei ole vakiintuneita porttinumeroita. 
- Reason kerää lisätietoja skannauksen tuloksista ja tunnistaa UDP-palvelinten tilaa, reason antaa lisätietoja, esim miksi portti on auki tai suljettu. Nämä voivat auttaa selvittämään onko UDP-palvelin vastannut.


## Lähteet: 

https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/
https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h2
https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/?fromSearch=ffuf#your-turn---challenge
https://nmap.org/book/man-port-scanning-techniques.html
https://nmap.org/book/man-port-scanning-basics.html
https://www.google.com/search?q=port+80&sca_esv=579431573&sxsrf=AM9HkKkzmXiwgN1nU8crBarbKXibugcIdA%3A1699100850136&ei=sjhGZb3yB9aGwPAP6tWUmA8&ved=0ahUKEwi9k_D0q6qCAxVWAxAIHeoqBfMQ4dUDCBA&uact=5&oq=port+80&gs_lp=Egxnd3Mtd2l6LXNlcnAiB3BvcnQgODAyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyCBAAGMsBGIAEMggQABjLARiABDIIEAAYywEYgAQyCBAAGMsBGIAESJEQUPEFWMsOcAF4AZABAJgBZqAB8wOqAQM2LjG4AQPIAQD4AQGoAgrCAgcQIxjqAhgnwgIHEC4Y6gIYJ8ICCxAAGIoFGLEDGIMBwgIIEAAYgAQYsQPCAhEQLhiABBixAxiDARjHARjRA8ICCxAuGIoFGLEDGIMBwgILEAAYgAQYsQMYgwHCAgQQIxgnwgINEC4YigUYxwEYrwEYJ8ICBxAjGIoFGCfCAgsQLhiABBixAxiDAcICCxAuGIMBGLEDGIAEwgIHEAAYigUYQ8ICCBAuGIAEGLEDwgINEC4YigUYsQMYgwEYQ8ICBBAAGAPCAgsQLhiABBjHARjRA-IDBBgAIEGIBgE&sclient=gws-wiz-serp








