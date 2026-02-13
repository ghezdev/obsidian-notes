# 2) Código bloque binario (longitud fija)

Para un alfabeto de $M=8$ símbolos, bits por símbolo:

$$L_\text{bloque}=\lceil \log_2 8\rceil=3\ \text{bits/símbolo}$$

Archivo de 100 símbolos → **$100\times 3=300$**.

# 3) Código compacto óptimo (Huffman)

Pasos que debés saber:

1. Ordená probabilidades (menores a mayores).
    
2. Uní de a pares las dos menores y reemplazalas por su suma. Repetí hasta quedar en 1.
    
3. Recorriendo el árbol, asigná 0/1 para obtener palabras prefijo.
    
4. Calculá la **longitud media** Lˉ=∑pi⋅li\bar L=\sum p_i \cdot l_iLˉ=∑pi​⋅li​.
    

Para estas pip_ipi​ (0.06, 0.06, 0.07, 0.08, 0.13, 0.18, 0.21, 0.21), una codificación posible es:

- D: 00 (2)
    
- F: 01 (2)
    
- A: 111 (3)
    
- H: 101 (3)
    
- B: 1100 (4)
    
- E: 1101 (4)
    
- C: 1000 (4)
    
- G: 1001 (4)
    

_(Los códigos pueden cambiar por empates, pero las longitudes lil_ili​ quedan iguales)._

Longitud media:

Lˉ=0.21⋅2+0.21⋅2+0.18⋅3+0.13⋅3+(0.08+0.07+0.06+0.06)⋅4=2.85 bits/sıˊmbolo.\bar L = 0.21\cdot2 + 0.21\cdot2 + 0.18\cdot3 + 0.13\cdot3 + (0.08+0.07+0.06+0.06)\cdot4 = \mathbf{2.85\ bits/símbolo}.Lˉ=0.21⋅2+0.21⋅2+0.18⋅3+0.13⋅3+(0.08+0.07+0.06+0.06)⋅4=2.85 bits/sıˊmbolo.

Archivo de 100 símbolos → **100×2.85=285100\times 2.85 = 285100×2.85=285 bits**.

# 4) Porcentaje de compresión

Compresioˊn=1−taman˜o compactotaman˜o bloque=1−285300=5%.\text{Compresión} = 1-\frac{\text{tamaño compacto}}{\text{tamaño bloque}} =1-\frac{285}{300}=\mathbf{5\%}.Compresioˊn=1−taman˜o bloquetaman˜o compacto​=1−300285​=5%.

> Bonus (intuición): la entropía de la fuente es ≈2.82\approx 2.82≈2.82 bits/símbolo, así que 2.85 está muy cerca del límite teórico—tu Huffman es casi óptimo.