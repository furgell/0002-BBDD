# 03. Arquitectura ANSI/SPARC

> Sessió 3 · RA1 · Gestió i seguretat de bases de dades (DAM 2n)

És un **model de tres nivells** proposat per a sistemes de bases de dades amb l'objectiu de separar la manera com les dades es **representen físicament**, com es **veuen lògicament** i com els **usuaris hi interactuen**.

```
 Nivell extern      Vista externa 1  ...  Vista externa n
                          \              /
 Nivell conceptual      Esquema conceptual
                                |
 Nivell intern            Esquema intern
                                |
                       Base de dades emmagatzemada
```

1. Nivell físic (capa física)
2. Nivell conceptual (capa lògica)
3. Nivell extern (capa d'aplicació o vista externa)

## 1. Capa física (nivell intern)

- Correspon al nivell més baix.
- Gestiona l'emmagatzematge físic de les dades en dispositius de memòria (discs, SSD…).
- Conté la descripció dels mecanismes d'accés, índexs i arxius físics.

**Funcions:**
- Control d'entrada i sortida (E/S).
- Gestió de la memòria secundària.
- Optimització dels temps d'accés.

**Exemples:** estructures de dades com blocs, pàgines, B-trees.

## 2. Capa lògica (nivell conceptual)

- Representa la visió general de la base de dades des d'una perspectiva independent del maquinari i del programari específic.
- Conté la definició de les estructures lògiques de les dades: taules, columnes, relacions, etc.

**Funcions:**
- Descripció de les dades en termes d'esquemes.
- Definició de restriccions d'integritat.
- Proporciona **independència lògica** de les dades.

**Exemple:** un esquema relacional amb entitats i relacions.

## 3. Capa d'aplicació (vista externa)

- Correspon al nivell més alt de l'arquitectura.
- Defineix com els usuaris i les aplicacions veuen les dades.
- Permet **múltiples vistes** per a diferents tipus d'usuaris o aplicacions.

**Funcions:**
- Proporciona independència de dades externes.
- Control d'accés basat en necessitats individuals.

**Exemples:** vistes SQL creades per a aplicacions específiques o perfils d'usuari.

## 4. Avantatges de l'arquitectura ANSI/SPARC

- **Independència física de les dades:** els canvis en l'estructura física no afecten l'estructura lògica o externa.
- **Independència lògica de les dades:** els canvis en la capa conceptual no afecten les vistes externes dels usuaris.
- **Flexibilitat i seguretat:**
  - Possibilitat de crear vistes personalitzades per a diferents usuaris.
  - Control d'accés detallat a les dades.

## 5. Exemple d'aplicació

Una empresa amb tres nivells d'usuaris: **directors, empleats i clients**.

| Capa | Exemple |
|---|---|
| **Física** | Les dades es guarden en discs, amb índexs optimitzats. |
| **Lògica** | L'esquema de la base de dades mostra taules de productes, clients i transaccions. |
| **Aplicació** | Els directors veuen informes complets, els empleats només accedeixen a dades limitades i els clients només poden veure les seves pròpies comandes. |
