# 10. La clàusula LIMIT .. OFFSET

Per mig de la clàusula **LIMIT - OFFSET** podrem fer que no apareguen totes
les files que torna la sentència, sinó unes quantes.

  * **LIMIT número** : especificarem quantes files volem que es tornen
  * **OFFSET número** : especificarem a partir de quina posició volem que es tornen les files

Si no posem la part del OFFSET, apareixeran les primeres, i si especifiquem
OFFSET, se saltaran les primeres, tantes com s'indica en OFFSET. Per a que
realment tinga sentit aquesta clàusula, és conveninet ordenar la informació,
ja que al dir les primeres ja s'està assumint que seran les primeres respecte
algun ordre. Així, per exemple ens podrem plantejar traure coses com les 10
poblacions més altes, o les més habitades.

L'ordre implícit que acabem de comentar s'haurà de fer per mig de la clàusula
ORDER BY. Així, si volem traure els clients més joves haurem d'ordenar per la
data de naixement en ordre descendent, per a després traure els primenrs. Per
tant és molt difícil veure una clàusula LIMIT si no tenim una clàusula ORDER
BY.

!!! note "Nota"
    En el SQL d'Access no existeix la clàusula LIMIT. Per a fer coses similar
    disposa del predicat <b>TOP</b> , que es posa immediatament després del SELECT,
    però sempre traurà les primeres, no té possibilitat d'OFFSET.


**<u>Sintaxi</u>**

    SELECT <columnes>  
      FROM <taules>  
      [LIMIT _n_] [OFFSET _m_]

El número _**n**_ ha de ser un enter, i se seleccionaran únicament les _**n**_
primeres files (les de dalt). En cas de posat OFFSET se saltaran  _**m**_
files. En cas de no posar **LIMIT** , se saltaran _**m** _files i es trauran
totes les altres fins el final.

Per exemple, si volem traure les 10 poblacions més altes, haurem d'agafar les
10 primeres, ordenant per altura en forma descendent:

    SELECT nom , altura  
      FROM POBLACIONS  
      ORDER BY altura DESC  
      LIMIT 10

L'exemple anterior sembla correcte, però no funciona del tot bé perquè amb les
dades que tenim, hi ha 3 poblacions que no tenen altura, i el valor nul el
posa al final de tots els altres valors, en ordre ascendent, i per tant al
principi en ordre descendent.

Ho podem arreglar senzillament saltant les 3 primeres (que són les del nul)

    SELECT nom , altura  
      FROM POBLACIONS  
      ORDER BY altura DESC  
      LIMIT 10 OFFSET 3

Encara que sembla millor llevar les d'altura nula, així no estem obligats a
saber quantes poblacions amb altura nula hi ha

    SELECT nom , altura  
      FROM POBLACIONS  
      WHERE altura IS NOT NULL  
      ORDER BY altura DESC  
      LIMIT 10

Si vulguérem traure totes les poblacions i altures, excepte les que tenen nul,
i sabem que aquestes en són 3, podem posar OFFSET sense LIMIT, per a saltar
les 3 primeres, i traure-les totes fins el final

    SELECT nom , altura  
      FROM POBLACIONS  
      ORDER BY altura DESC  
      OFFSET 3

**<u>Exemples</u>**

  1) Traure les 5 poblacions més poblades

    SELECT nom , poblacio  
      FROM POBLACIONS  
      ORDER BY poblacio DESC  
      LIMIT 5

  2) Traure les 4 comarques amb més pobles.

    SELECT nom_c , COUNT(*)  
      FROM POBLACIONS  
      GROUP BY nom_c  
      ORDER BY 2 DESC  
      LIMIT 4

  3) Traure les 10 poblacions amb més instituts, saltant-nos les 3 primeres.

    SELECT cod_m , COUNT(*)  
      FROM INSTITUTS  
      GROUP BY cod_m  
      ORDER BY 2 DESC  
      LIMIT 10 OFFSET 3


## :pencil2: Exercicis

**Ex_44** Traure tota la informació dels dos articles més cars.

**Ex_45** Traure el codi de les tres ciutats amb més clients

**Ex_46** Traure el venedor que ha venut menys factures  

**Ex_47** Traure les tres factures més cares (sense comptar els descomptes)

**Ex_48** Modificar l'anterior per a traure totes les factures, excepte les 3
més cares.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

