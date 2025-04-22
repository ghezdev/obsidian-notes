![[/image 4.png|image 4.png]]

  

> [!important] Las BD relacionales se basan en el modelo relacional de datos
> 
> ![[/image 1 3.png|image 1 3.png]]

  

### Modelo relacional

Está basado en la teoría de conjuntos

![[/image 2 3.png|image 2 3.png]]

  

### Relación

- Los atributos poseen un “dominio”. _==En matemáticas el dominio son los valores en los cuales está definida la función==_
- Grado: cantidad de atributos de la relación
- Cardinalidad: cantidad de tuplas de la relación

  

### Propiedades de la relación

- No existen tuplas repetidas
- Las filas y atributos no están ordenadas
- Los valores de los atributos son atómicos

  

> [!important] Existen relaciones recursivas, son campos pertenecientes a una tabla que referencian a la misma tabla

  

### Relación - Catálogo

- El DBMS debe proporcionar una función de catálogo o diccionario
- Es el lugar donde se guardan todos los objetos de la BD
- El Optimizador utiliza información del catálogo para decidir cómo ejecutar las peticiones del usuario
- El componente de Seguridad utiliza esta información de usuarios y restricciones de seguridad para autorizar o negar digas peticiones

  

> [!important] El catálogo consiste en tablas de la BD que describen los objetos y datos (Metadata)

  

### Operaciones

- Select: FIltrar/restringir
- Project: Proyectar
- Join: Juntar

  

![[/image 3 3.png|image 3 3.png]]

  

Conclusiones:

- Se pueden anidar y combinar operaciones
- Se producen resultados intermedios
- Las operaciones se realizan sobre las relaciones
- Se cumple la propiedad de Cierre o Clausura. _==Se refiere a que si aplicamos una operación sobre un conjunto de datos dentro de la base, el resultado también pertenece al mismo conjunto o es un conjunto válido dentro de la misma estructura.==_

  

  

### Operaciones - Optimizador

- Todas las operaciones relacionales son a nivel de conjunto
- Los usuarios especifican el qué y no el cómo
- Los lenguajes como SQL están en un nivel más alto de abstracción que lenguajes como C++ y COBOL
- La responsabilidad de cómo ejecutar es del optimizador
- Es trabajo del optimizador seleccionar una forma eficiente de implementar las peticiones

  

### Integridad

Se refiere a la correctitud y completitud de la información de una base de datos

- Integridad de Dominio
- Integridad de Entidad
- Integridad Referencial

  

### Integridad de Dominio

Conjunto de valores válidos que puede tomar un atributo

- Cada atributo tiene asociado un dominio
- Menor unidad de información
- Atómicos
- De igual tipo

  

### Implementación de un dominio

- Tipos de datos
- Null / Not null
- Chequeos de valores
- Convención de nombres

  

### Integridad de las entidades

- Claves candidatas. _==Aquellas que son candidatas a ser claves primarias==_
- Claves primarias. _==Me doy cuenta que es una clave primaria porque es la forma de recuperar una única tupla==_
- Claves alternativas

![[/image 4 2.png|image 4 2.png]]

  

- La clave primaria identifica unívocamente. _==1 y solo 1==_
- No puede existir una instancia de relación sin identidad
- Sólo debe existir una clave primaria en una relación
- Puede estar compuesta por varios atributos
- Ningún atributo de la clave primaria de una relación puede aceptar nulos

  

### Integridad referencial

**Clave foránea (FK)**

- Es un atributo o conjunto de atributos que hacen referencia a una clave primaria de otra tabla
- Las entidades que interactúan no son necesariamente distintos
- Todos los valores que toma una clave foránea deben ser valores existentes en la clave primaria de referencia
- Una clave foránea y la clave primaria correspondiente se definen sobre el mismo dominio
- La clave foránea no necesita ser parte de la PK de la relación que la contiene
- Una relación puede ser tanto una relación referida como una relación referente
- Las FK pueden tomar valores nulos

![[image 5.png]]

  

**Clave subrogada**

Clave sin significado dentro del negocio que identifica unívocamente una fila

  

### Equivalencias de conceptos

![[image 6.png]]