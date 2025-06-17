---
~
---

# Sintaxis 

## CASE 

CASE  
    WHEN @dia = 1 THEN ‘Lunes’  
    WHEN @dia = 1 THEN ‘Martes‘  
    ELSE ‘Miércoles‘
END;


## FUNCTION 

**DEFINICIÓN**

```sql
CREATE FUNCTION nombreDelDiaDeLaSemana(@fecha DATE) RETURNS VARCHAR(10) AS
BEGIN

	DECLARE @dia INT;
	DECLARE @nombre VARCHAR(10);

	SET @dia = DATEPART(WEEKDAY, @fecha)

	SET @nombre = CASE WHEN @dia = 2 THEN 'Lunes'
					   WHEN @dia = 3 THEN 'Martes'
					   WHEN @dia = 4 THEN 'Miércoles'
					   WHEN @dia = 5 THEN 'Jueves'
					   WHEN @dia = 6 THEN 'Viernes'
					   WHEN @dia = 7 THEN 'Sabado'
					   ELSE 'Domingo'
				  END;

	RETURN @nombre;

END
```


**USO**

```sql
SELECT f.factura_num, f.fecha_emision, dbo.nombreDelDiaDeLaSemana(f.fecha_emision) AS fechaa
FROM facturas f
WHERE f.fecha_pago IS NULL
```


- - - 
# JOINS 

**Combinación de una tabla con la otra según una relación**

## _INNER_ JOIN 

- La relación tiene que cumplirse
- Si no se cumple la condición, no se mostraran en la tabla resultante 

## LEFT JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de la tabla **IZQUIERDA**  dejando **NULL** en la columna que las relaciona

## RIGHT JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de la tabla **DERECHA** dejando **NULL** en la columna que las relaciona

## FULL _OUTER_ JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de ámbas tablas dejando **NULL** en las columnas que las relaciona

## CROSS JOIN 

- No hay relación
- Por cada fila de una tabla, se junta con todas las filas de la otra tabla


- - - 
# SUBCONSULTA

## CORRELACIONADA 

- Depende de una consulta externa
- Se re-ejecuta para cada fila de la consulta externa

### Usos 

1. **Para cada X, encontrar el Y relacionado con X que cumple una condición**
	- _Ejemplo. Encontrar el empleado con el salario más alto dentro de cada departamento._
	  
	```sql
SELECT E.Nombre, E.Salario, E.DepartamentoID
FROM Empleados E
WHERE E.Salario = (SELECT MAX(E2.Salario)
				   FROM Empleados E2
				   WHERE E2.DepartamentoID = E.DepartamentoID);
	```



2. **Verificar la existencia (o no existencia) de registros relacionados**
   
   ```sql
SELECT f.fabricante_cod,
(CASE WHEN EXISTS (
	SELECT 1
	FROM fabricantes f2
	JOIN productos p
	ON f2.fabricante_cod = p.fabricante_cod
	JOIN facturas_det fd
	ON p.producto_cod = fd.producto_cod
	WHERE f2.fabricante_cod = f.fabricante_cod
) THEN 'Si' ELSE 'No' END) AS 'Posee ventas'
FROM fabricantes f
   ```
   
   
	1. **Si la subconsulta devuelve alguna fila, la condición es verdadera.**
		- _Ejemplo: Obtener productos que nunca han sido vendidos._
	
	```sql
SELECT C.ClienteID, C.Nombre 
FROM Clientes C 
WHERE EXISTS (SELECT 1 
			FROM Pedidos P 
			WHERE P.ClienteID = C.ClienteID);
```
	
	2. **Si la subconsulta NO devuelve ninguna fila, la condición es verdadera.**
		- Ejemplo: Obtener productos que _nunca_ han sido vendidos.

	```sql
SELECT P.ProductoID, P.Descripcion
FROM Productos P
WHERE NOT EXISTS (SELECT 1
                  FROM DetallesPedido DP
                  WHERE DP.ProductoID = P.ProductoID);
```



3. **Calcular una agregación por grupo, pero mostrarla junto a los detalles de cada fila individual del grupo:**
	- _Ejemplo: Mostrar cada producto junto con el precio promedio de todos los productos de su misma categoría._
	
```sql
SELECT PR.ProductoID, PR.NombreProducto, PR.Precio,
	   (SELECT AVG(PR2.Precio)
		FROM Productos PR2
		WHERE PR2.CategoriaID = PR.CategoriaID) AS PrecioPromedioCategoria
FROM Productos PR;
```


- - -
# CURSOR 

- Permite iterar fila por fila en una tabla
- No se definen con **@**

## USO 

```sql
CREATE FUNCTION Lala(@fabricante_cod VARCHAR(MAX)) RETURNS VARCHAR(MAX) AS
BEGIN
	DECLARE cursor_productos CURSOR FOR SELECT p.producto_desc
										FROM productos p
										WHERE p.fabricante_cod = @fabricante_cod; -- Declara el cursor
										
	OPEN cursor_productos; -- Ejecuta la consulta asociada al cursor
	
	DECLARE @producto_desc VARCHAR(MAX);
	DECLARE @producto_desc_acumulado VARCHAR(MAX);
	
	SET @producto_desc_acumulado = '';
	
	FETCH NEXT FROM cursor_productos INTO @producto_desc; -- Obtiene la primera fila de la tabla del cursor y la setea en una variable
	
	WHILE (@@FETCH_STATUS = 0)
	BEGIN
		SET @producto_desc_acumulado += @producto_desc + ',';
		FETCH NEXT FROM cursor_productos INTO @producto_desc;
	END
	
	CLOSE cursor_productos; -- Libera el conjunto de resultados del cursor
	
	DEALLOCATE cursor_productos; -- Elimina el cursor de la memoria
	
	RETURN @producto_desc_acumulado;
END
```


- - - 
# PROCEDURES 

- Conjunto de instrucciones que recibe parametros por referencia y no devuelve nada
- Parametros opcionales
- Puede tener parametros de entrada o salida según si se pone el **OUT**
- Se puede ejecutar explicitando los nombres de los parametros o sin explicitarlos

## DEFINICION 

```sql 
CREATE PROCEDURE miprocedimiento 
@Parametro1 NVARCHAR(50),  
@Parametro2 DECIMAL(10, 2) = 0, 
@ParametroSalida INT OUT
AS
BEGIN
	...
END
```

## USO 

```sql
DECLARE @Salida INT;
EXEC miprocedimiento @Parametro1 = "Hola", @Parametro2 = 10.0, @ParametroSalida = @Salida OUT;
```

```sql 
DECLARE @Salida INT;
EXEC miprocedimiento "Hola", 10.0, @Salida OUT;
```

## BORRAR 

```sql 
DROP PROCEDURE miprocedimiento;
```

- - -
# TABLAS TEMPORALES 

- Tablas que duran solo en la sesión del usuario, no permanecen

## GLOBALES 

## USO 

```sql 
CREATE TABLE ##TablaTemporal(
	Nombre VARCHAR(10) PRIMARY KEY
)
```


## LOCALES
## USO 

```sql 
CREATE TABLE #TablaTemporal(
	Nombre VARCHAR(10) PRIMARY KEY
)
```


- - -
# Errores 

- Se usa para tirar errores
- Primer parametro: Numeros mayores o igual a 50000
- Segundo parametro: Mensaje de error
- Tercer parametro: Estado del error

## USO 

```sql 
THROW 50000, 'Tiempo de entrega negativo', 1;
```


- - -
# EXCEPCIONES

- Se usa dentro de un **PROCEDURE** o **FUNCTION**
- Permite capturar errores y así continuar operando

```sql
CREATE PROCEDURE insertaFabNuevos
AS
BEGIN
	BEGIN TRY
		...
	END TRY
	BEGIN CATCH
		...
		PRINT 'Número de error: ' + CAST(ERROR_NUMBER() AS VARCHAR);
		PRINT 'Mensaje: ' + ERROR_MESSAGE();
		PRINT 'Status: ' + CAST(ERROR_STATE() AS VARCHAR);
	END CATCH
END
```


- - - 
# TRANSACTIONS

- Se usa dentro de un **PROCEDURE**
- Permite ejecutar operaciones y hacer un rollback revirtiendo las ejecuciones que se hicieron

## USO 

```sql
CREATE PROCEDURE insertaFabNuevos
AS
BEGIN
	BEGIN TRY
		BEGIN TRANSACTION
			...
		COMMIT;
	END TRY
	BEGIN CATCH
		ROLLBACK;
	END CATCH
END
```


- - - 
# CREATE 

- Crea una tabla

```sql 
CREATE TABLE #FabricantesNuevos (
	fabricante_cod VARCHAR(4) PRIMARY KEY,
	fabricante_nom VARCHAR(100),
	tiempo_entrega INT,
	provincia_cod VARCHAR(2)
)
```


- - -
# INSERT 

- Inserta datos en una tabla 
- Las nombres de las columnas al lado del nombre de la tabla son **OPCIONALES**

```sql 
INSERT INTO #FabricantesNuevos (fabricante_cod, fabricante_nom, tiempo_entrega, provincia_cod)
VALUES
('FAB1', 'Componentes del Sur S.A.', 7, 'BA'),
('FAB2', 'TecnoNorte SRL', 10, 'SF')
```


- - - 
# DELETE 

- Borra registros de una tabla

```sql 
DELETE FROM NombreDeLaTabla WHERE CondicionParaBorrarFilas;
```

- - - 
# UPDATE 

- Actualiza registros de una tabla

```sql 
UPDATE #FabricantesNuevos
SET fabricante_nom = 'PALAPA',
provincia_cod = 'codd'
WHERE fabricante_cod = 'FAB1'
```

```sql 
UPDATE c
SET c.estado = 'I'
FROM clientes c
WHERE EXISTS (
	SELECT 1
	FROM INSERTED i
	WHERE i.cliente_num = c.cliente_num
)
```


- - - 
# ASIGNACIÓN DE COLUMNAS 

- De una consulta con un solo registro, se setea los valores de las columnas en variables

```sql
DECLARE @fecha_emision DATE;
DECLARE @cliente_num INT;
DECLARE @cant_renglones INT;
DECLARE @monto_total DECIMAL(10,2);

SELECT
	@fecha_emision = f.fecha_emision,
	@cliente_num = f.cliente_num,
	@cant_renglones = COUNT(fd.renglon),
	@monto_total = SUM(fd.precio_unit * fd.cantidad)
FROM facturas f
JOIN facturas_det fd
ON f.factura_num = fd.factura_num
WHERE f.factura_num = @factura_num
GROUP BY f.factura_num, f.fecha_emision, f.cliente_num
```


- - - 
# TRIGGERS 

- Eventos que se disparan según el tipo de operación y tabla en el que se definieron
- Eventos:
	- BEFORE 
	- INSTEAD OF 
	- AFTER 
- Operaciones:
	- INSERT 
	- UPDATE 
	- DELETE 

```sql 
CREATE TRIGGER nombre
ON clientes
evento operacion AS
BEGIN
	SELECT * FROM INSERTED;
	SELECT * FROM DELETED;
END
```

## INSERT 

- Los valores que operaron en esta operación se encuentran en la tabla **INSERTED**

```sql 
CREATE TRIGGER updateInactivos
ON clientes
INSTEAD OF INSERT AS
BEGIN
	UPDATE clientes
	SET estado = 'I'
	WHERE cliente_num IN (
		SELECT i.cliente_num
		FROM INSERTED i
	)
END
```

## DELETE 

- Los valores que operaron en esta operación se encuentran en la tabla **DELETED**

```sql 
CREATE TRIGGER updateInactivos
ON clientes
INSTEAD OF DELETE AS
BEGIN
	UPDATE clientes
	SET estado = 'I'
	WHERE cliente_num IN (
		SELECT d.cliente_num
		FROM DELETED d
	)
END
```

## UPDATE

- Los valores que operaron en esta operación se encuentran en la tabla **DELETED** y **INSERTED**
- En **DELETED**, las filas que se borraron
- En **INSERTED**, las filas que se reemplazan

```sql 
CREATE TRIGGER updateInactivos
ON clientes
INSTEAD OF UPDATE AS
BEGIN
	SELECT * FROM INSERTED;
	SELECT * FROM DELETED;
END
```


- - - 
# VIEW

- Es una tabla virtual basada en el conjunto de resultados de una consulta SQL. 
- Las vistas no almacenan datos en sí mismas, sino que actúan como una ventana o una "consulta predefinida" sobre una o más tablas subyacentes.

```sql 
CREATE VIEW ProductosFabricanteV AS
SELECT producto_cod, producto_desc, precio_unit, f.fabricante_cod, fabricante_nom, provincia_cod
FROM productos p
JOIN fabricantes f
ON p.fabricante_cod = f.fabricante_cod
```


# FUNCIONES STRING 

- **`+` (Operador de Concatenación)**:
    
    - **Explicación**: Une dos o más cadenas de caracteres. Si alguna parte de la expresión es `NULL`, el resultado completo es `NULL`.
    - **Ejemplo**:
        ```sql
        SELECT 'Hola' + ' ' + 'Mundo';
        -- Resultado: 'Hola Mundo'
        
        SELECT 'Parte1' + NULL + 'Parte2';
        -- Resultado: NULL
        ```
        
- **CONCAT(cadena1, cadena2, ..., cadenan)**:
    
    - **Explicación**: Une dos o más cadenas de caracteres. A diferencia del operador `+`, `CONCAT` trata los valores `NULL` como cadenas vacías (`''`), lo que a menudo es más conveniente.
    - **Ejemplo**:        
        ```sql
        SELECT CONCAT('Nombre:', ' ', 'Juan', ' ', 'Perez');
        -- Resultado: 'Nombre: Juan Perez'
        
        SELECT CONCAT('Valor: ', NULL, ' unidades');
        -- Resultado: 'Valor:  unidades'
        ```
        
- **LEN(expresion_cadena)**:
    - **Explicación**: Devuelve el número de caracteres de la expresión de cadena especificada, excluyendo los espacios en blanco finales.
    - **Ejemplo**:
        ```sql
        SELECT LEN('  SQL Server   ');
        -- Resultado: 10 (contando 'SQL Server')
        
        SELECT LEN('Palabra');
        -- Resultado: 7
        ```
        
- **SUBSTRING(expresion, inicio, longitud)**:
    - **Explicación**: Extrae una parte de una cadena de caracteres, comenzando en una posición específica y con una longitud determinada. La posición de inicio es 1-basada.
    - **Ejemplo**:
        ```sql
        SELECT SUBSTRING('Desarrollo SQL', 5, 6);
        -- Resultado: 'rrollo' (empieza en la 5ta posición 'r', toma 6 caracteres)
        ```
        
- **LEFT(expresion_cadena, longitud)**:
    - **Explicación**: Devuelve la parte izquierda de una cadena con el número de caracteres especificado.
    - **Ejemplo**:
        ```sql
        SELECT LEFT('Código Postal', 5);
        -- Resultado: 'Código'
        ```
        
- **RIGHT(expresion_cadena, longitud)**:
    - **Explicación**: Devuelve la parte derecha de una cadena con el número de caracteres especificado.
    - **Ejemplo**:
        ```sql
        SELECT RIGHT('Nombre Completo', 8);
        -- Resultado: 'Completo'
        ```
        
- **CHARINDEX(subcadena, expresion_cadena `[, inicio]`)**:
    - **Explicación**: Devuelve la posición inicial de la primera aparición de una subcadena dentro de una cadena. La búsqueda puede comenzar desde una posición opcional.
    - **Ejemplo**:
        ```sql
        SELECT CHARINDEX('mundo', 'Hola mundo, lindo mundo');
        -- Resultado: 6 (la 'm' de la primera ocurrencia de 'mundo')
        
        SELECT CHARINDEX('mundo', 'Hola mundo, lindo mundo', 7);
        -- Resultado: 19 (la 'm' de la segunda ocurrencia de 'mundo', buscando desde pos 7)
        ```
        
- **PATINDEX('%patron%', expresion_cadena)**:
    - **Explicación**: Devuelve la posición inicial de la primera aparición de un patrón en una expresión de cadena. Permite el uso de comodines (`%`, `_`, `[]`, `[^]`) como en `LIKE`.
    - **Ejemplo**:
        ```sql
        SELECT PATINDEX('%[0-9]%', 'ABC123XYZ');
        -- Resultado: 4 (la posición del primer dígito)
        
        SELECT PATINDEX('%[^a-zA-Z]%', 'TextoSinNumeros');
        -- Resultado: 0 (no encontró ningún carácter que no sea letra)
        ```
        
- **REPLACE(expresion_cadena, cadena_a_buscar, cadena_reemplazo)**:
    - **Explicación**: Reemplaza todas las apariciones de una subcadena específica dentro de una cadena con otra cadena de reemplazo.
    - **Ejemplo**:
        ```sql
        SELECT REPLACE('www.ejemplo.com', '.com', '.org');
        -- Resultado: 'www.ejemplo.org'
        
        SELECT REPLACE('Uno, Dos, Tres, Dos', 'Dos', 'Cuatro');
        -- Resultado: 'Uno, Cuatro, Tres, Cuatro'
        ```
        
- **LTRIM(expresion_cadena)**:
    - **Explicación**: Elimina los espacios en blanco iniciales (a la izquierda) de una cadena.
    - **Ejemplo**:
        ```sql
        SELECT '(' + LTRIM('   Mi Texto') + ')';
        -- Resultado: '(Mi Texto)'
        ```
        
- **RTRIM(expresion_cadena)**:
    - **Explicación**: Elimina los espacios en blanco finales (a la derecha) de una cadena.
    - **Ejemplo**:
        ```sql
        SELECT '(' + RTRIM('Mi Texto   ') + ')';
        -- Resultado: '(Mi Texto)'
        ```
        
- **TRIM(`[caracteres_a_recortar FROM]` expresion_cadena)**:
    - **Explicación**: Elimina el carácter especificado (o espacios por defecto) de ambos extremos de una cadena. Si no se especifican `caracteres_a_recortar`, recorta espacios.
    - **Ejemplo**:
        ```sql
        SELECT TRIM('  Texto con espacios  ');
        -- Resultado: 'Texto con espacios'
        
        SELECT TRIM('._' FROM '._.Mi.Texto._.');
        -- Resultado: 'Mi.Texto'
        ```
        
- **UPPER(expresion_cadena)**:
    - **Explicación**: Convierte todos los caracteres alfabéticos de una cadena a mayúsculas.
    - **Ejemplo**:
        ```sql
        SELECT UPPER('mi nombre');
        -- Resultado: 'MI NOMBRE'
        ```
        
- **LOWER(expresion_cadena)**:
    - **Explicación**: Convierte todos los caracteres alfabéticos de una cadena a minúsculas.
    - **Ejemplo**:
        ```sql
        SELECT LOWER('Mi Nombre');
        -- Resultado: 'mi nombre'
        ```
        
- **REPLICATE(expresion_cadena, numero_de_veces)**:
    - **Explicación**: Repite una expresión de cadena un número especificado de veces.
    - **Ejemplo**:
        ```sql
        SELECT REPLICATE('X', 5);
        -- Resultado: 'XXXXX'
        
        SELECT REPLICATE('0', 3) + '123';
        -- Resultado: '000123' (útil para rellenar a la izquierda)
        ```
        
- **FORMAT(valor, formato_string, `[cultura]`)**:
    - **Explicación**: Formatea un valor de tipo numérico, fecha/hora o string con el formato y la cultura especificados. Muy flexible para la presentación.
    - **Ejemplo**:
        ```sql
        SELECT FORMAT(GETDATE(), 'yyyy-MM-dd HH:mm:ss');
        -- Resultado: '2025-06-16 16:00:00' (aproximadamente, dependiendo de la hora actual)
        
        SELECT FORMAT(12345.67, 'C', 'es-ES');
        -- Resultado: '12.345,67 €' (símbolo de moneda y separadores según la cultura)
        ```
        
- **CAST(expresion AS tipo_dato)**:
    - **Explicación**: Convierte una expresión de un tipo de dato a otro. Es una conversión genérica.
    - **Ejemplo**:
        ```sql
        SELECT CAST(12345 AS VARCHAR(10));
        -- Resultado: '12345' (string)
        
        SELECT CAST(GETDATE() AS VARCHAR(20));
        -- Resultado: 'Jun 16 2025  4:00PM' (o similar, depende del formato por defecto)
        ```
        
- **CONVERT(tipo_dato, expresion, `[estilo]`)**:
    - **Explicación**: Convierte una expresión de un tipo de dato a otro, similar a `CAST`, pero ofrece un parámetro `estilo` adicional para conversiones de fecha/hora y algunos tipos de datos especiales.
    - **Ejemplo**:
        ```sql
        SELECT CONVERT(VARCHAR(10), GETDATE(), 103);
        -- Resultado: '16/06/2025' (formato dd/mm/yyyy)
        
        SELECT CONVERT(INT, '123');
        -- Resultado: 123 (entero)
        ```

- **LIKE (Operador)**:
    - **Explicación**: Se utiliza en la cláusula `WHERE` para buscar patrones específicos en una columna de tipo cadena. Es sensible a la intercalación (collation) de la columna.
    - **Comodines (Wildcards)**:
        - `%`: Representa cero, uno o varios caracteres.
        - `_` (guion bajo): Representa un único carácter.
        - `[]`: Representa un conjunto de caracteres (ej. `[aeiou]` para cualquier vocal).
        - `[^]`: Representa cualquier carácter _que no esté_ en el conjunto.
    - **Ejemplo**:
        ```sql
        -- Buscar nombres que empiezan con 'A'
        SELECT Nombre FROM Clientes WHERE Nombre LIKE 'A%';
        
        -- Buscar nombres que tienen 'an' en cualquier posición
        SELECT Nombre FROM Clientes WHERE Nombre LIKE '%an%';
        
        -- Buscar códigos de producto que tienen 'X' como segundo carácter
        SELECT CodigoProducto FROM Productos WHERE CodigoProducto LIKE '_X%';
        
        -- Buscar palabras que empiezan con una vocal
        SELECT Palabra FROM Diccionario WHERE Palabra LIKE '[AEIOU]%';
        ```