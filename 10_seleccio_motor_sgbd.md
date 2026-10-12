# 10. Selecció del motor de SGBD

> Gest&Seg BBDD · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

## 1. Què és un motor de BBDD?

- Un motor de base de dades és el **programari que permet crear, gestionar i consultar** bases de dades.
- S'encarrega de l'**organització, emmagatzematge, seguretat i accés** a les dades.
- És la base de qualsevol aplicació que utilitzi dades.
- Forma part del SGBD.

## 2. Per què és important escollir el motor adequat?

- **Rendiment:** un motor inadequat pot alentir aplicacions i provocar ineficiències.
- **Costos:** alguns motors són de codi obert (gratuïts), però d'altres tenen costos elevats de llicència.
- **Escalabilitat:** motors inadequats poden no suportar el creixement d'un projecte.
- **Necessitats concretes:** no tots els motors estan optimitzats per a cada tipus d'aplicació (p. ex. dades en temps real o grans transaccions).

## 3. Criteris per seleccionar un motor de BBDD

### 3.1. Segons tipus de dades i estructura *(criteri fonamental)*

Ens centrem en les necessitats de les dades que gestionarem.

- **Relacionals (SQL):**
  - Ideals per a sistemes amb dades **estructurades** i relacions ben definides (taules amb clau primària i forana).
  - Garanteixen la consistència i suporten transaccions **ACID** (Atomicitat, Consistència, Aïllament, Durabilitat).
- **No relacionals (NoSQL):**
  - Més flexibles per a dades **no estructurades o semiestructurades** (documents JSON, XML, etc.).
  - Ideals quan el format de les dades pot variar o les relacions són menys importants.

### 3.2. Segons escalabilitat

El tipus de dades i la quantitat d'usuaris determinen si el sistema ha de créixer de manera **vertical** o **horitzontal**.

- **SQL:** normalment escalen **verticalment** (més CPU, RAM en un sol servidor). Té límits físics i pot ser més car en sistemes grans.
- **NoSQL:** escalen **horitzontalment** (afegint més servidors per distribuir la càrrega). Més efectiu amb milions d'usuaris o grans volums de dades.

### 3.3. Segons rendiment i velocitat

Essencial, sobretot en aplicacions amb dades en temps real.

- **SQL:** robustes i eficients en **consultes complexes** gràcies a SQL. Suport natiu per a índexs, funcions i vistes per optimitzar consultes.
- **NoSQL:** algunes estan optimitzades per a velocitat extrema. Per exemple, **Redis** utilitza emmagatzematge en memòria i permet consultes instantànies. També són ideals per a operacions massives i no transaccionals.

### 3.4. Segons el cost

Pot ser determinant en projectes amb pressupost limitat.

- **SQL:** motors de codi obert (MySQL, PostgreSQL) gratuïts; motors comercials (Oracle, SQL Server) poden ser costosos, però ofereixen funcionalitats avançades i suport tècnic.
- **NoSQL:** molts són gratuïts o *open source* (MongoDB, Cassandra). Els costos solen venir del manteniment o de les necessitats d'escala.

### 3.5. Segons compatibilitat i ecosistema

El motor ha d'integrar-se bé amb les tecnologies del projecte.

- **SQL:** compatibles amb la majoria de llenguatges (Java, Python, PHP) i fàcils d'integrar amb eines empresarials (Power BI, Tableau…).
- **NoSQL:** connectors moderns per a llenguatges com Node.js i *frameworks* web. MongoDB, per exemple, té una API amigable per a desenvolupadors moderns.

### 3.6. Segons facilitat d'ús i comunitat

Els motors populars tenen comunitats grans i actives, cosa que facilita trobar recursos i solucions.

- **SQL:**
  - PostgreSQL: excel·lent documentació i comunitat molt activa.
  - MySQL: un dels més utilitzats, amb molts recursos gratuïts.
  - SQL Server: bona documentació, però ecosistema més tancat.
- **NoSQL:**
  - MongoDB: gran comunitat i documentació extensa, amb cursos oficials gratuïts.
  - Redis: popularitat creixent, però documentació més tècnica.

## 4. Resum: SQL vs NoSQL

| Criteri | SQL | NoSQL |
|---|---|---|
| Tipus de dades | Estructurades | No estructurades / semiestructurades |
| Escalabilitat | Vertical | Horitzontal |
| Rendiment | Bo per a consultes complexes | Ideal per a dades en temps real |
| Cost | Gratuït (*open source*) o comercial | Generalment gratuït |
| Compatibilitat | Tradicional (Java, Python, PHP) | Moderna (Node.js, *frameworks* web) |
| Comunitat | Molt activa (PostgreSQL, MySQL) | Activa (MongoDB, Redis) |

## 5. Motors de BBDD principals

| Motor | Ús recomanat |
|---|---|
| **MySQL** | Aplicacions web senzilles i comerç electrònic. Econòmic i fàcil d'usar. |
| **PostgreSQL** | Gestió avançada de dades i solucions híbrides SQL/JSON. |
| **Microsoft SQL Server** | Empreses que fan servir l'ecosistema Microsoft. Integració amb BI. |
| **Oracle Database** | Grans empreses i sistemes crítics (funcionalitats avançades i suport tècnic). |
| **MongoDB** | Dades no estructurades i sistemes en temps real (xats, IoT). |
| **Cassandra** | Big Data i sistemes distribuïts amb alta disponibilitat. |
| **Redis** | Memòria cau (*caché*) en memòria per a baixes latències i alta velocitat. |

## 6. Conclusions

Cal triar adequadament el motor de BBDD segons aquests criteris:

- El **tipus de dades** que utilitzarem segons les necessitats de l'empresa.
- El **pressupost** de l'empresa.
- El **volum de dades**, l'escalabilitat o creixement futur de l'empresa.
- La **compatibilitat** del programari i amb el sistema operatiu.
- La **documentació** i la informació que pot aportar la comunitat.
- L'**escalabilitat** de l'empresa, així com els seus recursos.
