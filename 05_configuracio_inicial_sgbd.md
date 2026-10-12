# 05. Configuració inicial d'un SGBD

> Sessió 5 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

## 1. Configuració de seguretat de MySQL

```bash
sudo mysql_secure_installation
```

Aquest assistent permet:

- Establir **contrasenyes segures** per als usuaris administradors (com `root` en MySQL o `postgres` en PostgreSQL).
- **Eliminar o restringir els usuaris anònims** que vénen per defecte en alguns sistemes.
- **Desactivar l'accés remot** per a l'usuari administrador, limitant l'accés a usuaris locals o amb configuracions segures.

## 2. Estructura de permisos i usuaris

### 2.1 Usuaris

Són entitats (persones, aplicacions o serveis) que poden accedir al SGBD per interactuar amb les bases de dades. Cada usuari té un **nom d'usuari (login)** i, en la majoria de casos, una **contrasenya** associada per verificar la seva identitat.

### 2.2 Permisos

Són les autoritzacions que defineixen les accions que un usuari pot realitzar sobre la base de dades. Poden ser **generals** (aplicables a tot el sistema) o **específics** d'una taula, vista o columna.

**Exemples de permisos:**

| Permís | Funció |
|---|---|
| `SELECT` | Permet consultar dades. |
| `INSERT` | Permet afegir noves dades. |
| `UPDATE` | Permet modificar dades existents. |
| `DELETE` | Permet esborrar dades. |
| `CREATE` | Permet crear noves taules o bases de dades. |
| `DROP` | Permet eliminar taules o bases de dades. |
| `GRANT` | Permet atorgar permisos a altres usuaris. |

## 3. Creació d'un usuari

```sql
CREATE USER 'nou_usuari'@'localhost' IDENTIFIED BY 'contrasenya';
GRANT ALL PRIVILEGES ON *.* TO 'nou_usuari'@'localhost';
FLUSH PRIVILEGES;
```

## 4. Arxius de configuració d'un SGBD

Els arxius de configuració contenen els paràmetres que defineixen **com funciona el servidor** de bases de dades. Permeten modificar opcions del sistema per ajustar-lo a les necessitats de l'entorn o aplicació.

En MySQL, l'arxiu de configuració principal es troba normalment (Linux/Ubuntu) a:

```
/etc/mysql/my.cnf
```

## 5. El fitxer `my.cnf`

**Configuracions inicials importants:**

- Port per defecte (**3306** per a MySQL).
- Màxim nombre de connexions.
- Directori de dades.

**Paràmetres clau a ajustar segons les necessitats de l'empresa:**

| Paràmetre | Descripció |
|---|---|
| `max_connections` | Màxim nombre de connexions simultànies. |
| `query_cache_size` | Memòria per a la cache de consultes. |
| `innodb_buffer_pool_size` | Optimitza l'ús de memòria (en bases de dades grans). |

## 6. Configuració de còpies de seguretat

Les còpies de seguretat protegeixen contra pèrdues de dades degudes a fallades del sistema, corrupció de dades o errors humans.

**Generar una còpia de seguretat:**

```bash
mysqldump -u root -p nom_base_dades > copia_segur.sql
```

**Carregar una còpia de seguretat:**

```bash
mysql -u usuari -p nom_base_dades < copia_segur.sql
```

## 7. Comandes bàsiques de manteniment

Permeten monitorar l'estat del servidor, gestionar serveis i realitzar tasques bàsiques de manteniment.

| Tasca | Comanda |
|---|---|
| Reiniciar el servei de MySQL | `sudo systemctl restart mysql` |
| Connexió amb el servidor | `mysql -u usuari -p` |
| Comprovar les bases de dades | `SHOW DATABASES;` |
| Verificar la integritat d'una taula | `CHECK TABLE nom_taula;` |
| Altres | Iniciar i aturar el servidor |

## 8. Comprovar usuaris i permisos

**Usuaris existents (per consola SQL):**

```sql
SELECT User, Host FROM mysql.user;
```

**Permisos d'un usuari:**

```sql
SHOW GRANTS FOR 'nom_usuari'@'localhost';
```
