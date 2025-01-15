# 1. La consulta SELECT

Com el mateix nom indica SQL (_Structured Query Language_), la consulta o
interrogació de la Base de Dades és l'ànima del SQL. I la instrucció que ens
ho permet és **SELECT**.

És una instrucció molt flexible i de molta potència, que permet consultar
dades d'una o més taules, filtrar per files i/o columnes, ordenar el resultat,
agrupar les dades (comptant o sumant alguna columna), ... Fins i tot permet
crear taules noves que serien el resultat d'una consulta d'altres taules.

Veurem a continuació la sintaxi general de la instrucció, i posteriorment
cadascuna de les clàusules:

**<u>Sintaxi</u>**

    SELECT [DISTINCT] <columnes>  
    [ INTO <clàusula> ]  
    FROM <clàusula>  
    [ WHERE <clàusula> ]  
    [ GROUP BY <clàusula> ]  
    [ HAVING <clàusula> ]  
    [ ORDER BY <clàusula> ]  
    [ LIMIT num1 OFFSET num2 ]

Com veieu, les úniques clàusules obligatòries són la del **SELECT** (on es diu les columnes que volem que isquen com a resultat) i la del **FROM** (on es diu d'on venen les dades).

!!! note "Nota"
    En PostgreSQL no es distingeix entre majúscules i minúscules. Millor dit,
    PostgreSQL passa de majúscules a minúscules tots els noms de taula o de camp o
    del que siga, excepte si van entre cometes dobles, que aleshores es respecten
    mayúscules i minúscules. Com a qüestió d'estil, jo no pose mai entre cometes els
    noms de taules i camps. I per a una millor lectura, intentaré posar sempre els
    noms de taula en majúscules, i els noms de camp en minúscules. També posaré en
    majúscules les clàusules de sentències SQL (SELECT , FROM , WHERE , ...). Però
    recordeu que és per a una millor lectura. Podria anar tot en minúscules
    perfectament.



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

