# 14. Polítiques de seguretat II — Còpies, rotació, suports i restauració

*NF1: Seguretat lògica*

[← Tornar a l'índex](README.md)

Continguts:

1. Objectius de les còpies de seguretat
2. Realització de còpies seguint diverses estratègies
3. Programació temporal de còpies seguint esquemes de rotació
4. Utilització de suports d'emmagatzematge remots i extraïbles
5. Restauració de còpies de seguretat

---

## 14.1 Objectius de les còpies de seguretat

Les còpies de seguretat garanteixen dos objectius:

- **Integritat**
- **Disponibilitat**

Serveixen per restaurar el sistema operatiu, les aplicacions i les dades en cas de desastre.

- Es poden fer en molts suports: cintes, CD, DVD, discos externs o emmagatzematge remot.
- Cal pensar com **destruir de forma segura** els suports on s'han guardat les dades; hi ha mètodes al mercat que en garanteixen la destrucció.

> **Activitat**: visitar les webs de Blancco i EDR Solutions i analitzar els mecanismes de destrucció de discos i ordinadors que ofereixen.

---

## 14.2 Tipus de còpia segons la quantitat de fitxers

### Completa
Còpia de **tots els arxius i directoris** seleccionats.

### Diferencial
Es copien tots els arxius **creats o actualitzats des de l'última còpia completa**.

- Exemple: completa cada divendres a les 00:00 i diferencial la resta de dies → cada diferencial guarda tot el que s'ha creat o modificat des del divendres a les 00:00.
- **Avantatge** respecte a la completa: menys espai i temps de còpia.

### Incremental
Es copien els arxius **modificats des de l'última còpia completa o diferencial (o incremental)** feta.

- Exemple: completa el divendres a les 00:00 i incrementals la resta de dies → cada incremental només guarda el que s'ha creat o modificat aquell dia.
- **Avantatge** respecte a la diferencial: còpia més ràpida i que ocupa menys.
- **Inconvenient**: per restaurar cal la còpia completa **i totes les incrementals** fetes des d'aleshores.

| Tipus | Què copia | Temps/espai de còpia | Restauració necessita |
|---|---|---|---|
| Completa | Tot | Màxim | Només la completa |
| Diferencial | Canvis des de l'última completa | Mitjà (creix cada dia) | Completa + última diferencial |
| Incremental | Canvis des de l'última còpia | Mínim | Completa + totes les incrementals |

---

## 14.3 Programació temporal: esquemes de rotació

Un **esquema de rotació** és un mètode òptim per guardar informació en formats o contenidors múltiples. N'hi ha tres:

- GFS (*Grandfather-Father-Son*)
- Torre de Hanoi
- Backup incremental

### GFS (Grandfather-Father-Son)

L'esquema més popular:

- **Avi (Grandfather)**: còpia completa **mensual** (preferiblement *off-site*).
- **Pare (Father)**: còpia completa **setmanal** (*on-site*).
- **Fill (Son)**: còpia incremental **diària** (*on-site*).

**Benefici**: conserva còpies recents i, alhora, còpies anteriors durant un període determinat.

**Exemple** (completa els divendres):

| Diu (1) | Dil (2) | Dim (3) | Dc (4) | Dij (5) | Div (6) | Diss (7) |
|---|---|---|---|---|---|---|
| Dif./Inc. o res | Dif./Inc. | Dif./Inc. | Dif./Inc. | Dif./Inc. | **Completa** | Dif./Inc. o res |
| **Diu (8)** | **Dil (9)** | **Dim (10)** | **Dc (11)** | **Dij (12)** | **Div (13)** | **Diss (14)** |
| Dif./Inc. o res | Dif./Inc. | Dif./Inc. | Dif./Inc. | Dif./Inc. | **Completa** | Dif./Inc. o res |

Si el sistema falla el **dijous 12**:

- Cal la còpia completa del **divendres 6**.
- Amb diferencials: només la diferencial del **dimecres 11**.
- Amb incrementals: totes les incrementals del **dissabte 7 al dimecres 11**.

### Torre de Hanoi

Còpia amb diversos discos (p. ex. 5, etiquetats de la A a la E):

- El disc **A** es reutilitza cada 2 sessions (dia sí, dia no).
- El disc **B** cada 4 sessions.
- El disc **C** cada 8, i així successivament fins a cobrir el període.
- Nombre de sessions cobertes: **2^(n−1)**, on *n* és el nombre de discos (5 discos → 16 dies).

**Exemple: 5 discos, 16 sessions**

| Nivell | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 (Incremental) | | A | | A | | A | | A | | A | | A | | A | | A |
| 2 (Diferencial) | | | B | | | | B | | | | B | | | | B | |
| 3 (Diferencial) | | | | | C | | | | | | | | C | | | |
| 4 (Diferencial) | | | | | | | | | D | | | | | | | |
| 5 (Completa) | E | | | | | | | | | | | | | | | |

- **Benefici**: més simple de fer i de restaurar, i més econòmic que GFS (que fa servir el triple de discos).
- **Desavantatges**: cal un suport de gran capacitat i, en entorns automatitzats, programari especialitzat.

### Backup incremental

Es copien els arxius modificats des de l'última còpia completa o diferencial feta.

---

## 14.4 Suports d'emmagatzematge remots i extraïbles

**Error habitual**: guardar les còpies al mateix suport que les dades o al mateix lloc físic que els equips. Si la còpia és al mateix disc (o en una partició d'aquest) i hi ha una avaria física, es perden les dades **i** la còpia.

- Suports possibles: discos durs externs, CD, DVD, cintes, memòries flash, SSD…
- Fer còpies en un lloc diferent de l'original s'anomena **Off-site Data Protection**; hi ha empreses especialitzades en aquest servei.

| Suport | Característiques |
|---|---|
| **CD/DVD regravables** | Nombre molt limitat d'escriptures; després de diverses desenes fallen ("el suport és de només lectura"). |
| **Cinta** | Un dels suports més antics encara en ús. Gran capacitat i alta fiabilitat. Més lenta que els discos durs perquè l'accés és **seqüencial**. |
| **Memòries flash** (pendrive, microSD, CompactFlash…) | Poc recomanables: s'espatllen fàcilment per cops o pics de voltatge i tenen poca capacitat. |
| **Discos durs** | Gravació per **imantació** del suport. Han evolucionat en capacitat, temps d'accés i fiabilitat. |
| **SSD** | **Desavantatges**: cars i capacitat limitada. **Avantatges**: sense parts mecàniques (més fiables), més rendiment i temps d'accés per sota d'1 ms davant de diverses desenes de ms dels discos durs. |

---

## 14.5 Restauració de còpies de seguretat

- Punts de restauració
- Arrencada amb l'última configuració vàlida
- Recuperació automàtica del sistema
- Creació i restauració d'imatges

### Punts de restauració

També cal fer còpies del **sistema operatiu**, per restablir-lo ràpidament sense reinstal·lar-lo de zero. A Windows es pot tornar el sistema a l'estat anterior a l'acció que va causar l'avaria; la restauració retorna els arxius del sistema a un moment anterior.

Per això cal crear i guardar punts de restauració. Activar la protecció del sistema a Windows 7:

1. Obrir el **Tauler de control**.
2. Clicar **Sistema**.
3. Clicar **Protecció del sistema** al panell esquerre.
4. Seleccionar la unitat, clicar **Configurar** i triar la configuració desitjada.

### Arrencada amb l'última configuració vàlida

Quan no es pot fer la restauració (no hi ha punts de restauració o el sistema està massa degradat) i Windows no arrenca:

- En reiniciar, prémer **F8** → **Opcions d'inici avançades** → **Última configuració vàlida coneguda**. L'equip arrencarà amb normalitat.
- Si no funciona, restaurar des del símbol del sistema amb **`rstrui.exe`**.

**Reparació d'inici de Windows** (soluciona la falta d'arxius del sistema o arxius corruptes):

1. Reiniciar l'equip.
2. Prémer **F8** en arrencar → *Opcions d'inici avançades*.
3. Seleccionar *Reparar l'equip*.
4. Triar la distribució del teclat.
5. Introduir usuari i contrasenya.
6. Al menú d'opcions de recuperació, clicar **Reparació d'inici**.

### Recuperació automàtica del sistema (ASR)

Si el sistema no arrenca ni en mode a prova d'errors, però s'ha fet una còpia amb l'eina **ASR (Automated System Recovery)** en un suport extern:

1. Arrencar amb el CD original del sistema operatiu.
2. Als primers moments de la instal·lació, prémer **F2**.
3. Seguir els passos indicats.
4. Indicar el suport i el fitxer de la còpia.

### Creació i restauració d'imatges

Per fer la reinstal·lació més còmoda, senzilla i ràpida hi ha aplicacions que creen imatges del sistema, com **Symantec Ghost** i **Acronis True Image**.

[← Anterior](13_copies_seguretat_conceptes.md) · [Següent: mysqldump →](15_mysqldump.md)
