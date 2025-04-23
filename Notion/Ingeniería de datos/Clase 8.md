# Indices

Es una estructura de datos que permite acceder más rápidamente a la información en las tablas

- Asociando a una tabla
- No produce acoplamiento
- Tabla independiente del índice
- Diferentes tipos
- Algunos se crean en forma implícita

## Clasificación por tipo

Los índices puede ser **únicos o duplicados** y **simples o compuestos**

- Único: No puede estar repetido
- Duplicado: Puede contener valores repetidos
- Simple: Conformado por un solo atributo
- Compuesto: Formado por varios atributos

## Tipos según su estructura física

- Binary tree, Binary tree +
- Cluster
- Hash
- Bitmap

# Índices - Binary Tree

Es una estructura de datos de tipo árbol balanceado compuesto por nodos que contienen varios valores y punteros

- Posee un nodo raiz, nodos internos y nodos hojas.
- Se dice de **orden n** cuando cada nodo que no sea hoja tiene entre n/2 y n hijos

![[Pasted image 20250422202149.png]]

# Índices - Binary Tree +

Lo que cambia entre un Binary Tree, es que si hacemos una búsqueda secuencial, solo vemos los nodos hojas y cada nodo hoja esta conectado a su nodo adyacente a través de un puntero.

![[Pasted image 20250422202337.png]]


# Índices - Cluster

- Es una estructura de datos de tipo árbol balanceado compuesto por nodos que contienen varios valores y punteros cuyas hojas contienen los datos del registro de la tabla correspondiente
- Los registros de la tabla se ordenan por los valores del índice
- Solo puede haber un índice Cluster por tabla

La parte de “datos” representaría el disco. Este índice evita saltar al disco ya que cada nodo tiene sus datos asociados

![[Pasted image 20250422202649.png]]

> [!Tip]
> Todos los bd relacionales utilizan Binary Tree


# Índices - Hash

- Utilizados para búsquedas puntuales “=”
- Búsquedas con TODOS los atributos de la clave
- Menor tamaño que Binary Tree
- Más rápidos que BInary tree

![[Pasted image 20250422203202.png]]

## Conceptos

- Bucket: Es una unidad de almacenamiento que ocupa normalmente un bloque de disco con varios registros. Cada bucket contiene una colección de pares **(clave, valor, puntero)**
- Hash function: Funcion h(k) cuyo resultado mapea a una dirección donde se encuentra un bucket

## Tipos - Hashing estático

El tamaño del bucket es fija

- Open Hashing
	- ![[Pasted image 20250422203348.png]]
- Closed Hashing
	- ![[Pasted image 20250422203452.png]]


## Tipos - Hashing dinámico o extendido

- Supongamos que la **dirección global es 2** → usamos los primeros 2 bits del hash.
- Tenemos 4 entradas en el directorio (`00`, `01`, `10`, `11`), apuntando a buckets.
- Insertamos claves hasta que un bucket se llena.
- Si el bucket de `01` se llena:
    - Si su dirección local es menor que la global → se divide solo ese bucket.
    - Si no, se **duplica** el directorio a 8 entradas (3 bits), y se redistribuyen las claves.

![[Pasted image 20250422203810.png]]

### Desventajas

- Ante el aumento de colisiones pierden eficiencia
- No están ordenados
- No son eficientes para búsquedas por rangos
- No son eficientes para búsquedas por NOT =
- No son eficientes para búsquedas con LIKE


## Índices - Bitmap

- Utiliza mapas de bits
- Un índices de mapas de bits sobre el atributo A de la relación r consiste en un mapa de bits para cada valor que pueda tomar A
- Cada mapa de bits tiene tantos bits como el número de registros de la tabla
- Se utilizan en atributos con baja cardinalidad

![[Pasted image 20250422204738.png]]

### Ventajas

- Reducidos tiempos de respuesta
- Reducido tamaño de almacenamiento
- Buena performance
- Incluye en el índice valores NULL
- Sistemas OLAP (On-Line Analytical Processing)

### Desventajas

- Costoso para aplicaciones con muchas actualizaciones concurrentes (OLTP)


## Índices en general

### Ventajas

- Acceso más rápido a la información
- Integridad (Pk, Fk)

### Desventajas

- Espacio en disco
- Mantenimiento (insert, update, delete)


# Ejemplos de Índices

![[Pasted image 20250422205201.png]]


# Select - Join / Inner Join

![[Pasted image 20250422210623.png]]

![[Pasted image 20250422210642.png]]

![[Pasted image 20250422210653.png]]

![[Pasted image 20250422210712.png]]

> [!Usar Alias]
> Siempre utilizar alias por dos motivos. 
> 1. Cada vez que se refiera a una columna, va a ser muy extenso referirse a la columna de una tabla.
> 2. Siempre que hagamos una referencia a una columna, usar un alias, como la tercera imágen “SELECT c.cliente_num”, no como la primera “SELECT legajo”


# Select - Left Outer Join / Left Join

Si la de la izquierda no matchea, lo trae igual

![[Pasted image 20250422211712.png]]

![[Pasted image 20250422211721.png]]


# Select - Right Outer Join / Right Join

Si la de la derecha no matchea, lo trae igual

![[Pasted image 20250422211842.png]]

![[Pasted image 20250422211857.png]]

> [!Consejo]
> Utilizar siempre el LEFT JOIN ya que, si se dan vuelta las tablas, se obtiene un RIGHT JOIN


# Select - Full Outer Join / Full Join

Matchee o no matchee lo de la izquierda o lo de la derecha, lo trae igual

![[Pasted image 20250422212039.png]]

![[Pasted image 20250422212049.png]]


# Select - Union

Agarra las filas de una tabla en relación de una query y las agrega al resultado de otra query. Además, elimina los duplicados, es decir, los registros cuyas columnas son exactamente igual, si existe alguna columna distinta, son registros distintos, por ende no se eliminan.

![[Pasted image 20250422212205.png]]

> [!Consejo]
> Deben ser compatibles, mismas columnas y mismo dominio


# Select - Union All

Igual que el Union, pero no elimina los duplicados

![[Pasted image 20250422212411.png]]


# Select - Intersect

![[Pasted image 20250422212753.png]]

> [!Consejo]
> No es lo mismo un inner join por que el inner join trabaja con tablas, y el intersect con filas, por lo tanto, el intersect siempre devuelve la misma cantidad de columnas que con las que se trabaja, y el inner join puede traer más o menos columnas


# Select - Except / Minus

![[Pasted image 20250422213052.png]]


**Tarea para el hogar, ver ejercicios de la clase 7.**