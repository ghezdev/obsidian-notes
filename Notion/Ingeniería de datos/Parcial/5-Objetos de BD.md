# Objetos en una BD

- Esquemas
- Tablas 
- índices 
- Secuencias 
- Vistas 
- Sinónimos 
- Tablas temporales 
- Vistas materializadas 
- DBLinks 
- Store Procedures 
- Triggers 

- - - 
### Estructura

![[/image 3 6.png|image 3 6.png]]

- - -
# Esquemas

- Agrupación lógica de objetos
- Su implementación depende del motor
- Un nombre de objeto de BD debe ser único en cada esquema
- En SQL Server el esquema default es **dbo**
- En Oracle no existe el esquema como tal

- - -
# Tablas

- Objeto que funciona como contenedor de información
- Compuesta por filas y columnas

```sql 
 CREATE TABLE PARTIDOS (
    codCamp INT PRIMARY KEY, -- PK
    codClub INT,
    puntosObtenidos INT,
    descClub VARCHAR(200),
    fechaComienzo DATE,
    codClub1 INT,
    codClub2 INT,
    fechaPartido DATE NOT NULL,
    golesClub1 INT,
    golesClub2 INT,
    PRIMARY KEY (codCamp, codClub, codClub1, codClub2, fechaPartido), -- PK COMPUESTA
    FOREIGN KEY (codClub1) REFERENCES CLUBES(codClub),
    FOREIGN KEY (codClub2) REFERENCES CLUBES(codClub),
    UNIQUE (codCamp, codClub)
);
 ```

![[/image 4 5.png|image 4 5.png]]

- - -  
# Tipos de datos 

Los tipos de datos dependen del motor utilizado, algunos de sql server son

![[/image 5 4.png|image 5 4.png]]

- - -  
# Tablas - Constraints

- Integridad de Dominio 
- Integridad de Entidad 
- Integridad Referencial 

- Tipos de datos
- Obligatoriedad
- Checks
- Default
- PKs, UKs
- Claves foráneas

## Constraint - Tipos de datos y obligatoriedad

![[/image 6 4.png|image 6 4.png]]

## Constraint - Check

![[/image 7 4.png|image 7 4.png]]

## Constraint - Default

![[/image 8 3.png|image 8 3.png]]

## Constraint - Primary key

- Corresponde a la clave primaria
- Identifica unívocamente cada fila
- Puede ser simple o compuesta
- Sólo puede haber una en cada tabla
- No pueden contener valores nulos

## Constraint - Unique

- Corresponde a las claves alternativas o secundarias
- Identifica unívocamente cada fila
- Puede ser simple o compuesta
- Puede haber más de una en cada tabla
- Puede contener valores nulos

![[/image 9 3.png|image 9 3.png]]

## Constraint - Foreign key

- Atributos que hacen referencia a una clave de otra tabla
- Puede ser simple o compuesta
- Pueden haber varias en cada tabla
- Representan relaciones entre tablas

![[/image 10 3.png|image 10 3.png]]

- - -
# Operador ALTER

- Se utiliza para modificar objetos
- En el caso de las tablas se puede utilizar para agregar, modificar o borrar columnas y/o constraints  

![[/image 11 3.png|image 11 3.png]]

- - -  
# Operador DROP

- Se utiliza para borrar objetos de la BD
- Una vez borrados no se pueden recuperar

![[/image 12 3.png|image 12 3.png]]

- - -
# Índices

- **Qué hacen**: Los índices son estructuras de datos especiales que se crean en las tablas de la base de datos para **mejorar la velocidad de recuperación de datos** en las consultas. Funcionan de manera similar al índice de un libro: en lugar de leer todo el libro para encontrar un tema, vas al índice, encuentras la página y vas directamente a ella.
    
- **Tipos de Índices:**
    
    - **Índice Clúster (Clustered Index)**:
        
        - **Qué hace**: Define el **orden físico de almacenamiento** de las filas de datos en la tabla. La tabla misma _es_ el índice clúster; los datos se almacenan en los nodos hoja del índice.
        - **Características**: Solo puede haber **uno por tabla** porque las filas no pueden tener más de un orden físico. La clave primaria de una tabla suele ser el índice clúster por defecto.
        - **Ventajas**: Muy rápido para búsquedas de rango y para recuperar todas las columnas de una fila, ya que los datos están físicamente ordenados.
        - **Desventajas**: La inserción de nuevas filas o la actualización de la clave del índice puede ser costosa si requiere reordenar físicamente los datos.
    - **Índice No Clúster (Non-Clustered Index)**:
        
        - **Qué hace**: Es una estructura de datos **separada** de los datos de la tabla. Contiene los valores de las columnas indexadas y un puntero (un localizador de fila o la clave del índice clúster) a la fila de datos real en la tabla.
        - **Características**: Una tabla puede tener **múltiples índices no clúster**.
        - **Ventajas**: Excelente para búsquedas rápidas en las columnas indexadas y para soportar la unicidad de valores (UNIQUE constraints).
        - **Desventajas**: Requiere espacio de almacenamiento adicional. Las consultas que necesitan todas las columnas de una fila pueden requerir una operación adicional de "lookup" a la tabla real (o al índice clúster) si la columna no está incluida en el índice no clúster (covered index).
- **Estructura Física de Índices (Árbol B - B-Tree)**:
    
    - La mayoría de los índices en SQL Server se implementan como **árboles B** (B-Trees). Esta estructura jerárquica permite búsquedas, inserciones y eliminaciones eficientes.
    - **Nodos Raíz**: El nodo superior del árbol.
    - **Nodos Intermedios**: Contienen valores clave y punteros a los siguientes niveles del árbol.
    - **Nodos Hoja**: Contienen las claves de índice reales y los punteros a las filas de datos (en índices no clúster) o los datos reales de la fila (en índices clúster). Los nodos hoja están enlazados para permitir escaneos de rango eficientes.
- **Ventajas y Desventajas de los Índices**:
    
    - **Ventajas**:
        
        - **Mejora el rendimiento de las consultas `SELECT`**: Especialmente para búsquedas (`WHERE`), ordenación (`ORDER BY`) y uniones (`JOIN`).
        - **Acelera la aplicación de restricciones `UNIQUE` y `PRIMARY KEY`**: Los índices subyacentes son usados para asegurar la unicidad.
    - **Desventajas**:
        
        - **Coste en operaciones DML (`INSERT`, `UPDATE`, `DELETE`)**: Cada vez que se modifican los datos en la tabla, el índice también debe ser actualizado, lo que añade sobrecarga.
        - **Requieren espacio de almacenamiento adicional**: Los índices son estructuras de datos que ocupan espacio en disco.
        - **Riesgo de uso incorrecto**: Demasiados índices o índices mal diseñados pueden perjudicar el rendimiento general en lugar de mejorarlo.

**Ejemplo de Creación de Índices:**

```sql
-- Tabla de ejemplo
CREATE TABLE Empleados (
    EmpleadoID INT PRIMARY KEY, -- Esto crea un índice clúster automáticamente
    Nombre VARCHAR(100),
    DepartamentoID INT,
    Salario DECIMAL(10, 2)
);

-- Crear un índice no clúster en la columna DepartamentoID para búsquedas rápidas por departamento
CREATE NONCLUSTERED INDEX IX_Empleados_DepartamentoID
ON Empleados (DepartamentoID);

-- Crear un índice no clúster en el Nombre para búsquedas alfabéticas rápidas
CREATE NONCLUSTERED INDEX IX_Empleados_Nombre
ON Empleados (Nombre);
```

---
# Secuencias

- **Qué hacen**: Una secuencia es un objeto de base de datos que genera números secuenciales (enteros) únicos en un orden predefinido (ascendente o descendente) a partir de un valor inicial y con un incremento específico. A diferencia de `IDENTITY`, las secuencias son **independientes de las tablas**.
    
- **Características**:
    
    - Puede ser utilizada por múltiples tablas.
    - Los valores de la secuencia no se revierte si una transacción que los utiliza hace `ROLLBACK`.
    - Puede tener valores máximos/mínimos, ciclos (reiniciar la secuencia) y cacheo de valores.

**Ejemplo de Secuencia:**

```sql
-- Crear una secuencia que empieza en 1000 y se incrementa en 1
CREATE SEQUENCE sq_NumeroPedido
    START WITH 1000
    INCREMENT BY 1
    MINVALUE 1000
    NO MAXVALUE -- No tiene un valor máximo definido
    CACHE 10; -- Almacena 10 valores en memoria para un acceso más rápido

-- Obtener el siguiente valor de la secuencia
SELECT NEXT VALUE FOR sq_NumeroPedido; -- 1000
SELECT NEXT VALUE FOR sq_NumeroPedido; -- 1001

-- Usar la secuencia al insertar datos en una tabla
CREATE TABLE Pedidos (
    PedidoID INT PRIMARY KEY DEFAULT NEXT VALUE FOR sq_NumeroPedido, -- Usar secuencia como default
    ClienteID INT,
    FechaPedido DATE
);

INSERT INTO Pedidos (ClienteID, FechaPedido) VALUES (10, GETDATE());
INSERT INTO Pedidos (ClienteID, FechaPedido) VALUES (20, GETDATE());

SELECT * FROM Pedidos; -- PedidoID será 1002, 1003
```

---
# Diferencias entre Secuencias e IDENTITYs

| Característica             | `IDENTITY`                                                                                | `SEQUENCE`                                                                                       |
| :------------------------- | :---------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------- |
| **Ámbito**                 | Genera números para una **columna específica** en **una sola tabla**.                     | Genera números de forma **independiente de la tabla**. Puede ser utilizada por múltiples tablas. |
| **Control de transacción** | Los valores generados se revierten si la transacción hace `ROLLBACK`.                     | Los valores generados **no se revierten** si la transacción hace `ROLLBACK` (se "pierden").      |
| **Uso**                    | Se define directamente en la columna de la tabla (`[col] INT IDENTITY(seed, increment)`). | Es un objeto de esquema independiente que se referencia (`NEXT VALUE FOR sequence_name`).        |
| **Reiniciabilidad**        | Se reinicia usando `DBCC CHECKIDENT` (lo cual es delicado).                               | Se reinicia alterando la secuencia o recreándola.                                                |
| **Brechas**                | Pueden tener brechas si hay `ROLLBACK`s o eliminaciones.                                  | Más propensas a brechas si hay `ROLLBACK`s o si se usa `CACHE`.                                  |
| **Portabilidad**           | Sintaxis específica de SQL Server.                                                        | Más estándar SQL (`CREATE SEQUENCE`), aunque la implementación puede variar.                     |

- **Cuándo usar `IDENTITY`**: Cuando necesitas un número único y autoincremental para la clave primaria de una sola tabla y te preocupan menos las brechas exactas o si la numeración es estrictamente secuencial sin reusar números en caso de rollback.
- **Cuándo usar `SEQUENCE`**: Cuando necesitas una fuente de números únicos para múltiples tablas (ej. un mismo rango de números para pedidos y facturas) o cuando necesitas más control sobre el inicio, incremento y ciclo de la serie numérica.

---
# Vistas

- **Qué hacen**: Una vista es una **tabla virtual** basada en el resultado de una consulta `SELECT`. No almacena datos por sí misma; en cambio, cuando consultas una vista, la base de datos ejecuta la consulta subyacente y presenta el conjunto de resultados como si fuera una tabla.
    
- **Características de Vistas**:
    
    - **Abstracción y Simplificación**: Simplifican consultas complejas. Puedes ocultar la complejidad de uniones y cálculos, presentando solo los datos relevantes.
    - **Seguridad**: Puedes restringir el acceso a ciertas columnas o filas, o permitir que los usuarios vean datos sin darles acceso directo a las tablas base.
    - **Consistencia**: Presentan una visión consistente de los datos, incluso si la estructura de las tablas subyacentes cambia (mientras la definición de la vista sea válida).
    - **Mantenimiento**: Si la estructura de la tabla base cambia, la vista puede necesitar ser actualizada.
    - **Actualizabilidad (limitada)**: Algunas vistas pueden ser utilizadas para operaciones `INSERT`, `UPDATE` o `DELETE` si cumplen ciertas condiciones (ej. se basan en una única tabla, no usan `GROUP BY`, `DISTINCT`, etc.).

**Ejemplo de Vista:**

```sql
-- Crear una vista para ver solo los detalles de los productos con stock bajo
CREATE VIEW vw_ProductosConPocoStock AS
SELECT ProductoID, Nombre, Stock
FROM Productos
WHERE Stock < 50;

-- Consultar la vista como si fuera una tabla
SELECT * FROM vw_ProductosConPocoStock;

-- Si la vista es actualizable (ej. basada en una sola tabla y sin agregados)
-- UPDATE vw_ProductosConPocoStock SET Stock = 60 WHERE ProductoID = 1;
```

---

# Vistas Materializadas (o Vistas Indexadas en SQL Server)

- **Qué hacen**: En SQL Server, una "vista materializada" se implementa como una **Vista Indexada**. A diferencia de las vistas estándar, el conjunto de resultados de una vista indexada **se almacena físicamente en el disco** (se "materializa") y se mantiene actualizado por el motor de base de datos a medida que cambian los datos de las tablas subyacentes.
- **Ventajas**:
    - **Rendimiento en `SELECT`**: Las consultas que utilizan vistas indexadas pueden ser mucho más rápidas porque no necesitan ejecutar la consulta subyacente en cada uso; los datos ya están pre-calculados y almacenados.
    - **Pre-cálculo de Agregados**: Ideales para consultas que implican agregaciones (`SUM`, `COUNT`, `AVG`) sobre grandes conjuntos de datos.
- **Desventajas**:
    - **Coste en DML**: Las operaciones `INSERT`, `UPDATE`, `DELETE` en las tablas base incurren en una sobrecarga adicional, ya que el motor debe mantener la vista indexada actualizada también.
    - **Requiere más espacio de almacenamiento**.
    - **Restricciones**: Las vistas indexadas tienen requisitos estrictos (ej. deben usar `WITH SCHEMABINDING`, no pueden usar `OUTER JOIN`, etc.).
    - **Mantenimiento**: Necesitan reconstruirse si la definición cambia.

**Ejemplo de Vista Indexada (Materializada):**

```sql
-- Crear una tabla para el ejemplo de vista indexada
CREATE TABLE Ventas (
    VentaID INT PRIMARY KEY IDENTITY,
    ProductoID INT,
    Cantidad INT,
    PrecioUnitario DECIMAL(10,2),
    FechaVenta DATE
);
INSERT INTO Ventas (ProductoID, Cantidad, PrecioUnitario, FechaVenta) VALUES
(1, 5, 10.00, '2024-01-01'),
(2, 2, 25.00, '2024-01-01'),
(1, 3, 10.00, '2024-01-02');

-- Crear una vista con SCHEMABINDING (requerido para índices)
CREATE VIEW vw_TotalVentasPorProducto
WITH SCHEMABINDING
AS
SELECT
    ProductoID,
    COUNT_BIG(*) AS TotalVentas, -- COUNT_BIG() es necesario para vistas indexadas
    SUM(Cantidad * PrecioUnitario) AS IngresoTotal
FROM dbo.Ventas -- dbo. prefijo de esquema es necesario con SCHEMABINDING
GROUP BY ProductoID;
GO

-- Crear un índice clúster único en la vista (esto la materializa)
CREATE UNIQUE CLUSTERED INDEX IX_vw_TotalVentasPorProducto_ProductoID
ON vw_TotalVentasPorProducto (ProductoID);
GO

-- Consultar la vista (ahora los resultados están pre-calculados)
SELECT * FROM vw_TotalVentasPorProducto;

-- Limpiar
DROP VIEW vw_TotalVentasPorProducto;
DROP TABLE Ventas;
```

---
# Sinónimos

- **Qué hacen**: Un sinónimo es un objeto de base de datos que proporciona un **nombre alternativo (alias)** para otro objeto de base de datos (tablas, vistas, procedimientos almacenados, funciones, etc.). Pueden referirse a objetos locales o remotos (en servidores enlazados).
- **Ventajas**:
    - **Simplificación de código**: Acorta nombres de objetos largos o complejos.
    - **Abstracción de la ubicación**: Si un objeto se mueve o su nombre cambia, solo necesitas actualizar el sinónimo, no todas las aplicaciones que lo referencian.
    - **Seguridad (limitada)**: Oculta el nombre real y la ubicación del objeto subyacente.
- **Características**: No almacenan datos ni tienen propiedades de seguridad propias; los permisos se basan en el objeto subyacente.

**Ejemplo de Sinónimo:**

```sql
-- Suponiendo que tienes una tabla llamada 'dbo.ClientesActuales'
-- y quieres un nombre más corto o abstracto.

CREATE SYNONYM CLIE FOR dbo.ClientesActuales;

-- Ahora puedes usar el sinónimo
SELECT * FROM CLIE;

-- Si 'dbo.ClientesActuales' se moviera a 'dbo.ClientesHistoricos',
-- solo tendrías que cambiar la definición del sinónimo:
-- ALTER SYNONYM CLIE FOR dbo.ClientesHistoricos;
-- Y el código de aplicación que usa 'CLIE' seguiría funcionando.

-- Limpiar
-- DROP SYNONYM CLIE;
```

---
# Tablas Temporales

- **Qué hacen**: Las tablas temporales son tablas especiales que se crean y existen solo por la **duración de una sesión o el alcance de un procedimiento almacenado/función**. Son útiles para almacenar conjuntos de datos intermedios en una consulta o script complejo.
    
- **Tipos en SQL Server**:
    
    - **Tablas Temporales Locales (`#nombre_tabla`)**:
        
        - **Ámbito**: Son visibles solo para la **sesión actual** que las creó.
        - **Eliminación**: Se eliminan automáticamente cuando la sesión que las creó finaliza.
        - **Uso**: Comúnmente usadas dentro de procedimientos almacenados o scripts para almacenar datos intermedios que no necesitan ser compartidos entre sesiones.
    - **Tablas Temporales Globales (`##nombre_tabla`)**:
        
        - **Ámbito**: Son visibles para **todas las sesiones** conectadas a la instancia de SQL Server.
        - **Eliminación**: Se eliminan automáticamente cuando la _última sesión_ que las está referenciando se desconecta.
        - **Uso**: Menos comunes; usadas cuando múltiples sesiones necesitan compartir temporalmente los mismos datos.

**Ejemplo de Tablas Temporales:**

```sql
-- Crear una tabla temporal local
CREATE TABLE #EmpleadosActivos (
    ID INT,
    Nombre VARCHAR(100),
    Departamento VARCHAR(50)
);

-- Insertar datos en la tabla temporal
INSERT INTO #EmpleadosActivos (ID, Nombre, Departamento) VALUES
(1, 'Ana', 'Ventas'),
(2, 'Luis', 'Marketing');

-- Consultar la tabla temporal
SELECT * FROM #EmpleadosActivos;

-- Crear una tabla temporal global (visible para otras sesiones también)
CREATE TABLE ##ReporteGlobal (
    FechaReporte DATE,
    TotalVentas INT
);

INSERT INTO ##ReporteGlobal VALUES (GETDATE(), 12345);
SELECT * FROM ##ReporteGlobal;

-- Nota: Las tablas temporales se eliminan automáticamente al finalizar la sesión.
-- También puedes eliminarlas explícitamente:
-- DROP TABLE #EmpleadosActivos;
-- DROP TABLE ##ReporteGlobal;
```

---
# DB Links (Linked Servers en SQL Server)

- **Qué hacen**: En SQL Server, el concepto de "DB Links" se implementa a través de **Servidores Enlazados (Linked Servers)**. Permiten a una instancia de SQL Server (el "servidor local") ejecutar comandos distribuidos contra otra instancia de SQL Server o contra otras fuentes de datos OLE DB (ej. Oracle, MySQL, Excel, Access, etc.).
- **Ventajas**:
    - **Consultas distribuidas**: Puedes unir tablas de diferentes bases de datos en diferentes servidores en una sola consulta.
    - **Ejecución remota de procedimientos**: Invocar procedimientos almacenados en servidores remotos.
    - **Integración de datos**: Consolidar o transferir datos entre sistemas heterogéneos.
- **Funcionamiento**: Necesitas configurar una conexión (Linked Server) especificando el tipo de proveedor (ej. SQL Server Native Client, Microsoft OLE DB Provider for Oracle), las credenciales de conexión y el nombre del servidor remoto.

**Ejemplo de Servidor Enlazado (Linked Server):**

```sql
-- Paso 1: Configurar un servidor enlazado
-- NOTA: Esto requiere permisos de administración y un servidor remoto disponible
-- Reemplaza 'NOMBRE_SERVIDOR_REMOTO' con el nombre real o IP del servidor remoto
-- Reemplaza 'NOMBRE_DB_REMOTO' con el nombre de la base de datos remota
-- Reemplaza 'UsuarioRemoto' y 'ContraseñaRemota' con credenciales válidas

EXEC sp_addlinkedserver
    @server = N'MiServidorRemoto',
    @srvproduct = N'', -- Vacío para SQL Server
    @provider = N'SQLNCLI11', -- Proveedor OLE DB para SQL Server (puede variar según la versión)
    @datasrc = N'NOMBRE_SERVIDOR_REMOTO'; -- Nombre del servidor o IP

EXEC sp_addlinkedsrvlogin
    @rmtsrvname = N'MiServidorRemoto',
    @useself = N'False',
    @locallogin = N'sa', -- Tu login local (ej. 'sa' o 'tu_usuario_admin')
    @rmtuser = N'UsuarioRemoto', -- Usuario en el servidor remoto
    @rmtpassword = N'ContraseñaRemota'; -- Contraseña en el servidor remoto
GO

-- Paso 2: Consultar una tabla en el servidor enlazado (consulta distribuida)
-- Formato: [NombreServidorEnlazado].[NombreBaseDeDatos].[Esquema].[NombreTabla]
SELECT TOP 10 *
FROM MiServidorRemoto.NOMBRE_DB_REMOTO.dbo.TablaDeClientesRemota;

-- Paso 3: Ejecutar un procedimiento almacenado en el servidor enlazado
EXEC MiServidorRemoto.NOMBRE_DB_REMOTO.dbo.sp_ActualizarReporte;

-- Limpiar (eliminar el servidor enlazado cuando ya no se necesite)
-- EXEC sp_dropserver N'MiServidorRemoto', 'droplogins';
```