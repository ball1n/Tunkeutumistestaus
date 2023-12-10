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
``` tar xf rockyou.txt.tar.gz
 rm rockyou.txt.tar.gz
```

-ja puran sen tämän jälkeen

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b01f0855-fda5-489a-a692-2d8f0fa432a6)












