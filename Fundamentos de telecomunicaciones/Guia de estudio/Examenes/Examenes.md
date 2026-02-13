**TEORICOS:** Responda las siguientes preguntas, justificando las respuestas:

**1.** Considere una fuente de información representada por un rodillo de una máquina tragamonedas, que puede mostrar 5 símbolos distintos: cereza, campana, limón, 7 y estrella.  
a) Suponga que todos los símbolos tienen igual probabilidad de aparecer. ¿Qué características tendría la entropía de esta fuente?  
b) ¿Cómo se vería afectada la entropía si la máquina estuviera programada para que ciertos símbolos, como el 7, aparezcan con mayor frecuencia que los demás? Explique.

**2.** Se desea **almacenar un mensaje de voz en memoria**. Indique y justifique **qué modulaciones intervienen en el proceso** (recepción y procesamiento de la señal).

**3.** Explique en qué consiste la **transmisión sincrónica**. ¿Qué ventajas presenta respecto de la transmisión asincrónica en términos de eficiencia?

**4.** ¿Cuáles son los elementos que caracterizan a las señales? Indíquelos y defina cada uno de ellos.

**5.** ¿Cuáles son los factores que afectan a las señales y no pueden ser evitados? Justifique y proporcione ejemplos.

**6.** Una _startup_ quiere desplegar medidores inteligentes de agua en edificios residenciales. Evalúe la siguiente alternativa:  
• **Tecnología Y:** Muy utilizada en el mercado y compatible con la mayoría de dispositivos existentes, pero sin aprobación formal por organismos internacionales.  
a) Indique si la Tecnología Y corresponde a un estándar de facto o un estándar de iure. Justifique su respuesta.  
b) Mencione una ventaja y una desventaja de usar este estándar en el contexto del proyecto, e indique por qué sería conveniente o no para compatibilidad inmediata con dispositivos ya instalados.


**PRÁCTICOS:**

**7.** Codificar, con paridad par, los siguientes símbolos, aplicando Hamming:  
a) 0110011

Y decodificar, con paridad impar, el siguiente símbolo recibido, determinando si hubieron errores:  
b) 1110010010

**8.** Calcular la cantidad de bits de información y redundancia si se sabe que:  
• La tasa de información es 400 kbps  
• La duración de cada bit es 2 μseg  
• La cantidad total de bits es 40

**9.** Se transmite a 9,6 Kbps con un módem de 2400 bauds.  
a) Calcular la cantidad de estados posibles.  
b) Graficar la constelación para un módem QAM con 2 amplitudes.

**10.** Calcular la eficiencia y la redundancia de la siguiente fuente, si se la codifica con Huffman:

|Símbolo|A|B|C|D|E|F|G|H|
|---|---|---|---|---|---|---|---|---|
|Probabilidad|x|0.20|0.03|0.06|0.08|0.08|x|0.15|

---


**1.** Determine la frecuencia central de la banda MF y calcule la longitud de onda correspondiente.

**2.** Dado un canal de transmisión de datos coaxial con una atenuación a la frecuencia de operación de **0,8 dB/100 metros** y donde la sensibilidad del receptor es **–10 dBm**. Calcular la potencia mínima que deberá tener el transmisor si la longitud del coaxial es de **1200 metros**. Indicar cuál es la potencia mínima del receptor en **miliwatt**.

**3.** Calcular la capacidad de un canal con ancho de banda de **2 MHz** y relación señal/ruido de **30 dB**.

**4.** Se transmite a **7.200 bps** con un módem **PSK** de **2.400 baudios**. A partir de los cálculos que deban hacerse, graficar todos los estados de la señal modulada.


**5.** Dada una fuente sin memoria con **32 símbolos equiprobables**:  
a) Calcular la **entropía** de la fuente.  
b) ¿Cuál es el significado del valor hallado en el punto anterior?  
c) Si los símbolos no fueran equiprobables, ¿la entropía sería mayor o menor?

**6.** El siguiente conjunto de bits incluye un **CRC** que fue generado por el polinomio  
**x⁴ + x + 1**. Verificar si se ha recibido correctamente o con errores: **1101011011110**


---


**1.** Determine la frecuencia central de la banda **SHF** y calcule la longitud de onda correspondiente.

**2.** Calcular la potencia de salida de una línea de transmisión de **1000 metros** donde la atenuación del cable coaxial es de **5 dB/100 metros** y la potencia del transmisor que excita a la línea es de **10 W**.

**3.** Calcular la capacidad de un canal telefónico (**3.1 kHz**) con relación señal/ruido de **50 dB**.

**4.** Se transmite a **12 Mbps** con un módem **QAM** de **3 Mbaudios** con **2 amplitudes diferentes**. A partir de los cálculos que deban hacerse, graficar todos los estados de la señal modulada en un **diagrama de amplitudes y fases**, con la mayor simetría posible.

**5.** Dada una fuente con **5 mensajes** con probabilidades  
**x₁ = x₂ = 0,2** y **x₃ = x₄ = 0,15**, calcule la entropía de la fuente, su eficiencia y redundancia si la misma está codificada con **Huffman**.

**6.** Un equipo receptor recibe el código **1011001101100** que fue codificado con **CRC** cuyo polinomio generador es  
**x³ + x² + 1**.  
Determinar si el código recibido es correcto o contiene errores.

- - -


**1.** Dada una señal cuya **frecuencia es 150 MHz**:  
• ¿Cuál será la **longitud recorrida en 5 períodos**?  
• Si se utiliza la señal para acceder a un datacenter ubicado en **San Francisco (15.000 km)**  
¿cuál será la **demora en recuperar una pantalla de CRM**, para la que se utilizan **10 consultas y respuestas**?  
• ¿Cómo se puede **reducir el tiempo calculado en el punto anterior**?

**2.** Se desea enviar el **símbolo 110111010100**, aplicando algún método de **detección de errores**.  
Agregar el **CRC**, sabiendo que el **polinomio generador es P(x) = x⁴ + x³ + 1**.

**3.** Si un canal cuenta con una **capacidad de 2,4 Mbps** y una **relación señal a ruido de 36 dB**, calcular su **ancho de banda**.

**4.** Cierta fuente está compuesta de **6 símbolos** que se transmiten con las siguientes probabilidades:

```
Símbolo        A     B     C     D     E     F     G     H
Probabilidad  0.12  0.16  0.12    x     x     x    0.05  0.07
```

a. Determinar la **Entropía** de la fuente.  
b. Si se la desea codificar con un **código bloque**, ¿cuántos bits tendrá, como mínimo? ¿Cuál será la **Eficiencia** y la **Redundancia** de ese código?

---

**1)** De los **3 parámetros característicos de la señal**, explique cuáles pueden ser observados en el **dominio de la frecuencia** y cuáles en el **dominio del tiempo**.

**2)** Explique qué sucede con la **entropía de una fuente** cuando los símbolos son **equiprobables**, e indique cómo se calcula.

**3)** Indique si las siguientes afirmaciones son correctas o no, justificando su respuesta:  
a) El proceso de digitalización de una señal analógica comienza aproximando los valores de dicha señal a una cantidad finita de niveles.  
b) La señal discreta obtenida luego del muestreo es del tipo PAM.

**4)** Indique cuáles de las siguientes afirmaciones identifican a la **modulación FSK**:  
a) Una moduladora digital que modula portadora analógica  
b) Se utiliza más de una frecuencia de portadora  
c) Ocupa menos ancho de banda que ASK  
d) Es similar a PSK pero modula en más de una amplitud.

**5)** **Indique cuáles de las siguientes afirmaciones identifican al método de Hamming:**  
a) Permite obtener un código de muy alta eficiencia  
b) Permite detectar y en algunos casos, corregir errores  
c) La posición de los bits de paridad se modifica según la cantidad de bits del mensaje original  
d) La palabra de Hamming contiene bits de información y de paridad.

**6)** Suponiendo que tiene una señal digital donde su primer armónico se ubica en los **200 kHz**, indique en qué frecuencias se ubican los próximos dos armónicos y cómo se modifican sus amplitudes.

### **PRÁCTICOS: Incluir los cálculos realizados en las hojas a entregar**

**1)** Calcular la relación señal a ruido en dB, para cierto canal cuya capacidad es de **1 Mbps** y su ancho de banda es de **200 kHz**.

**2)** Calcular la cantidad de bits de información y redundancia si se sabe que:

- La tasa de información es **1 Mbps**
    
- La duración de cada bit es **10 μseg**
    
- La cantidad total de bits es **20**
    

**3)** Se transmite a **28800 bps** con un módem de **9600 bauds** en **PSK**. Calcular la cantidad de bits, la cantidad de estados, y dibujar el diagrama de constelación.

**4)** Una fuente sin memoria tiene un alfabeto de **4 símbolos**, siendo **P(a) = 0,45; P(b) = 0,25 y P(c) = P(d)**.  
Construir un **código de Huffman** para esta fuente, con alfabeto binario y comprobar que se cumple la relación entre la entropía y la longitud media que predice la teoría.

---

## **TEÓRICOS: Responda las siguientes preguntas, justificando las respuestas:**

**1)** Según el teorema de **Shannon-Hartley**, indique qué parámetros puede modificar para aumentar la capacidad de un canal y cómo lo haría en una situación real.

**2)** Indique cuáles de las siguientes afirmaciones identifican al **ruido por impulso**:  
a) Es continuo, siempre presente  
b) Es causado por la agitación de los electrones en el material  
c) Puede modificar la frecuencia de la señal  
d) Puede modificar la amplitud de la señal

**3)** Indique si las siguientes afirmaciones son correctas o no, justificando su respuesta.  
a) QAM (Quadrature Amplitude Modulation) es una combinación entre modulación en amplitud y modulación en frecuencia.  
b) M-PSK utiliza una sola portadora analógica de amplitud única.

Explique brevemente cómo se realiza el proceso de muestreo de una señal analógica que da como resultado una señal PAM.

**5)** Explique brevemente cómo afecta a una señal ser transmitida por un medio a medida que su ancho de banda disminuye.

**6)** Indique cuál de las siguientes afirmaciones es correcta. El algoritmo de Huffman:  
a) Permite obtener un código con alta eficiencia.  
b) El árbol se construye agrupando en primer lugar los símbolos con mayor probabilidad de aparición.  
c) Su longitud media es menor que la entropía.  
d) El símbolo con menor probabilidad de aparición tiene el código más corto.

## **PRÁCTICOS: Incluir los cálculos realizados en las hojas a entregar**

**1)** Calcular el ancho de banda del cable sabiendo que la capacidad del canal es de **4 Mbps**, la potencia de la señal es de **50 dBm** y que la **densidad de ruido es de 1 nW**.

**2)** Se desean transmitir **4 bits** a través de un módem de **9600 bauds** modulando en **PSK**. Determinar la tasa en bits por segundo y la cantidad de estados, e indicar cómo será el diagrama de constelación (no es necesario dibujarlo).

**3)** Obtener el **código Hamming** a emitir para el mensaje **“111110”** (con paridad par).

**4)** Una fuente sin memoria tiene un alfabeto de **4 símbolos**, siendo:  
P(a) = 0,4 ; P(b) = 0,3 ; P(c) = P(d)

Construir un **código de Huffman** para esta fuente con alfabeto binario y comprobar que se cumple la relación entre la entropía y la longitud media que predice la teoría vista en clase.

---
## **TEÓRICOS: Responda las siguientes preguntas, justificando las respuestas:**

**1.** Si el dueño de una **radio AM** le pregunta qué debe hacer para lograr la mayor cobertura ¿usted qué le respondería? **Justifique.**

**2.** De los elementos que componen una **antena parabólica** ¿cuál es el elemento más importante? **Justifique.**

**3.** Explique y justifique por qué el **Encapsulamiento introduce Redundancia** en los paquetes del modelo OSI.

**4.** Describa las **características principales de un satélite LEO** y qué servicios pueden brindarse con él.

**5.** Describa y justifique qué medio utilizaría para interconectar **dos edificios de un campus universitario**, los cuales se encuentran en la **misma manzana**.

**7.** ¿Es correcto afirmar que un enlace que cuenta con una antena ubicada en una torre de **81 mts** y otra en una de **64 mts**, logra cubrir una distancia total de **más de 200 km**?

**8.** Determinar el tiempo que tarda un bit en ir y venir, desde una sucursal ubicada en **Buenos Aires** hasta el **datacenter ubicado en Bahía Blanca**, si se utiliza para comunicarlos un **satélite MEO ubicado a 22500 km**.

**9.** Determinar el **ruido máximo** – expresado en **mW** – que puede afectar al siguiente sistema de comunicaciones:

```
At = 0.4 dBm/100 m ; long = 3 km
```

```
Pin = 160 mW                         Sensibilidad = -10 dBm
                N = X mW
```

**10.** Calcular los posibles **dipolos** para una antena que debe transmitir una señal de **150 MHz**.

---

## **TEÓRICOS: Responda las siguientes preguntas, justificando las respuestas:**

**1.** Se desea **transmitir una señal** a través de un par de cables de cobre que ya se encuentra **instalado en un hogar (no se puede modificar la instalación)**. Indique y justifique qué **factores que afectan a las señales** pueden ser evitados, y cómo lo haría.

**2.** Describir qué características tiene la **entropía de una fuente con símbolos equiprobables** y cómo se vería afectada si sus probabilidades se **modificaran**.

**3.** ¿Cuáles son las **características principales de las modulaciones con portadora analógica**?  
Dé un ejemplo de cada una y en qué se utilizan.

**4.** Explique por qué tiene sentido aplicar un **código de corrección de errores** en un protocolo orientado al bit.

**5.** Describa los distintos tipos de comunicación según el **uso del medio**, detallando sus características y dé ejemplos de cada uno.

**6.** Dado un canal determinado, indique qué factores puede modificar para **aumentar su capacidad**. Justifique la respuesta.

## **PRÁCTICOS:**

**7.** Codificar, con paridad par, el siguiente símbolo, aplicando Hamming:  
a – **011001**

Y decodificar, con paridad par, el siguiente símbolo recibido, determinando si hubieron errores:  
b – **0111000101**


**8.** Calcular la **cantidad de bits de información y redundancia** si se sabe que:  
• La tasa de información es **600 kbps**  
• La duración de cada bit es **1.5 μseg**  
• La cantidad total de bits es **30**


**9.** Se transmite a **57.600 kbps** con un módem de **14.400 bauds**.  
a) Calcular la **cantidad de estados posibles**  
b) Graficar la **constelación para un módem QAM con 2 amplitudes**.


**10.** Calcular la **eficiencia y la redundancia** de la siguiente fuente, si se la codifica con **Huffman**:

|Símbolo|A|B|C|D|E|F|G|H|
|---|---|---|---|---|---|---|---|---|
|Probabilidad|x|0.20|0.04|0.07|0.08|0.08|x|0.13|

---

## **TEÓRICOS: Responda las siguientes preguntas, justificando las respuestas:**

**11.** Se desea **transmitir una señal** a través de un par de cables de cobre que ya se encuentra **instalado en un hogar (no se puede modificar la instalación)**. Indique y justifique qué **factores que afectan a las señales no pueden ser evitados**, y si se podría, cambiando el medio.

**12.** Describir los significados tiene la **entropía de una fuente** y cómo se relaciona con el proceso de **codificación**.

**13.** ¿Cuáles son las **características principales de las modulaciones con portadora digital**? Dé un ejemplo de cada una y en qué se utilizan.

**14.** Explique por qué tiene sentido aplicar un **código de detección de errores** en un protocolo orientado al bit.

**15.** Describa los distintos tipos de comunicación según el **uso del medio**, detallando sus características, y dé ejemplos de cada uno.

**16.** En un sistema de comunicación, ¿cuál es el factor más costoso, si se desea modificar, para aumentar su capacidad? Justifique la respuesta.

**17.** Codificar, con paridad par, los siguientes símbolos, aplicando Hamming:  
a – **110001**

Y decodificar, con paridad par, el siguiente símbolo recibido, determinando si hubieron errores:  
b – **0100111000**

**18.** Calcular la **cantidad de bits de información y redundancia** si se sabe que:  
• La tasa de información es **600 kbps**  
• La duración de cada bit es **1.5 μseg**  
• La cantidad total de bits es **40**

**19.** Se transmite a **230.4 kbps** con un módem de **76800 bauds**.  
a) Calcular la **cantidad de estados posibles**  
b) Graficar la **constelación para un módem QAM con 2 amplitudes**.

**20.** Calcular la **eficiencia y la redundancia** de la siguiente fuente, si se la codifica con **Huffman**:

|Símbolo|A|B|C|D|E|F|G|H|
|---|---|---|---|---|---|---|---|---|
|Probabilidad|x|0.19|0.05|0.07|0.07|0.10|x|0.14|
