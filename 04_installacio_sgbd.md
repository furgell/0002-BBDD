# 04. Instal·lació d'un SGBD

> Sessió 4 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

Procés d'instal·lació de **MySQL** en **Ubuntu**.

## 1. Actualitza els paquets del sistema

- **Seguretat:** els paquets del sistema inclouen actualitzacions de seguretat crítiques que poden solucionar vulnerabilitats descobertes recentment.
- **Estabilitat:** moltes vegades les actualitzacions inclouen correccions d'errors o millores de rendiment que fan el sistema més estable.

```bash
sudo apt update
sudo apt upgrade
```

## 2. Instal·la MySQL

Ubuntu ofereix MySQL en els seus repositoris per defecte:

```bash
sudo apt install mysql-server
```

## 3. Comprova l'estat del servei de MySQL

Un cop finalitzada la instal·lació, el servei hauria d'haver-se iniciat automàticament:

```bash
sudo systemctl status mysql
```

Si el servei està actiu, es veurà un missatge indicant que està en funcionament.
