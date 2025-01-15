# 4. La clàusula WHERE

Ens servirà per establir filtres. Només eixiran les files que satisfacen la
condició del filtre.

**<u>Sintaxi</u>**


    SELECT <columnes>  
      FROM <taules>  
      WHERE <condició>;

La condició podrà ser una o més d'una, unides en aquest cas pels operadors
lògics **AND** , **OR** i **NOT**. Cada condició serà una comparació entre
expressions, on poden entrar columnes, constants, paràmetres, funcions vàlides
de PostgreSQL, ... unides per operadors aritmètics. Els operadors que es poden
utilitzar per a fer les comparacions són:

![](where.png)
<!--
  * **<  <=    =   >=   >  <>  (!=)** (distint)

  * **BETWEEN** _valor1_**AND** _valor2_ (els valors compresos entre valor1 i valor2)

  * **IN** (_llista_de_valors_) si el valor amb què es compara està en la llista de valors (entre parèntesis i valors separats per comes)

  * També podem utilitzar **LIKE** en la condició. En els exemples 4, 7 i 8 es veu la seua utilització. L'operador LIKE s'utilitza junt amb els caràcters "**comodí** ": 
  * **%** (equival a 0 o més caràcters, els que siga)
  * **_** (1 i només un caràcter, això sí, el que siga).

  * **IS [NOT]** és un operador especial per a comparar amb el valor nul (**NULL**).
-->
Recordem per una altra banda com s'escriuen les constants:

  * les constants **numèriques** van tal qual, sense cometes ni res (amb el **punt** decimal, i no coma decimal)

  * les constants **alfanumèriques** (de text) van entre cometes simples

  * les constants de data van entre cometes simples, i PostgreSQL ja farà la conversió

  * per últim el valur nul s'escriu **NULL**

**<u>Exemples</u>**

1) Traure les comarques de la província de Castelló

    SELECT *  
      FROM COMARQUES  
      WHERE provincia = 'Castelló';

2) Traure totes les poblacions que tenen de llengua el valencià.

    SELECT *  
      FROM POBLACIONS  
      WHERE llengua = 'V';

3) Traure les poblacions de la comarca de la Plana Alta de més de 300 metres d'altura

    SELECT *  
      FROM POBLACIONS  
      WHERE nom_c = 'Plana Alta' AND altura > 300;

4) Traure els instituts dels codis postals 12001, 12002 o 12003)

    SELECT *  
      FROM INSTITUTS  
      WHERE codpostal=12001 OR codpostal=12002 OR codpostal=12003;


    SELECT *  
      FROM INSTITUTS  
      WHERE codpostal >= 12001 AND codpostal <= 12003;


    SELECT *  
      FROM INSTITUTS  
      WHERE codpostal BETWEEN 12001 AND 12003;


    SELECT *  
      FROM INSTITUTS  
      WHERE codpostal IN (12001,12002,12003);

5) Traure els pobles de la comarca **Plana d'Utiel** (Tenim la dificultat de la cometa simple, que ens serveix sempre per a delimitar una constant alfanumèrica) La manera de solucionar-ho és posar-la dues vegades

    SELECT *  
      FROM POBLACIONS  
      WHERE nom_c = 'Plana d''Utiel';

6) Traure nom i província dels pobles que comencen per **G** (el primer cognom)

    SELECT nom, nom_c  
      FROM POBLACIONS  
      WHERE nom LIKE 'G%';

7) Traure les poblacions que estan a 40º 1' (i els segons que siguen) de latitud nord

    SELECT *  
      FROM POBLACIONS  
      WHERE latitud LIKE '40º01____N';

Hem posat els 40º i 1 minut. A continuació hem posat exactament 4 caràcters,
els que siga. Hem posat 4, que serien la cometa que assenyala els minuts, les
2 xifres dels segons i la doble cometa que assenyala els segons. Observeu com
la cometa simple és problemàtica, ja que és la que serveix per a delimitar la
constant alfanumèrica. Si volem posar-la, en la constant l'haurem de doblar
(l'haurem de posar 2 vegades seguides)

    SELECT *  
      FROM POBLACIONS  
      WHERE latitud LIKE '40º01''__"N';

8) Traure totes les poblacions, el nom de les quals només consta d'una paraula (no tindran espais en blanc).

    SELECT *  
      FROM POBLACIONS  
      WHERE nom NOT LIKE '% %';

9) Traure els instituts que no tenen introduït el numero del carrer.

    SELECT *  
      FROM INSTITUTS  
      WHERE numero IS NULL;


## :pencil2: Exercicis

**Ex_7** Traure els **clients** de la **ciutat** amb codi **12309**.

**Ex_8** Traure totes les **factures** del mes de **març** de **2015**.

**Ex_9** Traure tots els articles de la **categoria** **BjcOlimpia** amb un
**stock** entre**2** i **7** unitats.

**Ex_10** Traure tots els **clients** que **no** tenen introduït el **codi
postal**.**  
**

**Ex_11** Traure tots els **articles** amb el **stock** introduït però que
**no** tenen introduït el **stock mínim**.

**Ex_12** Traure tots els **clients** , el**primer cognom** dels quals és
**VILLALONGA**.

**Ex_13.a** Modificar l'anterior per a traure tots els que són **VILLALONGA**
de **primer** o de **segon** cognom.  
**Ex_13.b** Modificar l'anterior per a traure tots els que **no** són
**VILLALONGA** ni de primer ni de segon cognom.

**Ex_14** Traure els **articles** "**Pulsador** " (la descripció conté aquesta
paraula), el **preu** dels quals oscila entre**2 i 4 €** i dels quals tenim un
**stock** estrictament **major** que el **stock mínim**.**  
**


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

