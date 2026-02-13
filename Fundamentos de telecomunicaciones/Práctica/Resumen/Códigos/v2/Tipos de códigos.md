## 1️⃣ **Código en bloque**

- Es un código en el que **todos los símbolos codificados** tienen **la misma longitud** en bits.
    
- Ejemplo:  
    Si tenemos los símbolos $\{A, B, C\}$ y usamos:
    
    - $A = 00$
        
    - $B = 01$
        
    - $C = 10$
        → Cada código tiene **2 bits** → es un **código en bloque**.
        
- Ventaja: fácil de sincronizar, rápida decodificación.
    
- Desventaja: no siempre es eficiente si las probabilidades de los símbolos son muy desiguales.
    

---

## 2️⃣ **Código no singular**

- Un código es **no singular** si **cada símbolo** del alfabeto de la fuente tiene un **código distinto**.
    
- Esto garantiza que no haya **dos símbolos diferentes con el mismo código**.
    
- Ejemplo:
    
    - $A = 0$, $B = 10$, $C = 11$ → **No singular**
        
    - $A = 0$, $B = 0$, $C = 11$ → **Singular** (A y B tienen el mismo código)
        

---

## 3️⃣ **Código singular**

- Es lo contrario: **sí hay** al menos **dos símbolos distintos** que comparten el mismo código binario.
    
- Esto genera **ambigüedad total**, incluso en la codificación de un solo símbolo.
    
- Ejemplo:
    
    - $A = 0$, $B = 0$, $C = 1$ → código **singular**
        

---

## 4️⃣ **Código unívocamente decodificable**

- Incluso si el código **no es en bloque**, se puede decodificar **sin ambigüedad** en un mensaje completo.
    
- Esto significa que **ninguna secuencia de bits válida para un símbolo puede ser confundida con parte de otra secuencia**.
    
- Ejemplo:
    
    - $A = 0$, $B = 01$, $C = 011$ → ❌ **No es unívocamente decodificable**, porque “011” puede interpretarse como C o como A+B.
        
    - $A = 0$, $B = 10$, $C = 11$ → ✅ **Unívocamente decodificable**
        

---

## 5️⃣ **Código instantáneo**

- También llamado **prefijo**: **ningún código de un símbolo es prefijo del código de otro símbolo**.
    
- Esto garantiza que pueda decodificarse **en el momento exacto** que termina un símbolo, sin esperar bits adicionales.
    
- Todos los códigos instantáneos son unívocamente decodificables, pero no al revés.
    
- Ejemplo instantáneo:
    
    - $A = 0$, $B = 10$, $C = 110$ → ✅
        
- Ejemplo no instantáneo:
    
    - $A = 0$, $B = 01$, $C = 011$ → ❌ (A es prefijo de B y C)
        

---

## 6️⃣ **Código compacto**

- Es un código que **usa el menor número posible de bits promedio** para la longitud de código, dado el alfabeto y sus probabilidades.
    
- Ejemplo típico: **Código de Huffman**
    
- En un código compacto, la **longitud promedio $L$** está muy cerca del **límite teórico de la entropía HHH**:
    
    $$H \le L < H+1$$

---

## 📊 Resumen en tabla:

|Tipo de código|Característica principal|Ejemplo válido|Ejemplo no válido|
|---|---|---|---|
|**En bloque**|Todos los códigos misma longitud|00, 01, 10|0, 10, 110|
|**No singular**|Cada símbolo tiene un código distinto|0, 10, 11|0, 0, 11|
|**Singular**|Dos símbolos con el mismo código|0, 0, 1|—|
|**Unívocamente decodificable**|Mensajes completos se decodifican sin ambigüedad|0, 10, 11|0, 01, 011|
|**Instantáneo**|Ningún código es prefijo de otro|0, 10, 110|0, 01, 011|
|**Compacto**|Longitud promedio mínima según probabilidades|Huffman|Código aleatorio|
