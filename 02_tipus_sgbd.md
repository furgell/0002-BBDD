# 02. Tipus de SGBD

> Sessió 2 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

Els SGBD es poden classificar segons diversos criteris.

## 1. Segons el model de dades

| Tipus | Descripció | Exemple |
|---|---|---|
| **Jeràrquic** | Organització en forma d'arbre amb relacions pare-fill. | IBM IMS |
| **En xarxa** | Estructura de grafs amb relacions molts a molts. | IDS |
| **Relacional** | Dades en taules amb relacions mitjançant claus primàries i foranes. | MySQL, Oracle DB |
| **Orientat a objectes** | Utilitza classes i objectes amb principis d'orientació a objectes. | ObjectDB |
| **NoSQL** | Gestió de dades no estructurades o semiestructurades. | MongoDB, Cassandra |
| **Multimodel** | Suporta diversos models de dades en un sol sistema. | Azure Cosmos DB |

## 2. Segons la distribució de les dades

- **Centralitzats:** totes les dades es gestionen en un únic lloc central.
  *Exemple:* Oracle en entorns locals.
- **Distribuïts:** les dades es distribueixen entre diferents ubicacions físiques o lògiques, connectades en xarxa.
  *Exemple:* Google Spanner, Apache Cassandra.

## 3. Segons l'accés dels usuaris

- **Monousuari:** només un usuari pot accedir i manipular la base de dades en un moment donat.
  *Exemple:* Microsoft Access en mode local.
- **Multiusuari:** permet que múltiples usuaris accedeixin a la base de dades de manera simultània.
  *Exemple:* MySQL, PostgreSQL.

## 4. Segons el tipus d'instal·lació

- **Locals (on-premise):** les bases de dades s'allotgen en servidors físics dins de l'empresa o organització.
  *Exemple:* Microsoft SQL Server instal·lat en una xarxa local.
- **Al núvol (cloud):** les bases de dades es gestionen a través de serveis de núvol i les dades s'allotgen en servidors remots.
  *Exemple:* Amazon RDS, Google BigQuery.

## 5. Segons la gestió de transaccions

- **SGBD amb ACID:** garanteixen les propietats **ACID** (**A**tomicitat, **C**onsistència, **A**ïllament i **D**urabilitat). Ideal per a aplicacions crítiques.
  *Exemple:* PostgreSQL, Oracle DB.
- **SGBD BASE:** sacrifiquen la consistència estricta per millorar l'escalabilitat i la disponibilitat en sistemes distribuïts.
  *Exemple:* Apache Cassandra (NoSQL).

## 6. Segons l'escala i el rendiment

- **Grans volums de dades (Big Data):** dissenyats per gestionar grans quantitats de dades de manera eficient.
  *Exemple:* Hadoop, Google Bigtable.
- **Aplicacions lleugeres:** destinats a aplicacions amb requisits lleugers o que funcionen en dispositius mòbils o locals.
  *Exemple:* SQLite.
