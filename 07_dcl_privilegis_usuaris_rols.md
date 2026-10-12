# 07. DCL: control d'accés, usuaris, privilegis i rols

> NF1 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

**DCL** (*Data Control Language*) és la part de SQL que gestiona permisos: `GRANT` i `REVOKE`.

## 1. Mecanismes bàsics de seguretat en un SGBD

La seguretat d'un SGBD ha de cobrir:

- L'**accés i l'ús de la base de dades a nivell de sistema**: creació d'usuaris, noms d'usuari i contrasenyes, assignació d'espai de disc als usuaris.
- L'**atorgament de privilegis del sistema** als usuaris per fer tasques com crear taules, vistes i seqüències.

Per fer-ho s'utilitzen tres mecanismes:

| Mecanisme | Descripció |
|---|---|
| **Identificació** | Manera com l'usuari proporciona la seva identitat al sistema (veure qui és). Una identitat pot descriure un individu, més d'un, o un o més individus només durant un període. |
| **Autenticació** | Manera com un individu estableix la validesa de la seva identitat (verificar que és qui diu ser). |
| **Autorització** | Mecanismes que asseguren que els usuaris accedeixen només als llocs autoritzats i només poden fer allò per al qual tenen permís. |

## 2. Elements bàsics de la seguretat en el SGBD

- **Usuaris:** cadascuna de les persones que accedeix al SGBD.
- **Objectes:** cadascun dels elements de la BD (dades, columnes, taules, vistes, procediments…).
- **Operacions:** accions que els usuaris poden fer sobre els objectes (lectura, escriptura, modificació, assignació de permisos).

## 3. Control d'accés

La gestió de la seguretat de la base de dades permet:

- **Controlar l'accés a la BD:** qui té permís per accedir, a quines dades i recursos i en quines condicions.
- **Donar accés a objectes específics:** a quins objectes pot accedir i què hi pot fer.
- **Confirmar els privilegis donats i rebuts** al **diccionari de dades** (metadades amb una llista organitzada dels noms, definicions i característiques dels camps i atributs d'una BD).

### Categories de seguretat

1. **Seguretat del sistema:** accés i ús de la BD a nivell de sistema (usuaris, contrasenyes, espai de disc) i privilegis de sistema (crear taules, vistes, seqüències…). Hi ha moltíssims privilegis de sistema diferents.
2. **Seguretat de dades** (o seguretat d'objectes): privilegis sobre objectes que cobreixen l'accés i l'ús dels objectes i les accions permeses, incloent l'execució d'instruccions **DML** (*Data Manipulation Language*).

### Control d'accés discrecional (DAC)

**Control d'accés:** conjunt de funcions del SGBD que asseguren que els accessos al sistema segueixen les regles de la política de protecció fixada pel model de negoci.

El **DAC** es basa en la **identitat dels usuaris o grups d'usuaris** per autoritzar o restringir l'accés als objectes. És el mecanisme **més comú** en els sistemes d'informació actuals.

> **Privilegi:** autorització d'un usuari per fer alguna operació sobre un objecte.

### Control d'accés basat en rols (RBAC)

Alternativa al DAC, **igual de segura però més flexible i fàcil de mantenir** per a l'administrador. Es creen **rols** que agrupen un conjunt de privilegis similars i després s'assignen un o més rols als usuaris.

> Un **rol** és un conjunt d'accions associades a una activitat concreta.

Exemple:

| Rol | Taula Sou | Taula Dades Personals | Vista Telèfons |
|---|---|---|---|
| Read-Only | - | x | r |
| Product-Creator | r | - | rwx |
| Full Access | rwx | rwx | rwx |

| Usuari | Read-Only | Product-Creator | Full Access |
|---|---|---|---|
| Luis | Sí | No | No |
| Alejandra | No | Sí | No |
| Karina | No | No | Sí |

## 4. Privilegis i esquemes

**Privilegis:** dret a executar determinades instruccions SQL.

- El **DBA** (*Database Administrator*), `root` en MySQL, és un usuari d'alt nivell que pot atorgar als usuaris accés a la BD i als seus objectes.
- Els usuaris necessiten **privilegis de sistema** per accedir a la BD.
- Calen **privilegis d'objectes** per manipular el contingut dels objectes.
- Els usuaris també poden tenir el privilegi d'atorgar privilegis a altres usuaris o rols.

**Esquema:** col·lecció d'objectes (taules, vistes, seqüències…). És propietat d'un usuari de la BD i pot tenir qualsevol nom, fins i tot el de l'usuari. És el que coneixem com a **base de dades**.

**Nivells de privilegis:**

- **Privilegis de sistema** (globals): permeten fer accions sobre **tots** els objectes de la BD.
- **Privilegis sobre objectes:** permeten actuar sobre objectes concrets (bases de dades, taules, vistes, seqüències…).

## 5. Creació d'usuaris

```sql
CREATE USER usr@'localhost' IDENTIFIED BY 'password';
```

- El nom d'usuari és: **nom d'usuari + `@` + host** des del qual accedirà (normalment `localhost`).
- El host pot contenir *wildcards* (`%` i `_`) o una adreça de xarxa amb màscara separada per `/`.
- El mínim és una clau d'accés amb la clàusula `IDENTIFIED BY`.
- Per crear usuaris cal el permís global `CREATE USER` o el permís `INSERT` sobre l'esquema `mysql`.

Exemples de format:

```
usuari@localhost
usuari@'192.168.0.0/255.255.255.0'
usuari@'192.168.0.%'
```

## 6. Creació de permisos

Un usuari acabat de crear **no pot accedir a cap base de dades**. Cal donar-li permisos.

**Veure permisos:**

```sql
SHOW GRANTS FOR 'usr'@'localhost';
-- Resultat inicial: GRANT USAGE ON *.* TO `usr`@`localhost`
```

- `GRANT` → atorgar permisos.
- `REVOKE` → treure permisos.
- Es poden donar permisos **generals** (tots els esquemes) o sobre **objectes** concrets (BD, taula, etc.).

### GRANT: sintaxi

```sql
GRANT <tipus_de_privilegi> [(llista_de_columnes)]
  ON [tipus_d_objecte] <objecte>
  TO <usuari_o_rol>
  [WITH GRANT OPTION];
```

- **Objecte:** `*` · `*.*` · `db_name.*` · `db_name.tbl_name` · `tbl_name` · `db_name.routine_name`
- **Tipus d'objecte:** `TABLE` · `FUNCTION` · `PROCEDURE`
- **`WITH GRANT OPTION`:** permet al receptor atorgar el mateix privilegi a altres.

### GRANT: exemples

```sql
GRANT ALL PRIVILEGES ON db1.* TO 'jeffrey'@'localhost';
GRANT ALL PRIVILEGES ON db1.* TO 'jeffrey'@'localhost' WITH GRANT OPTION;
GRANT 'role1', 'role2' TO 'user1'@'localhost', 'user2'@'localhost';
GRANT SELECT ON world.* TO 'role3';
GRANT SELECT ON world.paisos TO 'usuari'@'192.168.2.10';
GRANT SELECT ON world.paisos TO PUBLIC;
GRANT INSERT, UPDATE, DELETE ON database_name.table_name TO 'nom_usuari'@'localhost';
```

### Privilegis principals

| Privilegi | Descripció |
|---|---|
| `ALL PRIVILEGES` | Tots els privilegis disponibles en una BD o conjunt d'objectes. |
| `SELECT` | Seleccionar dades d'una taula. |
| `INSERT` | Inserir dades en una taula. |
| `UPDATE` | Actualitzar dades d'una taula. |
| `DELETE` | Eliminar registres d'una taula. |
| `CREATE` | Crear noves bases de dades o taules. |
| `DROP` | Eliminar bases de dades o taules. |
| `ALTER` | Canviar l'estructura d'una taula. |
| `SHOW DATABASES` | Veure la llista de bases de dades disponibles. |
| `USAGE` | Dret de connectar-se al servidor MySQL (sense altres privilegis). |

```sql
GRANT ALL PRIVILEGES ON nom_de_la_base_de_dades.* TO 'nom_d_usuari'@'localhost';
GRANT SELECT ON nom_de_la_base_de_dades.nom_de_la_taula TO 'nom_d_usuari'@'localhost';
```

### Privilegis segons l'objecte

```sql
-- Bases de dades
GRANT privilegis ON nom_bbdd.* TO 'nom_d_usuari'@'localhost';

-- Taules
GRANT privilegis ON nom_bbdd.nom_taula TO 'nom_d_usuari'@'localhost';

-- Procediments
GRANT EXECUTE ON PROCEDURE nom_bbdd.nom_procediment TO 'nom_d_usuari'@'localhost';

-- Funcions
GRANT EXECUTE ON FUNCTION nom_bbdd.nom_funcio TO 'nom_d_usuari'@'localhost';

-- Vistes
GRANT privilegis ON nom_bbdd.nom_vista TO 'nom_d_usuari'@'localhost';

-- Columnes
GRANT privilegis (col1, col2) ON nom_bbdd.nom_taula TO 'nom_d_usuari'@'localhost';

-- Events
GRANT privilegis ON EVENT nom_event TO 'nom_d_usuari'@'localhost';

-- Tots els objectes
GRANT privilegis ON *.* TO 'nom_d_usuari'@'localhost';
```

## 7. Creació de rols

Un **rol** és un grup de privilegis relacionats que es poden concedir a un usuari. Normalment es creen per a una aplicació de base de dades; faciliten **revocar i mantenir** els privilegis.

- Un usuari pot tenir diversos rols.
- Diversos usuaris poden tenir el mateix rol.
- Els rols es creen i eliminen amb `CREATE ROLE` i `DROP ROLE`.
- S'assignen als usuaris amb `GRANT`; els permisos es donen als rols amb el `GRANT` bàsic, com un privilegi més.

```sql
CREATE ROLE periodista;
GRANT SHOW DATABASES ON *.* TO periodista;
GRANT periodista TO usuari@localhost;
```

## 8. REVOKE

### Sintaxi

```sql
REVOKE <tipus_de_privilegi> [(llista_de_columnes)]
  ON [tipus_d_objecte] <objecte>
  FROM <usuari_o_rol>;
```

### Exemple

```sql
SHOW GRANTS FOR usuari@localhost;
-- GRANT `periodista` TO `usuari`@`localhost`
-- GRANT USAGE ON *.* TO `usuari`@`localhost` IDENTIFIED BY ***
-- GRANT ALL PRIVILEGES ON `basededades`.* TO `usuari`@`localhost`

REVOKE periodista FROM `usuari`@`localhost`;
REVOKE ALL PRIVILEGES ON `basededades`.* FROM `usuari`@`localhost`;
```
