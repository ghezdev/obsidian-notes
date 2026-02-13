## 🧠 ¿Qué es la tasa de información?

La **tasa de información** es la **cantidad de bits útiles (no los de control) transmitidos por segundo**.

Se calcula como:
$$R_i = \frac{\text{bits de información}}{\text{tiempo del bloque}}$$

- - -
### 📦 **Bloque**

Un **bloque** en este contexto es una **unidad de transmisión completa** que incluye lo bits de transmisión 

- - -

$$T = \frac{H(x)}{t} \quad \left[\frac{\text{bits/símbolo}}{\text{seg./símbolo}} = \text{bits/segundo}\right]$$

Esta fórmula representa la **tasa de información** (también llamada **rendimiento** o **throughput**) y ahora la explico paso a paso:

---

## 🧠 ¿Qué significa cada símbolo?

| Símbolo | Significado                                                               |
| ------- | ------------------------------------------------------------------------- |
| $T$     | **Tasa de información** en **bits por segundo (bps)**                     |
| $H(x)$  | **Entropía** de la fuente, en **bits por símbolo**                        |
| $t$     | **Tiempo promedio de emisión de un símbolo**, en **segundos por símbolo** |

---

## 🧮 Interpretación de la fórmula

$$T = \frac{H(x)}{t}$$
- Nos dice **cuántos bits útiles por segundo se están transmitiendo**, considerando tanto **cuánta información aporta cada símbolo** como **cuánto tarda en transmitirse un símbolo**.

---

## 🧪 Ejemplo para fijar conceptos

Supongamos:

- $H(x) = 2 \, \text{bits/símbolo}$
  
- $t = 0.00001 \, \text{s/símbolo} = 10 \, \mu s$
  

Entonces:
$$T = \frac{2}{10^{-5}} = 200,000 \, \text{bps}$$