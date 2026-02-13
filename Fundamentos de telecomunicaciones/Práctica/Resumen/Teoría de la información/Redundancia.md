
## 📐 ¿Qué es la longitud media $L$ de un código?

Es la **cantidad promedio de bits por símbolo** que se utilizan al codificar una fuente con un cierto código. Se calcula ponderando la longitud de cada código por la probabilidad del símbolo correspondiente.

---

## 📊 Fórmula de longitud media LLL

$$L=\sum^{n}_{i=1}p_i⋅l_i$$

Donde:
- $p_i$​: probabilidad del símbolo $i$,
  
- $l_i$​: cantidad de bits del código asignado al símbolo $i$,
  
- $n$: cantidad de símbolos distintos.

---

## 🧪 Ejemplo paso a paso

| Símbolo | Probabilidad $p_i$​ | Código binario | Longitud $l_i$​ |
| ------- | ------------------- | -------------- | --------------- |
| A       | 0.5                 | 0              | 1               |
| B       | 0.25                | 10             | 2               |
| C       | 0.125               | 110            | 3               |
| D       | 0.125               | 111            | 3               |

### Aplicamos la fórmula:

$$L=(0.5⋅1)+(0.25⋅2)+(0.125⋅3)+(0.125⋅3)$$
$$L=0.5+0.5+0.375+0.375=1.75\ bits/símbolo$$
- - -
## 🔁 ¿Qué es la redundancia?

La **redundancia** mide **cuánto de la información transmitida es predecible o no esencial**. Es decir, cuánto "exceso" hay sobre la cantidad mínima necesaria para representar los datos.

### 🧠 En términos simples:

- **Entropía** = cantidad mínima de bits _reales_ necesarios por símbolo.
  
- **Redundancia** = diferencia entre lo que realmente se transmite y lo que sería _teóricamente necesario_.

- - -
## 📊 Fórmulas involucradas

Supongamos una fuente que emite $n$ símbolos, y codificamos cada símbolo con un código de longitud media $L$ (en bits por símbolo).

- **Entropía**: $H=−\sum^{n}_{i=1} p_i * log_2(p_i)$
  
- **Redundancia $R$ (en porcentaje): $R=(1−\frac{H}{L})⋅100$
  
- **Eficiencia $\eta$**: 
  $\eta=\frac{H}{L}⋅100$ 
  $R=100−\eta$

---

## 🎯 ¿Para qué sirve la redundancia?

1. **Control de errores:** Se pueden agregar bits adicionales (paridad, CRC, etc.) para detectar o corregir errores en la transmisión.
   
2. **Seguridad:** A veces se introduce de forma deliberada para dificultar la interpretación de datos (como en criptografía).
   
3. **Compresión:** Un sistema con alta redundancia puede ser comprimido. Un texto en español o inglés tiene **mucha** redundancia.
   
4. **Diagnóstico:** Ayuda a saber cuán óptimo es tu sistema de codificación.

---

## 🧪 Ejemplo

Una fuente emite 4 símbolos con estas probabilidades:

|Símbolo|Probabilidad|
|---|---|
|A|0.4|
|B|0.3|
|C|0.2|
|D|0.1|

### Paso 1: Calcular la entropía

$$H=-\sum^{n}_{i=1}p_i⋅log_2(p_i)=−[0.4*log_2(0.4)+0.3*log_2(0.3)+… ]≈1.846 \ bits/símbolo$$

### Paso 2: Supongamos que usamos un código de longitud media $L=2$ (por ejemplo, todos los símbolos codificados con 2 bits: 00, 01, 10, 11)

Entonces:

- Eficiencia: $\eta=\frac{1.846\ bits/simbolo}{2\ símbolos}⋅100≈92.3\%$
  
- Redundancia: $R=100−92.3=7.7\%$

Este sistema tiene poca redundancia (eficiente), pero sí algo de "exceso" de bits.

---

## 🚨 Redundancia ≠ error

**¡Importante!** Redundancia no es lo mismo que **error**. Se refiere a información que **podría haberse evitado** transmitir, porque es **predecible** o **no aporta novedad**.

- - -

👉 Si estás usando un código de solo 2 bits/símbolo para una fuente que necesita 4 bits/símbolo, entonces **tu código es incapaz de representar toda la entropía** de la fuente.

### 📉 Eso significa:

- Estás **perdiendo información**.
  
- Tu código **no es suficiente** para codificar esa fuente correctamente.
  
- **No hay eficiencia mayor al 100%**, porque implicaría que estás transmitiendo **más información de la que realmente estás enviando**.

---

## ✅ Conclusión clave:

- Si $H>L$ → ❌ no es posible. **No se puede representar la fuente correctamente.**
  
- Si $H=L$ → ✅ eficiencia del 100%. **Código óptimo.**
  
- Si $H<L$ → ✅ eficiencia < 100%, hay **redundancia**.