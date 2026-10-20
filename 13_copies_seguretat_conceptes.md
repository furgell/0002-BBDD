# 13. Còpies de seguretat: conceptes generals

[← Tornar a l'índex](README.md)

## 13.1 Què són

Les **còpies de seguretat** (*backups*) tenen com a objectiu restaurar les dades del sistema informàtic després d'un desastre, o bé restaurar uns fitxers concrets que s'hagin esborrat accidentalment o s'hagin corromput.

## 13.2 Selecció de les dades

Cal seleccionar correctament quins arxius es copiaran i **documentar-ho**:

- Còpia parcial de fitxers
- Creació d'una imatge de tot el sistema
- Identificació de canvis

Un cop identificats els arxius, es decideix **amb quina freqüència** es copiarà cadascun. Aquest estudi previ és important perquè cada còpia ocupa espai en disc i requereix temps de procés.

## 13.3 Qui fa les còpies?

- Deixar les còpies en mans dels usuaris **no és una bona pràctica**.
- L'**administrador del sistema** ha de ser qui fa les còpies i qui s'assegura que s'han fet correctament.

## 13.4 Classificació segons el tipus de dades copiades

- No estructurat
- Còpia intermèdia
- Còpia total
- Còpia diferencial
- Còpia incremental
- Còpia del sistema

## 13.5 Mètodes de còpia

| Mètode | Descripció |
|---|---|
| **No estructurat** | Conjunt de còpies sense cap organització lògica. Facilita la creació però dificulta la recuperació. |
| **Còpia intermèdia** | Només es copien els arxius seleccionats. Sol ser una pràctica puntual per copiar un arxiu concret. |
| **Còpia total** | Es copien tots els arxius seleccionats. |
| **Còpia diferencial** | Copia tots els arxius creats o modificats des de l'**última còpia total**. |
| **Còpia incremental** | Copia els arxius modificats respecte a l'**última còpia** (de qualsevol tipus). |
| **Còpies externalitzades** | Còpies que es guarden fora de l'empresa (p. ex. en cintes). |

Exemple amb total el diumenge (Dl = dilluns, Dm = dimarts, Dc = dimecres):

| | Diumenge | Dilluns | Dimarts | Dimecres |
|---|---|---|---|---|
| **Diferencial** | Total | Dl | Dl + Dm | Dl + Dm + Dc |
| **Incremental** | Total | Dl | Dm | Dc |

## 13.6 Dispositius per a còpies de seguretat

- Cintes magnètiques
- Discos durs
- Discos òptics
- Emmagatzematge d'estat sòlid
- Servei de còpies de seguretat remot

## 13.7 Sistemes de còpies de seguretat

| Sistema | Característiques |
|---|---|
| **En línia (online)** | El més accessible. La restauració pot començar en mil·lisegons. Ràpid però més car, i les dades poden ser esborrades accidentalment o infectades per virus. Ex.: disc dur intern o RAID connectat en xarxa. |
| **Línia propera** | Més barat que l'en línia però menys accessible. La restauració triga de segons a minuts. Es basa en emmagatzematge terciari. Ex.: llibreria de cintes magnètiques. |
| **Fora de línia** | Cal intervenció humana per accedir als suports. Temps d'accés de segons a hores. |
| **Extern** | Les còpies s'externalitzen en altres ubicacions perquè un desastre no les comprometi. Pot ser la pròpia empresa (recomanable a 2 km de distància) o una empresa especialitzada. |
| **Centre de recuperació de desastres / de recolzament** | Entra en funcionament quan un incident impedeix treballar amb el CPD principal. Té màquines amb capacitat similar i dades actualitzades gràcies a còpies en calent. |

## 13.8 Còpies de seguretat en temps real

Per resoldre els problemes de concurrència (fitxers en ús mentre es copien):

- **Còpia instantània** (*snapshot*): el sistema es congela i es copia aquella imatge.
- **Copiar els fitxers oberts més tard.**
- **Còpia en fred**: durant la còpia, la BD no està disponible per als usuaris.
- **Còpia en calent**: a més de la còpia, es crea un fitxer amb les modificacions fetes mentre es copiava.

## 13.9 Metadades

A més del contingut dels fitxers, cal guardar metadades:

- Descripció del sistema
- Sector d'arrencada
- Esquema de particions
- Metadades dels fitxers (permisos, grups…)
- Metadades del sistema (informació del registre…)

## 13.10 Recuperació de les dades

Procés pel qual es recuperen les dades del sistema a partir d'una còpia de seguretat feta prèviament.

## 13.11 Limitacions

- **Finestra de còpies de seguretat**: temps durant el qual s'estan fent les còpies.
- Impacte en el rendiment.
- Cost del maquinari, programari i feina.
- Amplada de banda de xarxa.

## 13.12 Control i monitoratge

Cal assegurar que:

- Les còpies estan correctament planificades.
- El personal que les fa està autoritzat.
- No hi accedeix ningú no autoritzat.
- Si es transporten o canvien de mans (o d'empresa), es manté la **cadena de confiança**.

A més:

- **Verificació**: comprovar que les còpies s'han fet correctament i sense errors.
- **Creació d'informes**: historials generats per l'ordinador i registres d'activitat i de canvis per monitorar les còpies.
- **Validació**: ús de **checksums o hashes** per assegurar la integritat i correcció de les dades guardades.

## 13.13 Consells

- Com més important és una dada, més necessària és la seva còpia.
- Un sistema de còpies només és útil si hi ha una **estratègia de recuperació**.
- Les còpies s'han de guardar **lluny del CPD principal**.
- Cal comprovar que les còpies són correctes i es poden restaurar.
- Cal **automatitzar** les còpies: les manuals provoquen errors.
- Guardar les dades en **formats estàndard i oberts**.

[← Anterior](12_dcl_mysql_usuaris_permisos_rols.md) · [Següent: Polítiques de seguretat II →](14_politiques_copies_rotacio_restauracio.md)
