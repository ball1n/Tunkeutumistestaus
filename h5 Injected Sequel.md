# h5 Injected Sequel

## x) Lue/katso/kuuntele ja tiivistä.

### Karvinen 2016: [PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu](https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/) (Virtuaaliympäristöä ei tarvita, voit aloittaa kohdasta "Three line install"

- Oppaassa käydään läpi miten asentaa PostgreSQL palvelin ja kuinka CRUD toimii (Create, read, update and delete data)

- Getting Help:
  - Help on käytettävissä "help"
```
\h for help with SQL commands  
\? for help with psql commands  
```
- C: CREATE TABLE<br>
```
    tero=> CREATE TABLE students (id SERIAL PRIMARY KEY, name VARCHAR(200));  
CREATE TABLE  
```
  - "Serial ID" on hyvä pistää "Primary Key:ksi" jokaiselle taululle (table). -> on helpompi tehdä linkkejä, jotka viittaavat databaseen.
  

- C: Create Records: INSERT<br>
```
  tero=> INSERT INTO students(name) VALUES ('Tero');  
INSERT 0 1`  
```
  - Arvojen ympärille tarvitaan sulkumerkit, on käytettävä vain yhtä sulkumerkkiä per puoli.


- R: Read: SELECT<br>
```
tero=> SELECT * FROM students;  
 id | name  
----+-------  
 1 | Tero  
 2 | Matti  
 4 | Maija  
 5 | Liisa  
(4 rows)  
```
  - SQL on helppo etsiä tietoja. Yleisesti on helppo hakea numeroiden avulla "WHERE" avulla. Oppaassa demonstroitiin "LIKE" haku, mutta usein vältetään hakua tekstillä -> on hidasta<br>
```
tero=> SELECT * FROM students WHERE name LIKE 'Ma%';  
 id | name  
----+-------  
 2 | Matti  
 4 | Maija  
(2 rows)  
```

- U: UPDATE
```
tero=> UPDATE students SET name='Tero Karvinen' WHERE name='Tero';  
UPDATE 1  
```

- Huom. pitää käyttää yhtä sulkumerkkiä

``` 
tero=> SELECT * FROM students;  
 id |     name  
----+---------------  
 2 | Matti  
 4 | Maija  
 5 | Liisa  
 1 | Tero Karvinen  
(4 rows)  
```

- D: DELETE
``` 
tero=> DELETE FROM students WHERE name='Liisa';
DELETE 1
tero=> SELECT * FROM students;
 id |     name
----+---------------
 2 | Matti
 4 | Maija
 1 | Tero Karvinen
(3 rows)
``` 


## OWASP 2017: A1:2017-Injection

- Injectio oli OWAS TOP-10 #1 vuonna 2017.
- Lähes mikä tahansa tietolähde voi olla injektion kohde. Injektiohaavoja esiintyy kun hyökkääjä voi lähettää haitallista daataa tulkkijalle
- Injektio haavoja löytyy useimmiten SQL, LDAP, XPath, NoSQL queries, OS commands, XML parsers, SMTP headers, expression languages ja ORM queries. Skannerit ja fusserit ovat hyödyllisiä hyökkääjälle haavoittuvuuksien etsimisessä.


## PortSwigger Academy: SQL injection

- Mikä SQL injektio on?
  - [SQL-injektio on tekniikka tietoturva-aukkojen hyödyntämiseksi järjestelmiin tunkeutumisessa. Niitä esiintyy tietokantapohjaisissa sovelluksissa. Ne ovat varsin yleisiä WWW-pohjaisissa sovelluksissa joissa käyttäjät käyttävät tietokantaa WWW-rajapinnan yli, mutta SQL-injektiot eivät sinällään ole WWW-sidonnaisia.](https://fi.wikipedia.org/wiki/SQL-injektio)

- Kuinka löytää ja hyödyntää eri tyyppisiä SQL haavoittuvuuksia?
  - Manuaalisesti syöttämällä systemaattisesti samoja testauksia jokaista tulokohtaa kohti sovelluksessa. Esim. sulkumerkki ('), etsii erroreita tai muita anomaleita, boolean kuntoja kuten ```OR 1=!``` tai ```OR 1=2```, joka etsii erillaisia vastauksia

- Kuinka estää SQL haavoittuvuus?
  - Käyttämällä valmiiksi tehtyjä hakulauseita.


## a) CRUD. Tee uusi PostgreSQL-tietokanta ja demonstroi sillä create, read, update, delete (CRUD). Keksi taulujen ja kenttien nimet itse. Taulujen nimet monikossa, kenttien nimet yksikössä, molemmat englanniksi.

- Aloitan päivittämällä Kalin ja asentamalla SQL tietokannan. Starttaan postgresql

```
$ sudo apt-get update
$ sudo apt-get -y install postgresql
$ sudo systemctl start postgresql 
$ sudo -u postgres createdb $(whoami)
$ sudo -u postgres createuser $(whoami)
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/ad071c06-e604-407d-afa5-277b4b0c3aa0)
- Kuvassa olevat komennot ei toiminut itselleni, koska ne oli defaulttina valmiiksi jo Kalissa, kai? :D

## CREATE table
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/f89678e3-75fc-4897-a477-32fe4098fa5c)
- Ei toimi itselleni, yritän selvittää mistä syystä. 
- Yritin [täältä](https://www.cybertec-postgresql.com/en/error-permission-denied-schema-public/) löytää astausta ja saada session superuseriksi. Ei onnistunut -> jatkan ongelman selvittämistä
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6af5aae0-391a-4f2b-847d-c5ec940b29d6)

- Aivan, en startannut psql:ää sudona. Komennolla ->
```
sudo -u postgres psql  
```
tulee parempi mieli

![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/b9e3739b-0c8c-42ba-8d2a-802a9755a353)

## CREATE records

 - Komennolla vien HIFK taulukkoon "harjoitus"
```
INSERT INTO harjoitus(name) VALUES ('HIFK');
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/93002d7a-3adf-4a46-966e-474d73f53bd9)

## Read

- Komennolla haen sisällön
 ```
SELECT * FROM harjoitus;
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/60c7bbbf-d7fb-458f-b06b-e11153de1873)

## Update

- Päivitin 'HIFK' sanalla olevat tiedot taulukosta seuraavalla komennolla 
```
UPDATE harjoitus SET name='Suomen mestari' WHERE name='HIFK';
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e3e5427a-1b99-432b-978a-122e983f06d0)

## Delete

- Poistetaan taulukosta komennolla 
```
ELETE FROM harjoitus WHERE name='KVANTAA';
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/6567d04b-2d73-4325-9663-807418c15909)

## b) SQLi me. Kuvaile yksinkertainen SQL-injektio, ja demonstroi se omaan tietokantaasi psql-komennolla. Selitä, mikä osa on käyttäjän syötettä ja mikä valmiina ohjelmassa. 

- Omaa "harjoitus" tietokantaani olisi helppo suorittaa yksinkertainen kysely tällä hetkellä. [Lähde](https://portswigger.net/web-security/sql-injection)

```
SELECT * FROM harjoitus WHERE name ='' OR '1';
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/1c59a560-44c1-4f5d-b3ef-14d4fddd78a2)

- Tämä palauttaisi kaikki "name" kohdassa olevat tiedot, koska ehto '1'='1' on aina tosi. Valmiiksi tehdyillä kyselyillä voisi tämän estää. 


## PortSwigger Labs

## d) [SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

- Tässä harjoituksessa pitää löytää haavoittovuus kirjautumisessa. Pitää suorittaa SQL injektio, joka löytyy "administrator" käyttäjällä

- Avaan ensiksi ZAP:n kun sitä tullaan tarvitsemaan 
```
./zap.sh
```
- Avaan labran ja siirryn siellä "My Account" sivulle -> teen testi kirjautumisen
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/0bf1e772-ae82-4678-8012-e29be82cd6f3)
- Eli käyttäjänimen kohdalle pitää lisätä "administrator" sekä "'--", joka kommentoi jäljellä tulevaa sisältöä? [Lähde](https://portswigger.net/web-security/sql-injection/cheat-sheet)
- Katsoin myös [videon](https://www.youtube.com/watch?v=ML3aGaloczI), jossa käytiin läpi miten labra selvitetään ja kävin syöttämässä "username" kohtaan ``` administrator'--" ja "password" = ei ollut mitään väliä -> pääsin kirtjautumaan sisään täten myös.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/13f0cba0-d007-4151-ac7f-d8fb79535181)

## e) SQL injection attack, querying the database type and version on Oracle

- Tässä labrassa on SQL haavoittovuus tuote kategorian filterissä ja labrassa kerrotaan, että voidaan käyttää [UNION](https://portswigger.net/web-security/sql-injection/union-attacks) hyökkäystä
- Availen muutamia kategorioita ja tarkistelen miltä liikenne näyttää ZAP:ssa
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e855f2b5-cb50-4424-a1fb-60e22f1ba19f)
- Kokeilen muuttaa GET pyynnön urlia. Käytän tehtävään lähteenä [walkthrough](https://www.youtube.com/watch?v=s4CxZ0txb6g) apua. Muokkaan pyyntöön "+UNION+SELECT+'abc','def'+FROM+dual--" ja avaan sen firefoxilla
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/30f19d66-2d85-4dfa-956e-46476cc19ef6)
- Sieltä tulee esille syötetyt "abc" ja "def". Seuraavassa vaiheessa kokeillaan saada tietoa esim. mikä tietokanta sivulla on käytössä lisäämällä pyyntöön "+UNION+SELECT+%20banner,%20'def'%20FROM%20v$version--"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/cc9e8825-c911-4632-975e-b5553f0b06c6)
- ja sieltä selviää mitä on käytössä 
  - CORE 11.2.0.2.0 Production = Oracle database ja muut liittyy myös Oracleen

## f) SQL injection attack, querying the database type and version on MySQL and Microsoft

- Hieman samanlainen labra kuin edellisessä tehtävässä. Tässä haavoittovuus löytyy samasta paikasta ja methodina edellinen UNION hyökkäys. Eroa on, että vastassa on MySQL ja Microsoft.
- Aloitan avaamalla labran ja availemalla kategorioita taas. Liikenne ZAP:sta, muokataan taas "category=" jälkeen 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/30abed90-4b6b-4a50-ae6a-8aa369fc4201)
- [Täältä](https://portswigger.net/web-security/sql-injection/cheat-sheet) katsoin komennon Microsoftin osalta millä saa tietoon databasen. "'UNION%20SELECT@@version,%20NULL%23"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/2f87f541-41b0-4973-92af-59310c5d87e5)
- Pyyntö palauttaa version "8.0.35-0ubuntu0.20.04.1", olisko mikä palvelin ja versio? :D

## g) SQL injection attack, listing the database contents on non-Oracle databases

- Sama idea kuin aikaisemmissa, UNION hyökkäys mutta tällä kertaa pitää selvittää taulukon nimi ja "colums it contains" -> hakea taulukko, jossa on käyttäjänimet ja salasanat käyttäjille.
- Aloitan avaamalla labran -> avaan kategorian labrassa -> ZAP -> Manual request editor -> muokkaan GET pyyntöön "'+UNION+SELECT+'abc','def'+FROM+dual--" ja send 
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/a92746b5-2e61-41bd-b3ba-283e95bb7f0e)
- Seuraavaksi pitäisi selvittää taulukon nimi ja taulukot. Miten? Tarvin apua "solution" kohdasta, "
'+UNION+SELECT+table_name,NULL+FROM+all_tables--" on vastaus onnellisuuteen. Katsotaan mitä saadaan tulokseksi tuolla.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/745497a4-ed2b-40ff-9343-564238bc62da)
- Sieltä löytyy taulukot. Etsitään taulukko josta löytyy käyttäjien tiedot.
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/81b5ea8b-8654-4e5a-936f-5c1f7f2a7ab6)
- Seuraavaksi haluan saada tiedot miltä "colums" näyttää taulukossa [tietoon](https://portswigger.net/web-security/sql-injection/cheat-sheet). "'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_RKJTUE'--"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/98df462f-f39d-4b1f-9888-1b20280d7da4)
- Seuraavaksi haetaan käyttäjät ja salasanat kaikille käyttäjille -> "+UNION+SELECT+USERNAME_EURSUC,+PASSWORD_LIVQPN+FROM+USERS_RKJTUE--"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/4b01750e-aeaf-4da0-813d-92ea8077d03f)
- Yritetään kirjautua sisään "administrator"
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/2b78450e-9e10-4d1e-ba72-09bb628dd4be)
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/8cb405b9-ed1b-4249-9fb0-487ebc6a7fac)

# Lopetan tehtävät tähän ja jatkan sunnuntaina, jotta ehdin palauttaa ajoissa läksyt. Pahoittelut!












## Lähteet

- https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/
- https://portswigger.net/web-security/sql-injection/union-attacks
- https://github.com/ball1n/Tunkeutumistestaus/blob/main/h4%20Totally%20Legit%20Sertificate.md
- https://owasp.org/www-project-top-ten/2017/A1_2017-Injection
- https://www3.ntu.edu.sg/home/ehchua/programming/sql/PostgreSQL_GetStarted.html
- https://www.cybertec-postgresql.com/en/error-permission-denied-schema-public/
- https://www.youtube.com/watch?v=4UxUpsCZQfI
- https://www.youtube.com/watch?v=ZbwIbIq5-eE

  



