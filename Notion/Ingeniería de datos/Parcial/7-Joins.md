# JOINS 

**Combinación de una tabla con la otra según una relación**

- - -
# _INNER_ JOIN 

- La relación tiene que cumplirse
- Si no se cumple la condición, no se mostraran en la tabla resultante 

- **Qué hace**:
    - Devuelve solo las filas cuando hay una **coincidencia en AMBAS tablas** basándose en la condición de unión.
    - Las filas que no tienen una coincidencia en la otra tabla son excluidas del resultado.
- **Ejemplo**:
    ```sql
    SELECT E.Nombre, D.NombreDepartamento
    FROM Empleados AS E
    INNER JOIN Departamentos AS D
        ON E.DepartamentoID = D.DepartamentoID;
    ```

- - -
# LEFT JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de la tabla **IZQUIERDA**  dejando **NULL** en la columna que las relaciona

- **Qué hace**:
    - Devuelve **TODAS las filas de la tabla de la IZQUIERDA** (la primera tabla en la cláusula `FROM` o `JOIN`).
    - También devuelve las filas coincidentes de la tabla de la DERECHA.
    - Si no hay coincidencia en la tabla de la DERECHA para una fila de la izquierda, los valores de las columnas de la tabla de la derecha serán `NULL`.
- **Ejemplo**:
    ```sql
    SELECT E.Nombre, D.NombreDepartamento
    FROM Empleados AS E
    LEFT JOIN Departamentos AS D
        ON E.DepartamentoID = D.DepartamentoID;
    ```

- - -
# RIGHT JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de la tabla **DERECHA** dejando **NULL** en la columna que las relaciona

- **Qué hace**:
    - Devuelve **TODAS las filas de la tabla de la DERECHA** (la segunda tabla en la cláusula `JOIN`).
    - También devuelve las filas coincidentes de la tabla de la IZQUIERDA.
    - Si no hay coincidencia en la tabla de la IZQUIERDA para una fila de la derecha, los valores de las columnas de la tabla de la izquierda serán `NULL`.
- **Ejemplo**:
    ```sql
    SELECT E.Nombre, D.NombreDepartamento
    FROM Empleados AS E
    RIGHT JOIN Departamentos AS D
        ON E.DepartamentoID = D.DepartamentoID;
    ```

- - -
# FULL _OUTER_ JOIN

- La relación puede no cumplirse
- Si no se cumple la relación, se mantienen los registros de ámbas tablas dejando **NULL** en las columnas que las relaciona

- **Qué hace**:
    - Devuelve **TODAS las filas cuando hay una coincidencia** en cualquiera de las dos tablas.
    - Incluye todas las filas de la tabla de la IZQUIERDA y todas las filas de la tabla de la DERECHA.
    - Si no hay coincidencia en una de las tablas, los valores de las columnas de esa tabla serán `NULL`.
    - Es la combinación de `LEFT JOIN` y `RIGHT JOIN`.
- **Ejemplo**:
    ```sql
    SELECT E.Nombre, D.NombreDepartamento
    FROM Empleados AS E
    FULL JOIN Departamentos AS D
        ON E.DepartamentoID = D.DepartamentoID;
    ```

- - -
# CROSS JOIN 

- No hay relación
- Por cada fila de una tabla, se junta con todas las filas de la otra tabla

- **Qué hace**:
    - Devuelve el **producto cartesiano** de las dos tablas. Es decir, cada fila de la primera tabla se combina con cada fila de la segunda tabla.
    - No requiere una condición `ON`.
    - Genera un conjunto de resultados muy grande (Número de Filas Tabla A x Número de Filas Tabla B).
- **Ejemplo**:
    ```sql
    SELECT E.Nombre, D.NombreDepartamento
    FROM Empleados AS E
    CROSS JOIN Departamentos AS D;
    ```

- - -

# Regla de operadores de conjuntos 

**Sirven para combinar o comparar los resultados de dos o más consultas `SELECT`.**

**Regla Importante para todos los operadores de Conjuntos:**

- El número de columnas seleccionadas en cada consulta `SELECT` **debe ser el mismo**.
- El orden de las columnas debe ser el mismo.
- Los tipos de datos de las columnas correspondientes en cada `SELECT` deben ser **compatibles** (o se pueden convertir implícitamente).
  
- - -
# Tablas para ejemplos 

**Tabla: `Profesores_Matematicas`** 
| ID | Nombre | Especialidad | 
| :-- | :--------- | :------------- | 
| 1 | Ana | Álgebra | 
| 2 | Luis | Cálculo | 
| 3 | Carlos | Álgebra | 
| 5 | Miguel | Geometría |

**Tabla: `Profesores_Fisica`** 
| ID | Nombre | Especialidad | 
| :-- | :--------- | :------------- | 
| 2 | Luis | Cálculo | (Misma fila que en Matematicas) 
| 3 | Carlos | Electricidad | (Mismo ID/Nombre, diferente Especialidad) 
| 4 | Sofía | Mecánica | 
| 5 | Miguel | Geometría | (Misma fila que en Matematicas)

- - -
# UNION

- **Qué hace**:
    - Combina los conjuntos de resultados de dos o más consultas `SELECT`.
    - **Elimina filas duplicadas**. Si una fila es idéntica en ambas consultas, solo aparecerá una vez en el resultado final.
    - Ordena los resultados de forma predeterminada (aunque se puede añadir `ORDER BY` al final).
- **Ejemplo**:
    ```sql
    SELECT ID, Nombre, Especialidad FROM Profesores_Matematicas
    UNION
    SELECT ID, Nombre, Especialidad FROM Profesores_Fisica;
    ```
    
- **Resultado**: 
  | ID | Nombre | Especialidad | 
  | :-- | :--------- | :------------- | 
  | 1 | Ana | Álgebra | 
  | 2 | Luis | Cálculo | 
  | 3 | Carlos | Álgebra | 
  | 3 | Carlos | Electricidad | 
  | 4 | Sofía | Mecánica | 
  | 5 | Miguel | Geometría | 
  
  _(Nota: Luis y Miguel aparecen una sola vez porque sus filas son idénticas en ambas tablas. Carlos aparece dos veces porque su fila (ID, Nombre, Especialidad) no es idéntica en ambas tablas.)_

---

# UNION ALL

- **Qué hace**:
    - Combina los conjuntos de resultados de dos o más consultas `SELECT`.
    - **NO elimina filas duplicadas**. Todas las filas de ambas consultas se incluyen en el resultado final, incluso si son idénticas.
    - Es generalmente más rápido que `UNION` porque no necesita realizar el proceso de eliminación de duplicados.
- **Ejemplo**:
    ```sql
    SELECT ID, Nombre, Especialidad FROM Profesores_Matematicas
    UNION ALL
    SELECT ID, Nombre, Especialidad FROM Profesores_Fisica;
    ```
    
- **Resultado**: 
  | ID | Nombre | Especialidad | 
  | :-- | :--------- | :------------- | 
  | 1 | Ana | Álgebra | 
  | 2 | Luis | Cálculo | 
  | 3 | Carlos | Álgebra | 
  | 5 | Miguel | Geometría | 
  | 2 | Luis | Cálculo | 
  | 3 | Carlos | Electricidad | 
  | 4 | Sofía | Mecánica | 
  | 5 | Miguel | Geometría | 
  
  _(Nota: Luis y Miguel aparecen dos veces, una por cada tabla, porque UNION ALL no elimina duplicados. Todas las filas originales se mantienen.)_

---

# INTERSECT

- **Qué hace**:
    - Devuelve solo las filas que son **comunes a AMBOS conjuntos de resultados** de las consultas `SELECT`.
    - Solo se incluyen las filas que aparecen en la _primera_ consulta Y en la _segunda_ consulta (o en todas si hay más de dos).
    - Elimina duplicados (similar a `UNION` en este aspecto).
- **Ejemplo**:
    ```sql
    SELECT ID, Nombre, Especialidad FROM Profesores_Matematicas
    INTERSECT
    SELECT ID, Nombre, Especialidad FROM Profesores_Fisica;
    ```
    
- **Resultado**: 
  | ID | Nombre | Especialidad | 
  | :-- | :--------- | :------------- | 
  | 2 | Luis | Cálculo | 
  | 5 | Miguel | Geometría | 
  
  _(Nota: Solo Luis y Miguel aparecen, porque sus filas son _idénticas_ en ambas tablas. Carlos no aparece porque su Especialidad es diferente en la segunda tabla.)_

---

# EXCEPT (o `MINUS` en otros SQL como Oracle)

- **Qué hace**:
    - Devuelve las filas que están presentes en el **primer conjunto de resultados** (`SELECT` de la izquierda) pero **NO están presentes en el segundo conjunto de resultados** (`SELECT` de la derecha).
    - Es decir, "A menos B".
    - Elimina duplicados.
- **Ejemplo**:
    ```sql
    SELECT ID, Nombre, Especialidad FROM Profesores_Matematicas
    EXCEPT
    SELECT ID, Nombre, Especialidad FROM Profesores_Fisica;
    ```
    
- **Resultado**: 
  | ID | Nombre | Especialidad | 
  | :-- | :----- | :----------- | 
  | 1 | Ana | Álgebra | 
  | 3 | Carlos | Álgebra | 
  
  _(Ana es exclusiva de Profesores_Matematicas. Carlos tiene el mismo ID y Nombre, pero una Especialidad diferente, por lo tanto, la fila completa `(3, Carlos, Álgebra)` NO está en Profesores_Fisica, y por eso se incluye.)_
    
- **Ejemplo inverso (Profesores_Fisica EXCEPT Profesores_Matematicas)**:
    ```sql
    SELECT ID, Nombre, Especialidad FROM Profesores_Fisica
    EXCEPT
    SELECT ID, Nombre, Especialidad FROM Profesores_Matematicas;
    ```
    
- **Resultado (inverso)**: 
  | ID | Nombre | Especialidad | 
  | :-- | :----- | :------------- | 
  | 3 | Carlos | Electricidad | 
  | 4 | Sofía | Mecánica | 
  
  _(Sofía es exclusiva de Profesores_Fisica. Carlos aparece porque la fila `(3, Carlos, Electricidad)` NO está en Profesores_Matematicas.)_