# 8. La clàusula ORDER BY

Ordena les files del resultat respecte l'ordre especificat

**<u>Sintaxi</u>**

    SELECT <columnes>  
      FROM <taules>  
      ORDER BY camp1 [ASC | DESC] { , camp2 [ASC | DESC] }

Ací tenim un exemple:

    SELECT nom_c, provincia  
      FROM COMARQUES  
      ORDER BY nom_c

S'ordenaran les files pel camp, en l'ordre marcat: ascendent o descendent (per
defecte, ascendent). Si hi haguera un segon camp d'ordenació, aquest entraria
en joc en cas de valors iguals del primer. Aquest segon podrà ser en ordre
ascendent o descendent, independentment de l'ordre del primer camp.

    SELECT nom_c, provincia  
      FROM COMARQUES  
      ORDER BY provincia DESC, nom_c

Es podrà ordenar per qualsevol camp de la taula, estiga indexada per aquest
camp o no. L'avantatge d'estar indexada respecte a un camp és la rapidesa en
l'ordenació. Així, si tenim una taula gran i ordenem per un determinat camp,
es perdrà temps en aquesta ordenació. Si contínuament estem ordenant per
aquest camp, perdrem aquest temps moltes vegades. Aleshores seria convenient
crear un índex. Però hem de recordar que la creació d'un índex ocupa espai.
Per tant no és bona solució indexar per tots els camps. Únicament, en tot cas,
per aquells que més s'ordene. Veurem la creació d'índex en la tercera part
d'aquest tema.

I es pot especificar en l'ordenació, una expressió que agafe un o més d'un
camp amb operadors i funcions. Es pot posar un camp o una expressió que no
estiga en la llista de camps o expressions que es volen visualitzar (al costat
del SELECT), encara que normalment sí que ho visualitzarem, per a poder
comprovar que realment està ordenat pel que s'ha especificat. Per exemple, si
volem ordenar per la densitat d'habitants de les poblacions, que es calcula
dividint el número d'habitants per l'extensió:

    SELECT nom, poblacio, extensio  
      FROM POBLACIONS  
      ORDER BY poblacio/extensio DESC

> Observeu que estem ordenant per un camp (**poblacio / extensio**) que no
> estem visualitzant, encara que seria molt més il·lustratiu mostrar-lo

Opcionalment, en el moment d'especificar el camp o l'expressió per la qual
volem ordenar, si aquesta apareix en la llista de columnes a visualitzar,
podrem posar senzillament el número d'ordre de la columna. Així, per exemple,
podem fer el següent:

    SELECT nom, poblacio, extensio, poblacio/extensio  
      FROM POBLACIONS  
      ORDER BY 4 DESC

> On estem indicant que s'ordene de forma descendent per la quarta columna que
> va a visualitzar-se, és a dir, per **oblacio / extensio**

Hem d'observar que la clàusula ORDER BY és l'última, i que en cas d'haver
clàusula GROUP BY, s'intentarà ordenar després d'haver agrupat. Per tant en
cas de que la sentència continga un GROUP BY o s'haja utilitzat alguna funció
d'agregat (que implica fer grups), només podrem posar en el ORDER BY camps que
estiguen en el GROUP BY o que formen part d'una funció d'agregat. El raonament
és el mateix que el fet en la clàusula GROUP BY o HAVING i l'error en cas de
no respectar açò seria el matiex que el vist en aquell apartat.

**<u>Exemples</u>**

  1) Traure tota la informació de les poblacions ordenades pel nom de la població.

    SELECT *  
      FROM POBLACIONS  
      ORDER BY nom

  2) Traure tota la informació de les poblacions, ordenades pel nom de la comarca, i dins d'aquesta per l'altura (de forma descendent).

    SELECT *  
      FROM POBLACIONS  
      ORDER BY nom_c, altura DESC

  3) Traure les comarques amb el número de pobles i total d'habitants, d'aquelles que tenen més de 10 pobles, ordenades pel número de pobles, i dins d'aquest pel total de població de forma descendent.


    SELECT nom_c, COUNT(*), SUM(poblacio)  
      FROM POBLACIONS  
      GROUP BY nom_c  
      HAVING COUNT(*) > 10  
      ORDER BY COUNT(*) , SUM(poblacio) DESC




## :pencil2: Exercicis

**Ex_34** Traure tots els clients ordenats per codi de població, i dins
d'aquestos per codi postal.

**Ex_35** Traure tots els articles ordenats per la categoria, dins d'aquest pel
stock, i dins d'aquest per preu (de forma descendent)

**Ex_36** Traure els resultats de la consulta **Ex_33** ordenats pel total de la
factura quan ja s'ha aplicat el descompte, de forma descendent.

**Ex_37** Traure tots els articles ordenats per la diferència entre el stock i
el stock mínim de forma descendent. Com que en moltes ocasions el stock o el
stock mínim és nul, hem de considerar en aquestos casos com 0. Per tant hem de
tornar a utilitzar la funció **COALESCE(stock,0)** (i també per al stock
mínim).

**Ex_38** Traure els codis de venedor amb el número de factures venudes en el
segon semestre de 2015, ordenades per aquest número de forma descendent

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

