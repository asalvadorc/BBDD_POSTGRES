
# 11. Consulta de creació de taules


A banda de poder consultar informació de una o més d'una taula, la sentència
SELECT pot servir per a crear una nova taula, amb estructura i dades (les que
venen de la pròpia sentència SELECT). Això sí, no podrem definir d'aquesta
manera ni clau principal, ni claus externes, ni cap altra restricció de les
conegudes.

A més, aquesta característica escapa del estàndard ANSI SQL, per la qual cosa
no li donarem excessiva importància.

**<u>Sintaxi</u>**

    SELECT <columnes> INTO nova_taula  
      FROM <taules>

La sentència pot dur qualsevol clàusula o predicat dels vistos fins ara, i el
resultat que done aquesta sentència, es guardarà en una nova taula, amb el nom
especificat.

El nom dels camps de la nova taula seran els especificats en l'apartat
<columnes>. Per tant és especialment recomanable la utilització d'àlies, ja
que si en posem seran el noms dels camps de la nova taula.

Els tipus de dades dels camps seran els heretats de la consulta SELECT.

En cas d'existir ja una taula amb el nom especificat ens avisarà d'aquest fet,
donant-nos la possibilitat d'esborrar la taula anterior i crear la nova o
cancelar.
!!! note "Nota"
    És molt recomanable, com d'altres sentències de manipulació de dades que
    veurem més endavant, executar primer la sentència sense el <b>INTO</b> , per a
    no crear la taula encara. Quan estiguem segurs que el resultat és el que
    desitgem, afegim el INTO, i la taula es crearà a més garanties.


**<u>Exemples</u>**

  1) Crear una còpia de la taula comarques anomenada **COMARQUES_COPIA**.

    SELECT * INTO COMARQUES_COPIA  
      FROM COMARQUES

Per a no "embrutar" la Base de Dades, podem esborrar-la després d'haver vist
la seua creació amb la sentència

    DROP TABLE COMARQUES_COPIA

  2) Crear una taula anomenada **RESUM_COMARQUES** que continga el nom de la comarca, el número de pobles, el total de població i l'altura mitjana

    SELECT nom_c, COUNT(*) AS num_pobles, SUM(poblacio) AS poblacio , SUM(extensio) AS extensio , AVG(altura) AS altura_mitjana INTO RESUM_COMARQUES  
      FROM POBLACIONS  
      GROUP BY nom_c

Igual que en l'anterior, després d'haver vist la seua creació i contingut,
podem esborrar-la amb la sentència

  DROP TABLE RESUM_COMARQUES


## :pencil2: Exercicis

**Ex_49** Crear una taula anomenada **ARTICLE_999x** , on 999 han de ser les 3
últimes xifres del DNI, i x la lletra del teu NIF, que siga una còpia de la
taula ARTICLE, però substituint els valors nuls de **stock** i **stock_min**
per zeros.

**Ex_50** Utilitzar la taula anterior per a traure el stock màxim, el mínim i
la mitjana de stocks. Observeu que si utilitzàrem la taula ARTICLE, els
resultats no serien els mateixos (excepte el màxim), sobretot la mitjana, ja
que els valors nuls no entrarien en els càlculs d'aquesta mitjana.

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

