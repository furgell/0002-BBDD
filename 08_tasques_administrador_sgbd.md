# 08. Tasques de l'administrador de SGBD

> Sessió 7 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

## 1. Introducció

Un **administrador de SGBD** té la responsabilitat de garantir el funcionament **òptim, segur i fiable** de les bases de dades que suporten els processos crítics d'una organització. Inclou tasques de configuració, seguretat, manteniment i optimització del rendiment, així com la recuperació en cas de fallades.

## 2. Instal·lació i configuració del SGBD

Un dels primers passos és instal·lar i configurar el sistema segons les necessitats de l'empresa.

- **Desplegament inicial:** instal·lar el programari SGBD (PostgreSQL, MySQL, SQL Server, Oracle…).
- **Configuració de paràmetres:** ajustar paràmetres bàsics com l'espai d'emmagatzematge, els límits de connexió, la seguretat i l'assignació de recursos de maquinari.
- **Creació d'entorns de desenvolupament i producció:** mantenir la separació de dades i aplicacions per evitar errors a l'entorn de producció.

## 3. Gestió de la seguretat

La seguretat és crítica per protegir la informació de l'empresa i dels clients.

- **Control d'accés i permisos:** definir qui pot accedir a la BD i quines accions pot fer. S'assignen rols com «lectura», «escriptura» o «administració».
- **Protecció contra amenaces:** autenticació amb contrasenyes segures, **SSL** per a connexions xifrades i limitació de l'accés extern.
- **Monitoratge d'activitat:** veure quins usuaris accedeixen a dades específiques o modifiquen registres ajuda a detectar activitats sospitoses i mantenir el control.

## 4. Control de rendiment

L'optimització del rendiment és clau per evitar la lentitud o la caiguda del sistema.

- **Monitorització del rendiment:** revisar regularment l'ús de recursos (CPU, memòria, disc) per identificar problemes.
- **Optimització de consultes:** optimitzar les consultes SQL per evitar consum excessiu de recursos i millorar el temps de resposta.
- **Gestió de recursos de maquinari:** a mesura que la BD creix, ajustar recursos o coordinar-se amb TI per garantir prou espai d'emmagatzematge.

## 5. Còpies de seguretat i recuperació

Són essencials per evitar la pèrdua de dades en cas de fallada del sistema o errors.

- **Creació de còpies regulars:** còpies **completes** i **incrementals**, programades periòdicament.
- **Proves de recuperació de dades:** verificar amb proves periòdiques que les còpies funcionen correctament.
- **Plans de recuperació davant fallades:** un bon pla inclou passos clars per restablir la BD en cas de problemes tècnics.

## 6. Actualitzacions i manteniment

Les actualitzacions són crucials per evitar vulnerabilitats i garantir el millor rendiment.

- **Aplicació de pegats i actualitzacions:** aplicar actualitzacions de seguretat i pegats per corregir errors del sistema.
- **Manteniment preventiu:** revisió de la integritat de les dades, compactació de taules per estalviar espai i revisió de l'estructura de la BD per optimitzar-la.
