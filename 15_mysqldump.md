# 15. mysqldump — Guia pràctica

[← Tornar a l'índex](README.md)

`mysqldump` forma part dels *MySQL Client Programs* i serveix per:

- Generar còpies de seguretat de bases de dades.
- Transferir-les a un altre servidor SQL.

## 15.1 Ús bàsic

Tres formes d'invocar-lo:

```bash
# Una BD (i opcionalment algunes taules; si no se n'indiquen, es copien totes)
mysqldump [opcions] nom_bd [taula1 taula2 ...] > backup.sql

# Una o més BD completes (no es poden indicar taules)
mysqldump [opcions] --databases nom_bd1 nom_bd2 > backup.sql

# Totes les BD del servidor (no es poden indicar taules)
mysqldump [opcions] --all-databases > backup.sql
```

En tots els casos la sortida es redirigeix al fitxer `backup.sql`, que és el que després es fa servir per restaurar.

Per veure totes les opcions:

```bash
mysqldump --help
```

## 15.2 Opcions habituals

| Opció | Funció |
|---|---|
| `-u usuari` | Usuari de connexió |
| `-p` | Demana la contrasenya (`-psecret` la passa directament, no recomanable) |
| `--password=secret` | Passa la contrasenya directament |
| `-h host` | Servidor remot |
| `--databases` | Copia BD completes |
| `--all-databases` | Copia totes les BD |
| `--ignore-table=bd.taula` | Exclou una taula (cal indicar `bd.taula`) |
| `--opt` | Activa les opcions per defecte més habituals |
| `--single-transaction` | Còpia consistent de BD transaccionals (InnoDB) |
| `--quick` | Llegeix les files una a una (útil amb taules grans) |
| `--routines` | Inclou procediments emmagatzemats |
| `--create-options` | Inclou totes les opcions específiques de creació de taules |
| `--add-drop-database` | Afegeix `DROP DATABASE` abans de cada `CREATE DATABASE` |
| `--force` | Continua encara que hi hagi errors |
| `--master-data` | Inclou la posició del log binari per sincronitzar esclaus en replicació |
| `--complete-insert` | `INSERT` complets amb els noms de les columnes |
| `--no-data` | Només l'esquema, sense registres |
| `--compatible=oracle` | Sortida compatible amb un altre SGBD |

## 15.3 Exemples

```bash
# Una BD completa
mysqldump clients > clients.sql

# Una BD amb dues taules
mysqldump clients saldos factures > clients.sql

# Dues BD completes
mysqldump --databases clients vendes > copia_cli_ven_sep_2023.sql

# BD clients excepte les taules 'temporal' i 'brossa'
mysqldump clients --ignore-table=clients.temporal --ignore-table=clients.brossa > copia_clients_2023.sql

# Totes les BD
mysqldump --all-databases > copia_full_sep_2023.sql

# Amb usuari i demanant contrasenya
mysqldump -u root -p --all-databases > copia_full_sep_2023.sql

# Contrasenya directa (no recomanable) i opcions per defecte
mysqldump -u root -psecret --all-databases --opt > copia_full_sep_2023.sql

# BD transaccional (InnoDB) de manera consistent
mysqldump -u root -p --single-transaction --quick vendes > copia_vendes_2023.sql

# Totes les BD d'un host remot, incloent procediments
mysqldump -h 192.168.1.100 -u root -p --routines --all-databases > copia_vendes_2023.sql

# Recreació des de zero, ignorant errors
mysqldump -u root -p --create-options --add-drop-database --force --databases clients comandes > copia_ven_ped_2023.sql

# Servidor mestre en replicació, amb INSERT complets
mysqldump -u root --password=secret --all-databases --master-data --complete-insert > copia_2023.sql

# Només l'esquema
mysqldump --no-data clients > copia_esquema_clients_2023.sql

# Sortida compatible amb Oracle
mysqldump --compatible=oracle --databases clients > copia_clients_oracle_2023.sql
```

## 15.4 Compressió amb gzip

```bash
# Còpia comprimida
mysqldump -u root -p --all-databases | gzip > copia_2023.sql.gz

# Descomprimir per restaurar
gunzip copia_2023.sql.gz
```

## 15.5 Restaurar la còpia

```bash
# Restauració estàndard
mysql -u root -p < copia.sql

# Descomprimir i restaurar en una sola línia
gunzip < copia.sql.gz | mysql -u root -p

# Una sola BD sense DROP/CREATE DATABASE: indicar la BD de destí
mysql -u root -p clients < copia_clients.sql

# Alternativa quan la BD ja existeix
mysqlimport -u root -p clients copia_clients.sql

# Executar el fitxer amb l'opció -e (una còpia és un script SQL)
mysql -u root -p -e "source /ruta/a/copia.sql"
```

[← Anterior](14_politiques_copies_rotacio_restauracio.md) · [Tornar a l'índex](README.md)
