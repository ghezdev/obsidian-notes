## 📡 ¿Qué es la Modulación?

> _"Modulación: Técnica que permite adaptar una señal para su transmisión."_

En términos técnicos, **modular** significa **modificar una señal portadora (usualmente senoidal)** en función de una señal que contiene la información (señal moduladora).

_Modular es adaptar datos que quiero mandar a un medio. Permite expresar la información contenida en una señal (datos), mediante otra señal (modulada) con características similares a una tercera (portadora). Me apoyo en ciertas características de otras señales que, en el medio en el que me quiero comunicar, funcionan mejor._

![[Pasted image 20250804070431.png]]

• **Moduladora**: Señal de datos a transmitir

• **Portadora**: Señal con las características deseadas

• **Modulada**: Señal con datos de la moduladora y propiedades de la portadora.

Alguien del otro lado tiene que hacer el proceso contrario. Lo llamamos **demodular.**

![[Pasted image 20250804070447.png]]

- - -

## 🎯 Objetivos de la modulación

Tu resumen destaca sus finalidades principales:

- **Transmitir señales a largas distancias** sin perder integridad.

- **Adaptar la señal** al canal físico disponible.

- **Multiplexar varias señales** sobre un mismo medio.

- **Reducir el tamaño de las antenas** (subiendo la frecuencia).

- **Permitir la detección y recuperación eficientes** en el receptor.


---

## 🧱 Tipos de modulación

|                         | Moduladora Analógica      | Moduladora Digital    |
| ----------------------- | ------------------------- | --------------------- |
| **Portadora Analógica** | AM, FM, PM                | ASK, FSK, PSK, QAM    |
| **Portadora Digital**   | PAM, PDM, PPM, PCM, Delta | Codificación de Línea |

- - -

## 🧮 **¿Qué son los estados posibles?**

### 📌 Definición:

Los **estados posibles** en una modulación digital son **las diferentes combinaciones únicas de fase, frecuencia y/o amplitud** que puede adoptar un símbolo.

Cada **símbolo** representa varios bits, y los **estados posibles** son el total de **símbolos distintos** que se pueden transmitir.

### 🧠 ¿Cómo los calculo?

Cuando tenés:

- **Tasa de transmisión en bits por segundo (bps):** $T_t$
    
- **Baudios (símbolos por segundo):** $B$
    

Usás esta relación:
$$\text{bits por símbolo} = \frac{T_T}{B}$$​

Y los **estados posibles** se calculan como:
$$M = 2^{\frac{T_T}{B}}$$


- - -

## ✳️ ¿Qué es una constelación en modulación?

Una **constelación** es un **diagrama en el plano complejo** (o cartesiano) donde cada **símbolo** se representa como un punto según sus características:

- Eje X → amplitud en fase (componente I)
    
- Eje Y → amplitud en cuadratura (componente Q)
    

En **QAM (Quadrature Amplitude Modulation)**, los puntos están **distribuidos según combinaciones de amplitud y fase**, y la **distancia entre puntos afecta la robustez al ruido**.

![[Pasted image 20250805203204.png]]

**Ejemplo**

En QAM, si usás **2 niveles de amplitud** por eje (I y Q), tenés una constelación **2 × 2 = 4 amplitudes posibles por eje**.

Pero como te piden 16 estados, es un **4x4**: entonces es **QAM-16**, con 4 puntos por eje (fase + amplitud combinadas).

💡 **Esquema visual**: una cuadrícula 4x4 con 16 puntos bien separados.


> [!NOTE] Title
> Solo importa la cantidad de estados que debe tener la cuadrícula, luego dividirlo por 4 (cantidad de cuadriculas), si no queda perfecto, poner los estados en forma de **+**
