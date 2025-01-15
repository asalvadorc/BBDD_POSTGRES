# 4 Consultes d'operacions de conjunts

Agruparem en aquest apartat les consultes que tracten conjunts de files per a
fer operacions d'algebra de conjunts: **unió** , **intersecció** i
**diferència** de conjunts

Totes aquestes consultes ajunten els resultats de dues o més consultes.

## 4.1 Unió

**<u>Sintaxi</u>**


    [TABLE] consulta1  
    UNION [ALL]  
    [TABLE] consulta2 ...

Cadascuna de les consultes pot ser una taula (posant la paraula **TABLE**
davant) o el nom d'una consulta ja guardada, encara que el més habitual serà
posar directament la **sentència SQL**.

Els requisits són que les dues (o més) consultes tornen el mateix nombre de
camps, i que siguen sinó del mateix tipus, sí de tipus compatibles

Igual que en la unió de conjunts, el resultat seran totes les files de les
dues (o més) consultes individuals, però sense repetir files, és a dir, si de
les dues consultes s'obtenen files iguals, aquestes només eixiran una vegada.
L'anterior es pot evitar si posem el predicat ALL, i aleshores sí que eixiran
les files repetides.

Els noms dels camps vindran donats per la primera consulta.

Si volem ordenar per algun camp, ho haurem de posar al final de l'última
consulta, però referint-se en tot cas als camps de la primera consulta (ho
podem evitar posant el número d'ordre en el ORDER BY)

**<u>Exemples</u>**

  1) Volem veure en un únic resultat tant el nom de les comarques com el nom de les poblacions, sempre amb el nom de la província al costat

    SELECT nom_c, provincia  
      FROM COMARQUES  
    UNION  
    SELECT nom, provincia  
      FROM COMARQUES INNER JOIN POBLACIONS USING (nom_c)  
    ORDER BY nom_c;

Com a curiositat, eixiran 575 files, però si posàrem UNION ALL ens eixirien
576. Això és perquè la comarca de la ciutat de València es diu València i està
a la província de València. Per tant és una fila que apareixerà tant en la
primera com en la segona consulta. Si fem UNION no es repetirà, però si fem
UNION ALL sí que es repetirà.

## 4.2 Intersecció

És identica a la unió, però posant la paraula **INTERSECT** , i servirà per a
traure únicament les files que estan en les dues consultes.



**<u>Sintaxi</u>**

    [TABLE] consulta1  
    INTERSECT [ALL]  
    [TABLE] consulta2 ...

Igual que abans, cadascuna de les consultes pot ser una taula (posant la
paraula **TABLE** davant), i tenim el requisit que les dues (o més) consultes
tornen el mateix nombre de camps, i de tipus compatibles.

En principi no eixiran files repetides, a no ser que posem **ALL**

**Exemple**

  1) Com que en l'exemple de la unió havíem vist que la fila València València eixia en les 2 consultes, anem a comprovar que apareix en la intersecció:

    SELECT nom_c, provincia  
      FROM COMARQUES  
    INTERSECT  
    SELECT nom, provincia  
      FROM COMARQUES INNER JOIN POBLACIONS USING (nom_c)  
    ORDER BY nom_c;

## 4.3 Diferència

És identica a les anteriors, però posant la paraula **EXCEPT** , i servirà per
a traure les files que estan en la primera consulta però que no estan en la
segona.

**<u>Sintaxi</u>**

    [TABLE] consulta1  
    EXCEPT [ALL]  
    [TABLE] consulta2 ...

Igual que abans, cadascuna de les consultes pot ser una taula (posant la
paraula **TABLE** davant), i tenim el requisit que les dues (o més) consultes
tornen el mateix nombre de camps, i de tipus compatibles.

En principi no eixiran files repetides, a no ser que posem **ALL**

**<u>Exemple</u>**

  1) Aprofitem el mateix exemple d'abans per a comprovar que amb EXCEPT no eixirà la comarca València, ja que hi ha una fila idèntica en la segona consulta:

    SELECT nom_c, provincia  
      FROM COMARQUES  
    EXCEPT  
    SELECT nom, provincia  
      FROM COMARQUES INNER JOIN POBLACIONS USING (nom_c)  
    ORDER BY nom_c;

## :pencil2: Exercicis

**Ex_75** Traure el nom de tots els clients i venedors implicats en alguna
venda del primer trimestre de 2015.

**Ex_76a** Traure per mig de sentències d'operacions de conjunts els pobles on
tenim algun venedor o algun client. No volem resultats repetits, i ho volem
ordenat pel nom del poble.

**Ex_76b** Modificar l'anterior per a traure els pobles on tenim al mateix
temps venedors i clients

**Ex_76c** Modificar l'anterior per a traure els pobles on tenim venedors però
no tenim clients

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
SenseObraDerivada 2.5](http://creativecommons.org/licenses/by-nc-nd/2.5/)

