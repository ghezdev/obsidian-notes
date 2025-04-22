![[/image 3.png|image 3.png]]

  

![[/image 1 2.png|image 1 2.png]]

  

- Las preguntas de los multiple choice suelen ser directas
- Solo no está permitido usar internet y celular, todo lo demás podría usarse en un examen
- El examen puede ser un 90% que se hagan en las máquinas de UADE Labs
- Parcial 17/6
- Entrega de TP 27/5

  

### Temas que tratamos

![[/image 2 2.png|image 2 2.png]]

  

### Que es una base de datos?

Sistema de software cuyo objetivo es almacenar datos y permitirle a los usuarios realizar operaciones sobre dichos datos

  

### Componentes de una base de datos

Datos:

- Información consistente (mínima redundancia)
- Información compartida
- Se percibe a la BD de diferentes formas

  

Software:

- DBMS: Database Management System
- Interfaz entre la BD y los programas o usuarios finales
- Almacenamiento, lectura, actualización y borrado de información
- Accesos y control de la información
- Integridad
- Copias de seguridad

  

Hardware:

- Servidores
- Procesadores
- Memoria
- Unidades de almacenamiento

  

### Que hace un DBA

- Crear el nivel conceptual y físico de una BD
- Privilegios y accesos
- Asistencia a devs
- Almacenamiento
- Instalaciones
- Monitoreo
- Mantenimiento
- Backup

  

### Tipos de BD

- Relacionales: _Se utilizan para un sin número de casos, cuando se requiere manejo de transacciones y consistencia_
- No SQL: _No requieren un schema, no garantizan consistencia ACID, escalan horizontalmente, mayor volumen de datos_
    - Clave/Valor: _Buenos tiempos de respuesta, no implementan integridad, tamaño pequeño, usadas para cache o sesiones_
    - Documentales: _Almacenan los datos en forma de árbol, son schemaless, no suelen manejar transacciones_
    - Columnares
    - Grafos: _Estan formados por nodos y arcos_
- Otros
    - Time Series
    - Orientado a objetos

  

### RDBMS

Software en la que actúa una BD que almacena datos relacionados entre sí, representados por tablas con mínimo o nulo nivel de redundancia

  

### Entidades

Conjunto de objetos distinguibles y agrupados de los cuales se desea registrar información

  

### Relaciones

Vínculos entre las entidades

  

### Propiedades

Datos relativos a las entidades. Simples y de un tipo específico

  

### Ventajas de RDBMS

- Los datos pueden compartirse
- Control de la redundancia
- Minimizar la incosistencia de datos
- Manejo de transacciones
- Integridad de datos
- Seguridad
- Independencia de Datos
- Lenguaje estándar
- Diferentes “visiones” para diferentes usuarios

  

### Independencia de datos

- Independencia lógica: _Inmunidad de las aplicaciones frente a cambios en las tablas de la aplicación_
- Independencia Física: _Inmunidad de las aplicaciones frente a cambios en la representación física y acceso a los datos_

  

### Que es una transacción?

Es un conjunto de operaciones que deben (o no) realizarse en su totalidad.

En el conjunto de operaciones, o se ejecutan todas, o no se ejecutan ninguna. Por lo tanto, si una falla, de las n operaciones, todas se cancelan

  

### Propiedades de transacciones ACID

- A - Atomicidad: _Es como si fuera una operación_
- C - Consistencia: _Antes de empezar una transacción, la BD es consistente y una vez finalizada la transacción, también_
- I - Aislamiento: _Las operaciones de una transacción están ocultas a las demás_
- D - Durabilidad: _Las actualizaciones perduran en la BD aunque haya una caída posterior_

  

### Que es un sistema relacional?

Son aquellos que:

- Los datos son percibidos como tablas
- Las operaciones disponibles generan nuevas tablas a partir de las anteriores

  

### Que es un esquema de Base de Datos?

Es la visión que tienen los diferentes usuarios de la base de datos

  

### Arquitectura ANSI-SPARC

![[/image 3 2.png|image 3 2.png]]

  

- **Nivel Externo:** Nivel de abstracción más alto. Provee diferentes vistas de la misma BD a diferentes usuarios brindando seguridad escondiendo partes de la BD a usuarios particulares
- **Nivel Lógico:** Describe la estructura de la BD. Explica qué datos se almacenan en las tablas de la BD, tipos y relaciones entre las tablas. Hay un solo esquema conceptual por BD
- **Nivel Físico:** Nivel más bajo de abstracción. Describe cómo se almacenan los datos en la BD y provee los métodos para accederlos

  

### Interfaces entre los niveles de la Arquitectura ANSI-SPARC

- **Interfaz entre el nivel externo y conceptual**: Define la correspondencia entre los datos de la capa externa y la capa conceptual
- **Interface entre el nivel conceptual e interno**: La interfaz entre el nivel conceptual e interno identifica cómo se almacenan y acceden los registros lógicos en el nivel interno

  

### Funciones de un RDBMS

- Definición de datos
- Consulta y recuperación de datos
- Manipulación de datos
- Ejecución
- Optimización
- Integridad de datos
- Seguridad
- Catálogo