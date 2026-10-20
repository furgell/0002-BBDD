# Índex · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

Teoria del primer RA, organitzada per temes.

## Fonaments dels SGBD

1. [Introducció als SGBD](01_introduccio_sgbd.md) — definició, funcions, components i beneficis
2. [Tipus de SGBD](02_tipus_sgbd.md) — classificació segons model, distribució, accés, instal·lació, transaccions i escala
3. [Arquitectura ANSI/SPARC](03_arquitectura_ansi_sparc.md) — nivells físic, conceptual i extern

## Instal·lació i configuració

4. [Instal·lació d'un SGBD](04_installacio_sgbd.md) — MySQL a Ubuntu
5. [Configuració inicial d'un SGBD](05_configuracio_inicial_sgbd.md) — seguretat, usuaris, `my.cnf`, còpies i manteniment

## Seguretat

6. [Seguretat de la informació](06_seguretat_informacio.md) — CIA, vulnerabilitats, legislació (LOPD, RGPD) i amenaces
7. [DCL: privilegis, usuaris i rols](07_dcl_privilegis_usuaris_rols.md) — `CREATE USER`, `GRANT`, `REVOKE`, rols

## Administració

8. [Tasques de l'administrador de SGBD](08_tasques_administrador_sgbd.md) — instal·lació, seguretat, rendiment, còpies i manteniment
9. [Condicions d'inici i aturada del SGBD](09_inici_i_aturada_sgbd.md) — arrencada, aturada controlada, `systemctl` i activitat
10. [Selecció del motor de SGBD](10_seleccio_motor_sgbd.md) — criteris SQL vs NoSQL i motors principals

## Seguretat lògica: control d'accés i còpies de seguretat

11. [Seguretat en l'SGBD i control d'accés](11_seguretat_sgbd_control_acces.md) — identificació, autenticació i autorització, DAC, RBAC i ordre de comprovació de permisos a MySQL
12. [DCL a MySQL: usuaris, permisos i rols](12_dcl_mysql_usuaris_permisos_rols.md) — `CREATE USER`, `SHOW GRANTS`, `GRANT`, `REVOKE`, privilegis, objectes i rols
13. [Còpies de seguretat: conceptes generals](13_copies_seguretat_conceptes.md) — mètodes de còpia, dispositius, sistemes, còpies en temps real, control i consells
14. [Polítiques de seguretat II: còpies, rotació, suports i restauració](14_politiques_copies_rotacio_restauracio.md) — completa, diferencial i incremental, GFS, Torre de Hanoi, suports i restauració
15. [mysqldump: guia pràctica](15_mysqldump.md) — opcions, exemples, compressió amb gzip i restauració
