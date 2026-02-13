## 📌 1. ¿Qué es el método Huffman?

El **algoritmo de Huffman** es un método de **codificación óptima** (dentro de los códigos prefijo) que asigna **códigos binarios de distinta longitud** a cada símbolo, en función de su **probabilidad de aparición**.

🎯 **Objetivo:**  
Reducir la **longitud promedio del código** ($L$) lo más cerca posible de la **entropía** ($H$) de la fuente.

---

## 📌 2. Características clave

- Es **un código instantáneo** (prefijo) → ningún código es prefijo de otro.
    
- Es **unívocamente decodificable**.
    
- Es **compacto** → no existe otro código prefijo con menor longitud promedio para esas probabilidades.
    
- **Longitudes más cortas** para los símbolos **más probables**.
    
- **Longitudes más largas** para los símbolos **menos probables**.
    

---

## 📌 3. Procedimiento paso a paso

1. **Listar símbolos y probabilidades** de la fuente.
    
2. **Ordenar** de menor a mayor probabilidad.
    
3. **Combinar** los dos símbolos **menos probables en un nodo**, sumando sus probabilidades.
    
4. Repetir el paso anterior hasta quedar con un único nodo (árbol completo).
    
5. **Asignar** 0 y 1 a las ramas de cada unión (convención: izquierda 0, derecha 1).
    
6. Leer los códigos desde la raíz hasta cada símbolo.


> [!warning] IMPORTANTE
> Es importante **Combinar** los dos símbolos **menos probables en un nodo**


---

## 📌 4. Ejemplo

### Fuente:

|Símbolo|Probabilidad|
|---|---|
|A|0.4|
|B|0.3|
|C|0.2|
|D|0.1|

---

### Paso 1: Ordenar (menor a mayor)

D (0.1), C (0.2), B (0.3), A (0.4)

---

### Paso 2: Combinar los dos menores

- C (0.2) + D (0.1) → nodo CD (0.3)
    

Lista:  
CD (0.3), B (0.3), A (0.4)

---

### Paso 3: Repetir

- CD (0.3) + B (0.3) → nodo CDB (0.6)
    

Lista:  
CDB (0.6), A (0.4)

---

### Paso 4: Última unión

- CDB (0.6) + A (0.4) → nodo raíz (1.0)
    

---

### Paso 5: Asignar bits

```mathematica
           (1.0)
          /     \
       (0.6)     A:0.4
      /     \
   (0.3)     B:0.3
  /     \
D:0.1   C:0.2

```

Asignación de bits:

- Izquierda: 0
    
- Derecha: 1
    

Códigos:

- A = 1
    
- B = 01
    
- C = 001
    
- D = 000
    

![[Pasted image 20250730200007.png]]

---

## 📌 5. Cálculo de la longitud promedio

$$L = \sum p_i \cdot l_i$$$$L = (0.4 \cdot 1) + (0.3 \cdot 2) + (0.2 \cdot 3) + (0.1 \cdot 3) = 1.9 \, \text{bits/símbolo}$$
---

## 📌 6. Relación con la entropía

$$H = -\sum p_i \log_2 p_i$$​$$H \approx 1.846 \, \text{bits/símbolo}$$$$E = \frac{H}{L} \approx 97.16\%$$

→ Es muy eficiente.

---

## 📌 7. Usos del código Huffman

- Compresión de datos (ZIP, GZIP, 7z)
    
- Codificación de imágenes (JPEG)
    
- Compresión de audio (MP3, AAC)
    
- Transmisiones digitales con compresión de fuente