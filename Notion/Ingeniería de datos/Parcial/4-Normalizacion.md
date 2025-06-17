# Claves

- **Candidatas**
    - Sea K un conjunto de atributos de la relación R. K es una clave candidata de R sí y solo sí, posee las dos propiadades siguientes
        - Unicidad: NIngún valor de R contiene dos tuplas distintas con el mismo valor de K
        - Irreductibilidad: NIngún subconjunto propio de K tiene la propiedad de unicidad
- **Primarias**
    - Atributo que más probable que sea candidata
- **Alternativas**
    - Atributos que son menos probables en comparación de la primaria que sean candidatas
- **Foráneas**
    - Sea R2 una relación ⇒ una clave foránea en R2 es un conjunto de atributos de R2 (FK) tal que:
        - Exista una relación R1 (R1 y R2 pueden ser iguales) con una clave PK
        - Cada valor de la FK de R2 es igual al valor de la PK en alguna tupla de R1

**Las claves primarias y foráneas pueden ser simples o compuestas**



![[/image 13.png|image 13.png]]

- - -  
# Dependencia funcional

Sea **R** una relación y sean **X** e **Y** subconjuntos arbitrarios del conjunto de atributos de **R**. Entonces decimos que **Y depende funcionalmente** de **X** (o X **determina** funcionalmente a **Y**) sí y sólo sí cada valor de **X** está relacionado con **SOLO** un valor de **Y**

En símbolos: **X ⇒ Y**
**Determinante** ⇒ **Dependiente**

![[/image 1 5.png|image 1 5.png]]

En la tabla VP existe una dependencia funcional entre el conjunto de atributos {V#, P#} y el conjunto de atributos {CANT} si …

- Para cualquier valor del par de atributos V# y P#, sólo existe **un** valor correspondiente del atributo CANT …
- Aunque muchos valores distintos del par de atributos V# y P# pueden tener el mismo valor del atributo CANT
  
El determinante suele estar relacionado a los atributos **claves** mientras que los dependientes a los atributos **no claves**

- - -
# Normalizacion - Objetivos

- Eliminar redundancias
- Evitar anomalías en las actualizaciones
- Simplificar las reglas de integridad
- Crear un modelo que represente el mundo real

- - -
# Primera forma normal

- Una relación está en 1ra forma normal **si todos sus dominios contienen valores atómicos**
- Una relación está en 1ra forma normal **si toda tupla (fila) contiene exactamente un valor para cada atributo**


![[/image 2 5.png|image 2 5.png]]

- - -
# Segunda forma normal

Una relación está en 2da forma normal **sí y solo sí está en 1ra forma normal y todos los atributos no clave dependen completamente de la clave primaria**

![[/image 3 5.png|image 3 5.png]]
  
- - -
# Tercera forma normal

- Dependencia funcional transitiva
    - Si R(a,b), R(b,c) ⇒ R(a,c)
- Una relación está en 3ra forma normal **sí y solo sí está en 2da forma normal y todos los atributos no claves dependen de manera NO transitiva de la clave primaria**

![[/image 4 4.png|image 4 4.png]]

- - -  
# Forma normal Boyce/Codd

Una relación está en BCNF **sí y solo sí todo determinante es clave candidata**

***Determinante: Atributo del cual depende funcionalmente otro atributo***
  
![[/image 5 3.png|image 5 3.png]]

- La clave candidata es (Profesor, Materia)
- Existen 2 dependencias funcionales:
    - (Profesor, Materia) ⇒ aula
    - (aula) ⇒ (materia)
- Aula no es clave candidata pero sí es determinante


![[/image 6 3.png|image 6 3.png]]
  
- - -
# Cuarta forma normal

Una relación está en 4ta forma normal **sí y solo sí está en forma normal Boyce Codd y no contiene dependencias multivaluadas**

![[/image 7 3.png|image 7 3.png]]

- Dependencia multivaluada (DMV)
- Dada una R(a,b,c) la DMV R(a) ⇒ R(b) se cumple en R **sí y solo sí el conjunto de valores de b depende solo de a y no de c**
  

![[/image 8 2.png|image 8 2.png]]

**REQUISITOS**

Debe haber por lo menos 3 columnas (a, b, c)

A ⇒ B para un valor de **a** hay **muchos** valores de **b**

**No debe haber** dependencias entre b y c (independientes)


![[/image 9 2.png|image 9 2.png]]

- - -
# Quinta forma normal

Una relación se encuentra en 5ta forma normal

- Si se encuentra en 4ta forma normal
- No existen relaciones de **dependencias de join** (junta) que no se generen desde las claves. Si se aplicara una consulta entre 3 relaciones independientes entre sí dentro de la 4ta forma normal y se obtuvieran tuplas espurias, entonces no estaría en 5ta forma normal

***Se dice que hay dependencia de Join entre una tabla y sus proyecciones, si es posible obtener la tabla original por medio de la unión (join) de dichas proyecciones***

- - -
# Quinta forma normal - Project Join Normal Form (PJNF)

![[/image 10 2.png|image 10 2.png]]

Si a la relación **R** le agregamos la **regla o restricción**

- Si un **profesor** dicta una **materia**
- esa **materia** utiliza un **libro**
- y ese **libro** es usado por el **profesor**

Entonces

- el **profesor** también debe dictar la **materia** con ese **libro**


![[/image 11 2.png|image 11 2.png]]

Si agregásemos al **profesor White** queda **Matemáticas** utilizando el **libro Pr. Óptica** qué sucedería? Por qué?

![[/image 12 2.png|image 12 2.png]]


![[/image 13 2.png|image 13 2.png]]

Separamos la relación original en 3 proyecciones

![[image 14.png]]

- - -
# Desnormalización

1. Reduce la cantidad de tablas
2. Mejora la performance de lecturas
3. Reglas de negocio (totales, datos históricos)
4. Ralentiza las actualizaciones
5. Aumenta la redundancia
6. Aumenta la complejidad de las actualizaciones
7. Se utiliza en modelos dimensionales (aplicaciones OLAP)