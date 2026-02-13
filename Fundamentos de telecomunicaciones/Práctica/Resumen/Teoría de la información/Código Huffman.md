## 📦 ¿Qué es un código óptimo?

Un **código óptimo** es aquel que permite representar los símbolos de una fuente **con la menor cantidad promedio de bits posible**, **sin perder información**.

En otras palabras:

> Un código óptimo **minimiza la longitud media del código** $L$, y se acerca tanto como sea posible a la **entropía** $H$ de la fuente.

---

## 🧠 ¿Qué es el código de Huffman?

El **código de Huffman** es un algoritmo que:

- Genera un **código binario sin prefijos** (ningún código es prefijo de otro).
  
- Asigna **códigos más cortos a símbolos más probables**, y códigos más largos a los menos probables.
  
- Es **óptimo para fuentes sin memoria** y probabilidades conocidas.

---

## 🧮 ¿Cómo se construye un código de Huffman?

### Paso 1: Tener la lista de símbolos con sus probabilidades.

Ejemplo:

|Símbolo|Probabilidad|
|---|---|
|A|0.4|
|B|0.3|
|C|0.2|
|D|0.1|

### Paso 2: Ordenar los símbolos de menor a mayor probabilidad.

### Paso 3: Combinar los dos de menor probabilidad, formando un **nodo**.

- Se suman sus probabilidades.
  
- El nodo resultante entra en la lista.

### Paso 4: Repetir hasta que quede un solo nodo (el árbol completo).

### Paso 5: Asignar **0** y **1** a cada rama del árbol, recorriéndolo desde la raíz.

![[Pasted image 20250730200007.png]]

---

## 🔁 ¿Qué propiedades tiene el código de Huffman?

- Es **compacto**: se acerca lo más posible a la entropía.
  
- Es **sin ambigüedad**: se puede decodificar de forma única.
  
- Es **sin prefijos**: ideal para transmisión secuencial.
  
- No siempre es único (puede haber varios árboles equivalentes).

---

## 🧪 Ejemplo completo (rápido):

Dada esta fuente:

|Símbolo|Probabilidad|
|---|---|
|A|0.5|
|B|0.25|
|C|0.125|
|D|0.125|

### Paso 1: Construcción

1. Combinar C y D → nodo CD = 0.25
   
2. Combinar B y CD → nodo BCD = 0.5
   
3. Combinar A y BCD → raíz = 1
   

### Paso 2: Asignación de bits (una posible):

- A → 0
  
- B → 10
  
- C → 110
  
- D → 111
  

### Longitud media:
$$L=0.5⋅1+0.25⋅2+0.125⋅3+0.125⋅3=1.75\ bits/símbolo$$

### Entropía:
$$H=\sum^{n}_{i=1} p_i * log_2(p_i)≈1.75\ bits/símbolo$$

🔁 ¡El código es óptimo! $L=H$

[[CodigoHuffmanEjemplo.excalidraw]]

---

## 📌 Aplicaciones del código de Huffman

- Compresión de texto (ZIP, GZIP, PNG)
  
- Compiladores y representaciones binarias eficientes
  
- Transmisiones digitales con restricciones de ancho de banda