# 7. La clàusula HAVING

Aquesta clàusula acompanya normalment a la de **GROUP BY** , i servirà pera
poder triar alguns grups que acomplesquen una determinada condició.

Pot anar sense el GROUP BY, però aleshores el seu funcionament és com el
WHERE, i per tant no val la pena. És a dir, en la pràctica sempre que trobem
un HAVING hi haurà també el GROUP BY i servirà per seleccionar alguns grups,
els que acomplesquen la condició del HAVING.

També podríem dir que el HAVING és al GROUP BY, el que el WHERE és al SELECT

**<u>Sintaxi</u>**

    SELECT <columnes>  
      FROM <taules>  
      [GROUP BY <columnes>]  
      HAVING <condició>

Únicament comentarem el cas en què acompanya al GROUP BY. I com hem dit, el
que fa és filtrar els grups: dels grups resultants del GROUP BY, només eixiran
els que acomplesquen la condició.

Aquesta condició contindrà alguna funció d'agregat o contindrà columnes
incloses en el GROUP BY. Fixeu-vos que és lògic, ja que serveix per a triar
grups una vegada fets, i aleshores ja no es podrà anar a un element del grup.

Per exemple, aquesta sentència servirà per traure les comarques on hi ha més
de 20 pobles, i el número que hi ha:

    SELECT nom_c, COUNT(*)  
      FROM POBLACIONS  
      GROUP BY nom_c  
      HAVING COUNT(*) > 20;

**<u>Exemples</u>**

  1) Traure aquelles poblacions que tenen més d'un de Centres Integrats de Formació Professional. La manera de saber que és un Centre Integrat és perquè el seu nom comença per CIPFP. De moment només traurem el codi de la població, i així només ens fa falta la taula INSTITUTS. Més avant aprendrem a agafar les dades de més d'una taula, i aleshores traurem també el nom de la població

    SELECT cod_m, COUNT(*)  
      FROM INSTITUTS  
      WHERE nom LIKE 'CIPFP%'  
      GROUP BY cod_m  
      HAVING COUNT(*) > 1

> El que fem en aquesta sentència és, de la taula INSTITUTS seleccionar
> únicament els Centres Integrats (utilitzant l'operador LIKE per a que
> comencen per CIPFP)i i després agrupar pel codi de municipi. Una vegada fets
> els grups, eliminarem els grups que no acompleixen la condició de HAVING, és
> a dir, els que tenen 0 o 1 Centre Integrat. I d'aquestos grups seleccionats
> traurem el codi del municipi i el número de Centres Integrats (que sempre
> serà igual o major que 2).

  2) Calcular el número d'habitants màxim, el mínim i el número d'habitants mitjà de les poblacions de les comarques amb més de 20 pobles.

    SELECT nom_c , COUNT(cod_m) AS "Número de pobles" , Max(poblacio) AS Màxim , Min(poblacio) AS Mínim , Avg(poblacio) AS Mitjana  
      FROM POBLACIONS  
      GROUP BY nom_c  20;

  3) Traure l'altura mitjana, total de població i població mitjana, d'aquelles comarques que tenen una altura mitjana superior a 800 metres.

    SELECT nom_c , AVG(altura) AS "Altura mitjana" , SUM(poblacio) AS "Total població" , Avg(poblacio) AS "Població mitjana"  
      FROM POBLACIONS  
      GROUP BY nom_c  
      HAVING AVG(altura) > 800;


## :pencil2: Exercicis

**Ex_28** Calcular la mitjana de quantitats demanades d'aquells articles que
s'han demanat més de dues vegades. Observeu que la taula que ens fa falta és
LINIA_FAC, i que la condició (en el HAVING) és sobre el número de vegades que
entra l'article en una linia de factura, però el resultat que s'ha de mostrar
és la mitjana de la quantitat.

**Ex_29** Traure els pobles que tenen entre 3 i 7 clients. Traure només el codi
del poble i aquest número

**Ex_30** Traure les categories que tenen més d'un article "car" (de més de
100 €). Observeu que també ens eixirà la categoria NULL, és a dir, apareixerà
com una categoria aquells articles que no estan catalogats.

**Ex_31** Traure els clients que tenen més d'una factura, amb el número de
factures.

**Ex_32** Modificar l'anterior per a traure els clients que tenen més
d'una factura en el primer trimestre.

**Ex_33** Calcular el total de cada factura d'aquelles factures que
tenen 10 o més línies de factura, sense aplicar descomptes ni IVA (com la
consulta **Ex_26**), i també aplicant el descompte que consta en la línia de
factura (no el descompte de tota la factura). Tindrem el problema que el valor
NULL és especial, i en operar amb qualsevol altre valor donarà NULL. En aquest
cas clarament l'hem de considerar com un descompte 0. Podeu utilitzar una
funció que substitueix els 
HAVING COUNT(cod_m) > valors nuls trobats en el primer paràmetre, pel
segon paràmetre d'aquesta manera: **COALESCE(dte,0)**

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

