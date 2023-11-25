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
 ```SELECT * FROM harjoitus;```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/60c7bbbf-d7fb-458f-b06b-e11153de1873)

## Update

- Päivitin 'HIFK' sanalla olevat tiedot taulukosta seuraavalla komennolla 
```
UPDATE harjoitus SET name='Suomen mestari' WHERE name='HIFK';
```
![image](https://github.com/ball1n/Tunkeutumistestaus/assets/117892213/e3e5427a-1b99-432b-978a-122e983f06d0)
















