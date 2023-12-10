# h7 Hash

## x) Lue/katso/kuuntele ja tiivistä

## Karvinen 2022: [Cracking Passwords with Hashcat](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)

- Atrikkeli käsittelee hashcatin käyttöä. Päätin ottaa kuvankaappauksen omasta mielestäni tärkeimmästä kohdasta.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/fecc1d70-d3a4-4b6c-8fe2-df3d2642ba2f)


## Karvinen 2023: [Crack File Password With John](https://terokarvinen.com/2023/crack-file-password-with-john/)

- John the Ripper on vähän monimutkaisempi ja edistyneempi salasanojen kräkkäys softa. John voi käyttää esim sanakirja hyökkäystä ZIP filestä.


## a) Hashcat. Asenna Hashcat ja testaa sen toimivuus ratkaisemalla tiiviste.

-Lähteenä käytän Teron tekemää [opasta](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)
- Aloitan päivittämällä Kalin ja asentamalla hascatin mutta se olikin jo asennettu valmiiksi Kaliin. No muutama paketti taisi päivittyä siitä, eli ei mennyt ihan hukkaan. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/3185c318-b3b5-4ea5-91aa-b0c65f6104c0)
```
sudo apt-get update
```
```
sudo apt-get -y install hashid hashcat wget
```

- Tein kansion johon aion ladata sanakirjan
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8b227427-67a1-4adf-bf25-917c3a47aaa5)

- Lataan kansion 

```
wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
``` 
```
tar xf rockyou.txt.tar.gz
 rm rockyou.txt.tar.gz
```

-ja puran sen tämän jälkeen

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b01f0855-fda5-489a-a692-2d8f0fa432a6)

- Teen itselleni helpon MD5 hash [md5hashgenerator:n](https://www.md5hashgenerator.com/) avulla. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/a5319151-045f-41e6-8c08-f991ae83aa40)

- Tämän jälkeen kokeilen hascatin ettiä hashid:n ja lähen arvailemaan salasanaa
```
hashid -m 1f3870be274f6c49b3e31a0c6728957f 
```
-m näyttää numeron mitä käytetään salasanan avaamiseen
```
hashcat -m 0 '1f3870be274f6c49b3e31a0c6728957f' rockyou.txt -o solved
```
- tässä -m 0 = MD5, pitää muistaa pistää hash '' sisälle, koska joskus hasheissä voi olla erikoismerkkejä, rockyou.txt on sanakirja jota käytän ja -o solved luo kansion ja vie vastauksen sinne. 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/bb07c832-79e3-4806-9d7e-17db567fad76)
- Saan tekstin "* Device #1: Not enough allocatable device memory for this attack.", VM koneessani ei ole tarpeeksi muistia varmaankin tuon tekstitiedoston läpikäymiseen tjsp. Käyn lisäämässä, suljen kalin ja asetuksista tuplaan muistin.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6dd4a4ba-9a0c-4f76-88b6-a8742af3defb)
- Käyn suorittamassa samat komennot ja nyt pelittää. Hashcat löytää nopeasti salasanan joka oli "apple"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6b27b311-6928-4222-8faa-33a2045409ef)

## b) John. Asenna Jumbo John ja testaa sen toimivuus murtamalla jonkin tiedoston salasana.

- Lähteenä tähän tehtävään käytän Teron ohjetta [John The Ripperin asennukseen](https://terokarvinen.com/2023/crack-file-password-with-john/)
- Olin lataamassa seuraavia "build-essential libssl-dev  zlib1g zlib1g-dev zlib1g-gst libbz2-1.0 libbz2-dev atool zip" mutta kohtasin ongelman
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1afb00f7-4a52-4ece-9edd-b69cddd73616)
- Poistin "zlib1g-gst" ja latasin loput, katsotaan tuleeko hidasteita edessä vielä
- Lataan johnin github reposta 
```git clone --depth=1 https://github.com/openwall/john.git```
- Tämän jälkeen konfiguroin tiedoston, joka myös ilmoittaa jos jotain puuttuu

```
cd john/src/	
./configure
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/700b26f8-85b4-4111-ad50-0b1b80632207)
- Tämän jälkeen sovellus ns kasataan? ja sen jälkeen asennus pitäisi olla siinä
```
make -s clean && make -sj4
```

```
$HOME/john/run/john
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6eac7fa8-b3d2-4c39-baf0-ce9d1011ec63)
- ja homma rokkaa

- Lataan Teron [ohjeista](https://terokarvinen.com/2023/crack-file-password-with-john/) zippi tiedoston, ja ajan komennon mikä näyttää tietoja filusta 
```
$HOME/john/run/zip2john tero.zip >tero.zip.hash
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/c476eabf-b5be-46ae-94ee-701e92b9c482)

- Tämän jälkeen ajan sanakirjahyökkäyksen
```
$HOME/john/run/john tero.zip.hash
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b494090a-4f18-4baf-b0d1-4bc38a0b9721)
- Salasana on butterfly

## c) f5bc7fcc7f5b3b6af7ff79e0feafad6d1a948b6a2c18de414993c1226be48c1f on erään tällä tehtäväsivulla olevan yksittäisen sanan tiiviste. Käytin hyvin yleistä ja tunnettua tiivistealgoritmia. Sanassa voi olla isoja kirjaimia, mutta ei erikoismerkkejä. Minkä sanan tiiviste on kyseessä?

- Apuna käytin kurssikaverin tekemää ratkaisua miten sanalista tehdään URL:sta, kiitos Jana! [linkki Janan githubiin](https://github.com/JanaHalt/Ethical-Hacking-2023/blob/main/h7%20Hash.md)
- Aloitan luomalla sanalistan Teron kurssin sivusta "https://terokarvinen.com/2023/eettinen-hakkerointi-2023/", jälkeenpäin mietin, että olisiko ollut nopeampaa luoda url "https://terokarvinen.com/2023/eettinen-hakkerointi-2023/#h7-hash", ehkä kokeilen myöhemmin onnistuuko.

```
cewl https://terokarvinen.com/2023/eettinen-hakkerointi-2023/ -d 2 -w $HOME/teronlista.txt
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/03517f1f-45f6-4b7b-a407-1fcf7661d143)

- katotaan hashcatilla minkä muotoisella hashlla algoritmi aukeaa
```
hashid -m 'f5bc7fcc7f5b3b6af7ff79e0feafad6d1a948b6a2c18de414993c1226be48c1f'  
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/7d874e2a-f620-459f-9f10-82645e01c99a)

- Haisee vahvasti SHA256, lähetään sillä eteenpäincat
```
hashcat -m 1400 'f5bc7fcc7f5b3b6af7ff79e0feafad6d1a948b6a2c18de414993c1226be48c1f' teronlista.txt -o solved
```
- m 1400 = SHA256
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/83be1d41-55fc-40ad-a245-553a993671bc)
- Sertificate on salasana.



## d) Cheatsheet. Kerää kurssilaisten raporteista käteviä tekniikoita. Kerää itse tekniikat ja komennot, älä pelkästään kuvaile. Muista lähdeviitteet. Tee tiivis ja selkeä cheatsheet, josta löydät tarvittavat tiedot lipunryöstössä. 

- Tuntu, että astuin kultakaivoon kun selailin kurssikavereiden githubeja ja Ollikaisen [cheatsheet pämähti esille](https://github.com/sawulohi/PenTest/tree/main/h7). Sieltä löyty kultaakin arvokkaammat lähteet. 
- https://github.com/miljonka/Tunkeutumistestaus/wiki/h5_Final-Countdown#y-the-super-ultimate-hakk3r-che33tsheet-001-tee-tiivistelm%C3%A4-omista-ja-kavereiden-parhaista-tunketumistekniikoista-ole-t%C3%A4sm%C3%A4llinen-liit%C3%A4-komennot-mukaan-t%C3%A4m%C3%A4n-kohdan-vastaus-lienee-pidempi-kuin-aiempien-x-teht%C3%A4vien-viittaa-l%C3%A4hteisiin-t%C3%A4ss%C3%A4-alakohdassa-ei-tarvitse-ajaa-komentoja-tietokoneella
- https://github.com/therealhalonen/penetration_testing/blob/master/h5/personal_cheatsheet.md


## e) Viittaa. Tarkista, että jokaisessa raportissasi on lähdeviitteet kunnossa. Jokaisen raportin tulee viitata ainakin kurssiin / tehtäväsivuun. Kaikkiin muihinkin käytettyihin lähteisiin tulee viitata, kuten kurssikavereiden raportteihin, weppisivuihin, man-sivuihin... (Tässä alatehtävässä ei tarvitse tehdä testejä koneella).

- done


Lähteet: 

- https://terokarvinen.com/2022/cracking-passwords-with-hashcat/
- https://terokarvinen.com/2023/crack-file-password-with-john/
- https://www.md5hashgenerator.com/
- https://forum.howtoforge.com/threads/device-1-not-enough-allocatable-device-memory-for-this-attack.90161/
- https://github.com/JanaHalt/Ethical-Hacking-2023/blob/main/h7%20Hash.md
- https://github.com/sawulohi/PenTest/tree/main/h7
- https://github.com/therealhalonen/penetration_testing/blob/master/h5/personal_cheatsheet.md
- https://github.com/miljonka/Tunkeutumistestaus/wiki/h5_Final-Countdown#y-the-super-ultimate-hakk3r-che33tsheet-001-tee-tiivistelm%C3%A4-omista-ja-kavereiden-parhaista-tunketumistekniikoista-ole-t%C3%A4sm%C3%A4llinen-liit%C3%A4-komennot-mukaan-t%C3%A4m%C3%A4n-kohdan-vastaus-lienee-pidempi-kuin-aiempien-x-teht%C3%A4vien-viittaa-l%C3%A4hteisiin-t%C3%A4ss%C3%A4-alakohdassa-ei-tarvitse-ajaa-komentoja-tietokoneella
