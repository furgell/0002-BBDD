# 09. Condicions d'inici i aturada del SGBD

> Sessió 9 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

## 1. La importància de saber iniciar i aturar un SGBD

- **Garantir la disponibilitat del servei:** iniciar correctament un SGBD és essencial perquè aplicacions i usuaris puguin accedir a les dades en tot moment.
- **Prevenir corrupcions de dades i pèrdues:** aturar el SGBD de manera controlada evita la corrupció de dades. Un tancament brusc (per exemple, una fallada elèctrica) pot deixar operacions a mig fer i comprometre la integritat de la BD.
- **Assegurar que el sistema sigui segur i estable:** una bona gestió de l'inici i l'aturada garanteix seguretat i estabilitat.

## 2. Com funciona l'inici d'un SGBD

1. **Càrrega del servei al sistema operatiu:** el SO inicia el procés del servidor de BD i reserva els recursos inicials (memòria, ports de xarxa…).
2. **Connexió amb els arxius de configuració:** el servei carrega els paràmetres (ubicació de les dades, ports, límits de memòria…).
3. **Verificació de la consistència de les dades:** es revisa la integritat i consistència de la BD abans d'acceptar connexions (comprovació de transaccions pendents).
4. **Inici del procés de connexions i gestió de transaccions:** el SGBD obre els ports de connexió i inicia els processos per gestionar les transaccions entrants.

## 3. Com funciona l'aturada d'un SGBD

### 3.1. Tancar connexions actives

- Notificar els usuaris actius.
- Rebutjar noves connexions.
- Desconnectar usuaris inactius.

### 3.2. Finalitzar les transaccions pendents

- Completar les transaccions actives.
- Desfer les transaccions incompletes.
- Registrar l'estat: actualitzar els registres de transaccions (*logs*).

### 3.3. Detenir els processos associats

- Tancar els serveis del SGBD.
- Alliberar recursos del sistema (memòria, ports de xarxa…).
- Confirmar l'aturada: verificar que no queden processos residuals en execució.

## 4. Gestió manual de MySQL

| Acció | Comanda |
|---|---|
| Iniciar MySQL | `systemctl start mysql` |
| Comprovar l'estat del servei | `systemctl status mysql` |
| Aturar el servei | `systemctl stop mysql` |
| Reiniciar el servei | `systemctl restart mysql` |

## 5. Registre d'errors i problemes habituals

**Consultar el registre d'errors:**

```bash
sudo tail -f /var/log/mysql/error.log
```

**Problemes habituals durant l'inici:**
- Fitxer de configuració incorrecte.
- Falta d'espai al disc o permisos insuficients.
- Arxius de dades corruptes.

**Problemes habituals durant l'aturada:**
- Processos bloquejats o serveis que no es detenen.

**Identificar i aturar processos amb `kill`:**

```bash
ps aux | grep mysql
kill -9 <pid>        # <pid> = identificador del procés
```

## 6. Configuració de l'inici automàtic de MySQL

Habilitar que MySQL arrenqui automàticament cada vegada que el SO es reinicia:

```bash
sudo systemctl enable mysql
```

Deshabilitar l'inici automàtic:

```bash
sudo systemctl disable mysql
```

## 7. Activitat

1. Inicia MySQL.
2. Consulta l'estat del servei.
3. Atura el servei i comprova que no hi ha processos actius.
4. Edita el fitxer de configuració `mysqld.cnf` per canviar el port al **3307**.
5. Reinicia MySQL amb la comanda correcta.
6. Verifica el canvi:
   ```bash
   mysqladmin -u root -p variables | grep port
   ```
7. Canvia el port a un ja ocupat (per exemple, **80**).
8. Observa el log d'errors i resol el problema.
9. Torna a deixar el port al **3306** i posa en funcionament el servei.
