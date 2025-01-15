# 3. Àlies en les columnes

Tenim també la possibilitat de donar noms (_**àlies**_) a les columnes que
apareixeran en la capçalera de les columnes corresponents en el resultat.

**<u>Sintaxi</u>**

    SELECT columna1 [AS àlias1] [ , columna2 [AS àlias2] ]  
      FROM TAULA;

Si volem que en la capçalera apareguen més d'una paraula, les haurem de tancar
amb cometes dobles ( **"** ).

Per exemple:

    SELECT cod_m AS "Codi Municipi" , nom  
      FROM POBLACIONS;
   
És especialment útil la utilització d'àlies quan posem una expressió, en
compte d'una única columna. Si no posem àlies, apareix en la capçalera una
cosa semblant a **?column?**.

    SELECT nom_c || ' (' || provincia || ')' AS " Comarca (provincia)"  
      FROM COMARQUES;

I a banda del seu valor estètic, més avant veurem sentències SQL en les quals
obligatòriament haurem de posar àlies a les columnes que siguen el resultat
d'una expressió.

**<u>Exemples</u>**

  1) Traure de les poblacions, el nom i el número d'habitants (camp poblacio), aquest últim el nom **habitants**.

    SELECT nom, poblacio AS habitants  
      FROM POBLACIONS;

  2) Traure tots els camps de la taula INSTITUTS de forma elegant.

    SELECT codi AS "Codi Institut", nom as Nom, adreca AS Adreça, numero AS
    Número, codpostal AS "Codi Postal", cod_m AS "Codi Municipi"  
      FROM INSTITUTS;

Si volem que totes les capçaleres comencen per majúscula, haurem de posar tots
els àlies entre cometes dobles, encara que només consten d'una paruala

    SELECT codi AS "Codi Institut", nom as "Nom", adreca AS "Adreça", numero AS
    "Número", codpostal AS "Codi Postal", cod_m AS "Codi Municipi"  
      FROM INSTITUTS;


## :pencil2: Exercicis

**Ex_5** Traure el num_f, data i cod_ven de les factures amb les següents
capçaleres respectivament: **Número Factura** , **data** i **Codi Venedor**


**Ex_6** Donar àlias als camps que ho necessiten de la taula ARTICLE.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

