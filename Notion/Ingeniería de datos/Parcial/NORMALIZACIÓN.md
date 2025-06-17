# 1. Primera Forma Normal (1NF)

- **Requisitos**:
    - Todos los atributos deben ser **atómicos** (indivisibles). Es decir, una celda no debe contener múltiples valores.
    - No debe haber **grupos repetitivos** de columnas (múltiples columnas que representan lo mismo, ej. `Telefono1`, `Telefono2`).
    - Cada fila debe ser única (debe tener una clave primaria).
- **Qué hacen**: Eliminar la complejidad de datos en una sola celda y la redundancia de columnas repetidas, facilitando la búsqueda y manipulación.
    
- **Ejemplo**:
    
    **❌ NO en 1NF:** `Clientes (ClienteID, Nombre, Telefono)` 
    | ClienteID | Nombre | Telefono | 
    | :-------- | :-------- | :---------------- | 
    | 1 | Juan Pérez | 1123456789, 1198765432 | 
    | 2 | Ana Gómez | 1155554444 |
    
    **✅ EN 1NF:** _Opción 1: Múltiples filas para el mismo cliente_ 
    `Clientes (ClienteID, Nombre, Telefono)` 
    | ClienteID | Nombre | Telefono | 
    | :-------- | :-------- | :-------- | 
    | 1 | Juan Pérez | 1123456789 | 
    | 1 | Juan Pérez | 1198765432 | 
    | 2 | Ana Gómez | 1155554444 |
    
    _Opción 2: Crear una tabla separada para los teléfonos (preferido para N:M)_ 
    `Clientes (ClienteID, Nombre)` 
    | ClienteID | Nombre | 
    | :-------- | :-------- | 
    | 1 | Juan Pérez | 
    | 2 | Ana Gómez |
    
    `Telefonos_Cliente (TelefonoID, ClienteID, NumeroTelefono)` 
    | TelefonoID | ClienteID | NumeroTelefono | 
    | :--------- | :-------- | :------------- | 
    | 1 | 1 | 1123456789 | 
    | 2 | 1 | 1198765432 | 
    | 3 | 2 | 1155554444 |
    

---
# 2. Segunda Forma Normal (2NF)

- **Requisitos**:
    - La tabla debe estar en **1NF**.
    - Todos los atributos **no clave** deben depender **completamente** de la clave primaria compuesta (si la hay). Es decir, ningún atributo no clave puede depender solo de una _parte_ de la clave primaria compuesta.
- **Qué hacen**: Eliminar la redundancia donde los datos de atributos no clave se repiten porque dependen solo de una parte de una clave compuesta.
    
- **Ejemplo**:
    
    **❌ NO en 2NF:** 
    `DetallesPedido (PedidoID, ProductoID, Cantidad, PrecioUnitario, NombreProducto)` (Clave Primaria Compuesta: `(PedidoID, ProductoID)`) 
    | PedidoID | ProductoID | Cantidad | PrecioUnitario | NombreProducto | 
    | :------- | :--------- | :------- | :------------- | :------------- | 
    | 101 | P001 | 2 | 50.00 | Laptop | 
    | 101 | P002 | 1 | 20.00 | Mouse | 
    | 102 | P001 | 3 | 50.00 | Laptop | <-- NombreProducto se repite y solo depende de ProductoID
    
    **✅ EN 2NF:** `DetallesPedido (PedidoID, ProductoID, Cantidad, PrecioUnitario)` (Clave Primaria Compuesta: `(PedidoID, ProductoID)`) 
    | PedidoID | ProductoID | Cantidad | PrecioUnitario | 
    | :------- | :--------- | :------- | :------------- | 
    | 101 | P001 | 2 | 50.00 | 
    | 101 | P002 | 1 | 20.00 | 
    | 102 | P001 | 3 | 50.00 |
    
    `Productos (ProductoID, NombreProducto)` 
    | ProductoID | NombreProducto | 
    | :--------- | :------------- | 
    | P001 | Laptop | 
    | P002 | Mouse |
    

---
# 3. Tercera Forma Normal (3NF)

- **Requisitos**:
    - La tabla debe estar en **2NF**.
    - No debe haber dependencias transitivas de atributos no clave. Es decir, ningún atributo no clave debe depender de otro atributo no clave.
- **Qué hacen**: Eliminar la redundancia donde un atributo no clave se repite porque depende de otro atributo no clave, en lugar de depender directamente de la clave primaria.
    
- **Ejemplo**:
    
    **❌ NO en 3NF:** `Empleados (EmpleadoID, NombreEmpleado, Departamento, NombreJefeDepartamento)` (Clave Primaria: `EmpleadoID`) 
    | EmpleadoID | NombreEmpleado | Departamento | NombreJefeDepartamento | 
    | :--------- | :------------- | :----------- | :--------------------- | 
    | 1 | Luis | Ventas | María | 
    | 2 | Ana | Marketing | Pedro | 
    | 3 | Carlos | Ventas | María | <-- NombreJefeDepartamento depende de Departamento, no de EmpleadoID
    
    **✅ EN 3NF:** `Empleados (EmpleadoID, NombreEmpleado, DepartamentoID)` 
    | EmpleadoID | NombreEmpleado | DepartamentoID | 
    | :--------- | :------------- | :------------- | 
    | 1 | Luis | D01 | 
    | 2 | Ana | D02 | 
    | 3 | Carlos | D01 |
    
    `Departamentos (DepartamentoID, NombreDepartamento, NombreJefeDepartamento)` (Clave Primaria: `DepartamentoID`) 
    | DepartamentoID | NombreDepartamento | NombreJefeDepartamento | 
    | :------------- | :----------------- | :--------------------- | 
    | D01 | Ventas | María | 
    | D02 | Marketing | Pedro |
    

---
# 4. Forma Normal de Boyce-Codd (BCNF o 3.5NF)

- **Requisitos**:
    - La tabla debe estar en **3NF**.
    - Cada **determinante** (cualquier atributo o conjunto de atributos del que otro atributo o conjunto de atributos depende funcionalmente) debe ser una **clave candidata**. (Una clave candidata es cualquier columna o conjunto de columnas que puede servir como clave primaria).
- **Qué hacen**: Resuelve ciertas anomalías que 3NF podría no cubrir, especialmente en tablas con múltiples claves candidatas superpuestas o complejas. Garantiza que no haya dependencias de atributos no clave sobre determinantes que no sean claves candidatas.
    
- **Ejemplo**:
    
    **❌ NO en BCNF (pero sí en 3NF en este caso particular):** Imagina una tabla `InscripcionesAsignatura` con: `InscripcionesAsignatura (EstudianteID, Asignatura, Profesor)` (Clave Primaria: `(EstudianteID, Asignatura)`)
    
    - **Dependencia 1**: `(EstudianteID, Asignatura) -> Profesor` (Un estudiante en una asignatura tiene un profesor específico).
    - **Dependencia 2**: `Profesor -> Asignatura` (Un profesor solo enseña una asignatura específica en un momento dado). _Aquí, `Profesor` es un determinante, pero no es una clave candidata para la tabla completa._
    
    | EstudianteID | Asignatura | Profesor | 
    | :----------- | :--------- | :------- | 
    | S1 | BaseDatos | ProfA | 
    | S2 | BaseDatos | ProfA | 
    | S3 | Álgebra | ProfB | 
    | S4 | Álgebra | ProfB |
    
    **✅ EN BCNF:** `InscripcionesEstudiante (EstudianteID, Asignatura)` (Clave Primaria: `(EstudianteID, Asignatura)`) 
    | EstudianteID | Asignatura | 
    | :----------- | :--------- | 
    | S1 | BaseDatos | 
    | S2 | BaseDatos | 
    | S3 | Álgebra | 
    | S4 | Álgebra |
    
    `AsignaturaProfesor (Asignatura, Profesor)` (Clave Primaria: `Asignatura` o `(Asignatura, Profesor)` si el profesor es único por asignatura) 
    | Asignatura | Profesor | 
    | :--------- | :------- | 
    | BaseDatos | ProfA | 
    | Álgebra | ProfB |
    

---
# 5. Cuarta Forma Normal (4NF)

- **Requisitos**:
    - La tabla debe estar en **BCNF**.
    - No debe contener dependencias multivaluadas no triviales. Una dependencia multivaluada `A ->-> B` existe si para cada `A`, hay un conjunto de valores `B` asociados, y este conjunto es independiente de otros atributos no `A`.
- **Qué hacen**: Eliminar la redundancia que ocurre cuando una tabla describe múltiples hechos multivaluados e **independientes** sobre una entidad.
    
- **Ejemplo**:
    
    **❌ NO en 4NF:** `EmpleadoHabilidadIdioma (EmpleadoID, Habilidad, Idioma)` (Clave Primaria: `(EmpleadoID, Habilidad, Idioma)`)
    
    - Un empleado puede tener múltiples habilidades.
    - Un empleado puede hablar múltiples idiomas.
    - Las habilidades de un empleado son independientes de los idiomas que habla.
    
    | EmpleadoID | Habilidad | Idioma | 
    | :--------- | :--------- | :------ | 
    | E1 | SQL | Español | 
    | E1 | SQL | Inglés | 
    | E1 | Python | Español | 
    | E1 | Python | Inglés | <-- Redundancia por la independencia de Habilidad e Idioma
    
    **✅ EN 4NF:** `EmpleadoHabilidad (EmpleadoID, Habilidad)` (Clave Primaria: `(EmpleadoID, Habilidad)`) 
    | EmpleadoID | Habilidad | 
    | :--------- | :-------- | 
    | E1 | SQL | 
    | E1 | Python |
    
    `EmpleadoIdioma (EmpleadoID, Idioma)` (Clave Primaria: `(EmpleadoID, Idioma)`) 
    | EmpleadoID | Idioma | 
    | :--------- | :------ | 
    | E1 | Español | 
    | E1 | Inglés |
    

---
# 6. Quinta Forma Normal (5NF) o Forma Normal de Proyección-Unión (PJNF)

- **Requisitos**:
    - La tabla debe estar en **4NF**.
    - No debe contener ninguna dependencia de unión (Join Dependency) no trivial. Una tabla está en 5NF si cada dependencia de unión en ella es trivial (es decir, cada componente de la dependencia de unión contiene una clave para la relación original).
- **Qué hacen**: Eliminar la redundancia que puede surgir cuando una tabla se puede descomponer en tres o más tablas más pequeñas y unirse de nuevo sin pérdida de información ni generación de tuplas espurias. Esto generalmente ocurre en relaciones donde existen restricciones de "negocio" complejas que no pueden ser representadas por dependencias funcionales o multivaluadas simples. **Es la forma normal más estricta y rara vez se aplica en la práctica debido a su complejidad.**
    
- **Ejemplo**: Este ejemplo es más complejo de ilustrar concisamente, ya que requiere una condición donde una combinación de tres entidades solo existe si las tres relaciones binarias existen.
    
    **❌ NO en 5NF:** `SuministroProyectoParte (Proveedor, Proyecto, Parte)` (Un proveedor suministra una parte a un proyecto, pero solo si: el proveedor suministra esa parte; el proveedor participa en ese proyecto; la parte es usada en ese proyecto).
    
    | Proveedor | Proyecto | Parte | 
    | :-------- | :------- | :---- | 
    | P1 | ProyA | ParteX | 
    | P1 | ProyB | ParteX | 
    | P2 | ProyA | ParteY | 
    | P2 | ProyB | ParteZ | _Aquí, si sabemos que P1 suministra ParteX, P1 participa en ProyA y ParteX es usada en ProyA, entonces P1 suministrando ParteX a ProyA es un hecho._
    
    **✅ EN 5NF:** Descomposición en tablas más pequeñas:
    
    `ProveedorParte (Proveedor, Parte)` `ProyectoParte (Proyecto, Parte)` `ProveedorProyecto (Proveedor, Proyecto)`
    
    La tabla original `SuministroProyectoParte` puede ser reconstruida uniendo estas tres tablas, y la descomposición evita redundancia al representar explícitamente estas tres relaciones binarias. Solo una combinación de (Proveedor, Proyecto, Parte) es válida si todas las relaciones binarias correspondientes son válidas.
    