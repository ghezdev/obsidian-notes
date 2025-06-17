# **Triggers en SQL Server**

Un **Trigger** (o disparador) es un tipo especial de procedimiento almacenado que se ejecuta automáticamente cuando ocurre un evento específico en la base de datos. A diferencia de los procedimientos almacenados normales que se ejecutan explícitamente, los triggers son implícitamente invocados por el sistema de base de datos.

Los tipos más comunes son los **triggers DML** (Data Manipulation Language), que responden a eventos `INSERT`, `UPDATE` y `DELETE` en tablas. También existen **triggers DDL** (para `CREATE`, `ALTER`, `DROP` de objetos) y **triggers de inicio de sesión (LOGON triggers)**. Nos centraremos en los DML, que son los más utilizados.

---
# **Motivos para Utilizar Triggers**

Los triggers son valiosos para implementar y mantener la lógica de negocio y la integridad de los datos de forma automática:

1. **Auditoría y Registro**:
    - Registrar quién, cuándo y qué cambios se realizaron en los datos de una tabla (ej. registrar cada `INSERT`, `UPDATE` o `DELETE` en una tabla de log).
    - Mantener historiales de cambios en datos sensibles.
2. **Integridad Referencial Compleja**:
    - Implementar reglas de integridad referencial que no pueden ser manejadas por las restricciones `FOREIGN KEY` estándar. Por ejemplo, eliminaciones en cascada condicionales, o cuando la relación entre tablas es más compleja que una simple relación padre-hijo.
3. **Aplicación de Reglas de Negocio Complejas**:
    - Asegurar que los datos cumplen con reglas específicas que no pueden validarse con restricciones `CHECK` (ej. si el `Stock` de un producto baja de cierto nivel, crear una alerta en otra tabla o recalcular un `PrecioTotal` basado en múltiples factores en tiempo real).
    - Calcular y actualizar valores en otras tablas automáticamente cuando los datos en una tabla son modificados (ej. mantener el saldo de una cuenta bancaria al día cuando se registran transacciones).
4. **Sincronización de Datos y Replicación**:
    - Mantener copias de datos en diferentes tablas o incluso en diferentes bases de datos sincronizadas (aunque la replicación de SQL Server o ETL son a menudo mejores soluciones para escenarios de gran escala).
5. **Validación de Datos Avanzada**:
    - Realizar validaciones que requieren consultar otras tablas o aplicar lógica compleja antes de permitir un cambio.

---
# **Pseudotablas (`inserted` y `deleted`)**

Las **pseudotablas** son tablas lógicas temporales especiales que SQL Server crea y mantiene automáticamente durante la ejecución de un trigger DML. No son tablas reales en la base de datos, sino vistas en memoria que proporcionan una instantánea de los datos afectados por la operación DML.

- **`inserted`**:
    - Contiene copias de las filas **después** de una operación `INSERT` o `UPDATE`.
    - Para una operación `INSERT`, `inserted` contiene las filas que se acaban de insertar.
    - Para una operación `UPDATE`, `inserted` contiene los _nuevos valores_ de las filas que se están actualizando.
- **`deleted`**:
    - Contiene copias de las filas **antes** de una operación `DELETE` o `UPDATE`.
    - Para una operación `DELETE`, `deleted` contiene las filas que se acaban de eliminar.
    - Para una operación `UPDATE`, `deleted` contiene los _valores antiguos_ de las filas que se están actualizando.
- **Disponibilidad**:
    - **Trigger `AFTER INSERT`**: Solo la pseudotabla `inserted` está disponible.
    - **Trigger `AFTER DELETE`**: Solo la pseudotabla `deleted` está disponible.
    - **Trigger `AFTER UPDATE`**: Ambas pseudotablas (`inserted` y `deleted`) están disponibles, lo que permite comparar los valores antiguos con los nuevos.

**Nota Importante**: Los triggers se ejecutan para _cada sentencia_ DML, no para cada fila. Si una sentencia `INSERT` inserta 1000 filas, las pseudotablas `inserted` o `deleted` contendrán 1000 filas, no se ejecutará el trigger 1000 veces. Esto es crucial para escribir triggers eficientes que funcionen con conjuntos de datos.

---

### **Ejemplos de Triggers**

Usaremos las tablas `Productos` y `AuditoriaLog` definidas al inicio.

### **Ejemplo 1: `AFTER INSERT` (Trigger de Auditoría)**

- **Qué hace**: Registra un evento en `AuditoriaLog` cada vez que se inserta un nuevo producto en la tabla `Productos`.

```sql
CREATE TRIGGER trg_Productos_AfterInsert
ON Productos
AFTER INSERT
AS
BEGIN
    SET NOCOUNT ON; -- Evita que la sentencia INSERT subyacente interfiera con los mensajes del trigger

    INSERT INTO AuditoriaLog (TablaAfectada, TipoCambio, DetalleCambio)
    SELECT
        'Productos',
        'INSERT',
        'Nuevo producto insertado. ID: ' + CAST(i.ProductoID AS VARCHAR(10)) +
        ', Nombre: ' + i.Nombre +
        ', Precio: ' + CAST(i.Precio AS VARCHAR(20)) +
        ', Stock: ' + CAST(i.Stock AS VARCHAR(10))
    FROM inserted AS i; -- Accede a los datos de la fila insertada
END;
GO

-- Probar el trigger
INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Monitor Curvo', 350.00, 20);
INSERT INTO Productos (Nombre, Precio, Stock) VALUES ('Webcam HD', 70.00, 150);

SELECT * FROM AuditoriaLog; -- Deberías ver dos nuevas entradas de INSERT
```

### **Ejemplo 2: `AFTER UPDATE` (Trigger de Notificación/Alerta)**

- **Qué hace**: Si el stock de un producto se actualiza y baja de un cierto umbral (ej. 10 unidades), se registra una alerta en el log.

```sql
CREATE TRIGGER trg_Productos_AfterUpdate_StockBajo
ON Productos
AFTER UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    -- Solo actuamos si la columna Stock ha sido modificada y el nuevo stock es bajo
    IF UPDATE(Stock)
    BEGIN
        INSERT INTO AuditoriaLog (TablaAfectada, TipoCambio, DetalleCambio)
        SELECT
            'Productos',
            'ALERTA_STOCK_BAJO',
            'Alerta: El stock del producto "' + i.Nombre + '" (ID: ' + CAST(i.ProductoID AS VARCHAR(10)) +
            ') ha bajado a ' + CAST(i.Stock AS VARCHAR(10)) + ' (era ' + CAST(d.Stock AS VARCHAR(10)) + ').'
        FROM inserted AS i
        INNER JOIN deleted AS d ON i.ProductoID = d.ProductoID -- Unir inserted y deleted para comparar valores
        WHERE i.Stock <= 10 AND d.Stock > 10; -- Solo si baja del umbral
    END;
END;
GO

-- Probar el trigger
UPDATE Productos SET Stock = 8 WHERE Nombre = 'Laptop'; -- Debería activar la alerta
UPDATE Productos SET Stock = 5 WHERE Nombre = 'Mouse'; -- No debería activar si ya estaba por debajo o no cumple la condición d.Stock > 10
UPDATE Productos SET Stock = 15 WHERE Nombre = 'Teclado'; -- No debería activar (stock sube)
UPDATE Productos SET Precio = 80.00 WHERE Nombre = 'Teclado'; -- No debería activar (Stock no modificado)

SELECT * FROM Productos;
SELECT * FROM AuditoriaLog; -- Deberías ver la alerta de stock bajo para 'Laptop'
```

### **Ejemplo 3: `AFTER DELETE` (Trigger de Auditoría)**

- **Qué hace**: Registra un evento en `AuditoriaLog` cada vez que se elimina un producto.

```sql
CREATE TRIGGER trg_Productos_AfterDelete
ON Productos
AFTER DELETE
AS
BEGIN
    SET NOCOUNT ON;

    INSERT INTO AuditoriaLog (TablaAfectada, TipoCambio, DetalleCambio)
    SELECT
        'Productos',
        'DELETE',
        'Producto eliminado. ID: ' + CAST(d.ProductoID AS VARCHAR(10)) +
        ', Nombre: ' + d.Nombre +
        ', Precio: ' + CAST(d.Precio AS VARCHAR(20)) +
        ', Stock: ' + CAST(d.Stock AS VARCHAR(10))
    FROM deleted AS d; -- Accede a los datos de la fila eliminada
END;
GO

-- Probar el trigger
DELETE FROM Productos WHERE Nombre = 'Webcam HD';
DELETE FROM Productos WHERE Stock < 10; -- Eliminar la Laptop (ID 1, Stock 8)

SELECT * FROM Productos;
SELECT * FROM AuditoriaLog; -- Deberías ver las entradas de DELETE
```