# 06. Seguretat de la informació

> NF1 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

## 1. Seguretat de la informació

Actualment, les dades s'han convertit en un **actiu crític** per a empreses, organitzacions i individus. La informació que emmagatzemem, compartim i gestionem és essencial per al negoci i la seva seguretat és un tema de màxima importància.

En l'àmbit informàtic, la seguretat es centra a **protegir** els **sistemes** informàtics, les **xarxes**, les **dades** i la informació digital de les **amenaces**, els **atacs** i les **vulnerabilitats**.

- **Seguretat activa:** prendre mesures anticipades per **evitar** que les amenaces tinguin èxit.
- **Seguretat passiva:** mesures **després** que s'hagi produït un **incident** o amenaça. Està més orientada a la **recuperació**.

## 1.1. Confidencialitat, integritat i disponibilitat

La seguretat de les dades és el conjunt de precaucions que prenem per evitar que les dades es perdin o es malmetin, sigui per accident o deliberadament. Es basa en **3 principis** que s'han de complir sempre (**triada CIA**):

- **Confidencialitat:** només les persones autoritzades poden accedir i veure les dades.
- **Integritat:** les dades no han estat alterades.
- **Disponibilitat:** garantir que les dades estiguin sempre accessibles.

### 1.1.1. Confidencialitat

Garantia que **només les persones autoritzades** poden accedir i veure les dades. És com mantenir un secret: les dades confidencials s'han de protegir contra l'accés no autoritzat.

**Mesures:** contrasenyes segures, autenticació d'usuari, xifrat de dades i controls d'accés.

**Control d'accés:**

- **Control d'accés global:** creació d'usuaris que s'han d'autenticar amb usuari/clau. Els usuaris autenticats tenen accés a **tota** la informació.
- **Control d'accés discrecional:** l'autenticació limita a **quines dades en concret** té accés l'usuari. És el que ofereixen la majoria de SGBD.

### 1.1.2. Integritat

Implica garantir que les dades no hagin estat **alterades** de manera no autoritzada o accidental. Les dades íntegres són coherents i exactes, i no han estat modificades sense el coneixement o l'autorització adequats.

**Objectiu:** protegir la base de dades contra operacions que introdueixin **inconsistències**.

**Mesures:** firmes digitals, controls d'accés i sistemes de detecció d'intrusos.

**Tipus d'integritat:**

| Tipus | Descripció |
|---|---|
| **Integritat d'entitats** | No permet valors `NULL` a les claus primàries de les relacions. |
| **Integritat referencial** | Valida la concordança entre els valors d'una clau forana i els de la clau primària a la qual fa referència. |
| **Integritat semàntica** | Permet definir les regles de negoci. |

### 1.1.3. Disponibilitat

Garanteix que les dades estiguin **accessibles** quan sigui necessari: disponibles per als usuaris legítims quan ho requereixin i no bloquejades o inaccessibles per fallades tècniques o altres interrupcions.

**Mesures:** còpies de seguretat regulars, servidors redundants, sistemes de balanceig de càrrega, polítiques de recuperació d'urgència, etc.

## 1.2. Vulnerabilitats. Elements vulnerables

Les bases de dades són objectius comuns dels atacants i poden contenir gran quantitat de dades sensibles. Les vulnerabilitats poden exposar aquestes dades a riscos de **pèrdua, modificació o accés no autoritzat**. També factors externs poden provocar avaries que afectin la disponibilitat i la integritat.

**Elements vulnerables del sistema:** maquinari, programari i dades.

**Vulnerabilitats relacionades directament amb les dades:**

1. Injecció SQL
2. Accés no autoritzat
3. Manca de xifrat
4. Desactualització del programari
5. Manca de monitoratge i auditoria
6. Atacs de negació de servei (DoS)
7. Manca de polítiques de contrasenyes fortes
8. Exposició de metadades
9. Manca de desinfecció de dades
10. Exposició d'errors detallats
11. Manca de plans de seguretat i contingència

### 1.2.1. Injecció SQL

És una de les vulnerabilitats més conegudes. Permet als atacants **inserir comandes SQL malicioses** a través de formularis web o altres entrades d'usuari. Pot donar accés no autoritzat a les dades o fins i tot eliminar-ne o modificar-ne el contingut.

Exemple (consulta esperada vs. consulta injectada):

```sql
-- Entrada esperada
SELECT * FROM Users WHERE UserID = "941938" AND password = "XFNEifQwKH08";

-- Entrada injectada
SELECT * FROM Users WHERE UserID = "" OR 1=1 -- " AND password = "";
```

### 1.2.2. Accés no autoritzat

Les bases de dades han de protegir-se amb controls d'accés adequats. Si els permisos no estan ben configurats, els atacants poden accedir a dades sensibles.

### 1.2.3. Manca de xifrat

La manca de xifrat de dades **en trànsit o en repòs** pot exposar les dades a interceptacions malintencionades. Les dades sensibles haurien de xifrar-se sempre per protegir-ne la confidencialitat.

### 1.2.4. Desactualització del programari

No mantenir actualitzat el programari de la base de dades la deixa vulnerable a vulnerabilitats conegudes i a **atacs de dia zero**.

### 1.2.5. Manca de monitoratge i auditoria

Sense controls de monitoratge i auditoria, les amenaces poden passar desapercebudes. La falta de registres d'auditoria dificulta detectar activitats inusuals.

### 1.2.6. Atacs de negació de servei (DoS)

Sobrecarreguen la base de dades amb moltes peticions, provocant la indisponibilitat del servei per als usuaris legítims.

### 1.2.7. Manca de polítiques de contrasenyes fortes

Les contrasenyes febles o predeterminades faciliten l'accés no autoritzat.

### 1.2.8. Exposició de metadades

Una configuració inadequada pot revelar metadades sensibles (noms de taules o camps).

### 1.2.9. Manca de desinfecció de dades

Les dades d'entrada d'usuari no desinfectades poden contenir codi maliciós que s'executi dins la base de dades.

### 1.2.10. Exposició d'errors detallats

Mostrar errors detallats a aplicacions o usuaris pot donar als atacants informació útil per explotar vulnerabilitats.

### 1.2.11. Manca de plans de seguretat i contingència

Sense plans de seguretat i contingència, les bases de dades són vulnerables a la pèrdua de dades en cas d'incidents o desastres.

## 1.3. Caràcter personal i intimitat de les dades. Legislació

### LOPD (Llei Orgànica 15/1999)

- Definida a la **Llei Orgànica 15/1999 de Protecció de Dades de Caràcter Personal**. Considera la protecció de dades un **dret fonamental** de les persones.
- L'**Agencia Española de Protección de Datos (AEPD)** controla el compliment de la normativa.
- Especifica les obligacions d'empreses i administració pública relacionades amb la protecció de dades personals.
- Són dades personals qualsevol informació que identifiqui una persona (DNI, fotografia, nom), més dades laborals, econòmiques, etc.

### Drets ARCO

| Dret | Descripció |
|---|---|
| **Accés** | Els ciutadans poden controlar per si mateixos l'ús que es fa de les seves dades personals. |
| **Rectificació** | Si les dades són incompletes, inexactes, excessives o inadequades, es pot demanar al responsable del fitxer la rectificació o cancel·lació. |
| **Cancel·lació** | El ciutadà pot exigir la supressió de dades que consideri inadequades o excessives. |
| **Oposició** | Els titulars poden demanar que deixin de tractar les seves dades sense consentiment amb finalitats de publicitat o prospecció comercial. |

### Evolució de la legislació

| Any | Norma |
|---|---|
| 1999 | Llei Orgànica de Protecció de Dades de caràcter personal (LOPD) |
| 2002 | Llei de serveis de la societat de la informació i comerç electrònic (**LSSI**) |
| 2003 | Llei de firma electrònica (certificats digitals i validesa jurídica) |
| 2003 | Reglament de desenvolupament de la LOPD |
| 2007 | Llei de conservació de dades a les comunicacions electròniques i xarxes públiques |
| 2016 | Reglament General de Protecció de Dades (**RGPD**), aprovat el 27 d'abril; en vigor des del maig de 2018 |
| 2018 | Llei Orgànica 3/2018, Protecció de Dades Personals i Garanties dels Drets Digitals (**LOPDGD**), aprovada el 5 de desembre; adapta l'RGPD a Espanya |

L'RGPD **amplia els drets ARCO**. Amb la LOPDGD i l'RGPD es **deroga l'antiga LOPD**.

### El Reglament General de Protecció de Dades (RGPD)

Estableix l'obligació de les organitzacions d'adoptar mesures per garantir la protecció de les dades (sistemes informàtics, fitxers, suports d'emmagatzematge), demanar el **consentiment** per usar dades personals i definir procediments operatius. Afecta totes les organitzacions que operen amb **residents a la UE**, encara que no hi tinguin la seu.

**Canvis més importants respecte a la LOPD:**

- **Principi de responsabilitat proactiva:** les organitzacions han d'analitzar quines dades tracten i amb quines finalitats, quines operacions de tractament realitzen, i han de poder **demostrar el compliment** davant de tercers.
- **Principi d'enfocament de risc:** algunes mesures només s'apliquen quan hi ha un alt risc per als drets i llibertats. Les mesures s'han d'adaptar a les característiques de l'organització.

### Dada de caràcter personal

> «Qualsevol informació sobre una persona física identificada o identificable, com ara un nom, un número d'identificació, dades de localització, un identificador en línia o un o diversos elements propis de la identitat física, fisiològica, genètica, psíquica, econòmica, cultural o social d'aquesta persona.»

**Tenen la consideració de dades personals:**

- Nom i cognoms, data de naixement.
- Telèfon, adreça postal i electrònica.
- Dades biomètriques (empremtes, iris, dades genètiques, imatge, raça, veu…).
- Dades sanitàries (malalties, avortaments, cirurgia estètica…).
- Orientació sexual.
- Ideologia, creences religioses, afiliació sindical, estat civil…
- Dades econòmiques: bancàries, solvència, compres.
- Consums (aigua, gas, electricitat, telèfon…), subscripcions a premsa.
- Dades judicials (antecedents penals).

### Dades personals sensibles

Són les que, per la seva transcendència per a la intimitat i per evitar que s'usin per discriminar, requereixen més protecció: **raça, opinions polítiques, conviccions religioses, afiliació a partits o sindicats, salut, orientació sexual, dades genètiques i biomètriques**.

### Nivells de seguretat

| Nivell | Tipus de dades |
|---|---|
| **Bàsic** | Dades personals que no revelen informació sensible ni presenten riscos significatius. |
| **Mitjà** | Dades que poden revelar informació sensible: mèdiques, financeres, de recursos humans… |
| **Alt** | Dades que, en revelar-se, suposen un risc alt: salut, biomètriques, genètiques. |

### Drets i obligacions

**L'usuari que subministra les dades:**
- Ha de tenir ple coneixement de l'ús i tractament que se'n farà.
- Ha de consentir que se'n pugui fer ús.
- Ha de poder modificar i/o revocar les dades en qualsevol moment.

**El titular del fitxer ha de garantir:**
- Les obligacions imposades per al correcte tractament de les dades.
- La conservació, accés i destrucció de les mateixes.

### Obligacions dels responsables del tractament

- Proporcionar procediments senzills per exercir els drets.
- Disposar de formularis per informar els usuaris i perquè exerceixin els seus drets.
- **Pseudonimització** de les dades i bases de dades.
- Tenir en compte les mesures de seguretat abans d'iniciar el tractament i mentre es duu a terme.
- Tenir un **registre de les activitats del tractament**.
- Poder demostrar davant l'autoritat que es compleix la llei si ho sol·licita.
- **Xifrar** les dades personals, a més de guardar-les amb pseudònims.
- **Notificar les violacions de seguretat**.

## 1.4. Amenaces a la seguretat

En una situació bàsica es detecten tres actors que poden rebre amenaces pròpies, independents de les dades:

- Ordinador servidor.
- Xarxa (pròpia o Internet).
- Sistema de còpies de seguretat (propi o extern).

A aquestes cal afegir les amenaces pròpies dels motors de bases de dades.

### Amenaces accidentals

Actuacions que perjudiquen l'estabilitat i integritat de la base de dades **sense intenció**: manca de precaució, errada humana, fallada elèctrica, accions externes a la BD, vulnerabilitat de la base de dades.

**Exemples:**
- Accés a les contrasenyes d'usuaris (error humà, confiar les dades d'accés, clau massa senzilla).
- Manca de previsió de còpies de seguretat.
- **Sistema de privilegis de màniga ampla:** l'administrador dona accés total a tots els usuaris.
- Comptes d'usuari sense auditar.
- Fallada general del sistema elèctric (cal un SAI / sistema d'alimentació ininterrompuda).
- Contrasenyes no segures.
- Deixar sense validació l'accés a l'ordinador on són les dades.
- Accés físic senzill a la sala de màquines (un llapis USB pot copiar tota la informació).
- Transmissió de dades sense encriptar per les xarxes.
- Xarxes sense fil sense encriptar.

### Amenaces intencionades

Són les **més perilloses**. Una amenaça accidental pot convertir-se en una vulnerabilitat que deixi una porta oberta a una intencionada. Hi ha una persona interessada al darrere que cercarà els camins necessaris.

**Exemples:**
- **Robatoris** de documentació, bases de dades, claus d'usuaris, del servidor…
- **Frau:** accedir sense autorització per obtenir dades sensibles (números de compte, contrasenyes…).
- **Pèrdua de confidencialitat:** una persona aliena visualitza dades confidencials.
- **Pèrdua de privacitat:** algú observa dades personals d'una persona o organització.
- **Pèrdua d'integritat:** una persona aliena modifica informació de la base de dades.

### Solucions a les amenaces (preventives i de contingència)

- Comptes d'usuari i contrasenya (autenticació abans d'accedir).
- Privilegis i rols per limitar les parts de la BD accessibles i les accions permeses.
- Sistema de **còpies de seguretat**.
- **Fragmentació** de la base de dades en diferents ubicacions.
- **Encriptació** de les dades que viatgen per la xarxa.
- **Certificats digitals** per verificar la identitat de qui envia la informació.
- **Tallafocs (firewall)** per limitar l'accés a la xarxa.
- **Servidor intermediari (proxy)** per controlar les peticions que arriben al servidor.
