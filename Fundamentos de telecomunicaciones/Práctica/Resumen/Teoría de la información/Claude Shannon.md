## 🧠 ¿Qué es la fórmula de Shannon?

Es una expresión matemática que nos dice:

> ¿Cuál es la **máxima tasa de información** (bits por segundo) que se puede transmitir **sin errores** a través de un canal ruidoso, si usamos una codificación ideal?

---

## 📐 Fórmula de la Capacidad del Canal

$$C = B \cdot \log_2\left(1 + \frac{S}{N}\right)$$

Donde:

| Símbolo        | Significado                                            |
| -------------- | ------------------------------------------------------ |
| $C$            | **Capacidad del canal**, en **bits por segundo (bps)** |
| $B$            | **Ancho de banda** del canal, en **Hz**                |
| $\frac{S}{N}$​ | **Relación señal a ruido** (**SNR**), adimensional     |
| $\log_2$​      | Logaritmo base 2 (porque se mide en bits)              |

---

## 🎯 ¿Para qué sirve esta fórmula?

Te permite conocer:

- **Cuál es el límite teórico** de velocidad de transmisión de datos sin errores para un canal con ruido.
  
- Qué tan **eficiente es tu sistema de codificación/modulación** comparado con ese límite.
  
- Cuánto **ancho de banda o potencia** necesitas para alcanzar cierta velocidad de transmisión.


👉 **Nadie puede superar este límite sin aumentar B o mejorar la SNR**. Es una frontera física.

---

## 🧪 Ejemplo práctico:

Supongamos:

- Ancho de banda del canal: $B = 3 \, \text{kHz}$

- Relación señal a ruido: $\frac{S}{N} = 30$ (es decir, la señal es 30 veces más fuerte que el ruido)


Entonces:
$$C = 3000 \cdot \log_2(1 + 30) = 3000 \cdot \log_2(31)$$

Sabemos que:
$$\log_2(31) \approx 4.954$$

Entonces:
$$C \approx 3000 \cdot 4.954 = 14,862 \, \text{bps}$$

---

## 📉 Interpretación del resultado:

- **No importa qué codificador uses**: si querés transmitir **más de 14,862 bps** en ese canal, **vas a tener errores**.

- Si querés transmitir más sin errores, tenés que:

    - **Aumentar el ancho de banda $B$**.

    - **Mejorar la SNR (relación señal/ruido)**.


---

## 📊 ¿Cómo se expresa la SNR?

Si te dan la SNR en **decibeles (dB)**:
$$\text{SNR}_{\text{dB}} = 10 \cdot \log_{10} \left( \frac{S}{N} \right) \quad \Rightarrow \quad \frac{S}{N} = 10^{\frac{\text{SNR}_{\text{dB}}}{10}}$$

Ejemplo: si $\text{SNR}_{\text{dB}} = 20$
$$\frac{S}{N} = 10^{20/10} = 100$$

---

## 🧠 Conclusión clave:

La fórmula de Shannon:

- Es un **límite teórico**, no una técnica práctica.

- Guía el diseño de sistemas de telecomunicaciones para evaluar si un sistema es **eficiente o no**.

- Relaciona **ruido**, **ancho de banda** y **velocidad máxima posible de transmisión**.