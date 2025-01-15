# 5. Funcions d'agregat

Les **funcions d'agregat**, o funcions de domini agregat, són aquelles que
trauen un resultat a partir dels valors d'un determinat camp en un conjunt de
files. Així tindrem una funció per a **sumar** els valors d'una columna, o
**comptar** -los, o traure la **mitjana** , o el **màxim** , ...

Actuaran sobre un conjunt de files determinat, que en principi suposarem que
és tota la taula (totes les files de la taula). En la següent pregunta, veurem
que el conjunt de files sobre el qual es calcula una funció d'agregat, el
podrem canviar amb la clàusula **GROUP BY**.

**<u>Sintaxi</u>**

  * **COUNT (* | <expressió> )**: compta el número de files; si es posa una columna o expressió, no es comptaran els valors nuls.

  * **SUM ( <expressió> )**: torna la suma de la columna o expressió especificada. Ignora els valors nuls.

  * **AVG ( <expressió> )**: calcula la mitjana aritmètica de la columna o expressió especificada. Ignora els valors nuls.

  * **VAR_SAMP ( <expressió> )**: calcula la variància d'una mostra a partir de la columna o expressió especificada.

  * **STDDEV ( <expressió> )**: desviació típica d'una mostra.

  * **MAX ( <expressió> )**: calcula el màxim.

  * **MIN ( <expressió> )**: calcula el mínim.

Per exemple, si volem saber el nombre d'Instituts:

    SELECT COUNT(*) AS "Nombre d'Instituts"  
      FROM INSTITUTS;


!!! note "Nota"
      És interessant la utilització d'àlias, per a que no apareguen capçaleres com _**count**_
  

**<u>Exemples</u>**

  1) Comptar el nombre total de pobles.

    SELECT Count(*)  
      FROM POBLACIONS;

  2) Comptar el nombre de poblacions de la **Plana Alta**.

    SELECT Count(*)  
      FROM POBLACIONS  
      WHERE nom_c = 'Plana Alta';

  3) Calcular la mitjana d'habitants dels pobles de la **Plana Alta** i **Plana Baixa**.

    SELECT AVG(poblacio)  
      FROM POBLACIONS  
      WHERE nom_c = 'Plana Alta' OR nom_c = 'Plana Baixa'

  4) Calcular la mitjana de densitat de les poblacions. La densitat es calcula com el número d'habitants dividit per l'extensió.

    SELECT AVG(poblacio/extensio)  
      FROM POBLACIONS;

  5) Calcular l'altura màxima i mínima de tots els pobles.

    SELECT MAX(altura), MIN(altura)  
      FROM POBLACIONS


## :pencil2: Exercicis

**Ex_15** Comptar el nombre de **clients** que tenen el **codi postal nul**.

**Ex_16** Comptar el número de vegades que l'article **L76104** entra en les
línies de factura, i el número total d'unitats venudes d'aquest article. Només
us fa falta la taula LINIA_FAC.

**Ex_17** Traure la **mitjana** del **stock** dels articles.

**Ex_18** Modificar l'anterior per a**tenir en compte els valors nuls, com si
foren 0**. Us vindrà bé la funció **COALESCE** que converteix els nuls del
primer paràmetre al valor donat com a segon paràmetre (si és diferent de nul,
deixa igual el valor). Per tant l'heu d'utilitzar d'aquesta manera:
**COALESCE(stock,0)**

**Ex_19** Comptar **quantes factures** té el client **375**  

**Ex_20** Calcular el **descompte màxim** , el **mínim** i el descompte
**mitjà** de les **factures**.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

