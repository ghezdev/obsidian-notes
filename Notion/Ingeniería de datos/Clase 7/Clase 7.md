**SELECT** columnas

**FROM** tablas

**WHERE** filas

**GROUP BY**

**HAVING**

**ORDER BY** columna

  

  

![[/image 23.png|image 23.png]]

![[/image 1 8.png|image 1 8.png]]

  

> [!important] **AVG** calcula el promedio de la suma de un valor dividido las filas de la tabla

  

![[/image 2 8.png|image 2 8.png]]

  

  

### Ejemplo de HAVING y GROUPBY

SELECT codProv, count(*)

FROM clientes

GROUP BY codProv

HAVING count(*) > 3

  

22/04 TP en teams, grupo de 3 a 4