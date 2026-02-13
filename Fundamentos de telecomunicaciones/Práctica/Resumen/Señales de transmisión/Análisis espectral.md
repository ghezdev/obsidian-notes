## 🌊 ¿Qué es el análisis espectral?

El **análisis espectral** estudia cómo una señal se descompone en **frecuencias sinusoidales** básicas. Cada señal puede representarse como la **suma de múltiples senoidales** de distintas frecuencias, amplitudes y fases.

Esta idea viene del **Teorema de Fourier**, y nos permite ver una señal **en el dominio del tiempo** y **en el dominio de la frecuencia**.

---

## 🔁 Dominio del Tiempo vs Dominio de la Frecuencia

- En el **dominio del tiempo**, vemos cómo varía una señal con el tiempo: $s(t)$
  
- En el **dominio de la frecuencia**, vemos **qué frecuencias contiene la señal**, y con qué **intensidad** (amplitud): $S(f)$
  

---

## 🎚️ Conceptos clave

### 1. 📏 Frecuencia ($f$)

- Medida de cuántas veces ocurre un ciclo por segundo.
  
- Se mide en **Hertz (Hz)**.
  
- Relación con el período $T$: $$f = \frac{1}{T}$$​
Ejemplo: una señal de 1 kHz tiene 1000 ciclos por segundo.

---

### 2. 🌐 Ancho de banda ($B$)

Es la **diferencia entre la frecuencia más alta y la más baja** que contiene energía significativa en una señal.
$$B = f_{\text{máx}} - f_{\text{mín}}$$

Tipos de ancho de banda:

- **Absoluto**: intervalo total de frecuencias utilizadas.
  
- **Relativo**: proporción respecto a la frecuencia portadora.
  

🔁 El ancho de banda determina:

- Cuánta **información** se puede transmitir.
  
- Qué **medio físico** puede usarse (ej: cables, radio, fibra).
  

---

## 🧪 Ejemplo: Señal cuadrada

Una señal cuadrada (como una señal digital) no es una onda pura: tiene muchos **armónicos** (múltiplos de la frecuencia fundamental).

- Señal cuadrada de 1 MHz → contiene componentes en 1 MHz, 3 MHz, 5 MHz, ...
  
- Si se transmite por un canal que solo deja pasar hasta 3 MHz, se perderán armónicos → la señal **se distorsiona**.

---

## 🎛️ Aplicación: filtros y canal

El **análisis espectral** permite:

- Diseñar **filtros** (pasabajos, pasaaltos, pasabanda).
  
- Calcular la **capacidad de un canal** (usando la fórmula de Shannon-Hartley).
  
- Entender la **ocupación espectral** (eficiencia espectral, interferencias).
  

---

## 📉 Efecto del Ancho de Banda en la Transmisión

- A mayor ancho de banda: más datos se pueden transmitir (mayor capacidad).
  
- Pero también: mayor riesgo de interferencia, más exigencia en el canal físico.

---

## ⚠️ Relación con modulación

Cada técnica de modulación (AM, FM, QAM, etc.) ocupa un **ancho de banda diferente**. Por ejemplo:

- AM → ocupa el doble del ancho de banda de la señal base (por sus bandas laterales).
  
- FM → depende del índice de modulación (puede ocupar mucho más).
  
- PSK/QAM → su BW depende de la tasa de símbolos (baudios) y del filtrado.

- - -
## 🧮 Ejercicio:

Una señal digital se transmite a una **velocidad de datos** de:
$$R = 9600 \text{ bits/seg} = 9600 \text{ bps}$$

Se utiliza un módem que transmite a:
$$V = 2400 \text{ baudios} = 2400 \text{ símbolos/seg}$$

y la modulación utilizada es **QPSK** (Phase Shift Keying con 4 fases).

Queremos:

1. Calcular cuántos **bits por símbolo** se transmiten.
   
2. Determinar cuántos **estados diferentes** hay en la constelación.
   
3. Estimar el **ancho de banda mínimo teórico** necesario para transmitir esta señal.
   
4. Comparar con otras modulaciones.

---

### 🔢 Resolución paso a paso

#### **1. Bits por símbolo**

$$\text{bits/símbolo} = \frac{\text{velocidad de transmisión}}{\text{velocidad de modulación}} = \frac{9600}{2400} = 4 \text{ bits/símbolo}$$

🔁 ¡Atención! Esto **no coincide** con QPSK, que transmite **2 bits por símbolo**. Esto implica que en realidad estamos usando una modulación como **16-QAM** (que transmite 4 bits por símbolo).

👉 Entonces, modifiquemos:

- Supongamos ahora que **realmente es 9600 bps** con un módem **QPSK**.

Entonces:
$$\text{bits/símbolo} = 2 \Rightarrow \text{símbolos/seg} = \frac{9600}{2} = 4800 \text{ baudios}$$

---

#### **2. Estados en la constelación**

QPSK: 2 bits/símbolo → $2^2 = 4$ estados (fases posibles: 0°, 90°, 180°, 270°)

---

#### **3. Estimar ancho de banda mínimo**

Para modulación **PSK o QAM**, el ancho de banda mínimo se relaciona con la **velocidad de modulación**:
$$B_{\text{mín}} \approx V = 4800 \text{ Hz} = 4.8 \text{ kHz}$$

Esto se llama **ancho de banda de Nyquist**. Es el mínimo **teórico** necesario para evitar interferencia entre símbolos (**ISI**), suponiendo filtrado ideal.

---

#### **4. Comparación con otras modulaciones**

|Modulación|Bits/símbolo|BW aprox. = Baudios|
|---|---|---|
|BPSK|1|9600 Hz|
|QPSK|2|4800 Hz|
|8-PSK|3|3200 Hz|
|16-QAM|4|2400 Hz|

🔁 A mayor **eficiencia espectral** (más bits/símbolo), menor es el ancho de banda necesario.

---

### ✅ Conclusión del ejercicio

- El **ancho de banda mínimo** para transmitir 9600 bps usando **QPSK** es **4800 Hz**.
  
- Si usáramos **BPSK**, necesitaríamos el **doble** de BW.
  
- Si usáramos **16-QAM**, necesitaríamos solo **2400 Hz**, pero la señal sería más sensible al ruido.