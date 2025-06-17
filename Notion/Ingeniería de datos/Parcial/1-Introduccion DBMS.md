# Que es una base de datos?

Sistema de software cuyo objetivo es almacenar datos y permitirle a los usuarios realizar operaciones sobre dichos datos

- - -
# Componentes de una base de datos

## Datos

- Información consistente (mínima redundancia)
- Información compartida
- Se percibe a la BD de diferentes formas

## Software

- DBMS: Database Management System
- Interfaz entre la BD y los programas o usuarios finales
- Almacenamiento, lectura, actualización y borrado de información
- Accesos y control de la información
- Integridad
- Copias de seguridad

## Hardware

- Servidores
- Procesadores
- Memoria
- Unidades de almacenamiento

- - -   
# Que hace un DBA

- Crear el nivel conceptual y físico de una BD
- Privilegios y accesos
- Asistencia a devs
- Almacenamiento
- Instalaciones
- Monitoreo
- Mantenimiento
- Backup

- - -
# Tipos de BD

- **Relacionales**: Se utilizan para un sin número de casos, cuando se requiere manejo de transacciones y consistencia
- **No SQL**: No requieren un schema, no garantizan consistencia ACID, escalan horizontalmente, mayor volumen de datos
    - **Clave/Valor**: Buenos tiempos de respuesta, no implementan integridad, tamaño pequeño, usadas para cache o sesiones
    - **Documentales**: Almacenan los datos en forma de árbol, son schemaless, no suelen manejar transacciones
    - **Columnares**
    - **Grafos**: Estan formados por nodos y arcos
- **Otros**
    - Time Series
    - Orientado a objetos

- - -
# RDBMS

Software en la que actúa una BD que almacena datos relacionados entre sí, representados por tablas con mínimo o nulo nivel de redundancia

- - - 
# Ventajas de RDBMS

- Los datos pueden compartirse
- Control de la redundancia
- Minimizar la incosistencia de datos
- Manejo de transacciones
- Integridad de datos
- Seguridad
- Independencia de Datos
- Lenguaje estándar
- Diferentes “visiones” para diferentes usuarios

- - -
# Entidades

Conjunto de objetos distinguibles y agrupados de los cuales se desea registrar información

- - -  
# Relaciones

Vínculos entre las entidades

- - -
# Propiedades

Datos relativos a las entidades. Simples y de un tipo específico

- - -  
# Independencia de datos

- **Independencia lógica**: Inmunidad de las aplicaciones frente a cambios en las tablas de la aplicación
- **Independencia Física**: Inmunidad de las aplicaciones frente a cambios en la representación física y acceso a los datos

- - -  
# Que es una transacción?

Es un conjunto de operaciones que deben (o no) realizarse en su totalidad.

En el conjunto de operaciones, o se ejecutan todas, o no se ejecutan ninguna. Por lo tanto, si una falla, de las n operaciones, todas se cancelan

- - -
# Propiedades de transacciones ACID

- **A - Atomicidad:** Es como si fuera una operación
- **C - Consistencia**: Antes de empezar una transacción, la BD es consistente y una vez finalizada la transacción, también
- **I - Aislamiento:** Las operaciones de una transacción están ocultas a las demás
- **D - Durabilidad**: Las actualizaciones perduran en la BD aunque haya una caída posterior

- - -
# Que es un sistema relacional?

Son aquellos que:

- Los datos son percibidos como tablas
- Las operaciones disponibles generan nuevas tablas a partir de las anteriores

- - -
# Que es un esquema de Base de Datos?

Es la visión que tienen los diferentes usuarios de la base de datos

- - -
# Arquitectura ANSI-SPARC

- **Nivel Externo:** Nivel de abstracción más alto. Provee diferentes vistas de la misma BD a diferentes usuarios brindando seguridad escondiendo partes de la BD a usuarios particulares
- **Nivel Lógico:** Describe la estructura de la BD. Explica qué datos se almacenan en las tablas de la BD, tipos y relaciones entre las tablas. Hay un solo esquema conceptual por BD
- **Nivel Físico:** Nivel más bajo de abstracción. Describe cómo se almacenan los datos en la BD y provee los métodos para accederlos
  
## Interfaces entre los niveles de la Arquitectura ANSI-SPARC

- **Interfaz entre el nivel externo y conceptual**: Define la correspondencia entre los datos de la capa externa y la capa conceptual
- **Interface entre el nivel conceptual e interno**: La interfaz entre el nivel conceptual e interno identifica cómo se almacenan y acceden los registros lógicos en el nivel interno

- - -
# Funciones de un RDBMS

- Definición de datos
- Consulta y recuperación de datos
- Manipulación de datos
- Ejecución
- Optimización
- Integridad de datos
- Seguridad
- Catálogo