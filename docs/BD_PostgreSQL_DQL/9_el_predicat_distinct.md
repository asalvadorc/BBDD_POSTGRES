# 9. El predicat DISTINCT

Per defecte, si no especifiquem el contrari, eixiran _totes_ les files de la
taula o taules que acomplesquen les condicions. Així, per exemple, si de la
taula d'instituts volguérem treure únicament el codi de la població, ens
eixiria per exemple 12040 (el codi de Castelló) en tantes files com instituts
de Castelló tinguem (concretament 14). És el mateix resultat que si haguérem
posat el predicat **ALL** davant de les columnes, ja que aquest és el predicat
per defecte:

    SELECT ALL cod_m  
      FROM INSTITUTS

Aquest resultat no és el correcte, si volem consultes com "Poblacions on hi ha
instituts". Seria millor si isquera 12040 només una vegada. Açò ho
aconseguirem amb el predicat DISTINCT.

En definitiva el que farà el predicat DISTINCT serà traure les files diferents
del resultat que demanem. Si només demanem un camp, traurà els valors
diferents d'aquest camp. Si demanem més d'un camp, traurà els valors diferents
per al conjunt dels camps (és a dir les files diferents, que en un camp poden
coincidir, però no en el conjunt de tots els camps)

**<u>Sintaxi</u>**

    SELECT DISTINCT <columnes >  
      FROM <taules>

Així, en l'exemple anterior:

    SELECT DISTINCT cod_m  
      FROM INSTITUTS

Hi ha una variant del DISTINCT que suporta PostgreSQL, però que no suporten
altres SGBD més senzills, com Access o LibreOffice Base. És posar el DISTINCT
dins d'una funció d'agregat, com per exemple COUNT. El resultat és que
comptarà (o la funció implicada: sumarà calcularà la mitjana, ...) els valors
diferents del camp que vaja a continuació.

Així per exemple, si volem comptar en quantes poblacions diferents tenim
instituts, la consulta és tan senzilla com aquesta:

    SELECT COUNT(DISTINCT cod_m)  
      FROM INSTITUTS

**<u>Exemples</u>**

  1) Traure les diferents provincies.

    SELECT DISTINCT provincia  
      FROM COMARQUES

  2) Traure els distints districtes (codis postals) de Castelló (codi de municipi 12040) on hi ha instituts

    SELECT DISTINCT codpostal  
      FROM INSTITUTS  
      WHERE cod_m=12040

  3) Traure les distintes comarques i llengües que es parlen en elles

    SELECT DISTINCT nom_c , llengua  
      FROM POBLACIONS  
      ORDER BY 1


## :pencil2: Exercicis

**Ex_39** Traure els venedors que han venut alguna cosa el mes de gener de
2015.

**Ex_40** Traure els diferents tipus d'IVA que s'han aplicat a les factures de
cada venedor, també durant el mes de gener de 2015

**Ex_41** Traure els diferents caps de venedors (eviteu que aparega el valor
nul)

**Ex_42** Traure els diferents descomptes que s'han aplicat als articles, el
codi dels quals comença per **SAT**. Traure tant el codi d'article com el
descompte.

**43** Comptar en quantes poblacions tenim clients

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

