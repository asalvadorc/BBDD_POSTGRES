# 2. Consulta bàsica


El mínim que s'ha d'indicar en una instrucció SELECT és les columnes que volem
i la seua procedència, que pot ser una o més d'una taula.

**<u>Sintaxi</u>**

    SELECT <columnes>
      FROM <clàusula>

Opcionalment la sentència pot acabar en **punt i coma**. En **psql** és
obligatori acabar en punt i coma, ja que és la manera que té de saber que
acaba la instrucció (una instrucció pot ocupar més d'una línia)

I una altra consideració important és que en PostgreSQL els noms dels objectes
(taules, columnes, ...) poden constar de més d'una paraula. Si el nom només
consta d'una paraula es pot posar sense més problemes, però si consta de més
d'una paraula (amb espis en blanc pel mig) o té algun caràcter especial, o
coincideix amb alguna paraula reservada (per exemple _**any**_), haurà d'anar
entre **cometes dobles**. Per a estalviar problemes, és una bona pràctica fer
els noms sempre d'una paraula (si es volen posar dues, unides pel guió baix).

En **<columnes>** podrem posar (separades per **comes**):

  * **noms de les columnes** que volem; si hi ha confusió entre noms de camps de distintes taules, haurem de posar **Taula.columna**.

  * `*` : indica totes les columnes.

  * **Taula.*** : indica totes les columnes de la taula.

  * **Funcions** (veure apartat  _Operadors i Funcions de Postgres_)

  * **Constants** : son valors que posem directament. Els tipus de constants són:

    * **Numèriques** : es posen tal qual, amb punt decimal (no pot anar coma decimal, perquè serveix per a separar les columnes)
    * **Alfaumèriques** : es posen entre **cometes simples**
    * Per a altres tipus (com per exemple data-hora), posem la constant entre cometes simples, i PostgreSQL farà la conversió
  * **Expressions** que utilitzen operadors per a combinar columnes, funcions, constants numèriques o alfanumèriques, ...

En la **<clàusula>** del **FROM** posarem la taula o les taules (separades
per comes) d'on venen les dades.

Així el següent exemple trau tota la informació de la taula COMARQUES, és a
dir totes les files i totes les columnes:

    SELECT * FROM COMARQUES;

Mentre que la següent només trau el nom:

    SELECT nom_c FROM COMARQUES;

En el següent exemple es trau el nom de cada població, els habitants,
l'extensió i la densitat de població (habitants partit per extensió):

    SELECT nom , poblacio , extensio , poblacio/extensio FROM POBLACIONS;

I en aquest traem el nom de cada poble, l'altura i la mitat de la seua altura
(cosa un poc absurda però que serveix per a remarcar que si posem una constant
numèrica, hem de posar el **punt decimal** , no la coma decimal, ja que la
coma serveix per a separar els camps) :

    SELECT nom , altura , altura * 0.5 FROM POBLACIONS;

**<u>Exemples</u>**

  1) Traure tota la informació de la taula POBLACIONS.

    SELECT * FROM POBLACIONS;

  2) Traure el nom i l'altura de totes les poblacions.

    SELECT nom, altura  
      FROM POBLACIONS;

  3) Traure el nom de les poblacions, el número d'habitants, i aquest número incrementat en un 5%.

    SELECT nom, poblacio, poblacio * 1.05  
      FROM POBLACIONS;

Observa com hem d'utilitzar el punt decimal i no la coma decimal, ja que la
coma serveix per a separar els camps de la consulta SQL

  4) Traure nom, latitud i els graus de la latitud de totes les poblacions. Per a traure els graus de la latitud traurem els caràcters de l'esquerra, fins el primer el caràcter º.

    SELECT nom, latitud, SUBSTR(latitud,1,STRPOS(latitud,'º')-1)  
      FROM POBLACIONS;

## :pencil2: Exercicis

En la BD **factura** , connectant com a usuari **factura_alu** :

> **Ex_1** Traure tota la informació dels pobles.
>
> **Ex_2** Traure el codi postal, el nom i l'adreça, per aquest ordre, de tots
> els venedors.

> **Ex_3** Traure el codi d'article, la descripció, preu i preu incrementat en
> un 5%, de tots els articles.

> **Ex_4** Traure la informació dels clients amb el següent format (ha d'anar
> tot en una columna):

> > **Damborenea Corbato, Alicia. CALLE MADRID, 83 (12425)**
>

>> Fixeu-vos que està tot en una columna, i per tant haureu de concatenar de
la forma adequada. Fixeu-vos també que en en el nom només les inicials estan
en majúscules

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

