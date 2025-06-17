# Subqueries (Subconsultas)

- **Qué hace**: Una subconsulta es una consulta `SELECT` anidada dentro de otra consulta SQL (la consulta externa o principal). Actúa como una fuente de datos para la consulta principal, ya sea devolviendo un solo valor (subconsulta escalar), una lista de valores (subconsulta de múltiples valores) o una tabla (subconsulta de tabla/múltiples columnas y filas).
    
- **Tipos principales de Subconsultas:**
    
    - **Escalares**: Devuelven un solo valor (una fila, una columna). Se pueden usar en cualquier lugar donde se espere un valor único (SELECT, WHERE, HAVING, JOIN, etc.).
    - **De Múltiples Valores (Columna Única)**: Devuelven una lista de valores en una sola columna. Usadas comúnmente con operadores como `IN`, `NOT IN`, `ANY`, `ALL`, `SOME`.
    - **De Tabla (Múltiples Columnas/Filas)**: Devuelven un conjunto de resultados que puede ser tratado como una tabla temporal. Usadas en la cláusula `FROM` (conocidas como tablas derivadas) o con `EXISTS`/`NOT EXISTS`.
- **Ejemplo**: Encontrar empleados que ganan más que el salario promedio de _todos_ los empleados.
    
    **Tablas para ejemplo:** `Empleados (EmpleadoID, Nombre, Salario, DepartamentoID)` 
    | EmpleadoID | Nombre | Salario | DepartamentoID | 
    | :--------- | :------ | :------ | :------------- | 
    | 1 | Ana | 60000 | 101 | 
    | 2 | Luis | 75000 | 102 | 
    | 3 | Marta | 50000 | 101 | 
    | 4 | Pedro | 90000 | 102 | 
    | 5 | Sofía | 60000 | 103 |

    ```sql
    -- Subconsulta escalar para obtener el salario promedio
    SELECT Nombre, Salario
    FROM Empleados
    WHERE Salario > (SELECT AVG(Salario) FROM Empleados);
    ```
    
- **Resultado**: 
  | Nombre | Salario | 
  | :----- | :------ | 
  | Luis | 75000 | 
  | Pedro | 90000 | 
  
  _(El salario promedio es 69000. Los empleados con salario > 69000 son Luis y Pedro)_
    
---
# Queries Correlacionadas (Subconsultas Correlacionadas)

- **Qué hace**: Una subconsulta correlacionada es un tipo especial de subconsulta donde la consulta interna (subconsulta) **depende de la consulta externa** para su ejecución. Se ejecuta una vez por cada fila procesada por la consulta externa, usando un valor de la fila actual de la consulta externa.
    
- **Diferencia clave con subconsultas no correlacionadas**: Las subconsultas no correlacionadas se ejecutan una sola vez y devuelven su resultado a la consulta externa. Las correlacionadas se "re-evalúan" para cada fila de la consulta externa. Esto puede hacerlas menos eficientes en grandes conjuntos de datos, aunque a menudo son muy expresivas.
    
- **Ejemplo**: Encontrar empleados que ganan más que el salario promedio de _su propio departamento_.
    ```sql
    SELECT E.Nombre, E.Salario, E.DepartamentoID
    FROM Empleados AS E
    WHERE E.Salario > (SELECT AVG(E2.Salario)
                       FROM Empleados AS E2
                       WHERE E2.DepartamentoID = E.DepartamentoID); -- Aquí reside la correlación
    ```
    
- **Proceso (conceptual)**:
    
    - Para Ana (DepartamentoID 101): `AVG(Salario) WHERE DepartamentoID = 101` (Promedio Ventas) -> (60000 + 50000) / 2 = 55000. Ana (60000) > 55000? Sí.
    - Para Luis (DepartamentoID 102): `AVG(Salario) WHERE DepartamentoID = 102` (Promedio Marketing) -> (75000 + 90000) / 2 = 82500. Luis (75000) > 82500? No.
    - ...y así para cada fila.
- **Resultado**: 
  | Nombre | Salario | DepartamentoID | 
  | :----- | :------ | :------------- | 
  | Ana | 60000 | 101 | 
  | Pedro | 90000 | 102 | 
  
  _(Ana gana más que el promedio de su Dpto. 101 (60000 > 55000). Pedro gana más que el promedio de su Dpto. 102 (90000 > 82500).)_
    
---
# Cláusula `WITH` (Common Table Expressions - CTEs)

- **Qué hace**: Una CTE es un conjunto de resultados temporal y con nombre que puedes definir dentro del ámbito de una única sentencia de ejecución (`SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`). No se almacena físicamente, sino que se evalúa cada vez que se ejecuta la consulta. Mejoran la legibilidad y la modularidad de consultas complejas.
    
- **Ventajas**:
    - **Legibilidad**: Rompe consultas complejas en pasos lógicos más pequeños.
    - **Reutilización**: Puedes referenciar una CTE múltiples veces dentro de la misma consulta principal.
    - **Recursividad**: Permiten consultas recursivas (para jerarquías, grafos, etc.).
- **Ejemplo**: Encontrar empleados que ganan más que el salario promedio de su departamento (el mismo ejemplo anterior, pero usando CTEs para mayor claridad).
  
    ```sql
    WITH SalariosPromedioDepartamento AS (
        SELECT DepartamentoID, AVG(Salario) AS PromedioSalario
        FROM Empleados
        GROUP BY DepartamentoID
    )
    SELECT E.Nombre, E.Salario, D.NombreDepartamento
    FROM Empleados AS E
    JOIN SalariosPromedioDepartamento AS SPD
        ON E.DepartamentoID = SPD.DepartamentoID
    WHERE E.Salario > SPD.PromedioSalario;
    ```
    
- **Resultado**: 
  | Nombre | Salario | NombreDepartamento | 
  | :----- | :------ | :----------------- | 
  | Ana | 60000 | Ventas | 
  | Pedro | 90000 | Marketing | 
  
  _(Este enfoque es a menudo más legible y, a veces, más eficiente que una subconsulta correlacionada para el mismo problema.)_
    
---
# `ANY`, `SOME` y `ALL` (Operadores de Comparación con Subconsultas)

- **Qué hace**: Se utilizan para comparar un valor escalar con un conjunto de valores devueltos por una subconsulta.
    - `ANY` y `SOME` son sinónimos.
    - `ALL` tiene un comportamiento distinto.

- **`ANY` / `SOME`**:
    - **Qué hace**: `valor OPERADOR ANY (subconsulta)` o `valor OPERADOR SOME (subconsulta)` evalúa a `TRUE` si la comparación es verdadera para _AL MENOS UN_ valor en el conjunto devuelto por la subconsulta. ***Es como `IN` pero con operadores de comparación.***
    - **Ejemplo**: Encontrar empleados que ganan más que _al menos un_ empleado del departamento de IT.

        ```sql
        SELECT Nombre, Salario
        FROM Empleados
        WHERE Salario > ANY (SELECT Salario FROM Empleados WHERE DepartamentoID = 103);
        ```
        
    - **Interpretación**: Significa "Salario > SalarioMásBajoDeIT" (si hay múltiples salarios en IT, solo el más bajo necesita ser superado). Si el salario de IT es 60000, entonces si el empleado actual tiene 60001, ya cumple la condición.
    - **Resultado (con Sofía en Dpto 103, Salario 60000)**: 
      | Nombre | Salario | 
      | :----- | :------ | 
      | Luis | 75000 | 
      | Pedro | 90000 | 
      
      _(Estos ganan más que al menos un empleado de IT (Sofía con 60000). Ana (60000) y Marta (50000) no cumplen `Salario > 60000`)_
- **`ALL`**:
    - **Qué hace**: `valor OPERADOR ALL (subconsulta)` evalúa a `TRUE` si la comparación es verdadera para _TODOS_ los valores en el conjunto devuelto por la subconsulta.
    - **Ejemplo**: Encontrar empleados que ganan más que _todos_ los empleados del departamento de IT.
      
        ```sql
        SELECT Nombre, Salario
        FROM Empleados
        WHERE Salario > ALL (SELECT Salario FROM Empleados WHERE DepartamentoID = 103);
        ```
        
    - **Interpretación**: Significa "Salario > SalarioMásAltoDeIT". Para cumplir, el salario del empleado debe ser mayor que el salario más alto de todos los empleados del departamento de IT.
    - **Resultado (con Sofía en Dpto 103, Salario 60000)**: 
      | Nombre | Salario | 
      | :----- | :------ | 
      | Luis | 75000 | 
      | Pedro | 90000 | 
      
      _(Ambos ganan más que Sofía (60000), que es la única y, por tanto, la de mayor salario en Dpto 103. Si hubiera otro empleado en IT con 70000, Luis no aparecería, ya que 75000 no es > 70000.)_