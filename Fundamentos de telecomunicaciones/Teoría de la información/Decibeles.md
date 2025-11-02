
Para medir la intensidad del sonido, usamos los DECIBELES

## 🔊 ¿Qué representa la **amplitud $a$**?

En el contexto del sonido, la **amplitud $a$** representa:

- En acústica: la **amplitud de presión sonora**.

- En electricidad o telecomunicaciones: la **tensión o voltaje**.

- En general: **la "altura" de la onda**, es decir, cuán fuerte se manifiesta la señal físicamente.


---

## 📐 Fórmula de decibeles en función de amplitudes

Cuando expresamos decibeles en términos de **amplitud de onda**, usamos:
$$L = 20 \cdot \log_{10} \left( \frac{a}{a_0} \right)$$

Donde:

| Símbolo | Significado                                                             |
| ------- | ----------------------------------------------------------------------- |
| $L$     | Nivel en decibeles (dB)                                                 |
| $a$     | Amplitud de la señal medida                                             |
| $a_0$​  | Amplitud de referencia (la más baja perceptible, o base de comparación) |

---

### ❓¿Por qué 20 y no 10?

Porque la **potencia** es proporcional al **cuadrado de la amplitud**:
$$P \propto a^2 \quad \Rightarrow \quad 10 \cdot \log_{10}\left(\frac{P}{P_0}\right) = 10 \cdot \log_{10}\left(\frac{a^2}{a_0^2}\right) = 20 \cdot \log_{10}\left(\frac{a}{a_0}\right)$$

🔁 Por eso cuando trabajamos con **amplitudes** (no con potencia directamente), usamos **20** en lugar de **10**.

---

## 🧪 Ejemplo práctico:

Supongamos:

- $a = 0.1 \, \text{Pa}$ (presión de la onda sonora)

- $a_0 = 20 \, \mu \text{Pa} = 2 \cdot 10^{-5} \, \text{Pa}$ (amplitud de referencia auditiva)


Entonces:
$$L = 20 \cdot \log_{10}\left(\frac{0.1}{2 \cdot 10^{-5}}\right) = 20 \cdot \log_{10}(5000) \approx 20 \cdot 3.699 = 73.98 \, \text{dB}$$

✅ Ese sonido tendría un **nivel de presión sonora de aproximadamente 74 dB**.

---

## 🧠 Interpretación

- Si duplicás la amplitud: $a/a_0 = 2$ → $$L = 20 \cdot \log_{10}(2) \approx 6.02 \, \text{dB}$$
🔁 **Duplicar la amplitud** implica un aumento de **+6 dB**

- Si multiplicás por 10: $$L = 20 \cdot \log_{10}(10) = 20 \, \text{dB}$$

---

## 📊 Tabla resumen

| Relación de amplitud $\frac{a}{a_0}$​ | Nivel $L$ |
| ------------------------------------- | --------- |
| $1$ (igual)                           | 0 dB      |
| $2$ (doble)                           | +6 dB     |
| $10$                                  | +20 dB    |
| $0.5$ (mitad)                         | –6 dB     |
| $0.1$                                 | –20 dB    |
