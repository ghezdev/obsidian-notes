
### 1. Introducción al Modelo Relacional

El **modelo relacional** se basa en la **teoría de conjuntos**. Los datos se representan en **tablas** o **relaciones**, donde cada fila (tupla) corresponde a un registro, y cada columna (atributo) representa una propiedad de los datos. La estructura general de una relación es:

```
Nombre de la relación (tabla)
A1 A2 ... An (atributos)
Valor Valor Valor ... Valor
...
```

**Aspectos estructurales**:

- Cada relación tiene un **nombre**.
- Las **atributos** definen las propiedades de la relación.
- La **cabecera** de la tabla indica los nombres de los atributos.
- Las **tuplas** contienen los valores correspondientes.

---

### 2. Bases de Datos Relacionales

Las Bases de Datos Relacionales se basan en el modelo relacional de datos.
Un **sistema de gestión de bases de datos (DBMS)** relacional se fundamenta en:

- La **estructura**: definición de relaciones, atributos, claves, y restricciones.
- La **integridad**: asegurarse de que los datos sean correctos y consistentes.
- La **manipulación**: operaciones sobre las bases de datos, como inserciones, actualizaciones, borrados y consultas.

El **modelo relacional** tiene como referencia la teoría de conjuntos, permitiendo realizar operaciones sobre conjuntos de tuplas.

---

### 3. Estructura del Modelo Relacional, Catálogo y Catálogo en Línea

El **catálogo** o diccionario de la base de datos funciona como una **meta-información** que describe todos los objetos (relaciones, atributos, restricciones, usuarios). Es fundamental para:

- La organización interna del DBMS.
- La optimización de las consultas (el optimizador usa la información del catálogo).
- La seguridad y control de accesos (el componente de seguridad usa información del catálogo).

El **catálogo en línea** está siempre disponible para los usuarios autorizados, lo que permite acceder y modificar la estructura de la base de datos en tiempo de ejecución.

---

### 4. Reglas de Codd para un Sistema Relacional

Codd propuso **12 reglas**, pero en el contenido solo se mencionan algunas de ellas:

- **Regla 0 (fundacional)**: cualquier sistema que se proclame relacional debe gestionar bases de datos mediante sus capacidades relacionales.
- **Regla 1 (información)**: toda la información se representa mediante valores en las filas y columnas de las tablas.
- **Regla 2 (acceso garantizado)**: cada valor puede ser accedido mediante la especificación de la tabla, la columna y la clave primaria.
- **Regla 3 (tratamiento sistemático de valores nulos)**: los campos nulos deben estar soportados por el sistema.
- **Regla 4 (catálogo en línea)**: la estructura debe estar guardada en un catálogo accesible y actualizado en línea.

---

### 5. Integridad de Datos

La **integridad** en bases de datos asegura que la información sea **correcta** y **consistente**:

- **Integridad de dominio**: los valores de los atributos deben pertenecer a dominios definidos (por ejemplo, una edad debe ser un número positivo).
- **Integridad de entidad**: cada entidad (registro) debe ser identificable de forma única por una clave primaria.
- **Integridad referencial**: las relaciones entre tablas deben mantenerse; si una fila se referencia en otra, esa referencia debe existir.

Ejemplo de **integridad de entidad**:

- En una tabla de alumnos, la clave **Legajo** o **ID** debe ser única.

Ejemplo de **integridad referencial**:

- En una relación entre estudiantes y cursos, si un estudiante inscribe en un curso, el curso debe existir en la tabla de cursos.

---

### 6. Operaciones en el Modelo Relacional

Las operaciones básicas que permiten manipular conjuntos de datos son:

- **Selección** (`σ`): filtrar filas que cumplen con una condición.
- **Proyección** (`π`): seleccionar columnas específicas.
- **Unión** (`∪`), **intersección** (`∩`), **diferencia** (`−`), **producto cartesiano** (`×`).
- **Join**: combinar relaciones basadas en atributos relacionados.
- **Renombrar**: cambiar nombres de atributos o relaciones para evitar ambigüedades.

El **optimizador** de consultas decide automáticamente la mejor estrategia para ejecutar estas operaciones de manera eficiente, basándose en la información del catálogo.

---

### 7. Funciones y Restricciones del DBMS Relacional

- La base de datos debe **guardar todos los objetos** (tablas, vistas, índices) en un **catálogo**.
- La **seguridad** se soporta mediante control de accesos, roles y restricciones, apoyándose en el inventario del catálogo.
- El **optimizador** selecciona la mejor forma de ejecutar las consultas para obtener alta eficiencia, usando estadística y metadatos disponibles.

---

### 8. Aspectos de Integridad y Restricciones

Se consideran diferentes tipos:

- **Integridad de dominio**: atributos deben estar en sus dominios.
- **Integridad de entidad**: claves primarias deben ser únicas y no nulas.
- **Integridad referencial**: las relaciones entre tablas deben mantenerse consistentes.

Estas reglas previenen errores y mantienen la calidad de los datos.

---

### 9. Resumen de la estructura del modelo

El **modelo relacional** combina:

- La estructura **tablas** con atributos y valores.
- La **integridad** de los datos mediante reglas y restricciones.
- La **manipulación** mediante operaciones relacionales.
- La gestión mediante un **catálogo en línea** que soporta optimización y seguridad.

---

### 10. Ejemplo práctico: Tabla de alumnos

Se describe una relación con atributos como:

(Los que están en negrita serían claves candidatas)

- **Legajo (clave primaria)**
- Nombre
- Apellido
- Sexo
- **TipoDoc**
- **Nro.Doc**
- **CUIL**
- Domicilio
- Fecha Nacimiento

Se puede definir una **clave candidata** (un conjunto mínimo de atributos que identifican de forma única una fila). La **clave primaria** es una clave candidata seleccionada para identificación única.

---
### Preguntas

1. **¿Cuál fue el primer motor de BD relacional?**
    - El primer motor de base de datos relacional fue el System R, desarrollado por IBM en la década de 1970.
2. **¿Cuál fue el primer RDBMS en ser comercializado?**
    - El primer RDBMS comercializado fue Oracle, lanzado en 1979.
3. **¿Qué operaciones básicas se pueden realizar sobre las relaciones?**
    - Las operaciones básicas son Select, Project y Join.
4. **¿Qué es la propiedad de Cierre o Clausura?**
    - Es la propiedad que asegura que el resultado de realizar operaciones sobre relaciones también sea una relación.
5. **Nombre 3 componentes de una relación.**
    - Atributos, Tuplas y Dominio.
6. **¿Qué es DOMINIO?**
    - Es el conjunto de valores permitidos para un atributo en una relación.
7. **¿Qué es una clave primaria?**
    - Es un atributo que identifica de manera única cada tupla en una relación y no puede contener valores nulos.
8. **¿Qué es una clave foránea? Ejemplo?**
    - Es un atributo en una tabla que se refiere a la clave primaria de otra tabla. Por ejemplo, en la tabla "Empleados", "Depto#" puede ser una clave foránea que referencia a "Depto#" en la tabla "Departamentos".