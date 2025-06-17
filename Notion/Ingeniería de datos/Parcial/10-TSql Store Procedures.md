# **Procedimientos Almacenados (Stored Procedures)**

Un **procedimiento almacenado** es un conjunto de instrucciones SQL precompiladas y almacenadas en la base de datos. Se ejecutan como una única unidad lógica para realizar una tarea específica. Piensa en ellos como pequeñas aplicaciones o scripts que viven dentro de tu base de datos y que puedes invocar cuando los necesites.

## **Qué hacen**

- **Modularidad y Reutilización**: Permiten agrupar lógica de negocio compleja y reutilizarla varias veces sin reescribir el código.
- **Rendimiento**: Se compilan y optimizan la primera vez que se ejecutan, lo que puede resultar en una ejecución más rápida en usos posteriores.
- **Seguridad**: Puedes otorgar permisos para ejecutar un procedimiento sin dar acceso directo a las tablas subyacentes, lo que mejora la seguridad.
- **Transaccionalidad**: Pueden contener transacciones completas (`BEGIN TRAN`, `COMMIT`, `ROLLBACK`) para asegurar la integridad de los datos.
- **Manejo de Errores**: Permiten implementar lógica de manejo de errores robusta (con `TRY...CATCH`).
- **Parámetros**: Pueden aceptar **parámetros de entrada** (`INPUT`) y devolver **parámetros de salida** (`OUTPUT`).

## **Ejemplo: Procedimiento Almacenado**

**Tabla de Ejemplo:**

`Productos (ProductoID INT PRIMARY KEY IDENTITY(1,1), Nombre VARCHAR(100), Precio DECIMAL(10,2), Stock INT)`

```sql
-- Crear el Procedimiento Almacenado
CREATE PROCEDURE sp_GestionarProducto
    @p_Nombre VARCHAR(100),
    @p_Precio DECIMAL(10, 2),
    @p_Cantidad INT,
    @p_Operacion VARCHAR(10) -- 'INSERT' o 'UPDATE'
AS
BEGIN
    SET NOCOUNT ON; -- Para evitar que se envíen mensajes de 'X filas afectadas' al cliente

    IF @p_Operacion = 'INSERT'
    BEGIN
        -- Insertar un nuevo producto
        INSERT INTO Productos (Nombre, Precio, Stock)
        VALUES (@p_Nombre, @p_Precio, @p_Cantidad);
        PRINT 'Producto "' + @p_Nombre + '" insertado correctamente.';
    END
    ELSE IF @p_Operacion = 'UPDATE'
    BEGIN
        -- Actualizar el stock de un producto existente
        UPDATE Productos
        SET Stock = Stock + @p_Cantidad
        WHERE Nombre = @p_Nombre;

        IF @@ROWCOUNT > 0
            PRINT 'Stock de "' + @p_Nombre + '" actualizado correctamente.';
        ELSE
            PRINT 'ERROR: Producto "' + @p_Nombre + '" no encontrado para actualizar.';
    END
    ELSE
    BEGIN
        PRINT 'Operación no válida. Use "INSERT" o "UPDATE".';
    END
END;
GO
```

**Cómo Ejecutarlo:**

```sql
-- Insertar un nuevo producto
EXEC sp_GestionarProducto 'Laptop XYZ', 1200.00, 10, 'INSERT';
SELECT * FROM Productos;

-- Actualizar el stock de un producto existente
EXEC sp_GestionarProducto 'Laptop XYZ', 0, 5, 'UPDATE'; -- El precio no es relevante para el UPDATE de stock aquí
SELECT * FROM Productos;

-- Intentar actualizar un producto que no existe
EXEC sp_GestionarProducto 'Mouse Inexistente', 0, 2, 'UPDATE';
SELECT * FROM Productos;
```


---
# **Funciones Definidas por el Usuario (User-Defined Functions - UDFs)**

Una **función** en SQL Server es un objeto de base de datos que encapsula lógica y devuelve un valor (o una tabla de valores). A diferencia de los procedimientos almacenados, las funciones están diseñadas para ser utilizadas **en expresiones SQL** (como en `SELECT`, `WHERE`, `HAVING`, etc.) y **no pueden modificar la base de datos** directamente (es decir, no pueden usar `INSERT`, `UPDATE`, `DELETE`).

## **Tipos Comunes y Qué Hacen**

1. **Funciones Escalares**:
    - **Qué hacen**: Toman cero o más parámetros de entrada y devuelven un único valor escalar (ej. un `INT`, `VARCHAR`, `DECIMAL`).
    - **Uso típico**: Realizar cálculos complejos, formatear datos, validar entradas.
      
2. **Funciones con Valor de Tabla (Table-Valued Functions - TVFs)**:
    - **Qué hacen**: Toman cero o más parámetros de entrada y devuelven una tabla. Se pueden usar en la cláusula `FROM` como si fueran una tabla o vista.
    - **Tipos de TVFs**:
        - **Inline TVFs**: Son esencialmente vistas parametrizadas; su lógica es una única sentencia `SELECT`. Son muy eficientes porque el optimizador puede "incrustar" su lógica directamente en la consulta principal.
        - **Multi-statement TVFs**: Contienen múltiples sentencias SQL y lógica más compleja. Son menos eficientes que las Inline TVFs porque SQL Server no puede optimizar su plan de ejecución de la misma manera.

## **Ejemplo: Función Escalar**

```sql
-- Crear la Función Escalar
CREATE FUNCTION dbo.fn_CalcularPrecioVenta
(
    @p_PrecioCosto DECIMAL(10, 2),
    @p_MargenGanancia DECIMAL(5, 2) -- Ej: 0.20 para 20%
)
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @PrecioVenta DECIMAL(10, 2);
    SET @PrecioVenta = @p_PrecioCosto * (1 + @p_MargenGanancia);
    RETURN @PrecioVenta;
END;
GO
```

**Cómo Usarla:**
```sql
-- Usar la función en una sentencia SELECT
SELECT
    Nombre,
    Precio AS PrecioCosto,
    dbo.fn_CalcularPrecioVenta(Precio, 0.25) AS PrecioVentaCon25Margen
FROM Productos
WHERE Precio IS NOT NULL;

-- También se puede usar en otras cláusulas (ej. WHERE, HAVING)
SELECT
    Nombre,
    Precio
FROM Productos
WHERE dbo.fn_CalcularPrecioVenta(Precio, 0.10) > 100; -- Productos con precio de venta > 100 (con 10% margen)
```

## **Ejemplo: Función con Valor de Tabla (Inline TVF)**

Vamos a crear una función que devuelva los productos con un stock por encima de un umbral específico.

```sql
-- Crear la Inline Table-Valued Function
CREATE FUNCTION dbo.fn_ProductosConStockAlto
(
    @p_UmbralStock INT
)
RETURNS TABLE
AS
RETURN
(
    SELECT ProductoID, Nombre, Stock, Precio
    FROM Productos
    WHERE Stock > @p_UmbralStock
);
GO
```

**Cómo Usarla:**

```sql
-- Usar la función en la cláusula FROM como si fuera una tabla
SELECT
    p.Nombre,
    p.Stock,
    p.Precio
FROM dbo.fn_ProductosConStockAlto(10) AS p; -- Mostrar productos con stock > 10

SELECT
    p.Nombre,
    p.Stock,
    d.Comentarios -- Suponiendo que tienes una tabla de detalles de productos
FROM dbo.fn_ProductosConStockAlto(5) AS p
JOIN DetallesProducto AS d ON p.ProductoID = d.ProductoID; -- Unir con otras tablas
```


- - -
# TSQL Variables 

- **Qué hacen**: Las variables en T-SQL son objetos que se usan para almacenar un solo valor de datos. Son temporales y solo existen durante la ejecución del batch o procedimiento/función donde se declaran. Permiten escribir código más flexible, legible y reutilizable.
- **Sintaxis**:
    - Declaración: `DECLARE @nombre_variable TIPO_DATO [= valor_inicial];`
    - Asignación: `SET @nombre_variable = valor;` o `SELECT @nombre_variable = columna FROM tabla WHERE ...;`
- **Ejemplo**:
    ```sql
    -- Declarar una variable para almacenar un nombre
    DECLARE @nombreCliente VARCHAR(100);
    
    -- Asignar un valor usando SET
    SET @nombreCliente = 'Juan Pérez';
    PRINT 'El nombre del cliente es: ' + @nombreCliente;
    
    -- Declarar una variable y asignarle el promedio de salarios
    DECLARE @salarioPromedio DECIMAL(10, 2);
    SELECT @salarioPromedio = AVG(Salario) FROM Empleados; -- Asigna el resultado de la subconsulta
    PRINT 'El salario promedio de los empleados es: ' + CAST(@salarioPromedio AS VARCHAR(20));
    
    -- Usar la variable en una consulta
    SELECT Nombre, Salario
    FROM Empleados
    WHERE Salario > @salarioPromedio;
    ```
    
---
# TSQL Operadores

- **Qué hacen**: Los operadores son símbolos o palabras clave que se utilizan en sentencias T-SQL para realizar operaciones (matemáticas, lógicas, de comparación, etc.) con valores.
- **Categorías Principales**:
    - **Aritméticos**: `+` (suma), `-` (resta), `*` (multiplicación), `/` (división), `%` (módulo/resto).
	- **De Comparación**: =, `!=` (o `<>`), `<` (menor), `>` (mayor), `<=` (menor o igual), `>=` (mayor o igual), `!>` (no mayor), `!<` (no menor).
	- **Lógicos**: `AND`, `OR`, `NOT`. También `BETWEEN`, `IN`, `LIKE`, `EXISTS`.
	- **De Cadena**: `+` (concatenación).
	- **Bitwise**: `&` (AND bit a bit), `|` (OR bit a bit), `^` (XOR bit a bit).

- **Ejemplo**:
    ```sql
    DECLARE @num1 INT = 10;
    DECLARE @num2 INT = 3;
    DECLARE @resultado INT;
    
    -- Operadores Aritméticos
    SET @resultado = @num1 * @num2; -- 30
    PRINT 'Multiplicación: ' + CAST(@resultado AS VARCHAR);
    SET @resultado = @num1 % @num2; -- 1 (resto de la división)
    PRINT 'Módulo: ' + CAST(@resultado AS VARCHAR);
    
    -- Operadores de Comparación y Lógicos
    IF @num1 > @num2 AND @num1 != 0
    BEGIN
        PRINT '@num1 es mayor que @num2 y no es cero.';
    END;
    
    -- Operador de Cadena
    DECLARE @saludo VARCHAR(50) = 'Hola';
    DECLARE @nombre VARCHAR(50) = 'Mundo';
    PRINT @saludo + ' ' + @nombre + '!'; -- "Hola Mundo!"
    ```
    
---
# TSQL Sentencias de Control

- **Qué hacen**: Controlan el flujo de ejecución de un script o bloque de código, permitiendo la toma de decisiones, la repetición de instrucciones o la salida de bloques.
- **Comandos Principales**:
    - **`IF...ELSE`**: Ejecuta un bloque de código si una condición es verdadera; opcionalmente, ejecuta otro bloque si es falsa.
        ```sql
        DECLARE @stockActual INT = 5;
        IF @stockActual <= 10
        BEGIN
            PRINT 'Stock bajo. Realizar pedido.';
        END
        ELSE
        BEGIN
            PRINT 'Stock suficiente.';
        END;
        ```
        
    - **`BEGIN...END`**: Define un bloque de código que se ejecuta como una sola unidad. Es necesario cuando un `IF`, `WHILE`, etc., tiene más de una sentencia asociada.

    - **`WHILE`**: Repite un bloque de código mientras una condición sea verdadera.
        ```sql
        DECLARE @contador INT = 1;
        WHILE @contador <= 5
        BEGIN
            PRINT 'Iteración: ' + CAST(@contador AS VARCHAR);
            SET @contador = @contador + 1;
        END;
        ```
        
    - **`BREAK`**: Sale inmediatamente del bucle `WHILE` más interno.
        ```sql
        DECLARE @i INT = 1;
        WHILE @i <= 10
        BEGIN
            IF @i = 6
                BREAK; -- Sale del bucle cuando i llega a 6
            PRINT 'BREAK: ' + CAST(@i AS VARCHAR);
            SET @i = @i + 1;
        END;
        ```
        
    - **`CONTINUE`**: Salta a la siguiente iteración del bucle `WHILE` más interno, sin ejecutar el resto del código de la iteración actual.
        ```sql
        DECLARE @j INT = 0;
        WHILE @j < 5
        BEGIN
            SET @j = @j + 1;
            IF @j = 3
                CONTINUE; -- Salta la impresión cuando j es 3
            PRINT 'CONTINUE: ' + CAST(@j AS VARCHAR);
        END;
        ```
        
    - **`RETURN`**: Sale de la ejecución del batch, procedimiento almacenado o función. No devuelve un valor directamente en procedimientos (a menos que sea un código de estado).
        ```sql
        CREATE PROCEDURE sp_ValidarEdad @edad INT
        AS
        BEGIN
            IF @edad < 18
            BEGIN
                PRINT 'Edad insuficiente.';
                RETURN; -- Sale del procedimiento
            END;
            PRINT 'Edad válida.';
        END;
        GO
        EXEC sp_ValidarEdad 15;
        EXEC sp_ValidarEdad 20;
        ```
        
    - **`GOTO`**: Salta a una etiqueta definida. Generalmente **desaconsejado** por hacer el código difícil de leer y mantener ("spaghetti code").
        ```sql
        DECLARE @valor INT = 10;
        IF @valor = 10 GOTO EtiquetaFin;
        PRINT 'Esta línea no se ejecutará.';
        EtiquetaFin:
        PRINT 'Estamos en la etiqueta de fin.';
        ```
        
---
# TSQL Asignación de Columnas (`SET` vs `SELECT`)

- **Qué hacen**: Ambas se utilizan para asignar valores a variables, pero tienen diferencias sutiles y comportamientos importantes cuando se trata de subconsultas que devuelven múltiples filas o ninguna fila.
    
- **`SET`**:
    - **Explicación**: Asigna un valor a una **única variable**. Si la subconsulta utilizada para la asignación devuelve múltiples filas, `SET` generará un **error**. Si la subconsulta no devuelve ninguna fila, asigna `NULL`.
    - **Ejemplo**:
        ```sql
        DECLARE @nombreEmpleado VARCHAR(100);
        DECLARE @salarioEmpleado DECIMAL(10,2);
        
        -- Asignación simple
        SET @nombreEmpleado = 'Carlos';
        PRINT 'Nombre: ' + @nombreEmpleado;
        
        -- Asignación desde una subconsulta (única fila)
        SET @salarioEmpleado = (SELECT Salario FROM Empleados WHERE EmpleadoID = 1);
        PRINT 'Salario del empleado 1: ' + CAST(@salarioEmpleado AS VARCHAR);
        
        -- Intentar asignar desde una subconsulta que devuelve múltiples filas (ERROR)
        -- SET @nombreEmpleado = (SELECT Nombre FROM Empleados); -- Esto causaría un error
        ```
        
- **`SELECT`**:
    - **Explicación**: Puede asignar valores a **una o múltiples variables a la vez**. Si la subconsulta utilizada para la asignación devuelve múltiples filas, `SELECT` **no generará un error**, sino que asignará el valor de la _última fila_ devuelta por la subconsulta (el orden no está garantizado sin `ORDER BY`). Si la subconsulta no devuelve ninguna fila, asignará `NULL` a la variable.
    - **Ejemplo**:
        ```sql
        DECLARE @nombre VARCHAR(100), @salario DECIMAL(10,2);
        
        -- Asignación múltiple
        SELECT @nombre = Nombre, @salario = Salario FROM Empleados WHERE EmpleadoID = 2;
        PRINT 'Empleado 2: ' + @nombre + ', Salario: ' + CAST(@salario AS VARCHAR);
        
        -- Asignación desde una subconsulta que devuelve múltiples filas (NO ERROR, toma la última)
        -- El orden es indefinido si no hay ORDER BY
        SELECT @nombre = Nombre FROM Empleados; -- @nombre contendrá el nombre de la última fila procesada
        PRINT 'Nombre de la última fila: ' + @nombre; -- Puede ser cualquiera, no hay garantía
        
        -- Asignación desde una subconsulta que no devuelve filas
        SELECT @nombre = Nombre FROM Empleados WHERE EmpleadoID = 999;
        PRINT 'Nombre de empleado inexistente (será NULL): ' + ISNULL(@nombre, 'NULL');
        ```
        
    - **Recomendación**: Usa `SET` para asignaciones de una sola variable, especialmente si esperas un solo valor de una subconsulta, ya que te alertará sobre resultados inesperados. Usa `SELECT` cuando necesites asignar múltiples variables a la vez o cuando intencionalmente quieres el comportamiento de "última fila" o "NULL si no hay filas".

---
# TSQL Cursores

- **Qué hacen**: Un cursor permite procesar un conjunto de resultados **fila por fila**, a diferencia del procesamiento basado en conjuntos que es la forma nativa y más eficiente de SQL. Generalmente, los cursores **deben evitarse** a menos que no haya otra alternativa basada en conjuntos para resolver un problema específico, ya que son notoriamente ineficientes.
- **Ciclo de vida**:
    1. **`DECLARE`**: Define el cursor y la consulta `SELECT` que lo alimenta.
    2. **`OPEN`**: Ejecuta la consulta `SELECT` y rellena el conjunto de resultados.
    3. **`FETCH`**: Recupera una fila a la vez del conjunto de resultados y la coloca en variables.
    4. **`CLOSE`**: Cierra el cursor (libera los bloqueos pero mantiene la definición).
    5. **`DEALLOCATE`**: Libera todos los recursos asociados con el cursor.
- **Ejemplo**: Simplemente para ilustrar la sintaxis (no recomendado para tareas comunes).
    ```sql
    DECLARE @empleadoNombre VARCHAR(100);
    DECLARE @empleadoSalario DECIMAL(10,2);
    
    -- 1. Declarar el cursor
    DECLARE CursosEmpleados CURSOR FOR
    SELECT Nombre, Salario
    FROM Empleados
    WHERE Salario > 60000;
    
    -- 2. Abrir el cursor
    OPEN CursosEmpleados;
    
    -- 3. Recuperar la primera fila
    FETCH NEXT FROM CursosEmpleados INTO @empleadoNombre, @empleadoSalario;
    
    -- Bucle para procesar cada fila
    WHILE @@FETCH_STATUS = 0 -- @@FETCH_STATUS indica el estado de la última operación FETCH
    BEGIN
        PRINT 'Procesando empleado: ' + @empleadoNombre + ', Salario: ' + CAST(@empleadoSalario AS VARCHAR);
        -- Aquí iría la lógica de negocio para cada fila
        FETCH NEXT FROM CursosEmpleados INTO @empleadoNombre, @empleadoSalario;
    END;
    
    -- 4. Cerrar el cursor
    CLOSE CursosEmpleados;
    
    -- 5. Desasignar el cursor
    DEALLOCATE CursosEmpleados;
    ```
    
---
# TSQL Transacciones

- **Qué hacen**: Agrupan un conjunto de sentencias SQL en una **unidad lógica de trabajo**. Esto significa que todas las sentencias dentro de la transacción se ejecutan con éxito (se `COMMIT`en) o todas se deshacen (se `ROLLBACK`ean) si algo falla. Aseguran las propiedades ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad).
    
- **Comandos**:
    - **`BEGIN TRANSACTION`**: Marca el inicio de una transacción.
    - **`COMMIT TRANSACTION`**: Guarda permanentemente los cambios realizados durante la transacción.
    - **`ROLLBACK TRANSACTION`**: Deshace todos los cambios realizados desde el `BEGIN TRANSACTION`.
    - **`SAVE TRANSACTION nombre_punto`**: Establece un punto de guardado dentro de una transacción, permitiendo un `ROLLBACK` parcial hasta ese punto.
- **Ejemplo**: Transferencia de dinero entre cuentas (donde ambas operaciones deben tener éxito o ninguna).
    
    **Tabla de Ejemplo (para transacciones):** `CuentasBancarias (CuentaID INT PRIMARY KEY, Saldo DECIMAL(18,2))`   
    ```sql
    IF OBJECT_ID('CuentasBancarias', 'U') IS NOT NULL
        DROP TABLE CuentasBancarias;
    CREATE TABLE CuentasBancarias (CuentaID INT PRIMARY KEY, Saldo DECIMAL(18,2));
    INSERT INTO CuentasBancarias VALUES (101, 500.00), (102, 200.00);
    
    SELECT * FROM CuentasBancarias;
    
    -- Inicio de la transacción
    BEGIN TRANSACTION;
    BEGIN TRY
        -- Debitar de la cuenta 101
        UPDATE CuentasBancarias
        SET Saldo = Saldo - 100.00
        WHERE CuentaID = 101;
    
        -- Simular un error si el saldo se vuelve negativo (aunque ya tiene 500, es para el ejemplo)
        IF (SELECT Saldo FROM CuentasBancarias WHERE CuentaID = 101) < 0
        BEGIN
            RAISERROR('Saldo insuficiente en la cuenta de origen.', 16, 1);
        END;
    
        -- Acreditar a la cuenta 102
        UPDATE CuentasBancarias
        SET Saldo = Saldo + 100.00
        WHERE CuentaID = 102;
    
        -- Si todo fue bien, confirmar la transacción
        COMMIT TRANSACTION;
        PRINT 'Transferencia completada con éxito.';
    END TRY
    BEGIN CATCH
        -- Si hubo algún error, deshacer todos los cambios
        ROLLBACK TRANSACTION;
        PRINT 'Error en la transferencia. Cambios revertidos.';
        -- Obtener detalles del error (ver sección de excepciones)
        PRINT 'Mensaje de error: ' + ERROR_MESSAGE();
    END CATCH;
    
    SELECT * FROM CuentasBancarias; -- Ver el estado final
    ```
    
---
# TSQL Excepciones / Manejo de Errores (`TRY...CATCH`)

- **Qué hacen**: Permiten capturar y manejar errores de tiempo de ejecución de manera estructurada, evitando que un error detenga abruptamente la ejecución de un script o procedimiento.
    
- **Bloques**:
    - **`BEGIN TRY...END TRY`**: Contiene el código que se intenta ejecutar y que podría generar un error.
    - **`BEGIN CATCH...END CATCH`**: Contiene el código que se ejecuta si ocurre un error dentro del bloque `TRY`.
    
- **Funciones de Error**: Dentro del bloque `CATCH`, puedes usar funciones para obtener información sobre el error:
    - `ERROR_NUMBER()`: Número de error.
    - `ERROR_SEVERITY()`: Gravedad del error.
    - `ERROR_STATE()`: Estado del error (información de diagnóstico).
    - `ERROR_PROCEDURE()`: Nombre del procedimiento/función donde ocurrió.
    - `ERROR_LINE()`: Número de línea donde ocurrió el error.
    - `ERROR_MESSAGE()`: Mensaje completo del error.
- **`RAISERROR`**: Se usa para generar un error definido por el usuario (o reenviar un error del sistema).
    
- **Ejemplo**: Dividir por cero y manejar la excepción.
    ```sql
    DECLARE @dividendo INT = 10;
    DECLARE @divisor INT = 0;
    DECLARE @resultado INT;
    
    BEGIN TRY
        SET @resultado = @dividendo / @divisor; -- Esto causará un error de división por cero
        PRINT 'El resultado es: ' + CAST(@resultado AS VARCHAR);
    END TRY
    BEGIN CATCH
        PRINT '¡Se ha producido un error!';
        PRINT 'Número de Error: ' + CAST(ERROR_NUMBER() AS VARCHAR);
        PRINT 'Gravedad: ' + CAST(ERROR_SEVERITY() AS VARCHAR);
        PRINT 'Estado: ' + CAST(ERROR_STATE() AS VARCHAR);
        PRINT 'Línea: ' + CAST(ERROR_LINE() AS VARCHAR);
        PRINT 'Mensaje: ' + ERROR_MESSAGE();
    
        -- Opcional: Re-lanzar el error (si quieres que el error siga propagándose)
        -- RAISERROR ('Error personalizado re-lanzado.', 16, 1);
    END CATCH;
    
    -- También se puede generar un error intencionalmente:
    BEGIN TRY
        RAISERROR('Este es un error personalizado generado por RAISERROR.', 16, 1);
    END TRY
    BEGIN CATCH
        PRINT 'Capturado error personalizado: ' + ERROR_MESSAGE();
    END CATCH;
    ```
    
---
# TSQL Errores (Información y Generación)

- **Qué hacen**: Se refiere a cómo SQL Server gestiona los errores y cómo un desarrollador puede interactuar con esa gestión.
- **Variables de estado de error**:
    - `@@ERROR`: Devuelve el número de error de la última sentencia T-SQL ejecutada. Un valor de 0 indica éxito. (Legado, se prefiere `TRY...CATCH` para errores de tiempo de ejecución).
- **Generación de errores**:
    - `RAISERROR ('mensaje', nivel_gravedad, estado_error)`: Se utiliza para generar mensajes de error definidos por el usuario y lanzarlos como errores del sistema. El `nivel_gravedad` (de 0 a 25) indica cuán grave es el error; los niveles 11-16 son errores de aplicación que pueden ser manejados por el usuario. Niveles más altos (>19) son fatales y terminan la conexión.
    - `THROW`: (SQL Server 2012+) Es una alternativa más moderna y preferida a `RAISERROR` para lanzar excepciones. Requiere ser la primera sentencia en un bloque `CATCH` o ir precedida por un `RETURN` o `ROLLBACK`.
- **Ejemplo (recapitulando)**:
    ```sql
    -- Uso de @@ERROR (legado)
    INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('ProductoA', 10.00, 100);
    IF @@ERROR <> 0
    BEGIN
        PRINT 'Hubo un error al insertar el productoA.';
    END;
    
    -- Uso de THROW (moderno, preferido)
    BEGIN TRY
        DECLARE @denominador INT = 0;
        IF @denominador = 0
            THROW 50001, 'No se puede dividir por cero. El denominador es nulo.', 1; -- 50001 es un número de error personalizado
        SELECT 10 / @denominador;
    END TRY
    BEGIN CATCH
        PRINT 'Error capturado con THROW: ' + ERROR_MESSAGE();
    END CATCH;
    ```