## 📌 1. **Códigos de detección y corrección de errores**

Cuando transmitimos datos por un canal real, las señales pueden verse afectadas por **ruido, distorsión, interferencia**, etc. → Esto puede alterar bits.

Los **códigos de detección y corrección de errores** agregan **redundancia controlada** para que el receptor pueda:

- **Detectar** si hubo un error
    
- **Corregirlo** (en algunos casos) sin retransmisión
    

---

### 🔍 a) **Códigos de detección**

- Solo permiten saber que hubo un error, **no lo corrigen**.
    
- Se usa un conjunto de bits extra (_bits de verificación_) calculados a partir de los datos.
    
- Ejemplos:
    
    - **Bit de paridad** (par o impar)
        
    - **Checksum**
        
    - **CRC** (_Cyclic Redundancy Check_)
        

**Ejemplo de paridad:**

- Datos: `1010 110`
    
- Paridad par → agregar bit para que haya un número par de 1’s.
    
- Transmitido: `1010 110 1`
    

Si en recepción hay un número impar de 1’s, hay error.


- **Vertical redundancy check (VRC)**: SE AGREGA UN BIT DE PARIDAD EN HORIZONTAL

- **Longitudinal Redundancy Check (LRC)**: SE AGREGAN BITS DE PARIDAD EN VERTICAL

- **Cyclic Redundancy Check (CRC)**: ES LA DIVISIÓN. ES MEJOR QUE VRC Y LRC JUNTOS.

Gracias a su confiabilidad, CRC se volvió un método estándar de detección de errores para la transmisión de bloques de datos.

CRC permite detectar el 100% de los errores de igual o menor longitud del polinomio CRC. 99.99% si es mayor

---

### 🔍 b) **Códigos de corrección**

- Permiten **detectar y corregir** errores sin pedir retransmisión.
    
- Usan más redundancia que los de detección.
    
- Ejemplos:
    
    - **Código de Hamming**
        
    - **Códigos Reed–Solomon**
        
    - **Turbo codes**, **LDPC** en telecomunicaciones modernas
        

**Idea básica:**

- Cada palabra transmitida es suficientemente distinta de las demás en términos de bits (distancia de Hamming) para que, si se recibe con 1 o 2 bits cambiados, se pueda identificar cuál era la palabra original.
    

---

## 📌 2. **Distancia de Hamming**

La **distancia de Hamming** $d$ entre dos palabras binarias es el **número de bits en los que difieren**.

Ejemplo:

- Palabra 1: `101101`
    
- Palabra 2: `100001`
    
- Distancia de Hamming: $d = 2$ (difieren en la tercera y cuarta posición).
    

Te dice cómo medir la **distancia mínima** de un código $d_{min}$​ y cómo eso determina si podés detectar o corregir errores.

Para un código Hamming estándar:

- $d_{min} = 3$
    
- Eso implica que puede **corregir 1 error** y **detectar 2**.

---

### 🧮 **Distancia mínima de Hamming** $d_{min}$

En un **código**, es la **distancia más pequeña** entre **cualquier par de palabras de código válidas**.

Esta es **clave** para saber cuántos errores puedo detectar o corregir:

- **Capacidad de detección**:
    $$\text{Puede detectar hasta } e \text{ errores si } d_{min} \ge e+1$$
    
- **Capacidad de corrección**:
    $$\text{Puede corregir hasta } t \text{ errores si } d_{min} \ge 2t+1$$
    
    donde $t = \lfloor \frac{d_{min} - 1}{2} \rfloor$

• Detección: d=k+1

• Corrección: d=2k+1

---

### 📌 Ejemplo práctico:

Supongamos un código con:

$d_{min} = 3$

- Puede **detectar** hasta $e = 2$ errores
    
- Puede **corregir** hasta $t = 1$ error
    

Esto es precisamente lo que hace el **código de Hamming (7,4)**:

- Longitud: 7 bits (4 de datos, 3 de paridad)
    
- $d_{min} = 3$
    
- Detecta 2 errores, corrige 1.

- - -
## 📊 Resumen:

|Código|Redundancia|Detecta|Corrige|Ejemplo|
|---|---|---|---|---|
|Paridad simple|1 bit|1|0|UART|
|CRC|Varios bits|Muchos|0|Ethernet|
|Hamming (7,4)|3 bits|2|1|Memoria ECC|
|Reed–Solomon|Muchos bits|Muchos|Muchos|CDs, DVB|
- - -

### 1️⃣ Determinar cuántos bits de paridad usar



En un código de Hamming, los bits de paridad se colocan en posiciones que son potencias de 2 (1, 2, 4, 8, …) y cumplen:

$$2^p \ge m + p + 1$$
**Condición para calcular cuántos bits de paridad $p$ son necesarios** en un **código Hamming (7,4), (15,11), etc.**, en función de los bits de datos $m$. Es decir, la cantidad mínima de bits de paridad que se necesitan para lograr $d_{min}$

Donde:
- $m$ = bits de datos originales (en este caso, $m = 6$)
    
- $p$ = bits de paridad
    

Probamos:

- Con $p = 3$: $2^3 = 8$ y $8 \ge 6 + 3 + 1 = 10$ → **No** alcanza.
    
- Con $p = 4$: $2^4 = 16$ y $16 \ge 6 + 4 + 1 = 11$ → **Sí** alcanza.
    

Entonces, necesitamos **4 bits de paridad**.

---

### 2️⃣ Colocar los bits en sus posiciones

Se reservan las posiciones 1, 2, 4 y 8 para los bits de paridad (**P1, P2, P4, P8**) y se insertan los bits de datos en las posiciones restantes:

|Posición|1|2|3|4|5|6|7|8|9|10|
|---|---|---|---|---|---|---|---|---|---|---|
|Contenido|P1|P2|D1|P4|D2|D3|D4|P8|D5|D6|

Los datos **011001** se asignan como:

- D1 = 0
    
- D2 = 1
    
- D3 = 1
    
- D4 = 0
    
- D5 = 0
    
- D6 = 1
    

Queda así (con P’s vacíos por ahora):  
P1 P2 0 P4 1 1 0 P8 0 1

---

### 3️⃣ Calcular cada bit de paridad (paridad **par**)

Cada bit de paridad controla ciertas posiciones según la representación binaria de su número de posición:

- **P1** (pos 1): controla posiciones cuyo bit menos significativo es 1 → 1, 3, 5, 7, 9
    
- **P2** (pos 2): controla posiciones cuyo segundo bit en binario es 1 → 2, 3, 6, 7, 10
    
- **P4** (pos 4): controla posiciones cuyo tercer bit en binario es 1 → 4, 5, 6, 7
    
- **P8** (pos 8): controla posiciones cuyo cuarto bit en binario es 1 → 8, 9, 10
    

Se ajusta cada P para que la **cantidad total de unos** en su grupo sea **par**.

#### 📌 Diferencia clave

- **Paridad par:** el total de 1’s (incluyendo el bit de paridad) debe ser **par**.
    
- **Paridad impar:** el total de 1’s (incluyendo el bit de paridad) debe ser **impar**

---

**P1:** posiciones 1, 3, 5, 7, 9 → P1, 0, 1, 0, 0 → hay 1 uno → para que sea par, **P1 = 1**.

**P2:** posiciones 2, 3, 6, 7, 10 → P2, 0, 1, 0, 1 → hay 2 unos + P2 → para paridad par, **P2 = 0**.

**P4:** posiciones 4, 5, 6, 7 → P4, 1, 1, 0 → hay 2 unos → para paridad par, **P4 = 0**.

**P8:** posiciones 8, 9, 10 → P8, 0, 1 → hay 1 uno → para paridad par, **P8 = 1**.

---

### 4️⃣ Palabra final codificada

Sustituyendo los P calculados:

|Pos|1|2|3|4|5|6|7|8|9|10|
|---|---|---|---|---|---|---|---|---|---|---|
|Bit|1|0|0|0|1|1|0|1|0|1|

**Código Hamming (paridad par) = 1 0 0 0 1 1 0 1 0 1**

- - -

## 📌 Proceso general de decodificación (Hamming)

1. **Recibir la palabra codificada**  
    Puede que esté intacta o con 1 bit alterado (Hamming corrige 1 bit y detecta 2).
    
2. **Volver a calcular las paridades** usando los mismos grupos de posiciones que en la codificación.  
    En lugar de asignar valores, verificamos si el número de 1’s en cada grupo cumple la condición de paridad.
    
3. **Armar el “síndrome”**:
    
    - Si un grupo **no cumple** la paridad, ponemos un 1 en la posición correspondiente del síndrome.
        
    - Si la cumple, ponemos un 0.
        
    - El síndrome se escribe como número binario y nos da la **posición del bit con error**.
        
    - Si el síndrome es 0000 → **no hay error**.
        
4. **Corregir el bit** en la posición indicada (si el síndrome es distinto de 0).
    
5. **Eliminar los bits de paridad** para recuperar los datos originales.

## 🔹 Ejemplo rápido con tu palabra (paridad par)

Supongamos que codificamos 011001 y obtuvimos:

**1 0 0 0 1 1 0 1 0 1** (posiciones 1 a 10)

Ahora el receptor recibe:

**1 0 0 0 1 0 0 1 0 1** ← Se dañó el bit en la posición 6 (antes era 1, ahora es 0).

---
## 📌 Regla para ubicar los bits de paridad en Hamming

1. **Los bits de paridad se colocan en posiciones que son potencias de 2**  
    Es decir:
    
    $1,\ 2,\ 4,\ 8,\ 16,\ 32,\ \dots$
    
    (numerando las posiciones desde 1 empezando por la izquierda).
    
2. **Los demás lugares se llenan con bits de datos** del símbolo original, en orden.


### 1️⃣ Verificación de paridades

- **P1** (pos 1, 3, 5, 7, 9): 1, 0, 1, 0, 0 → hay 2 unos → ✅ cumple paridad par (0 en el síndrome).
    
- **P2** (pos 2, 3, 6, 7, 10): 0, 0, 0, 0, 1 → hay 1 uno → ❌ no cumple (1 en el síndrome).
    
- **P4** (pos 4, 5, 6, 7): 0, 1, 0, 0 → hay 1 uno → ❌ no cumple (1 en el síndrome).
    
- **P8** (pos 8, 9, 10): 1, 0, 1 → hay 2 unos → ✅ cumple (0 en el síndrome).
    

---

### 2️⃣ Formar el síndrome

El **síndrome** en el código Hamming es el resultado de **volver a calcular** esas paridades sobre la palabra recibida y comparar con los bits de paridad que vinieron en el mensaje.

- Síndrome = 0 → sin errores.
    
- Síndrome ≠ 0 → el número indica **posición del bit con error**.

**Importante que se debe ordenar de mayor a menos los bits de paridad**

P8 P4 P2 P1 = **0 1 1 0** (binario) = **6 en decimal**.

---

### 3️⃣ Interpretar y corregir

El síndrome indica que el bit con error está en la **posición 6**.  
Corregimos: en vez de 0 debe ser 1.

Palabra corregida: **1 0 0 0 1 1 0 1 0 1**

---

### 4️⃣ Recuperar los datos

Quitamos las posiciones de paridad (1, 2, 4, 8) → queda:  
0 1 1 0 0 1 ✅

---

📌 **Nota:**  
Si se usa **paridad impar**, el cálculo de cada paridad en el receptor es igual, pero la condición de “cumplir” cambia: debe haber un número **impar** de 1’s en cada grupo.