
# 1 - Dada una tabla PERSONAS que contenga la siguiente estructura, seleccione las filas de la tabla tal que los valores del atributo candidato a ser Primary Key estén repetidos más de una vez.  

**Estructura:**

**Id (Clave candidata)  
Nombre varchar(20)  
Apellido varchar(20)**


## Explicación

```sql
SELECT id
FROM personas
GROUP BY id
HAVING COUNT(id) > 1
```

Seleccionamos el Id de la tabla PERSONAS, agrupamos por Id para que en caso de que haya repetidos, aparezca una sola vez y luego filtramos por aquellos Id cuya cantidad de veces repetidas sea mayor a 1. Si es 1, ese Id no se repite.

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

A partir de esta tabla hecha a través de una subquery el cual llamamos p2, la combinamos con la tabla original de PERSONAS, el cual le pusimos el alias p1, a través de los Id. Esto para poder obtener el resto de los atributos de la tabla PERSONAS


> [!NOTE] Diferencia entre WHERE y HAVING
> `WHERE` filtra filas individuales antes de la agrupación, mientras que `HAVING` filtra grupos después de la agrupación y la agregación. `WHERE` se usa para condiciones que involucran columnas individuales de la tabla, mientras que `HAVING` se utiliza para condiciones que involucran funciones de agregación (como `SUM()`, `AVG()`, `COUNT()`) sobre los grupos.


# 2 - Realice una sentencia DELETE que borre las filas de la tabla PERSONAS del ejercicio 1 que estén duplicadas dejando sólo una fila con cada valor de la clave candidata.

```sql
ROW_NUMBER() OVER (PARTITION BY id ORDER BY id) AS fila
```

Enumeramos cada Id repetido dentro de la tabla PERSONAS, esto se hace gracias a que, a través del PARTITION BY le decimos que por cada Id repetido, haga un nuevo grupo, estos grupos van a estar ordenados por Id, luego con el ROW_NUMBER() le decimos que por cada grupo que generó, que enumere cada Id secuencialmente, cuando pase a otro grupo, vuelva a empezar de 0. A toda esta operación le pusimos el alias fila

```sql
WITH duplicados AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY id ORDER BY id) AS fila
  FROM personas
)
DELETE FROM duplicados
WHERE fila > 1;
```

Una vez obtenido cada registro de la tabla con el valor secuencial de cada Id repetido, borramos aquellos registros cuyo atributo fila sea mayor a 1. Si el valor de la fila es mayor a 1, es porque existe un Id repetido a ese, y además conservamos el primer Id repetido.


# 3 - Realizar una consulta que devuelva el monto total comprado por cliente en cada provincia de los fabricantes. Las columnas a mostrar son número de cliente, nombre del cliente, apellido del cliente, provincia_desc (de los fabricantes) y monto total comprado. Ordenar la información por número de cliente en forma ascendente y monto total comprado en forma descendente.

```sql
SELECT *
FROM provincias
```

Seleccionamos todos los atributos de la tabla PROVINCIAS
A esta tabla le pusimos el alias de PROV

```sql
SELECT f.fabricante_cod, f.fabricante_nom, f.tiempo_entrega, prov.*
FROM fabricantes f
JOIN (
	SELECT *
	FROM provincias
) prov
ON f.provincia_cod = prov.provincia_cod
```

De la tabla FABRICANTES, la combinamos con la tabla PROVINCIAS a través del atributo PROVINCIA_COD y nos quedamos con los atributos de la tabla PRONVICIAS y de la tabla FABRICANTES con FABRICANTE_COD, FABRICANTE_NUM, TIEMPO_ENTREGA.
A esta tabla le pusimos el alias de F_PROV

```sql
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
```

De la tabla PRODUCTOS, la combinamos con la tabla F_PROV a través del atributo FABRICANTE_COD.
A esta tabla le pusimos el alias PROD_FRAB_PROV

```sql
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
```

De la tabla FACTURAS_DET la combinamos con la tabla PROD_FRAB_PROV a través del atributo PRODUCTO_COD, además agrupamos los registros según los atributos FACTURA_NUM, PRODUCTO_COD, FABRICANTE_COD, PROVINCIA_COD, PROVINCIA_DESC.
Esto lo hacemos para poder obtener el costo total por cantidad del producto por factura.
A esta tabla le pusimos el alias FDET_PROB_FRAB_PROV

```sql
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
```

De la tabla FACTURAS la combinamos con la tabla FDET_PROB_FRAB_PROV a través del atributo FACTURA_NUM. Nos quedamos con los atributos CLIENTE_NUM de la tabla FACTURAS y el atributo TOTAL y PRONVICIA_DESC de la tabla FDET_PROB_FRAB_PROV.
A esta tabla le pusimos el alias FACT_FDET_PROB_FRAB_PROV

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

De la tabla CLIENTES la combinamos con la tabla FACT_FDET_PROB_FRAB_PROV a través del atributo CLIENTE_NUM. Agrupamos por los datos del cliente como CLIENTE_NUM, NOMBRE y APELLIDO y por los atributos PROVINCIA_DESC y TOTAL de FACT_FDET_PROB_FRAB_PROV. Por último ordenamos por CLIENTE_NUM de forma ascendente y el TOTAL de forma descendente. Le damos la forma de columnas que solicitó la consigna


# 4 - Sea una tabla VALORES que tiene un campo numérico secuencial Id, realizar una consulta que obtenga el valor del primer espacio libre de ese campo

```sql
SELECT MIN(V1.id + 1)
FROM VALORES V1
LEFT JOIN VALORES V2 ON V1.id + 1 = V2.id
WHERE V2.Id IS NULL
```

De la tabla VALORES V1 combinamos con la misma tabla VALORES V2. La combinación que hacemos es por izquierda, es decir por V1, para que en caso de que haya un campo en V1 y no en V2, aún así obtengamos los registros de V1.
La relación es a través del campo Id, pero con el valor siguiente de V1.Id. Esto lo hacemos para obtener todos los id junto a su siguiente. En caso de que haya un “espacio libre” entre ids, el siguiente sería NULL, por lo tanto filtramos por aquellos que su siguiente sea NULL.
Esta tabla quedaría con el primer valor que el siguiente Id sea NULL.

```sql
SELECT COALESCE(
 (SELECT MIN(V1.id + 1)
  FROM VALORES V1
  LEFT JOIN VALORES V2 ON V1.id + 1 = V2.id
  WHERE V2.Id IS NULL),
 1
) id
```

De la tabla anterior, lo ponemos en la sentencia COALESCE, para obtener el primer valor mínimo de los siguientes NULO. Si es nulo, se devuelve 1, ya que el primer valor siguiente NULO sería el primero.


# 5 - Mostrar por cada Producto (producto_cod) las cantidades totales mensuales vendidas (según la fecha de emisión de la factura). No importa si hay meses de diferentes años, se suman como si fueran del mismo año. La información se deberá mostrar en forma tabular como se muestra en la figura, ordenada por código de producto.

```sql
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
```

De la tabla FACTURAS_DET con alias FD, la combinamos con la tabla FACTURAS con alias F a través del atributo FACTURA_NUM, además agrupamos los atributos PRODUCTO_COD y FECHA_EMISION 

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

# 6 - Realizar UN query que asegure que dos tablas con la misma estructura tengan exactamente la misma cantidad de filas y exactamente los mismos datos en cada columna. Es decir, que las tablas sean exactamente iguales.

```sql
SELECT
CASE WHEN
NOT EXISTS (
    SELECT *
    FROM productos
    EXCEPT
    SELECT *
    FROM productos
)
AND
(SELECT COUNT(*) FROM productos) = (SELECT COUNT(*) FROM productos)
THEN 'Sí'
ELSE 'No'
END AS tablas_iguales
```

Generamos una tabla que devuelva una columna llamada tablas_iguales que va a contener los valores Si o No según si las dos tablas a trabajar son iguales, es decir, tienen la misma cantidad de filas y exactamente los mismos datos en cada columna.

Como partimos de dos tablas con la MISMA ESTRUCTRA, podemos utilizar el EXCEPT, que es obligatorio que tengan la misma estructura.

```sql
SELECT COUNT(*) FROM productos) = (SELECT COUNT(*) FROM productos
```

Para saber la misma cantidad de filas, lo hacemos a través de un count.

```sql
SELECT *
FROM productos1
EXCEPT
SELECT *
FROM productos2
```

Con esta query podemos obtener las filas con un valor distinto para la tabla productos1

Pero nos faltaría saber las filas que no están en productos2, por lo tanto faltaría agregar esta query

```sql
SELECT *
FROM productos2
EXCEPT
SELECT *
FROM productos1
```

```sql
SELECT
CASE WHEN
NOT EXISTS (
    SELECT *
    FROM productos1
    EXCEPT
    SELECT *
    FROM productos2
)
AND NOT EXISTS (
    SELECT *
    FROM productos2
    EXCEPT
    SELECT *
    FROM productos1
)
AND
(SELECT COUNT(*) FROM productos1) = (SELECT COUNT(*) FROM productos2)
THEN 'Sí'
ELSE 'No'
END AS tablas_iguales
```


# 7 - Realizar una consulta que tenga el siguiente formato (los datos son solo de ejemplo) que muestre para cada cliente que tenga referente los distintos niveles de referentes que posee. Cada referente se deberá mostrar en una columna diferente y debe mostrar hasta el tercer nivel si es que existe.

```sql
SELECT d.cliente_num, d.cliente_ref, f.cliente_ref AS REF_2
FROM clientes d
LEFT JOIN clientes f
ON d.cliente_ref = f.cliente_num
```

De la tabla clientes, la combinamos con la misma tabla clientes para la izquierda para mantener todos las filas de una tabla. La combinación la hacemos a través del client_num y client_ref, así cada fila de la tabla clientes “d” se relaciona con otra fila de la tabla “f”, donde la referencia de un cliente en la tabla “d”, es el id de la tabla “f”, pero mostramos la referencia del cliente con el id de la tabla “f”

```sql
SELECT R.cliente_num, R.cliente_ref, R.REF_2, cr3.cliente_ref AS REF_3
FROM REF2 R
LEFT JOIN clientes cr3
ON R.REF_2 = cr3.cliente_num
```

Lo mismo que el anterior pero con la nueva tabla generada en la anterior query.

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


# 8 - Dado el siguiente modelo, realice una consulta que permita averiguar en qué equipo juega o jugó una jugadora en una fecha determinada.  La columna FechaDesde es la fecha de alta de la jugadora en un club determinado. La jugadora estará en un club hasta la fechaDesde del registro siguiente existente en la tabla. Si no hay una fila con fecha posterior de la jugadora se asume que aún sigue en ese equipo

```sql
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
```

Primero combinamos las tablas Pases alias p y Clubes alias c a través del código de club. Luego seleccionamos el primer valor de la combinación entre las tablas Jugadoras alias j y la anterior tabla a través del legajo de la jugadora. A esta tabla la filtramos por la diferencia de días de la fecha en que se dió de alta la jugadora en el club, la comparación sería: la fecha de alta de la jugadora en el club - la fecha que se ingresó. Si el valor es positivo, significa que la fecha recibida es mayor a la fecha de alta, y si es igual, es que es la misma fecha. Con esto obtenemos todos los clubes en el que perteneció la jugadora antes o igual de la fecha ingresada. Luego lo ordenamos de forma descendente para que el primer valor sea el más cercano a la fecha.

```sql
CREATE FUNCTION ObtenerClub(@LegajoJugadora INT, @FechaDesdeI DATE) RETURNS INT AS
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


# 9 - Realizar UN query sin utilizar subqueries, que muestre las cantidades de cada producto vendidas en cada provincia. La provincia se refiere a la del Fabricante. Mostrar código de provincia, código de producto, cantidad vendida del producto en la provincia, cantidad total de productos vendidos en la provincia y porcentaje del total vendido en la provincia respecto a la cantidad total de productos vendidos en el país. Mostrar la información ordenada por provincia en forma ascendente y cantidad total del producto vendido en forma descendente.

```sql
SELECT fabr.provincia_cod, fd.producto_cod, SUM(fd.cantidad) cant_prod_x_prov
FROM facturas f
JOIN facturas_det fd
ON f.factura_num = fd.factura_num
JOIN productos p
ON fd.producto_cod = p.producto_cod
JOIN fabricantes fabr
ON p.fabricante_cod = fabr.fabricante_cod
GROUP BY fd.producto_cod, fabr.provincia_cod
```

Hacemos una tabla temporal llamada ventas_x_prov, esta tabla temporal va a ser la combinación entre las tablas facturas, facturas detalle, productos y fabricantes. Agrupamos las filas por los campos código de producto y código de provincia. Hacemos esto para obtener la cantidad de productos vendidos por provincia.

```sql
SELECT vxp.provincia_cod, SUM(vxp.cant_prod_x_prov) total_cant_prod_x_prov
FROM ventas_x_prov vxp
GROUP BY vxp.provincia_cod
```

Hacemos otra tabla temporal utilizando la anterior tabla temporal el cual va a agrupar las filas por código de provincia para obtener la cantidad de ventas por provincia

```sql
SELECT SUM(vtxp.total_cant_prod_x_prov) ventas
FROM ventas_totales_x_prov vtxp
```

Hacemos otra tabla temporal utilizando la anterior tabla temporal para obtener las ventas totales que hubieron.

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

Al final haciendo uso de las 3 tablas temporales, le damos la estructura que se solicitaba, usamos un round con decimal para que el resultado sea con decimales y lo redondeamos con hasta 2 decimales. Combinamos las tablas temporales ventas por provincia y ventas de los productos por provincia. Luego hacemos otra combinación haciendo uso del cross join. Como la tabla ventas_totales tiene una sola fila, al hacer uso del cross join combina todas las filas de una tabla con la otra, por lo tanto no sería tan peligroso hacer uso de esta query ya que la combinación sería por unitario. Esto lo hacemos para poder tener la estructura que se solicitaba, luego lo ordenamos porque era lo que se pedía.

# 10 - Dada el siguiente modelo, desarrolle e implemente un mecanismo que cuando se dé de alta un nuevo pase de una jugadora, controle y evite que la jugadora esté fichada para dos equipos al mismo tiempo (inclusive al mismo). Es decir, que no permita que dos filas en la tabla Pases se superpongan dentro de un periodo para una misma jugadora.

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