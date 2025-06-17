# **DDL (Data Definition Language - Lenguaje de Definición de Datos)**

- **Qué hace**: Los comandos DDL se utilizan para **definir y modificar la estructura de los objetos de la base de datos** (como tablas, bases de datos, índices, vistas, funciones, procedimientos almacenados, etc.). Las operaciones DDL suelen ser transacciones implícitas (autocommit) y no son reversibles con un simple `ROLLBACK` a menos que se ejecuten dentro de una transacción explícita.

## CREATE

- **Qué hace**: Se utiliza para **crear nuevos objetos** dentro de la base de datos.
- **Ejemplo**: Crear una tabla.
    ```sql
    -- Ejemplo de CREATE TABLE (ya definida arriba, pero aquí está el concepto)
    CREATE TABLE Empleados (
        EmpleadoID INT PRIMARY KEY,
        Nombre VARCHAR(100) NOT NULL,
        Salario DECIMAL(10, 2),
        FechaContratacion DATE
    );
    -- Este comando crearía una nueva tabla llamada 'Empleados'.
    ```


## ALTER

- **Qué hace**: Se utiliza para **modificar la estructura** de un objeto existente de la base de datos.
- **Ejemplo**: Añadir una nueva columna a la tabla `Empleados`.
    ```sql
    ALTER TABLE Empleados
    ADD DepartamentoID INT;
    -- Este comando añade la columna 'DepartamentoID' a la tabla 'Empleados'.
    
    -- También se puede usar para modificar columnas existentes:
    ALTER TABLE Empleados
    ALTER COLUMN Nombre VARCHAR(150); -- Cambia la longitud de la columna Nombre
    ```


## DROP

- **Qué hace**: Se utiliza para **eliminar completamente** un objeto de la base de datos (una tabla, base de datos, vista, etc.). Esto elimina tanto la estructura como todos los datos contenidos.
- **Ejemplo**: Eliminar la tabla `Empleados`.
    ```sql
    DROP TABLE Empleados;
    -- Este comando eliminaría la tabla 'Empleados' y todos sus datos de forma permanente.
    ```
    

## TRUNCATE

- **Qué hace**: Se utiliza para **eliminar rápidamente TODAS las filas** de una tabla. Es más rápido y utiliza menos recursos de log que `DELETE` sin una cláusula `WHERE` para borrar todas las filas, porque no elimina las filas una por una. También **reinicia los contadores de identidad (IDENTITY)** a su valor inicial. Es una operación DDL.
- **Ejemplo**: Vaciar la tabla `Productos`.
    ```sql
    INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Libro', 25.00, 100);
    INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Bolígrafo', 1.50, 500);
    
    SELECT * FROM Productos; -- Mostrará 2 filas
    
    TRUNCATE TABLE Productos; -- Elimina todas las filas y reinicia IDENTITY
    
    SELECT * FROM Productos; -- Mostrará 0 filas
    INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Cuaderno', 5.00, 200);
    SELECT * FROM Productos; -- Si ProductoID era IDENTITY, el nuevo ID será 1 de nuevo.
    ```
    
- **Diferencia con `DELETE` sin `WHERE`**:
    - **`TRUNCATE`**: DDL, más rápido para borrar todo, reinicia `IDENTITY`, menos log, no se puede usar con `WHERE`, no activa triggers de DELETE.
    - **`DELETE`**: DML, más lento (logea cada fila), no reinicia `IDENTITY` automáticamente, más log, se puede usar con `WHERE`, activa triggers de DELETE.


---
#  DML (Data Manipulation Language - Lenguaje de Manipulación de Datos)

- **Qué hace**: Los comandos DML se utilizan para **manipular los datos** dentro de los objetos de la base de datos (insertar, actualizar, eliminar, consultar datos). Las operaciones DML son transaccionales y pueden ser revertidas (`ROLLBACK`).

## INSERT

- **Qué hace**: Añadir una o más filas nuevas a una tabla.
    
- **`INSERT` sin Subqueries**:
    
    - **Explicación**: Se insertan valores específicos directamente en las columnas.
    - **Ejemplo**:
        ```sql
        -- Insertar una sola fila especificando columnas y valores
        INSERT INTO Productos (Nombre, Precio, Stock)
        VALUES ('Teclado', 75.99, 50);
        
        -- Insertar una sola fila sin especificar columnas (todos los valores deben estar en orden y coincidir)
        -- Peligroso si la estructura de la tabla cambia
        -- INSERT INTO Productos VALUES (DEFAULT, 'Monitor', 199.99, 30); -- DEFAULT para IDENTITY
        
        SELECT * FROM Productos;
        ```
        
- **`INSERT` con Subqueries**:
    
    - **Explicación**: Inserta filas en una tabla copiando datos de otra tabla (o del resultado de una consulta).
    - **Ejemplo**: Suponiendo que tenemos una tabla `ProductosPromocion` y queremos copiar algunos a `Productos`.
        ```sql
        -- Crear una tabla temporal para el ejemplo de subquery
        CREATE TABLE ProductosPromocion (
            PromoProductoID INT,
            NombrePromo VARCHAR(100),
            PrecioPromo DECIMAL(10,2)
        );
        
        INSERT INTO ProductosPromocion (PromoProductoID, NombrePromo, PrecioPromo)
        VALUES (10, 'Auriculares', 49.99), (11, 'Webcam', 29.99);
        
        -- Insertar productos de promoción en la tabla Productos con stock inicial de 10
        INSERT INTO Productos (Nombre, Precio, Stock)
        SELECT NombrePromo, PrecioPromo, 10 -- Stock fijo de 10 para los productos promocionales
        FROM ProductosPromocion
        WHERE PrecioPromo < 50.00; -- Solo los de bajo precio
        
        SELECT * FROM Productos;
        DROP TABLE ProductosPromocion; -- Limpiar tabla temporal
        ```
        

## UPDATE

- **Qué hace**: Modificar datos existentes en una o más filas de una tabla.
    
- **`UPDATE` sin Subqueries**:
    
    - **Explicación**: Se actualizan los valores de columnas para las filas que cumplen una condición `WHERE`.
    - **Ejemplo**:
        ```SQL
        -- Aumentar el stock de 'Teclado'
        UPDATE Productos
        SET Stock = Stock + 10
        WHERE Nombre = 'Teclado';
        
        -- Poner en NULL el precio de productos con stock cero
        UPDATE Productos
        SET Precio = NULL
        WHERE Stock = 0;
        
        SELECT * FROM Productos;
        ```
        
- **`UPDATE` con Subqueries**:
    
    - **Explicación**: Se actualizan valores basándose en el resultado de una subconsulta, a menudo relacionada con datos de otra tabla.
    - **Ejemplo (actualización basada en otra tabla usando `FROM`)**:
        ```sql
        -- Suponiendo que tenemos una tabla de 'UltimosPreciosProveedores'
        CREATE TABLE UltimosPreciosProveedores (
            ProductoID_Ref INT,
            NuevoPrecio DECIMAL(10,2)
        );
        INSERT INTO UltimosPreciosProveedores VALUES (1, 70.00), (2, 45.00); -- Asumiendo ProductoID 1 y 2 existen
        
        -- Actualizar el precio de productos en base a la tabla de proveedores
        UPDATE P
        SET Precio = UPP.NuevoPrecio
        FROM Productos AS P
        INNER JOIN UltimosPreciosProveedores AS UPP
            ON P.ProductoID = UPP.ProductoID_Ref;
        
        SELECT * FROM Productos;
        DROP TABLE UltimosPreciosProveedores; -- Limpiar tabla temporal
        ```
        
    - **Ejemplo (actualización de una columna con un valor de subconsulta escalar)**:
        ```sql
        -- Actualizar el stock de un producto si su precio está por debajo del promedio de todos los productos
        UPDATE Productos
        SET Stock = Stock - 5 -- Descontar 5 unidades
        WHERE Precio < (SELECT AVG(Precio) FROM Productos WHERE Precio IS NOT NULL);
        
        SELECT * FROM Productos;
        ```
        

## DELETE

- **Qué hace**: Eliminar una o más filas existentes de una tabla.
    
- **`DELETE` sin Subqueries**:
    
    - **Explicación**: Se eliminan filas que cumplen una condición `WHERE`. Si no se especifica `WHERE`, se eliminan todas las filas (similar a `TRUNCATE` pero con las diferencias mencionadas).
    - **Ejemplo**:
        ```sql
        -- Eliminar productos con stock cero
        DELETE FROM Productos
        WHERE Stock = 0;
        
        -- Eliminar el producto 'Bolígrafo'
        DELETE FROM Productos
        WHERE Nombre = 'Bolígrafo';
        
        SELECT * FROM Productos;
        ```
        
- **`DELETE` con Subqueries**:
    
    - **Explicación**: Se eliminan filas basándose en la existencia o no existencia de datos relacionados en otra tabla o el resultado de una subconsulta.
    - **Ejemplo**: Eliminar productos que nunca han sido vendidos (asumiendo una tabla `Ventas` con `ProductoID`).
        ```sql
        -- Crear una tabla temporal para el ejemplo
        CREATE TABLE Ventas (
            VentaID INT PRIMARY KEY,
            ProductoID INT,
            Cantidad INT
        );
        INSERT INTO Ventas VALUES (1, 1, 10), (2, 3, 5); -- Venta de ProductoID 1 y 3 (Teclado y Cuaderno, si existen)
        
        -- Insertar un producto que no ha sido vendido
        INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Ratón', 19.99, 80);
        
        -- Eliminar productos que no tienen ventas registradas
        DELETE FROM Productos
        WHERE ProductoID NOT IN (SELECT ProductoID FROM Ventas);
        
        SELECT * FROM Productos;
        DROP TABLE Ventas; -- Limpiar tabla temporal
        ```
        

## MERGE

- **Qué hace**: Realiza operaciones de `INSERT`, `UPDATE` y `DELETE` en una tabla de destino basándose en las diferencias entre ella y una tabla de origen. Es ideal para sincronizar datos entre dos tablas (por ejemplo, para cargar datos incrementalmente en un data warehouse).
    
- **Sintaxis básica**: `MERGE INTO destino USING origen ON (condición) WHEN MATCHED THEN UPDATE/DELETE WHEN NOT MATCHED BY TARGET THEN INSERT WHEN NOT MATCHED BY SOURCE THEN DELETE;`
    
- **Ejemplo**: Sincronizar la tabla `DestinoClientes` con los datos de `OrigenClientes`.
    ```sql
    -- Insertar datos iniciales en la tabla de destino
    INSERT INTO DestinoClientes (ClienteID, Nombre, Email) VALUES
    (1, 'Alice', 'alice@example.com'),
    (2, 'Bob', 'bob@example.com'),
    (3, 'Charlie', 'charlie@example.com');
    
    -- Insertar/actualizar/eliminar datos en la tabla de origen
    INSERT INTO OrigenClientes (ClienteID, Nombre, Email) VALUES
    (1, 'Alice', 'alice_new@example.com'), -- Alice tiene email actualizado
    (2, 'Bob', 'bob@example.com'),           -- Bob no cambia
    (4, 'David', 'david@example.com');     -- Nuevo cliente David
    -- (Charlie, ID 3, no está en OrigenClientes, debe ser eliminado del destino)
    
    MERGE DestinoClientes AS TARGET
    USING OrigenClientes AS SOURCE
    ON (TARGET.ClienteID = SOURCE.ClienteID)
    WHEN MATCHED THEN
        -- Si hay coincidencia y el email o nombre es diferente, actualizar
        UPDATE SET TARGET.Nombre = SOURCE.Nombre,
                   TARGET.Email = SOURCE.Email,
                   TARGET.UltimaActualizacion = GETDATE()
    WHEN NOT MATCHED BY TARGET THEN
        -- Si hay una fila en SOURCE que no está en TARGET, insertarla
        INSERT (ClienteID, Nombre, Email)
        VALUES (SOURCE.ClienteID, SOURCE.Nombre, SOURCE.Email)
    WHEN NOT MATCHED BY SOURCE THEN
        -- Si hay una fila en TARGET que no está en SOURCE, eliminarla
        DELETE;
    
    SELECT * FROM DestinoClientes ORDER BY ClienteID;
    ```
    
- **Resultado de `DestinoClientes` después del `MERGE`**: 
  | ClienteID | Nombre | Email | UltimaActualizacion | 
  | :-------- | :------ | :------------------ | :---------------------- | 
  | 1 | Alice | alice_new@example.com | (Fecha/Hora Actual) | 
  | 2 | Bob | bob@example.com | (Fecha/Hora Original) | 
  | 4 | David | david@example.com | (Fecha/Hora Actual) | 
  
  _(Charlie fue eliminado. Alice fue actualizada. David fue insertado. Bob no se tocó.)_