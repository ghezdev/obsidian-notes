# BD Relacionales 

Las BD relacionales se basan en el modelo relacional de datos
  - - - 
# Modelo relacional

Está basado en la teoría de conjuntos

- - -
# Relación

- Los atributos (columnas) poseen un “dominio”. _En matemáticas el dominio son los valores en los cuales está definida la función_
- Grado: cantidad de atributos de la relación
- Cardinalidad: cantidad de tuplas de la relación

- - -
# Propiedades de la relación

- En una relación no existen tuplas repetidas
- Las filas y atributos no están ordenadas
- Los valores de los atributos son atómicos

**Existen relaciones recursivas, son campos pertenecientes a una tabla que referencian a la misma tabla**

- - -
# Relación - Catálogo

- El DBMS debe proporcionar una función de catálogo o diccionario
- Es el lugar donde se guardan todos los objetos de la BD
- El Optimizador utiliza información del catálogo para decidir cómo ejecutar las peticiones del usuario
- El componente de Seguridad utiliza esta información de usuarios y restricciones de seguridad para autorizar o negar digas peticiones

**El catálogo consiste en tablas de la BD que describen los objetos y datos (Metadata)**

- - -  
# Operaciones

- Select: FIltrar/restringir
- Project: Proyectar
- Join: Juntar  
  
Conclusiones:

- Se pueden anidar y combinar operaciones
- Se producen resultados intermedios
- Las operaciones se realizan sobre las relaciones
- Se cumple la propiedad de Cierre o Clausura. _Se refiere a que si aplicamos una operación sobre un conjunto de datos dentro de la base, el resultado también pertenece al mismo conjunto o es un conjunto válido dentro de la misma estructura._

- - -
# Operaciones - Optimizador

- Todas las operaciones relacionales son a nivel de conjunto
- Los usuarios especifican el qué y no el cómo
- Los lenguajes como SQL están en un nivel más alto de abstracción que lenguajes como C++ y COBOL
- La responsabilidad de cómo ejecutar es del optimizador
- Es trabajo del optimizador seleccionar una forma eficiente de implementar las peticiones

- - -
# Integridad

El término integridad de datos se refiere a la correctitud y completitud de la información de una base de datos

- Integridad de Dominio
- Integridad de Entidad
- Integridad Referencial

- - -
# Integridad de Dominio

Conjunto de valores válidos que puede tomar un atributo

- Cada atributo tiene asociado un dominio
- Menor unidad de información
- Atómicos
- De igual tipo

Ej. de errores de integridad de dominio 
- Atributo con valores inválidos. 
- Fecha con formato erróneo 
- Tipo de dato erróneo 
- Etc
- - -  
# Implementación de un dominio

- Tipos de datos
- Null / Not null
- Chequeos de valores
- Convención de nombres

- - -
# Claves - Integridad de las entidades

- **Claves candidatas**. _Aquellas que son candidatas a ser claves primarias_
- **Claves primarias**. _Me doy cuenta que es una clave primaria porque es la forma de recuperar una única tupla_
- **Claves alternativas**

- - -
# Integridad de las entidades

- La clave primaria identifica unívocamente. _1 y solo 1_
- No puede existir una instancia de relación sin identidad
- Sólo debe existir una clave primaria en una relación
- Una clave primaria puede estar compuesta por varios atributos
- Ningún atributo de la clave primaria de una relación puede aceptar nulos

- - -
# Integridad referencial

La integridad referencial es una restricción fundamental en bases de datos relacionales que garantiza la consistencia de las relaciones entre tablas mediante claves foráneas. Esto significa que si una tabla A tiene una clave foránea que referencia a una clave primaria en otra tabla B, los valores en la clave foránea deben existir ya en la tabla B para mantener la coherencia de datos.

## Clave foránea (FK)

- Es un atributo o conjunto de atributos que hacen referencia a una clave primaria de otra tabla
- Las entidades que interactúan no son necesariamente distintos
- Todos los valores que toma una clave foránea deben ser valores existentes en la clave primaria de referencia
- Una clave foránea y la clave primaria correspondiente se definen sobre el mismo dominio
- La clave foránea no necesita ser parte de la PK de la relación que la contiene
- Una relación puede ser tanto una relación referida como una relación referente
- Las FK pueden tomar valores nulos  

## Clave subrogada

Clave sin significado dentro del negocio que identifica unívocamente una fila
Ej. (Id, Legajo, Nombre, apellido, Dni, …)


## Qué hacer ante la Inserción de una FK (clientes, órdenes)

Al insertar registros en una tabla que contiene claves foráneas, el sistema de gestión de bases de datos (DBMS) necesita seguir ciertas reglas para mantener la integridad referencial. Estas reglas pueden configurarse para determinar el comportamiento cuando se realiza una operación de inserción o actualización que involucra claves foráneas.

Existen varias acciones posibles que puede tomar el DBMS en estos casos, entre ellas:

- **Restricción (Restrict):** La inserción o actualización será denegada si la clave foránea no tiene un valor correspondiente en la tabla referenciada. Es decir, no se permite insertar un registro que tenga una clave foránea con un valor inexistente en la tabla primaria. _Ejemplo:_ No se puede crear una orden con un cliente que no exista en la tabla de clientes. 
  
- **Cascada (Cascade):** Cuando se realiza una operación (como eliminar o actualizar) en un registro clave, las acciones correspondientes se propagan automáticamente a los registros relacionados. Por ejemplo, si eliminas un cliente, todas las órdenes relacionadas también se eliminarán automáticamente. _Importancia:_ Esto asegura que no queden registros huérfanos en las tablas relacionadas.
  
- **Nulo (Set Null):** En lugar de impedir la operación, el sistema pone en null los valores de las claves foráneas que están relacionadas cuando la fila referenciada se elimina o actualiza. _Ejemplo:_ Si un cliente es eliminado, las órdenes que tenían ese cliente pueden tener su clave foránea puesta en null, indicando que ahora no están relacionadas con ningún cliente.

Para este caso, solo se usaría 

- **Restricción (Restrict)**
## Qué hacer ante la Eliminación de una PK (clientes, órdenes)

- **Restricción (Restrict)**
- **Cascada (Cascade)**
- **Nulo (Set Null)**

## Qué hacer ante la Modificación de una PK (clientes, órdenes)

- **Restricción (Restrict)**
- **Cascada (Cascade)**
- **Nulo (Set Null)**

- - -
# Equivalencias de conceptos

Es como un glosario. Se comparten conceptos, pero tienen diferentes nombres. 
Lo que es relación para Modelo Relacional, para Base de datos es tabla, y para Archivo es archivo.

![[image 6.png]]

- - -
# Reglas de Codd

**Las doce** reglas de Codd son un conjunto de trece reglas diseñadas para definir lo que se requiere de un sistema de gestión de bases de datos para que sea considerado relacional, es decir, un sistema de gestión de bases de datos relacionales (RDBMS).

## Regla 0: **Regla de fundación**

Cualquier sistema que se proclame como relacional, debe ser capaz de gestionar sus bases de datos mediante sus capacidades relacionales.


## Regla 1: **Regla de la información**

Toda la información en la base de datos es representada unidireccionalmente por valores en posiciones de las columnas dentro de filas de tablas.


## Regla 2: **Regla del acceso garantizado**

Cada valor escalar individual en la base de datos debe ser lógicamente direccionable especificando el nombre de la tabla, la columna que lo contiene y la clave primaria.


## Regla 3: **Regla del tratamiento sistemático de valores nulos**

El sistema de gestión de base de datos debe permitir que haya campos nulos.


## Regla 4: **Catálogo basado en el modelo relacional**

El sistema debe soportar un catálogo en línea que da acceso a la estructura de la base de datos y que debe ser accesible a los usuarios autorizados.


## Regla 5: **Regla comprensiva del sublenguaje de los datos**

El sistema debe soportar un lenguaje relacional tenga soporte de operaciones de definición de datos, operaciones de manipulación de datos (actualización así como la recuperación), de control de la seguridad e integridad y operaciones de administración de transacciones.


## Regla 6: **Regla de actualización de vistas**

Todas las vistas que son teóricamente actualizables deben poder ser actualizadas.


## Regla 7: **Alto nivel de inserción, actualización y borrado**

El sistema debe permitir la manipulación de los datos.


## Regla 8: **Independencia física de los datos**


## Regla 9: **Independencia lógica de los datos**


## Regla 10: **Independencia de la integridad**

Las restricciones de integridad se deben especificar por separado de los programas de aplicación y almacenarse en la base de datos. Debe ser posible cambiar esas restricciones sin afectar necesariamente a las aplicaciones existentes.


## Regla 11: **Independencia de la distribución**

La distribución de porciones de base de datos en distintas localizaciones debe ser transparente para los usuarios de la base de datos.


## Regla 12: **La regla de la no subversión**

Si el sistema proporciona una interfaz de bajo nivel de registro, aparte de una interfaz relacional, esa interfaz de bajo nivel no debe permitir su utilización por ejemplo para sortear las reglas de seguridad relacional o las restricciones de integridad.

- - -
# Preguntas

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