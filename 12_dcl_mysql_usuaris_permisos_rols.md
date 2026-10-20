# 12. DCL a MySQL: usuaris, permisos i rols

[← Tornar a l'índex](README.md)

## 12.1 Creació d'usuaris

```sql
CREATE USER <nomUsuari> IDENTIFIED BY '<contrasenya>';
```

- El nom d'usuari té el format **`usuari@host`**: nom, separador `@` i el host des del qual accedirà (normalment `localhost`).
- El host pot contenir **comodins** (`%` i `_`) o una **adreça de xarxa amb màscara** separades per `/`.
- Com a mínim s'hi posa una contrasenya amb la clàusula **`IDENTIFIED BY`**.

Exemples de noms d'usuari:

```text
usuari@localhost
usuari@'192.168.0.0/255.255.255.0'
usuari@'192.168.0.%'
```

Per crear usuaris cal el permís global **`CREATE USER`** o el permís **`INSERT`** sobre l'esquema `mysql`.

```sql
CREATE USER usr@'localhost' IDENTIFIED BY 'password';
```

## 12.2 Consulta de permisos

Un usuari acabat de crear encara no pot accedir a cap BD. Per veure els permisos que té:

```sql
SHOW GRANTS FOR 'usr'@'localhost';
```

```text
+-----------------------------------------+
| Grants for usr@localhost                |
+-----------------------------------------+
| GRANT USAGE ON *.* TO `usr`@`localhost` |
+-----------------------------------------+
```

- **`GRANT`** → dona permisos.
- **`REVOKE`** → treu permisos.

Els permisos poden ser **generals** (per a tots els esquemes) o per a **objectes** concrets (una BD, una taula, una rutina…).

## 12.3 GRANT — Sintaxi

```sql
GRANT <tipus_de_privilegi> [(llista_de_columnes)]
    ON [tipus_d_objecte] <nivell>
    TO <usuari_o_rol>
    [WITH GRANT OPTION];
```

- **nivell**: `*` | `*.*` | `db_name.*` | `db_name.tbl_name` | `tbl_name` | `db_name.routine_name`
- **tipus_d_objecte**: `TABLE` | `FUNCTION` | `PROCEDURE`
- **`WITH GRANT OPTION`**: permet al receptor del privilegi atorgar aquest mateix privilegi a altres.

### Exemples

```sql
GRANT ALL PRIVILEGES ON db1.* TO 'jeffrey'@'localhost';
GRANT ALL PRIVILEGES ON db1.* TO 'jeffrey'@'localhost' WITH GRANT OPTION;
GRANT 'role1', 'role2' TO 'user1'@'localhost', 'user2'@'localhost';
GRANT SELECT ON world.* TO 'role3';
GRANT SELECT ON world.paisos TO 'usuari'@'192.168.2.10';
GRANT SELECT ON world.paisos TO PUBLIC;
GRANT INSERT, UPDATE, DELETE ON database_name.table_name TO 'nombre_de_usuario'@'localhost';
```

## 12.4 Privilegis principals

| Privilegi | Permet… |
|---|---|
| `ALL PRIVILEGES` | Tots els privilegis disponibles sobre una BD o conjunt d'objectes |
| `SELECT` | Seleccionar dades d'una taula |
| `INSERT` | Inserir dades en una taula |
| `UPDATE` | Actualitzar dades d'una taula |
| `DELETE` | Eliminar registres d'una taula |
| `CREATE` | Crear noves bases de dades o taules |
| `DROP` | Eliminar bases de dades o taules |
| `ALTER` | Canviar l'estructura d'una taula |
| `SHOW DATABASES` | Veure la llista de bases de dades |
| `USAGE` | Només connectar-se al servidor MySQL |

```sql
GRANT ALL PRIVILEGES ON nom_bd.* TO 'nom_usuari'@'localhost';
GRANT SELECT ON nom_bd.nom_taula TO 'nom_usuari'@'localhost';
```

## 12.5 Objectes sobre els quals es donen permisos

| Objecte | Sintaxi |
|---|---|
| Base de dades | `GRANT privilegis ON nom_bd.* TO 'usuari'@'localhost';` |
| Taula | `GRANT privilegis ON nom_bd.nom_taula TO 'usuari'@'localhost';` |
| Procediment | `GRANT EXECUTE ON PROCEDURE nom_bd.nom_proc TO 'usuari'@'localhost';` |
| Funció | `GRANT EXECUTE ON FUNCTION nom_bd.nom_funcio TO 'usuari'@'localhost';` |
| Vista | `GRANT privilegis ON nom_bd.nom_vista TO 'usuari'@'localhost';` |
| Columnes | `GRANT privilegis (col1, col2) ON nom_bd.nom_taula TO 'usuari'@'localhost';` |
| Events | `GRANT privilegis ON EVENT nom_event TO 'usuari'@'localhost';` |
| Tots els objectes | `GRANT privilegis ON *.* TO 'usuari'@'localhost';` |

## 12.6 Rols

Un **rol** és un grup de privilegis relacionats que es pot concedir a un usuari. Normalment es creen per a una aplicació de BD i faciliten mantenir i revocar privilegis.

- Un usuari pot tenir diversos rols, i un mateix rol es pot assignar a diversos usuaris.
- Es creen i s'eliminen amb **`CREATE ROLE`** i **`DROP ROLE`**.
- Els **permisos es donen al rol** amb el `GRANT` bàsic.
- El **rol s'assigna a l'usuari** amb una extensió de `GRANT` (com si fos un privilegi més).

```sql
CREATE ROLE periodista;
GRANT SHOW DATABASES ON *.* TO periodista;
GRANT periodista TO usuari@localhost;
```

## 12.7 REVOKE — Sintaxi

```sql
REVOKE <tipus_de_privilegi> [(llista_de_columnes)]
    ON [tipus_d_objecte] <nivell>
    FROM <usuari_o_rol>;
```

Els valors de `nivell` i `tipus_d_objecte` són els mateixos que a `GRANT`.

### Exemple

```sql
SHOW GRANTS FOR usuari@localhost;
```

```text
+-----------------------------------------------------------------+
| Grants for usuari@localhost                                     |
+-----------------------------------------------------------------+
| GRANT `periodista` TO `usuari`@`localhost`                      |
| GRANT USAGE ON *.* TO `usuari`@`localhost` IDENTIFIED BY ***    |
| GRANT ALL PRIVILEGES ON `basededades`.* TO `usuari`@`localhost` |
+-----------------------------------------------------------------+
```

```sql
REVOKE periodista FROM `usuari`@`localhost`;
REVOKE ALL PRIVILEGES ON `basededades`.* FROM `usuari`@`localhost`;
```

[← Anterior](11_seguretat_sgbd_control_acces.md) · [Següent: Còpies de seguretat →](13_copies_seguretat_conceptes.md)
