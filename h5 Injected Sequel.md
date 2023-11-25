# h5 Injected Sequel

## x) Lue/katso/kuuntele ja tiivistä.

### Karvinen 2016: [PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu](https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/) (Virtuaaliympäristöä ei tarvita, voit aloittaa kohdasta "Three line install"

- Oppaassa käydään läpi miten asentaa PostgreSQL palvelin ja kuinka CRUD toimii (Create, read, update and delete data)

- Getting Help:
  - Help on käytettävissä "help"

`\h for help with SQL commands`<br>
` \? for help with psql commands`

- C: CREATE TABLE<br>
    `tero=> CREATE TABLE students (id SERIAL PRIMARY KEY, name VARCHAR(200));
CREATE TABLE`

  - "Serial ID" on hyvä pistää "Primary Key:ksi" jokaiselle taululle (table). -> on helpompi tehdä linkkejä, jotka viittaavat databaseen.
  

- C: Create Records: INSERT<br>
  `tero=> INSERT INTO students(name) VALUES ('Tero');
INSERT 0 1`<br>
- Arvojen ympärille tarvitaan sulkumerkit, on käytettävä vain yhtä sulkumerkkiä per puoli.


- R: Read: SELECT<br>




