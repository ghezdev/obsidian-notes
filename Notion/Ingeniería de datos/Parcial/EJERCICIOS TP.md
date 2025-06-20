# 1 

***Dada una tabla PERSONAS que contenga la siguiente estructura, seleccione las filas de la tabla tal que los valores del atributo candidato a ser Primary Key estén repetidos más de una vez.***  
***Id (Clave candidata)***  
***Nombre varchar(20)***  
***Apellido varchar(20)***

  

Resolución: 
```sql 
SELECT p1.*
FROM personas p1
JOIN (
	SELECT id
	FROM personas
	GROUP BY id
	HAVING COUNT(id) > 1
) p2
ON p1.id = p2.id
```

  

Explicación:
En esta solucion empleamos una subconsulta. Recordemos que una subconsulta es simplemente una consulta SQL anidada dentro de otra.


En este caso sería la función dentro del JOIN: 

SELECT id

FROM personas

GROUP BY id

HAVING COUNT(id) > 1

  

Selecciona los id dentro de la tabla personas que se encuentran repetidos. 

  

Luego en el metodo JOIN junta las dos tablas (p1 y p2) sobre el atributo id que se encuentra en las dos, devolviendo todas las columnas de la tabla personas de las filas que se encuentren en ambas.
  - - -
# 2

***Realice una sentencia DELETE que borre las filas de la tabla PERSONAS del ejercicio 1 que estén duplicadas dejando sólo una fila con cada valor de la clave candidata.***

  
Resolución:

```sql
WITH duplicados AS (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY id ORDER BY id) AS fila
  FROM personas
)
DELETE FROM duplicados
WHERE fila > 1;
```

Explicación:

Resolvimos este ejercicio usando la palabra clave WITH que crea una tabla temporal cumpliendo la lógica que le pongamos dentro.

En este caso la tabla temporal será parecida a personas pero con una diferencia, se agrupan los id que estén duplicados y se les asigna un número dentro de ese grupo.


Explicacion de las funciones utilizadas:

PARTITION BY id: Agrupa las filas por cada valor de id

ORDER BY id: Define el orden dentro de cada grupo

ROW_NUMBER(): Asigna un número secuencial (1, 2, 3...) a cada fila dentro de cada grupo, es decir si hay un id repetido dos veces, al primero se le asigna 1 y al segundo 2

  

Teniendo la tabla personas con las siguientes filas con id duplicados:  
1, juana, torres

1, tomas, torres

2, juan, silla

  

La tabla temporal nos devolvera la misma tabla pero con una columna fila nueva:

1, juana, torres, 1 (primer elemento con ese id)

1, tomas, torres, 2 (segundo elemento con ese id)

2, juan, silla, 1 (primer elemento con ese id)

  

Luego borramos los elementos que tengan la nueva columna fila con valor mayor a 1  
  

  

  - - -
# 3

***Realizar una consulta que devuelva el monto total comprado por cliente en cada provincia de los fabricantes. Las columnas a mostrar son número de cliente, nombre del cliente, apellido del cliente, provincia_desc (de los fabricantes) y monto total comprado. Ordenar la información por número de cliente en forma ascendente y monto total comprado en forma descendente.***

  

Resolución:

```sql
SELECT c.cliente_num, c.nombre, c.apellido, fact_fdet_prob_frab_prov.provincia_desc, fact_fdet_prob_frab_prov.total
FROM clientes c
JOIN (
	SELECT fact.cliente_num, fdet_prob_frab_prov.total, fdet_prob_frab_prov.provincia_desc
	FROM facturas fact
	JOIN (
		SELECT fdet.factura_num, fdet.producto_cod, SUM(fdet.cantidad * fdet.precio_unit) total, prod_frab_prov.fabricante_cod, prod_frab_prov.provincia_cod, prod_frab_prov.provincia_desc
		FROM facturas_det fdet
		JOIN (
			SELECT p.producto_cod, p.fabricante_cod, f_prov.provincia_cod, f_prov.provincia_desc, p.precio_unit
			FROM productos p
			JOIN (
				SELECT f.fabricante_cod, f.fabricante_nom, f.tiempo_entrega, prov.*
				FROM fabricantes f
				JOIN (
					SELECT *
					FROM provincias
				) prov
				ON f.provincia_cod = prov.provincia_cod
			) f_prov
			ON p.fabricante_cod = f_prov.fabricante_cod
		) prod_frab_prov
		ON fdet.producto_cod = prod_frab_prov.producto_cod
		GROUP BY fdet.factura_num, fdet.producto_cod, prod_frab_prov.fabricante_cod, prod_frab_prov.provincia_cod, prod_frab_prov.provincia_desc
	) fdet_prob_frab_prov
	ON fact.factura_num = fdet_prob_frab_prov.factura_num
) fact_fdet_prob_frab_prov
ON c.cliente_num = fact_fdet_prob_frab_prov.cliente_num
GROUP BY c.cliente_num, c.nombre, c.apellido, fact_fdet_prob_frab_prov.provincia_desc, fact_fdet_prob_frab_prov.total
ORDER BY c.cliente_num ASC, fact_fdet_prob_frab_prov.total DESC
```

  
Explicación:

Para obtener la información que se solicita, debemos realizar JOINS entre las diferentes tablas para obtener la información agrupada en una tabla. Entre alguns JOINS, obtenemos el total que refiere a la cantidad del producto comprado multiplicado por el precio unitario de cada producto. Por último, mostramos los campos solicitados ordenandolos por cliente_num de forma ascendente y total de forma descendente.

  
- - -
# 4

***Sea una tabla VALORES que tiene un campo numérico secuencial Id, realizar una consulta que obtenga el valor del primer espacio libre de ese campo***

  

Resolución:

```sql
SELECT COALESCE(
 (SELECT MIN(V1.id + 1)
  FROM VALORES V1
  LEFT JOIN VALORES V2 ON V1.id + 1 = V2.id
  WHERE V2.Id IS NULL),
 1
) id
```

  

Explicación :

Comparamos cada id con su posible siguiente valor usando un LEFT JOIN consigo mismo. Con la subquery obtenemos el valor más chico de los valores con saltos o huecos entre ids. Si existe un registro, devuelve eso en la columna, si no existe, devuelve 1

- - -
# 5

***Mostrar por cada Producto (producto_cod) las cantidades totales mensuales vendidas (según la fecha de emisión de la factura). No importa si hay meses de diferentes años, se suman como si fueran del mismo año. La información se deberá mostrar en forma tabular como se muestra en la figura, ordenada por código de producto.*** 

  

Resolución:

```sql
WITH ventas_mensuales_por_factura AS (
	SELECT
	fd.producto_cod,
	(CASE WHEN MONTH(f.fecha_emision) = 1 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "1",
	(CASE WHEN MONTH(f.fecha_emision) = 2 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "2",
	(CASE WHEN MONTH(f.fecha_emision) = 3 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "3",
	(CASE WHEN MONTH(f.fecha_emision) = 4 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "4",
	(CASE WHEN MONTH(f.fecha_emision) = 5 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "5",
	(CASE WHEN MONTH(f.fecha_emision) = 6 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "6",
	(CASE WHEN MONTH(f.fecha_emision) = 7 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "7",
	(CASE WHEN MONTH(f.fecha_emision) = 8 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "8",
	(CASE WHEN MONTH(f.fecha_emision) = 9 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "9",
	(CASE WHEN MONTH(f.fecha_emision) = 10 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "10",
	(CASE WHEN MONTH(f.fecha_emision) = 11 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "11",
	(CASE WHEN MONTH(f.fecha_emision) = 12 THEN SUM(fd.cantidad * fd.precio_unit) ELSE 0 END) AS "12"
	FROM facturas_det fd
	JOIN facturas f
	ON fd.factura_num = f.factura_num
	GROUP BY fd.producto_cod, f.fecha_emision
)
SELECT
ventas_mensuales_por_factura.producto_cod,
SUM(ventas_mensuales_por_factura."1") AS "1",
SUM(ventas_mensuales_por_factura."2") AS "2",
SUM(ventas_mensuales_por_factura."3") AS "3",
SUM(ventas_mensuales_por_factura."4") AS "4",
SUM(ventas_mensuales_por_factura."5") AS "5",
SUM(ventas_mensuales_por_factura."6") AS "6",
SUM(ventas_mensuales_por_factura."7") AS "7",
SUM(ventas_mensuales_por_factura."8") AS "8",
SUM(ventas_mensuales_por_factura."9") AS "9",
SUM(ventas_mensuales_por_factura."10") AS "10",
SUM(ventas_mensuales_por_factura."11") AS "11",
SUM(ventas_mensuales_por_factura."12") AS "12"
FROM ventas_mensuales_por_factura
GROUP BY ventas_mensuales_por_factura.producto_cod
ORDER BY ventas_mensuales_por_factura.producto_cod
```


A través de la función MONTH, podemos saber el número de mes que le corresponde a la fecha de emisión, comparandolo en un case, decidímos que valor va a tener esa columna. Por último, ahora del WITH, hacemos la suma de todas las columnas.

  
- - -
# 6

***Realizar UN query que asegure que dos tablas con la misma estructura tengan exactamente la misma cantidad de filas y exactamente los mismos datos en cada columna. Es decir, que las tablas sean exactamente iguales.*** 

  

Resolución:

```sql
SELECT
CASE WHEN
NOT EXISTS (
    SELECT *
    FROM productosA
    EXCEPT
    SELECT *
    FROM productosB
    )
AND NOT EXISTS (
    SELECT *
    FROM productosB
    EXCEPT
    SELECT *
    FROM productosA
    )
AND
(SELECT COUNT(*) FROM productosA) = (SELECT COUNT(*) FROM productosB)
THEN 'Sí'
ELSE 'No'
END AS tablas_iguales
```

  

Primero comparamos si las dos tablas devuelven registros a través de un except, si devuelven, es porque tienen datos distintos, luego, comparamos sus cantidades. En este ejemplo se usa la misma tabla, pero modificando la tabla productos de la segunda sentencia SELECT y SELECT COUNT(*) FROM a otra tabla se podría verificar si ámbas tienen los mismos datos y misma cantidad de filas.

- - -
# 7

Consigna:

***Realizar una consulta que tenga el siguiente formato (los datos son solo de ejemplo) que muestre para cada cliente que tenga referente los distintos niveles de referentes que posee. Cada referente se deberá mostrar en una columna diferente y debe mostrar hasta el tercer nivel si es que existe.*** 

  

Resolución:

```sql
WITH REF2 AS (
	SELECT d.cliente_num, d.cliente_ref, f.cliente_ref AS REF_2
	FROM clientes d
	LEFT JOIN clientes f
	ON d.cliente_ref = f.cliente_num
),
REF3 AS (
	SELECT R.cliente_num, R.cliente_ref, R.REF_2, cr3.cliente_ref AS REF_3
	FROM REF2 R
	LEFT JOIN clientes cr3
	ON R.REF_2 = cr3.cliente_num
)
SELECT * from REF3
```


Explicación :

primero creamos un CTE llamado REF2 que va a tener las columnas cliente_num, cliente ref, REF_2(esta columna es el cliente ref de cliente ref), hacemos un join de clientes con clientes donde compara que el cliente_ref = a cliente_num  donde comparamos el cliente ref de la primera tabla de clientes con el cliente num de la segunda tabla de clientes(el resultado de ese join es cliente_num,cliente_ref, cliente_num de la segunda tabla que es igual a ref de la primera, y cliente_ref de la segunda tabla que es el dato que queremos).

de eso solo seleccionamos cliente_num de la primera tabla, cliente_ref de la primera tabla, y cliente ref de la segunda tabla y lo nombramos REF_2. Formando asi REF2.

Creamos una segunda CTE llamada REF3 que es casi el mismo proceso que REF2 solo que las tablas que joineamos son REF2 y Clientes, donde comparamos REF_2 sea igual a cliente_num de clientes, despues de eso seleccionamos los valores que pertenecian REF2 con cliente_ref de clientes ahora llamado REF_3 asi formamos REF3.

al final seleccionamos REF3

- - -
# 8

Consigna:

***Dado el siguiente modelo, realice una consulta que permita averiguar en qué equipo juega o jugó una jugadora en una fecha determinada.*** 
***La columna FechaDesde es la fecha de alta de la jugadora en un club determinado. La jugadora estará en un club hasta la fechaDesde del registro siguiente existente en la tabla. Si no hay una fila con fecha posterior de la jugadora se asume que aún sigue en ese equipo***

  

Resolución:

```sql
CREATE FUNCTION ObtenerClub(@LegajoJugadora INT, @FechaDesdeI DATE) RETURNS INT A
BEGIN
	DECLARE @CodigoClub INT;
	SELECT TOP 1 @CodigoClub = pc.CodigoClub FROM Jugadoras j
	JOIN (
		SELECT p.Legajo, p.fechaDesde, p.CodigoClub, c.Nombre
		FROM Pases p
		JOIN Clubes c
		ON p.CodigoClub = c.Codigo
	) pc
	ON j.Legajo = pc.Legajo
	WHERE DATEDIFF(DAY, pc.fechaDesde, @FechaDesdeI) >= 0 AND j.Legajo = @LegajoJugadora
	ORDER BY pc.fechaDesde DESC
	RETURN @CodigoClub;
END;

SELECT dbo.ObtenerClub(103, '2023-06-05');
```

ya que el ejercicio decia que daba  una jugadora(suposimos el Legajo) y una Fecha lo que hicimos fue crear una funcion que retorna el codigo del club que jugo la jugadora en determinada fecha. donde se una subquery que hace un JOIN entre PASES y CLUBES y la llama PC a ese tabla

- - -
# 9

Consigna:

***Realizar UN query sin utilizar subqueries, que muestre las cantidades de cada producto vendidas en cada provincia. La provincia se refiere a la del Fabricante. Mostrar código de provincia, código de producto, cantidad vendida del producto en la provincia, cantidad total de productos vendidos en la provincia y porcentaje del total vendido en la provincia respecto a la cantidad total de productos vendidos en el país. Mostrar la información ordenada por provincia en forma ascendente y cantidad total del producto vendido en forma descendente.*** 

  

Resolución:

```sql
WITH ventas_x_prov AS (
	SELECT fabr.provincia_cod, fd.producto_cod, SUM(fd.cantidad) cant_prod_x_prov
	FROM facturas f
	JOIN facturas_det fd
	ON f.factura_num = fd.factura_num
	JOIN productos p
	ON fd.producto_cod = p.producto_cod
	JOIN fabricantes fabr
	ON p.fabricante_cod = fabr.fabricante_cod
	GROUP BY fd.producto_cod, fabr.provincia_cod
),
ventas_totales_x_prov AS (
	SELECT vxp.provincia_cod, SUM(vxp.cant_prod_x_prov) total_cant_prod_x_prov
	FROM ventas_x_prov vxp
	GROUP BY vxp.provincia_cod
),
ventas_totales AS (
	SELECT SUM(vtxp.total_cant_prod_x_prov) ventas
	FROM ventas_totales_x_prov vtxp
)
SELECT
vtxp.provincia_cod AS provincia,
vxp.producto_cod AS producto,
vxp.cant_prod_x_prov AS cant_producto,
vtxp.total_cant_prod_x_prov AS cant_provincia,
ROUND(100.0 * vtxp.total_cant_prod_x_prov / vt.ventas, 2) AS prov_pais
FROM ventas_totales_x_prov vtxp
JOIN ventas_x_prov vxp
ON vtxp.provincia_cod = vxp.provincia_cod
CROSS JOIN ventas_totales vt
ORDER BY vtxp.provincia_cod ASC, vxp.cant_prod_x_prov DESC
```

  

Debido a la limitación de no utilizar subqueries, la otra forma que se nos ocurrió de llevar a cabo el enunciado fue utilizando la cláusula WITH, obteniendo tablas temporales con los datos necesarios para luego al manipularlos, así obtener la query que se solicitó.  
‘ventas_prod_x_prov’ corresponde a los productos vendidos por provincia.

‘ventas_totales_x_prov’ corresponde a las ventas por provincia

‘ventas_totales’ corresponde a las ventas totales que hubieron.

Juntando toda la información logramos obtener la tabla de ejemplo del enunciado.

  - - -
# 10

Consigna:

***Dada el siguiente modelo, desarrolle e implemente un mecanismo que cuando se dé de alta un nuevo pase de una jugadora, controle y evite que la jugadora esté fichada para dos equipos al mismo tiempo (inclusive al mismo). Es decir, que no permita que dos filas en la tabla Pases se superpongan dentro de un periodo para una misma jugadora.***

  

Resolución:

```sql
CREATE TRIGGER ValidacionPases
ON Pases
INSTEAD OF INSERT AS
BEGIN
IF EXISTS (
       SELECT 1
       FROM INSERTED i
       JOIN Pases p ON p.Legajo = i.Legajo
       WHERE p.FechaHasta >= i.FechaDesde OR p.FechaHasta IS NULL
   )
   BEGIN
       THROW 50000, 'Existen jugadoras ingresadas que actualmente ya estan fichadas en otro equipo', 1;
   END
   INSERT INTO Pases (Legajo, FechaDesde, FechaHasta, CodigoClub)
   SELECT Legajo, FechaDesde, FechaHasta, CodigoClub
   FROM INSERTED;
END
```

  

Con este trigger logramos hacer que cuando el usuario intente realizar un INSERT de la tabla Pases, se ejecute este trigger que valida si la jugadora a insertar, su fecha de ingreso es menor o igual a la fecha de egreso de otro equipo, si es así, entonces las fechas de la nueva jugadora son incorrectos, es decir, no puede la misma jugadora jugar para dos equipos en la misma fecha, o en su defecto, mantener dos registros con fechas que se solapen para la misma jugadora.

Informamos al usuario el motivo del cual no se realizó el INSERT y en caso de que no haya solapamiento, se realiza el INSERT normalmente.
