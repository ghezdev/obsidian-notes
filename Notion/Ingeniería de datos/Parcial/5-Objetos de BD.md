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

Es una estructura de datos que permite acceder más rápidamente a la datos de las tablas

- Asociado a una tabla. 
- No produce acoplamiento. 
- Tabla independiente del índice. 
- Diferentes tipos. 
- Algunos se crean en forma implícita.

***Clasificación por tipo*** 
- Único o Duplicado 
- Simple o Compuesto

- Único: No puede estar repetido.
- Duplicado: Puede contener valores repetidos. 
- Simple: Conformado por un solo atributo. 
- Compuesto: Formado por varios atributos.

***Tipos según su estructura física*** 
- Btree, Btree+ 
- Cluster 
- Hash
- Bitmap

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

- - -
# Preguntas Indices

### 1. Tipos de Índices (Conceptos Generales)

Los índices en bases de datos son estructuras especiales de búsqueda que mejoran la velocidad de las operaciones de recuperación de datos en una tabla. Son análogos a un índice en un libro: en lugar de leer el libro completo, vas al índice para encontrar rápidamente la página con la información que buscas.

Los tipos de índices se pueden clasificar de varias maneras, pero las principales son:

- **Índices de columna única:** Se crean sobre una sola columna de una tabla.
- **Índices compuestos (o concatenados):** Se crean sobre dos o más columnas de una tabla. El orden de las columnas en el índice es importante para su eficiencia.

Además, por su naturaleza y la forma en que se gestionan, se pueden distinguir:

- **Índices únicos (Unique Indexes):** Garantizan que todos los valores en la columna (o combinación de columnas, si es compuesto) sean únicos. Esto se usa comúnmente para aplicar restricciones de clave primaria o clave única.
- **Índices no únicos (Non-Unique Indexes):** Permiten valores duplicados en la columna (o combinación de columnas) indexada. Se usan para acelerar búsquedas en columnas con valores repetidos.

---

### 2. Tipos de Índice Según su Organización Física (Almacenamiento de Datos)

Aquí es donde entran las clasificaciones más importantes sobre cómo el índice almacena y organiza los datos en el disco. Los dos tipos principales son:

- **Índices Clúster (Clustered Indexes):**
    - Determinan el **orden físico** en que se almacenan las filas de datos en el disco.
    - Una tabla solo puede tener **un índice clúster** porque las filas solo pueden ser ordenadas físicamente de una manera.
    - Contienen las **filas de datos completas** en sus nodos hoja.
    - Son muy eficientes para rangos de búsqueda (`BETWEEN`, `>` , `<`) y para recuperar todas las columnas de una fila, ya que los datos ya están ordenados.
        
- **Índices No Clúster (Non-Clustered Indexes):**
    - No afectan el orden físico de las filas de datos en el disco. Las filas de datos permanecen en su orden original o en el orden dictado por un índice clúster.
    - Una tabla puede tener **múltiples índices no clúster** (cientos en teoría, aunque en la práctica se limita para no impactar el rendimiento de inserciones/actualizaciones).
    - Contienen **punteros** (o la clave clúster, si existe) a la ubicación física de las filas de datos reales. No contienen los datos completos.
    - Son útiles para búsquedas rápidas en columnas específicas, pero si se necesitan todas las columnas de la fila, el sistema debe realizar una búsqueda adicional (un "bookmark lookup" o "key lookup") usando el puntero para ir a la ubicación real de los datos.
        

---

### 3. Diferencias entre Índice Clúster y No Clúster

|Característica|Índice Clúster|Índice No Clúster|
|---|---|---|
|**Organización Física**|Define el orden físico de almacenamiento de los datos.|No define el orden físico; los datos se almacenan de forma independiente.|
|**Cantidad por Tabla**|Solo puede haber **uno** por tabla.|Puede haber **múltiples** por tabla.|
|**Contenido del Nodo Hoja**|Contiene las **filas de datos completas** de la tabla.|Contiene los valores de las columnas indexadas y **punteros** a las filas de datos (o la clave clúster).|
|**Velocidad de Lectura**|Muy rápido para consultas de rango y recuperaciones de fila completa, ya que los datos están ordenados.|Rápido para buscar los valores indexados. Para recuperar la fila completa, requiere un paso adicional (lookup) para ir a los datos reales.|
|**Overhead de Escritura**|Alto para inserciones y actualizaciones, ya que mantener el orden físico puede requerir reordenamiento de datos.|Menor que el clúster, pero aún así añade overhead ya que el índice debe ser actualizado.|
|**Tamaño en Disco**|No añade espacio extra significativo para los datos en sí (solo para la estructura del índice).|Requiere espacio adicional en disco para almacenar la estructura del índice y los punteros.|
|**Caso de Uso Típico**|Claves primarias o columnas usadas frecuentemente en consultas de rango (ej. fechas, IDs secuenciales).|Columnas usadas frecuentemente en cláusulas `WHERE` o `JOIN` donde no se requiere el orden físico.|

---

### 4. Diferencias entre B-Tree y Hash (Tipos de Estructuras de Índice)

Estos son dos algoritmos o estructuras de datos fundamentales para implementar índices:

- **Índice B-Tree (Árbol B):**
    - **Estructura:** Es la estructura de índice **más común** y versátil. Se organiza como un árbol balanceado donde cada nodo puede tener múltiples hijos. Los nodos hoja (o nodos finales) contienen los valores del índice y punteros (o los datos, si es un índice clúster) ordenados.
    - **Orden:** Mantiene los datos indexados en un **orden lógico y físico (si es clúster)**. Esto permite búsquedas eficientes de rangos.
    - **Operaciones Soportadas:**
        - **Búsquedas de igualdad:** (ej. `WHERE nombre = 'Juan'`) Muy eficientes.
        - **Búsquedas de rango:** (ej. `WHERE fecha BETWEEN '2023-01-01' AND '2023-12-31'`) Extremadamente eficientes debido al orden.
        - **Ordenamiento:** (ej. `ORDER BY columna_indexada`) Ya que los datos están ordenados, la recuperación es rápida.
        - **Prefijos de columnas compuestas:** Eficiente si la búsqueda utiliza el prefijo de las columnas en un índice compuesto (ej. índice en `(apellido, nombre)` es bueno para `WHERE apellido = 'Smith'`).
            
    - **Uso:** Ideal para la mayoría de los escenarios de búsqueda y para claves primarias o únicas. Es el tipo de índice por defecto en la mayoría de las bases de datos relacionales.
        
- **Índice Hash:**
    - **Estructura:** Utiliza una función hash para calcular una dirección de memoria (o un "bucket") para cada valor indexado. Cada bucket contiene punteros a las filas con ese valor. No hay un orden subyacente.
    - **Orden:** **No mantiene ningún orden** de los datos.
    - **Operaciones Soportadas:**
        - **Búsquedas de igualdad:** (ej. `WHERE id = 123`) Extremadamente rápido para búsquedas de igualdad, ya que la función hash lleva directamente a la ubicación del dato.
        - **Búsquedas de rango:** **Muy ineficientes o no soportadas**. Dado que no hay orden, para un rango se tendría que escanear una gran parte del índice.
        - **Ordenamiento:** No son útiles para ordenar datos.
        - **Prefijos de columnas compuestas:** No son útiles para esto.
            
    - **Uso:** Adecuado solo para búsquedas de igualdad exactas. Menos común como tipo de índice primario que el B-Tree debido a sus limitaciones con rangos. Algunas bases de datos los usan internamente para tablas de hash o memoria.

---

### 5. Índice Bitmap (Mapa de Bits)

- **Concepto:** Un índice Bitmap es una estructura de índice especializada que se utiliza comúnmente en **data warehousing (almacenes de datos)** y **sistemas OLAP (Procesamiento Analítico en Línea)**, donde las columnas tienen una **baja cardinalidad** (es decir, tienen un número pequeño y fijo de valores distintos, por ejemplo, género, estado civil, región, verdadero/falso).
    
- **Funcionamiento:** En lugar de almacenar directamente los valores de las columnas o punteros a filas, un índice Bitmap crea un mapa de bits (una secuencia de 0s y 1s) para cada valor distinto en la columna indexada.
    - Si una columna `EstadoCivil` tiene los valores 'Soltero', 'Casado', 'Divorciado'.
    - Para 'Soltero', se crearía un bitmap: `01010010...` (donde 1 indica que la fila corresponde a 'Soltero', y 0 que no).
    - Para 'Casado', otro bitmap: `10101000...`
        
- **Ventajas:**
    - **Eficiencia de Almacenamiento:** Muy compacto para columnas de baja cardinalidad.
    - **Velocidad en Consultas COMPLEJAS (AND/OR/NOT):** Extremadamente eficiente para combinar múltiples condiciones con operadores lógicos (`AND`, `OR`, `NOT`) porque las operaciones se realizan directamente a nivel de bits (booleanos). Por ejemplo, `Estado = 'Casado' AND Sexo = 'Femenino'` puede resolverse muy rápidamente combinando los bitmaps.
        
- **Desventajas:**
    - **Ineficiente para Columnas de Alta Cardinalidad:** Si una columna tiene muchos valores únicos (ej. nombres, direcciones, IDs), generar y manejar un bitmap para cada valor sería muy ineficiente y consumiría mucho espacio.
    - **Pobre Rendimiento en Transacciones (OLTP):** No son adecuados para sistemas transaccionales (OLTP) donde hay muchas inserciones, actualizaciones o eliminaciones, ya que cualquier cambio en una fila requiere la actualización de múltiples bitmaps, lo que es costoso.
        

---

### 6. Ventajas y Desventajas de los Índices

#### Ventajas:
1. **Mejora de la Velocidad de Consulta (Reads):** Es la ventaja principal. Los índices aceleran significativamente las operaciones `SELECT` que utilizan cláusulas `WHERE`, `JOIN`, `ORDER BY` y `GROUP BY`.
2. **Imposición de Unicidad:** Los índices únicos (y las claves primarias/únicas que los utilizan) garantizan que no haya valores duplicados en las columnas especificadas, manteniendo la integridad de los datos.
3. **Ordenamiento Rápido:** Si una consulta requiere que los resultados estén ordenados (`ORDER BY`), y hay un índice en las columnas de ordenamiento, el motor de base de datos puede usar el índice directamente, evitando una operación de ordenamiento costosa.
4. **Búsquedas de Rango Eficientes:** Especialmente con índices B-Tree, las consultas que buscan rangos de valores son muy eficientes.
5. **Optimización de JOINs:** Los índices en las columnas de unión (`JOIN`) pueden acelerar considerablemente las operaciones de unión entre tablas.

#### Desventajas:
1. **Overhead de Escritura (Writes):** Cada vez que se inserta, actualiza o elimina una fila en una tabla, el motor de la base de datos debe también actualizar (o al menos verificar) los índices asociados a esa tabla. Esto añade un costo de rendimiento significativo a las operaciones `INSERT`, `UPDATE` y `DELETE`. Demasiados índices pueden ralentizar drásticamente las escrituras.
2. **Consumo de Espacio en Disco:** Los índices son estructuras de datos que deben almacenarse en el disco, consumiendo espacio adicional. En tablas muy grandes con muchos índices, este espacio puede ser considerable.
3. **Aumento del Tiempo de Respaldo y Restauración:** Bases de datos con muchos índices tardarán más en ser respaldadas y restauradas debido al mayor volumen de datos que deben ser procesados.
4. **Complejidad en el Mantenimiento:** Los índices deben ser monitoreados y ocasionalmente reconstruidos o reorganizados para mantener su eficiencia (esto lo hace el DBA o automáticamente el sistema si está configurado). Los índices fragmentados pueden reducir el rendimiento.
5. **Selección Incorrecta:** Un índice mal diseñado o aplicado a las columnas incorrectas puede no ofrecer ninguna mejora de rendimiento, e incluso puede degradarlo, ya que el sistema sigue incurriendo en el overhead de escritura y almacenamiento sin obtener beneficios de lectura.


---
# Secuencias

- Objeto que genera números secuenciales. 
- Se utiliza para numerar registros en forma secuencial sin repeticiones. 
- Se implementa mediante un tipo de columna o mediante un objeto separado en la BD.

- **Qué hacen**: Una secuencia es un objeto de base de datos que genera números secuenciales (enteros) únicos en un orden predefinido (ascendente o descendente) a partir de un valor inicial y con un incremento específico. A diferencia de `IDENTITY`, las secuencias son **independientes de las tablas**.
    
- **Características**:
    
    - Puede ser utilizada por múltiples tablas.
    - Los valores de la secuencia no se revierte si una transacción que los utiliza hace `ROLLBACK`.
    - Puede tener valores máximos/mínimos, ciclos (reiniciar la secuencia) y cacheo de valores.

**Ejemplo de Secuencia:**

```sql
CREATE SEQUENCE seqPedidos INCREMENT START BY 1 WITH 10 MINVALUE 1 MAXVALUE CYCLE;

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

- Los IDENTITYs se implementan mediante una propiedad en los atributos de una tabla. 
- Las SEQUENCEs son independientes de las tablas 
- Los valores de las IDENTITYs se generan cuando se inserta una fila 
- Los valores de las SEQUENCEs se generan utilizando la cláusula NEXT VALUE 
- Los valores de las IDENTITYs no son cíclicos y su valor máximo está dado por el tamaño del atributo. 
- En las SEQUENCES pueden ser seteados los valores máximos y pueden ser cíclicas.

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

- Es otro objeto de una BD 
- Consta de una sentencia SELECT que simula ser una tabla. 
- Referencia a otras tablas o vistas. 
- Tiene un nombre 
- No contiene datos almacenados 
- No ocupa espacio en disco (salvo la metadata

***CARACTERÍSTICAS*** 
- Permite implementar algún grado de seguridad. 
- Enmascarar complejidad a los usuarios. 
- Desacopla las aplicaciones de cambios a nivel lógico. 
- Algunas permiten ejecutar sentencias insert, update y delete. 
- No se pueden declarar con ORDER BY


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

- Es un objeto que persiste los datos devueltos por un query en una tabla junto con los cambios producidos en las tablas origen. 
- Estos datos se actualizan manual o automáticamente. 
- Dependiendo del motor la actualización puede ser total o incremental. 
- Los datos se almacenan en tablas físicas. 
- Se utilizan principalmente en DW.

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



- - -
# Preguntas 

### 1. ¿Qué tipo de trigger utilizaría para realizar modificaciones sobre los datos de una Vista?

Para realizar modificaciones (INSERT, UPDATE, DELETE) sobre los datos de una Vista, se utilizaría un **Trigger `INSTEAD OF`**.

**Explicación:**

Las vistas son objetos virtuales que no almacenan datos por sí mismas. Su contenido se deriva de una o más tablas subyacentes. La mayoría de las veces, las vistas son directamente actualizables por el motor de base de datos si la vista es simple (es decir, se basa en una sola tabla, no tiene funciones de agregación, `GROUP BY`, `DISTINCT`, etc.).

Sin embargo, cuando una vista es **compleja** (por ejemplo, involucra múltiples tablas mediante JOINs, contiene funciones de agregación, cláusulas `GROUP BY`, o `DISTINCT`), el motor de la base de datos no puede determinar automáticamente cómo una operación de `INSERT`, `UPDATE` o `DELETE` en la vista debe traducirse en operaciones en las tablas base. Aquí es donde entra el trigger `INSTEAD OF`.

- Un trigger `INSTEAD OF` (en lugar de) se dispara **en lugar de** la acción DML (INSERT, UPDATE, DELETE) que lo activó en la vista.
    
- Dentro del cuerpo del trigger, el desarrollador escribe la lógica SQL necesaria para realizar las operaciones DML adecuadas en las tablas base subyacentes, de manera que la modificación en la vista se refleje correctamente en los datos reales.
    
- En el contexto de SQL Server, estos triggers operan sobre las tablas virtuales `INSERTED` y `DELETED` (que contienen los datos que se intentarían insertar/actualizar o los datos antiguos que se intentarían eliminar, respectivamente) para saber qué datos deben ser manipulados en las tablas base.
    

**Ejemplo mental:** Si tienes una vista `Vista_Pedidos_Cliente` que une `Clientes` y `Pedidos`, y quieres poder "insertar un pedido" a través de esta vista, un trigger `INSTEAD OF INSERT` en `Vista_Pedidos_Cliente` tomaría los datos del `INSERTED` pseudo-tabla y los usaría para insertar filas en la tabla `Pedidos` (y quizás verificar el `id_cliente` en la tabla `Clientes`).

---

### 2. ¿Qué tipo de trigger utilizaría para registrar auditoría sobre las modificaciones de los datos de una Tabla?

Para registrar auditoría sobre las modificaciones de los datos de una tabla, se utilizarían **Triggers `AFTER`** (también conocidos como `FOR` triggers en algunos sistemas, como SQL Server).

**Explicación:**

Los triggers `AFTER` (o `FOR`) se disparan **después** de que la operación DML (INSERT, UPDATE, DELETE) que los activó se ha completado en la tabla y los cambios ya se han aplicado a los datos (aunque la transacción aún no haya hecho `COMMIT`).

Para auditoría, esto es ideal porque:

- **Acceso a los datos finales:** Puedes acceder a los datos tal como quedaron después de la modificación (`INSERTED` tabla virtual para INSERTS y UPDATES) y/o a los datos como estaban antes de la modificación (`DELETED` tabla virtual para DELETES y UPDATES).
    
- **Registrar el evento:** Una vez que la operación ha ocurrido y los datos son "estables" (dentro de la transacción), el trigger puede insertar una fila en una tabla de auditoría separada, registrando:
    
    - Quién realizó la acción.
        
    - Cuándo se realizó.
        
    - Qué tipo de acción (INSERT, UPDATE, DELETE).
        
    - Qué datos fueron afectados (valores antiguos y/o nuevos).
        
    - Desde dónde se realizó la acción (ej. IP del cliente, nombre de la aplicación, si está disponible).
        

**Ejemplo:** Un `AFTER UPDATE` trigger en la tabla `Productos` podría registrar en una tabla `Auditoria_Productos` el `id` del producto, el `precio_anterior`, el `precio_nuevo`, la `fecha_modificacion` y el `usuario_modificador` cada vez que el precio de un producto es actualizado.

---

### 3. Ejemplos Prácticos o de Negocios de Utilización de Triggers

Los triggers son herramientas poderosas para automatizar la lógica de negocio y mantener la integridad y consistencia de los datos. Aquí algunos ejemplos prácticos:

1. **Mantenimiento de Datos Derivados o Resúmenes (AFTER INSERT/UPDATE/DELETE):**
    
    - **Ejemplo de Negocio:** Mantener un `stock_actual` en la tabla `Productos` que se actualiza automáticamente cada vez que se registra una venta (DELETE) o una entrada de inventario (INSERT) en una tabla `MovimientosInventario`.
        
    - **Trigger:** Un `AFTER INSERT` o `AFTER UPDATE` en `MovimientosInventario` que modifica el `stock_actual` en la tabla `Productos`.
        
2. **Auditoría y Registro de Cambios (AFTER INSERT/UPDATE/DELETE):**
    
    - **Ejemplo de Negocio:** Registrar cada cambio de estado de un pedido en una tabla de `Historico_Pedidos`, incluyendo la fecha, el usuario que realizó el cambio y el estado anterior/nuevo.
        
    - **Trigger:** Un `AFTER UPDATE` en la tabla `Pedidos` que inserta una fila en `Historico_Pedidos` cada vez que la columna `estado_pedido` cambia.
        
3. **Aplicación de Reglas de Negocio Complejas (BEFORE/AFTER):**
    
    - **Ejemplo de Negocio:** Asegurar que un empleado no pueda registrar más de 40 horas semanales.
        
    - **Trigger:** Un `BEFORE INSERT` o `BEFORE UPDATE` en la tabla `HorasTrabajadas` que verifique la suma total de horas para ese empleado en la semana. Si excede 40, el trigger podría lanzar un error y abortar la operación.
        
    - **Ejemplo de Negocio:** Asignar automáticamente un número de serie único o un código de producto basado en una lógica compleja (no solo una secuencia simple).
        
    - **Trigger:** Un `BEFORE INSERT` en la tabla `Productos` que calcule y asigne el `codigo_producto` antes de que la fila se inserte.
        
4. **Sincronización de Datos entre Tablas (AFTER INSERT/UPDATE/DELETE):**
    
    - **Ejemplo de Negocio:** Cuando un cliente es marcado como "inactivo" en la tabla `Clientes`, automáticamente cancelar todos sus pedidos pendientes en la tabla `Pedidos`.
        
    - **Trigger:** Un `AFTER UPDATE` en la tabla `Clientes` que, si el `estado_cliente` cambia a 'Inactivo', actualice el `estado_pedido` a 'Cancelado' para todos sus pedidos pendientes en la tabla `Pedidos`.
        
5. **Notificaciones o Alertas (AFTER INSERT/UPDATE/DELETE):**
    
    - **Ejemplo de Negocio:** Enviar una notificación por correo electrónico a un gerente cuando un pedido importante (ej. monto > $10,000) es insertado o actualizado.
        
    - **Trigger:** Un `AFTER INSERT` o `AFTER UPDATE` en la tabla `Pedidos` que llame a un procedimiento almacenado para enviar un correo electrónico. (Nota: Esto a menudo se hace de forma asíncrona para no bloquear la transacción, a través de colas de mensajes activadas por el trigger).
        
6. **Validaciones de Datos Complejas (BEFORE INSERT/UPDATE):**
    
    - **Ejemplo de Negocio:** Asegurarse de que la fecha de fin de un proyecto siempre sea posterior a la fecha de inicio.
        
    - **Trigger:** Un `BEFORE INSERT` o `BEFORE UPDATE` en la tabla `Proyectos` que compare `fecha_inicio` y `fecha_fin`. Si `fecha_fin` es anterior, lanza un error.