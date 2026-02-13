# Teoría de la información 

### Sistema de comunicación

![[Pasted image 20250804075951.png]]

### Información 

Medida de la **reducción de incertidumbre** en el receptor al recibir un mensaje. Cuanto menos probable es un evento, **más información** proporciona si ocurre.


### Cantidad de información $I(x)$

Asociada a un mensaje $x$ que tiene una probabilidad $P(x)$ de ocurrir, se define como:
$$I(x) = -\log_2 P(x)$$
$$o $$
$$I(x) = \log_2(\frac{1}{P(x)})$$

### 🎲 Fuente de memoria nula

Es una fuente que emite símbolos de manera **independiente entre sí**, es decir, sin "memoria" de los anteriores. Ejemplo clásico: lanzar un dado justo.


### ♻️ Entropía ( $H$ )

Mide la **incertidumbre promedio** de una fuente de información, o sea, cuánta información en promedio produce un símbolo emitido por esa fuente.
$$H(X) = - \sum_{i=1}^{n} P(x_i) \cdot \log_2 P(x_i)$$
$$o$$
$$H(X) = \sum_{i=1}^{n} P(x_i) \cdot I(x_i) = \sum_{i=1}^{n} P(x_i) \cdot \log_2 (\frac{1}{P(x_i)})$$


Donde:

- $X$: variable aleatoria que representa los símbolos.
- $x_i$​: cada símbolo posible.
- $P(x_i)$: probabilidad del símbolo $x_i$​.
- El logaritmo es en base 2 porque la unidad es el **bit** 
- Se asume que $0*log(0)=0$ por convención matemática
- $\sum_{i=1}^{n} p_i = 1 \quad \text{y} \quad 0 \leq p_i \leq 1 \, \text{para todo } i$

#### Interpretaciones:

- Si un símbolo es **muy probable**, su $I(x)$ es baja ⇒ aporta poca información.
- Si todos los símbolos son **igualmente probables**, la entropía es **máxima**.


### 🟢 Entropía mínima:

Cuando **un símbolo tiene probabilidad cercana a 1** y los demás a 0:

- La incertidumbre es **muy baja**, porque ya sabés casi seguro qué va a ocurrir.
    
- Entonces:    $$H = 0$$
**Ejemplo**: Una fuente que siempre emite "A".


### 🔴 Entropía máxima:

Cuando todos los símbolos tienen **la misma probabilidad** $p_i = \frac{1}{n}$​, la entropía se **maximiza**. En ese caso:
$$H = -n \cdot \frac{1}{n} \cdot \log_2\left(\frac{1}{n}\right) = \log_2(n)$$

- Esto significa que **cada símbolo aporta la máxima información posible**.
    
- La fuente es **más impredecible**, y por lo tanto **más eficiente** desde el punto de vista informativo.

- La incertidumbre es máxima (no podés anticipar nada).


**Ejemplo**: En una fuente con 8 símbolos equiprobables:
$$H = \log_2(8) = 3 \text{ bits}$$

Para una **máxima entropía**, la fuente debe:

1. Ser **sin memoria** (símbolos independientes).
    
2. Tener símbolos **equiprobables** dentro de su alfabeto.


### 📘 Tasa de Información

La **tasa de información** mide **cuántos bits útiles por segundo** estás transmitiendo, **sin contar errores ni redundancias**. Es una medida **teórica** del flujo de información

$$\text{Tasa de información} = \frac{\text{Información total transmitida}}{\text{tiempo total}}$$
$$T = \frac{H}{t}\  \frac{bits./símbolo}{seg./símbolo}$$

Donde:

- $H$: **Entropía ideal** de la fuente (medida en bits por símbolo).
    
- $t$: **Tiempo** que se tarda en mandar esos bits (en segundos por símbolo).


## Velocidad de transmisión 

La **tasa de transmisión** mide **cuántos bits por segundo** estás transmitiendo, **contando errores y redundancias**


### 🔢 ¿Qué es un **baudio**?

Un **baudio** es una **unidad de medida** que representa la **cantidad de símbolos transmitidos por segundo** **en un sistema de comunicación digital**.

$$B\ = \frac{T_T}{k}$$

Donde: 
- $B$: Baudio o símbolo por segundo 
- $T_t$: Tasa de transmisión o bits por segundo 
- $k$: Cantidad de bits por símbolo $$k = \log_2(M)$$con $M$ = número de **estados posibles** de la modulación.

> **1 baudio = 1 símbolo por segundo**

> [!note] 
> El **baudio** refleja la **velocidad de cambio en el canal físico** (es decir, cuántas veces por segundo cambia la señal). Por eso está directamente relacionado con el **ancho de banda** necesario.




### 🔁 Redundancia ( $R$ )

La **redundancia** mide cuánto **exceso de codificación** hay respecto al ideal (cuando todos los símbolos transmiten la máxima información posible).


### ⚙️ Eficiencia ( $E$ )

La eficiencia es lo opuesto a la redundancia: cuánta **información útil** se transmite respecto al total de símbolos codificados:


- **Eficiencia:** $$E = \frac{T}{T_t}$$
- **Eficiencia de codificación:** $$E = \frac{H}{L}$$
Donde: 
- $L$: **longitud media del código** (promedio de bits por símbolo que estás usando en la codificación).
- $T$: Tasa de información 
- $T_t$: Tasa de transmisión


- **Redundancia (relativa):** $$R = 1 - R = 1 - \frac{T}{T_t}$$$$o$$ $$R = 1 - \frac{H}{L}$$​
- **Redundancia por símbolo (en bits):** $$\text{Redundancia} = L - H$$

- **Redundancia por entropía**

$$R = \frac{H_0 - H}{H_0}$$
Donde:

- $H$: entropía real (información efectiva)
    
- $H_0$​: entropía máxima posible (cuando todos los símbolos son equiprobables)


También podés calcular **cantidad de bits redundantes** si conocés la cantidad total de bits transmitidos: $$\text{Redundancia en bits} = n \cdot (1 - E)$$
Donde: 
- **n:** cantidad total de bits



### 📡 ¿Qué es un canal de comunicación?

> **Canal de comunicación**: Medio por el cual viaja la información desde un emisor hasta un receptor.

- **Físico** (como un cable coaxial, par trenzado, fibra óptica)
- **No guiado** (como ondas de radio, microondas, láser, etc.)

#### 🧱 Componentes del modelo de comunicación

Según el modelo básico de Shannon:

1. **Fuente**: genera los datos.
2. **Codificador**: transforma los datos en señales transmisibles.
3. **Canal**: medio por el que viajan las señales (puede introducir errores o ruido).
4. **Decodificador**: interpreta la señal recibida.
5. **Receptor**: recibe el mensaje final.


#### 🌐 Tipos de canales

1. **Canal sin ruido**: teórico, ideal. La información llega perfecta.
2. **Canal con ruido**: hay perturbaciones, errores, pérdida de información.
	1. **Canal Binario Simétrico (BSC)**: transmite bits 0 o 1 con probabilidad de error $p$.
	2. **Canal Discreto con Entrada/Salida Finita**
	3. **Canal Continuo**: para señales analógicas, caracterizado por su **ancho de banda** y **relación señal/ruido (SNR)**.


### 📊 Capacidad del canal

> **Capacidad del canal**: máxima cantidad de información que puedo transmitir sin errores.

Esto lleva al **Segundo Teorema de Shannon**, que establece:
$$C = B \cdot \log_2(1 + \frac{S}{N})$$

Donde:

- $C$: capacidad del canal (bps)
- $B$: ancho de banda del canal (Hz)
- $\frac{S}{N}$​: relación señal a ruido

Esto significa que **cuanto más ancho de banda y mejor relación señal-ruido**, **mayor capacidad tiene el canal para transmitir información útil**.

Este teorema establece un **límite superior teórico**: no importa qué tan buena sea tu codificación, **no podés superar esta tasa de bits sin que haya errores** si hay ruido en el canal.

#### ¿Qué podés modificar?

**Puedo**
- Ancho de banda
- Relación señal/ruido 

**No puedo**
- Ruido térmico natural del canal 
- Limites regulatorios o físicos del canal 


### 📉 **Decibelios (dB) y conversión con Watts**

$$\text{dB} = 10 \cdot \log_{10}\left(\frac{P_1}{P_0}\right)$$

Donde:

- $P_1$​: potencia que estás midiendo
- $P_0$​: potencia de referencia (usualmente 1 mW en dBm)


### ¿Qué es $S/N$?

La **relación señal-ruido (SNR)** compara la potencia de la señal ($S$) contra la potencia del ruido ($N$):

$$\frac{S}{N} = \frac{P_{señal}}{P_{ruido}}$$

- Si $S/N = 10$ → la señal es 10 veces más fuerte que el ruido.
    
- Esto se llama **SNR en forma lineal** (un número real simple).
    

---

### ¿Qué es $S/N$ en dB?

En telecomunicaciones solemos expresar relaciones en **decibeles (dB)** porque simplifica las comparaciones:
$$SNR_{dB} = 10 \cdot \log_{10}\left(\frac{S}{N}\right)$$

Ejemplo:

- Si $S/N = 100$ (lineal) →
$$SNR_{dB} = 10 \cdot \log_{10}(100) = 20 \, dB$$


### Relación con la fórmula de Shannon:

Para usar $S/N$ en la fórmula de capacidad, tenés que **convertir los dB a razón lineal**:
$$\frac{S}{N} = 10^{\left(\frac{\text{SNR (dB)}}{10}\right)}$$


### 🔻 **Efecto Umbral**

> _"A partir de cierto S/N no mejora la relación de error."_

Este fenómeno ocurre especialmente en **modulaciones digitales complejas**: aunque sigas aumentando la potencia (S), llega un punto en el que la mejora en calidad **ya no reduce los errores**. Esto se llama **efecto umbral**.

Se da porque:

- El receptor necesita cierto **mínimo SNR** para poder diferenciar entre símbolos.
- Si no se alcanza, **el BER (bit error rate)** es inaceptable.
- Si se supera el umbral, el BER cae rápidamente a 0 (esto es lo que se quiere).


### Tipos de comunicación según el medio

Esta clasificación se basa en **la dirección del flujo de datos** y cómo **comparten el medio de transmisión** los dispositivos involucrados.

![[Pasted image 20250804074553.png]]

### 🔹 1. **Simplex (unidireccional)**

La comunicación se realiza **en una sola dirección**. Un dispositivo **transmite siempre** y el otro **recibe siempre**.

#### 📌 Características:

- El **canal** se usa en **una sola dirección**.
- No hay posibilidad de enviar respuesta.
- Simple implementación.


#### 🟢 Ventajas:

- Simplicidad.

- Económico.


#### 🔴 Desventajas:

- Falta de retroalimentación (no se pueden detectar errores en tiempo real).


#### 🧪 Ejemplos:

- Televisión.

- Señal de radio FM.

- Monitores médicos (cuando solo miden y no reciben comandos).


### 🔹 2. **Half-Duplex (semidireccional alternado)**

La comunicación es **bidireccional**, pero **no simultánea**. Los dispositivos **pueden transmitir o recibir,** pero **no al mismo tiempo**.

#### 📌 Características:

- Se necesita un mecanismo para **controlar el turno** de envío/recepción.

- Se alterna el uso del canal.


#### 🟢 Ventajas:

- Permite interacción en ambas direcciones.

- Menor complejidad que full-duplex.


#### 🔴 Desventajas:

- Latencia al alternar turnos.

- No permite comunicación en tiempo real exacto.


#### 🧪 Ejemplos:

- Walkie-talkies.

- Redes Wi-Fi en modo básico (cuando hay colisiones).

- Sistemas de comunicación de buses industriales simples.


### 🔹 3. **Full-Duplex (bidireccional simultáneo)**

La comunicación se da en **ambas direcciones al mismo tiempo**.

#### 📌 Características:

- Puede usar **dos canales físicos** (uno por dirección) o técnicas como **multiplexación**.

- Requiere más ancho de banda o complejidad.


#### 🟢 Ventajas:

- Comunicación fluida y simultánea.

- Ideal para servicios interactivos en tiempo real.


#### 🔴 Desventajas:

- Mayor costo y complejidad técnica.


#### 🧪 Ejemplos:

- Llamadas telefónicas.

- Redes Ethernet modernas.

- Comunicación entre CPU y memoria RAM (en buses dedicados).


|Tipo|Dirección|Simultaneidad|Complejidad|Ejemplos|
|---|---|---|---|---|
|**Simplex**|Una|No|Baja|TV, radio, sensores unidireccionales|
|**Half-Duplex**|Ambas|No (turnos)|Media|Walkie-talkie, Wi-Fi básico|
|**Full-Duplex**|Ambas|Sí|Alta|Teléfono, red Ethernet|




# Señales
### 📡 ¿Qué es una señal?


> _"Señal: Toda perturbación física que puede ser detectada y manipulada para transportar información."_

En telecomunicaciones, una **señal** es una variación de una magnitud física (como voltaje, corriente, presión, luz) que representa datos o información.

### 🗂️ Clasificación de Sistemas de Señales

#### 1. **Según el tipo de señal**:

- **Señales analógicas**:
    
    - Continuas en el tiempo y en amplitud.
        
    - Pueden tomar infinitos valores dentro de un rango.
        
    - Ejemplo: voz humana, onda de radio AM.
        
- **Señales digitales**:
    
    - Discretas en amplitud (y a veces en tiempo).
        
    - Solo toman ciertos valores (como 0 y 1).
        
    - Ejemplo: datos binarios de una computadora.


#### 2. **Según el número de valores que puede tomar la señal**:

- **Binaria**: solo 2 valores (típicamente 0 y 1).
    
- **Multinivel**: más de dos niveles (por ejemplo, 4 niveles en 2 bits por símbolo).


#### 3. **Según la periodicidad**:

- **Periódicas**:
    
    - Se repiten en intervalos regulares.
        
    - Permiten análisis con series de Fourier.
        
    - Ejemplo: onda senoidal continua.
        
- **No periódicas**:
    
    - No tienen repetición regular.
        
    - Requieren análisis de Fourier integral (espectro continuo).
        
    - Ejemplo: pulso de datos o una conversación real.


### 🔍 Tipos de Señales

- **Determinísticas**: conocidas y predecibles.
    
- **Aleatorias**: su evolución en el tiempo depende del azar (ej. ruido térmico).
    
- **En tiempo continuo**: definidas para cualquier valor del tiempo.
    
- **En tiempo discreto**: definidas solo en instantes específicos.


### 📈 **Señal Senoidal**

> _"La señal senoidal es la base de toda señal periódica."_

Esto es clave porque **cualquier señal periódica** (por más compleja que sea) puede expresarse como **una suma de senoidales** mediante análisis de **Fourier**.

$$s(t) = A \cdot \sin(2\pi f t + \phi)$$

Donde:

- $A$: **Amplitud** (valor máximo de la onda)
	- Define el **valor máximo** que alcanza la señal.
    - En señales eléctricas puede representarse en voltios.
- $f$: **Frecuencia** (en Hz, ciclos por segundo)
	- Cuántas veces la onda se repite **por segundo**.
    - Afecta el **tono** en audio o el **ancho de banda** en telecomunicaciones.
- $t$: **Tiempo** (en segundos)
- $\phi$: **Fase** (en radianes)
	- Desplazamiento horizontal de la señal.
    - Dos ondas con la misma amplitud y frecuencia pero diferente fase **no están sincronizadas**.


### 📐 **Relación con el período $T$**

El **período $T$** es el tiempo que tarda en completarse un ciclo de la onda:

$T = \frac{1}{f}$

Ejemplo: si $f = 50 \, \text{Hz}$, entonces $T = \frac{1}{50} = 0.02 \, \text{s}$


## 🔹 Velocidad de propagación $v$

- Es la **rapidez con la que viaja la onda en el medio**.
    
- En el vacío: $$v = c = 3 \times 10^8 \, m/s$$
- En otros medios, depende de la **constante dieléctrica** (material):
    
    - En cables coaxiales: $v \approx 0.8 \, c$
        
    - En pares trenzados (UTP): $v \approx 0.67 \, c$
        
    - En fibra óptica: $v \approx 0.66 \, c$
        



## 🔹Longitud de onda $\lambda$

- Es la **distancia** que ocupa un ciclo completo de la onda en el espacio.
- Se mide en metros (m).
- Relaciona la velocidad de la onda con su frecuencia:$$\lambda = \frac{v}{f}$$​

Ejemplo: si una onda viaja a $3 \times 10^8 \, m/s$ (la velocidad de la luz) y tiene $f = 100 \, MHz$:

$$\lambda = \frac{3 \times 10^8}{100 \times 10^6} = 3 \, m$$

→ Cada ciclo ocupa 3 metros en el espacio.


## 🔹 Relación entre las tres

Siempre se cumple:

$v = \lambda \cdot f$

- $T$ = 1/f (tiempo de un ciclo).
    
- $\lambda$ = v/f (distancia de un ciclo).
    

👉 O sea:

- Si aumenta la frecuencia → disminuye la longitud de onda.
    
- Si cambia el medio → cambia $v$, y por ende también $\lambda$.

> [!note] 
> En los ejercicios de **Fundamentos de Telecomunicaciones**, salvo que el enunciado diga lo contrario, **se asume que la onda es electromagnética en el vacío o en el aire ideal**.
> 
> 👉 Entonces, se toma la velocidad de la luz:
> 
> $$v = c = 3 \times 10^8 \, m/s$$


### 🌊 Visualización de variaciones

- Cambiar $A$ → afecta la **altura** de la onda.
    
- Cambiar $f$ → afecta cuán **apretadas** están las oscilaciones.
    
- Cambiar $\phi$ → **desplaza** la onda hacia la izquierda o derecha.


### 📦 Aplicaciones de la señal senoidal

- Es la **portadora fundamental** en modulación AM, FM y PM.
    
- Se usa como base en las **series de Fourier** para construir señales complejas.
    
- Tiene un **espectro espectral limpio**: una sola frecuencia.



### 🟫 **Señal Cuadrada**

Una **señal cuadrada** es una onda periódica que alterna entre dos niveles fijos (por ejemplo: alto/bajo, 1/0, +V/−V), con transiciones abruptas.

#### 🧮 Forma típica:

$$s(t) = \begin{cases} A & \text{si } 0 < t < T/2 \\ -A & \text{si } T/2 < t < T \end{cases} \quad \text{(y se repite cada T)}$$

Donde:

- $A$: amplitud
    
- $T$: período
    
- La frecuencia fundamental es $f_0 = 1/T$



#### 🧠 ¿Por qué es importante?

Porque **los sistemas digitales usan señales cuadradas** para representar bits (0 y 1). Sin embargo, aunque parecen simples, **su espectro es complejo**: ¡no es una sola frecuencia!




### 🎼 **Análisis con Fourier**

> _"Toda señal periódica se puede descomponer en senoidales mediante Fourier."_

Esto es crucial. La **serie de Fourier** nos permite expresar la señal cuadrada como **una suma infinita de senoidales** (armónicos impares):

$$s(t) = \frac{4A}{\pi} \left( \sin(\omega t) + \frac{1}{3} \sin(3\omega t) + \frac{1}{5} \sin(5\omega t) + \cdots \right)$$

Donde:

- $\omega = 2\pi f_0$​: frecuencia angular fundamental
    
- Solo se suman armónicos **impares**: $f_0, 3f_0, 5f_0, \dots$



### 📊 Consecuencias prácticas:

1. **Ancho de banda**:
    
    - Una señal cuadrada "ideal" tiene **componentes infinitas** → **ancho de banda infinito**.
        
    - En sistemas reales, se **filtran los armónicos más altos**, lo que suaviza los bordes → forma más parecida a una senoidal.
        
2. **Distorsión**:
    
    - Si el canal no puede transmitir todos los armónicos necesarios, **la señal cuadrada se distorsiona**.
        
    - Esto es clave para el diseño de filtros, transmisores y medios de transmisión.
        



### ⚠️ **Problema de las señales (en canales reales)**

En el mundo real, las señales **no viajan intactas** por el canal. Sufren diversos **problemas físicos**, que pueden **distorsionar, debilitar o corromper** la información que transportan.



### 📉 1. **Atenuación**

> _"Pérdida de energía."_

La **atenuación** es la **reducción de la amplitud** (o potencia) de una señal al propagarse por un medio físico. Se mide típicamente en **decibelios (dB)**.

- Es **proporcional a la distancia** y al tipo de medio.
    
- Implica que en largas distancias se necesita **amplificación** o **regeneración**.


### 🌫️ 2. **Ruido**

> _"Perturbación no deseada que se suma a la señal."_

El **ruido** es cualquier **energía ajena** a la señal original que se suma durante la transmisión. Puede tener distintos orígenes:

#### 🔥 a. **Ruido térmico (Johnson-Nyquist)**

> _"Ruido generado por el movimiento de electrones en conductores."_

- Es **aleatorio**, **constante** y **predecible estadísticamente**.
    
- Afecta a todos los dispositivos electrónicos.
    
- Su potencia se calcula con:
$$P = kTB$$

Donde:

- $k$: constante de Boltzmann
    
- $T$: temperatura absoluta en Kelvin
    
- $B$: ancho de banda
    

#### ⚙️ b. **Ruido de intermodulación**

> _"Ocurre cuando señales de diferentes frecuencias se combinan y generan productos de mezcla."_

- Sucede en **amplificadores no lineales**.
    
- Genera frecuencias espurias que **interfieren con la señal útil**.


#### 🔀 c. **Crosstalk (diafonía)**

> _"Una señal interfiere con otra a través del acoplamiento eléctrico o magnético."_

- Ocurre en **cables trenzados, coaxiales, o circuitos integrados**.
    
- Hay **crosstalk próximo (NEXT)** y **lejano (FEXT)**.
    
- Se combate con **apantallamiento** y técnicas de diseño físico.


#### ⚡ d. **Ruido por impulsos**

> _"Ruido breve, de alta amplitud, no predecible."_

- Tiene causas como **rayos, motores, o conmutaciones**.
    
- Afecta mucho a señales digitales (puede hacer perder bits).
    
- Muy difícil de filtrar porque **no tiene espectro uniforme**.


### 📉 3. **Distorsión por retardo (Retardo de grupo)**

> _"Ocurre cuando diferentes frecuencias de una señal llegan en momentos distintos."_

- En canales con **respuesta en frecuencia no plana**, los armónicos se retrasan **de forma desigual**.
    
- Resultado: la señal se **deforma en el tiempo** ⇒ **interferencia entre símbolos (ISI)**.
    
- Especialmente crítico en **modulación multicanal** (como DSL).



| Problema               | Causa                                 | Efecto                              |
| ---------------------- | ------------------------------------- | ----------------------------------- |
| Atenuación             | Pérdida natural por distancia y medio | Señal débil ⇒ error                 |
| Ruido térmico          | Agitación electrónica                 | Fondo constante de interferencia    |
| Ruido intermodulación  | No linealidad de equipos              | Nuevas frecuencias espurias         |
| Crosstalk (diafonía)   | Acoplamiento electromagnético         | Señales cruzadas                    |
| Ruido por impulsos     | Fenómenos transitorios                | Interrupciones severas              |
| Distorsión por retardo | Canal no ideal (dispersivo)           | Diferencias de tiempo ⇒ deformación |

| Medio            | Atenuación | BW       | SNR      | Ruido externo | Crosstalk | Costo   |
| ---------------- | ---------- | -------- | -------- | ------------- | --------- | ------- |
| **Par de cobre** | Alta       | Bajo     | Bajo     | Alta          | Sí        | Bajo    |
| **Coaxial**      | Media      | Medio    | Medio    | Medio         | Bajo      | Medio   |
| **Fibra óptica** | Muy baja   | Muy alto | Muy alto | Nulo          | Nulo      | Alto    |
| **Aire (ondas)** | Variable   | Medio    | Bajo     | Alta          | No aplica | Depende |

### 🧱 ¿Qué problemas de las señales se pueden evitar y cómo?

| **Problema**                            | **¿Se puede evitar?** | **¿Cómo se mitiga?**                                                                                 | **Medio más afectado**            |
| --------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------------- | --------------------------------- |
| **Atenuación**                          | ❌ No se puede evitar  | - Uso de amplificadores o repetidores  <br>- Señales digitales regenerativas                         | Todos, especialmente cobre y aire |
| **Ruido térmico**                       | ❌ No se puede evitar  | - Filtros pasa banda  <br>- Mejor relación SNR  <br>- Codificación robusta                           | Todos (es inherente al material)  |
| **Intermodulación**                     | ✅ Sí, parcialmente    | - Usar componentes lineales  <br>- Evitar sobrecarga en amplificadores                               | Coaxial, cobre                    |
| **Crosstalk (diafonía)**                | ✅ Sí, parcialmente    | - Uso de par trenzado con buen trenzado  <br>- Blindajes  <br>- Separación física                    | Par de cobre                      |
| **Ruido por impulsos**                  | ✅ Sí, parcialmente    | - Filtros  <br>- Códigos de detección/corrección  <br>- Supresión de fuentes (motores, etc.)         | Aire, cobre                       |
| **Distorsión por retardo (dispersión)** | ✅ Sí, parcialmente    | - Ecualización del canal  <br>- Uso de modulaciones resistentes  <br>- Limitación del ancho de banda | Fibra (modal), cobre              |

### 💡 Estrategias generales de mitigación

1. **Filtros**: eliminan ruido fuera del ancho de banda útil.
    
2. **Modulación adecuada**: elegir una modulación robusta (PSK o QAM con pocos niveles si hay ruido).
    
3. **Codificación de canal**: agregar bits para detectar y corregir errores (CRC, Hamming, etc.).
    
4. **Repetidores y regeneradores**: restauran la señal en transmisiones largas (digitales).
    
5. **Aislamiento físico**: reducir interferencia externa o entre cables.




# Modulación 

### 📡 ¿Qué es la Modulación?

> _"Modulación: Técnica que permite adaptar una señal para su transmisión."_

En términos técnicos, **modular** significa **modificar una señal portadora (usualmente senoidal)** en función de una señal que contiene la información (señal moduladora).

_Modular es adaptar datos que quiero mandar a un medio. Permite expresar la información contenida en una señal (datos), mediante otra señal (modulada) con características similares a una tercera (portadora). Me apoyo en ciertas características de otras señales que, en el medio en el que me quiero comunicar, funcionan mejor._

![[Pasted image 20250804070431.png]]

• **Moduladora**: Señal de datos a transmitir

• **Portadora**: Señal con las características deseadas

• **Modulada**: Señal con datos de la moduladora y propiedades de la portadora.

Alguien del otro lado tiene que hacer el proceso contrario. Lo llamamos **demodular.**

![[Pasted image 20250804070447.png]]



### 🎯 Objetivos de la modulación

Tu resumen destaca sus finalidades principales:

- **Transmitir señales a largas distancias** sin perder integridad.

- **Adaptar la señal** al canal físico disponible.

- **Multiplexar varias señales** sobre un mismo medio.

- **Reducir el tamaño de las antenas** (subiendo la frecuencia).

- **Permitir la detección y recuperación eficientes** en el receptor.


### 🧱 Tipos de modulación

|                         | Moduladora Analógica      | Moduladora Digital    |
| ----------------------- | ------------------------- | --------------------- |
| **Portadora Analógica** | AM, FM, PM                | ASK, FSK, PSK, QAM    |
| **Portadora Digital**   | PAM, PDM, PPM, PCM, Delta | Codificación de Línea |



### ✳️ ¿Qué es una constelación en modulación?

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


- PSK → poné **M** puntos igualmente espaciados en **un círculo**.

- QAM → hacé una **rejilla** M×M\sqrt{M}\times\sqrt{M}M​×M​ (p. ej. 16-QAM = 4×4).

- APSK → repartí **M** puntos en **2–3 círculos** (por ejemplo 8-APSK = 4 dentro + 4 fuera).

- En **APSK** ponés los $M$ puntos en **anillos concéntricos**.
    
- Para que los puntos queden **más o menos igual de separados**, cada anillo debería tener **más puntos cuanto mayor sea su radio** (su circunferencia es mayor).
    

Una **regla práctica**: repartir $M$ como

- **16-APSK:** $4+12$ (2 anillos)
    
- **32-APSK:** $4+12+16$ (3 anillos)
    
- **64-APSK:** $4+12+20+28$ (4 anillos)


### Modulación portadora analógica a moduladora analógica

> _"Se modulan parámetros de una onda portadora senoidal: amplitud, frecuencia o fase."_

![[Pasted image 20250803173026.png]]

#### 🔊 a. Amplitud (AM)
En **AM**, se usa una **portadora senoidal continua** (analógica) cuya **amplitud se modifica** en proporción a los valores instantáneos de una **señal moduladora analógica** (por ejemplo, voz o música).
 
Fórmula típica:
$$s(t) = [A + m(t)] \cdot \cos(2\pi f_c t)$$

Donde:

- $A$: amplitud de la portadora.

- $m(t)$: señal moduladora analógica.

- $f_c$​: frecuencia de la portadora.

- La señal modulada contiene la **frecuencia portadora** y dos **bandas laterales**.

- La **frecuencia y fase** de la portadora permanecen constantes.

- Se varía la **amplitud** de la portadora en proporción a la señal de información.

- Sensible al **ruido**.

- Usada en radiodifusión AM.


#### 🎶 b. Frecuencia (FM)

En **FM**, la **frecuencia de la portadora** varía en función del valor instantáneo de la **señal moduladora analógica**.

Fórmula:
$$s(t) = A \cdot \cos\left(2\pi f_c t + 2\pi k_f \int m(t) dt\right)$$

Donde:

- $k_f$​: sensibilidad de frecuencia.

- $m(t)$: señal moduladora.

- Se varía la **frecuencia** de la portadora.

- Mucho más **robusta al ruido** que AM. No hay ruido

- Usada en radio FM y enlaces de microondas.

- La **amplitud y fase** permanecen constantes.


![[Pasted image 20250803173115.png]]


#### 🔁 c. Fase (PM)

En **PM**, es la **fase de la portadora** la que se modifica proporcionalmente al valor de la señal moduladora.    

Fórmula:
$$s(t) = A \cdot \cos\left(2\pi f_c t + k_p \cdot m(t)\right)$$

Donde:

- $k_p$​: sensibilidad de fase.

- $m(t)$: señal moduladora analógica.

- PM es conceptualmente similar a FM, pero la modulación se aplica **directamente a la fase**.

- Se varía la **fase** de la portadora según la señal.

- Menos común en analógica, pero base de muchas técnicas digitales.

- La **amplitud y frecuencia** permanecen constantes.

![[Pasted image 20250803173325.png]]



### Modulación Portadora analógica a Moduladora digital

> _"Se representan bits modificando algún parámetro de la portadora senoidal."_

![[Pasted image 20250803172027.png]]

En este caso, lo que se transmite no es una señal analógica continua, sino **secuencias binarias (0s y 1s)**. Las técnicas más comunes son:

- La **portadora** es una **señal senoidal** (analógica, continua en el tiempo y frecuencia).
- La **moduladora** es una **señal digital**, una secuencia binaria que representa los datos a transmitir.

#### 🧲 a. Amplitude Shift Keying (ASK)

Utiliza una onda portadora analógica cuya amplitud se modifica según los valores digitales (0 o 1) de la señal de entrada.

El principio de ASK es:
$$s(t) = \begin{cases} A \cdot \cos(2\pi f t), & \text{si el bit es 1} \\ 0, & \text{si el bit es 0} \end{cases}$$

![[Pasted image 20250803124328.png]]

| Aplicación                                | Detalle técnico                                                                  |
| ----------------------------------------- | -------------------------------------------------------------------------------- |
| **RFID de baja frecuencia (LF/HF)**       | ASK es común en etiquetas RFID pasivas, por su simplicidad.                      |
| **Controles remotos IR**                  | Algunos controles usan ASK para modular datos en portadoras infrarrojas.         |
| **Modems antiguos (nivel básico)**        | ASK fue una de las primeras modulaciones usadas en modems de muy baja velocidad. |
| **Sistemas de transmisión óptica simple** | ASK se usa en transmisores LED sin técnicas complejas.                           |
| **Sistemas embebidos de corto alcance**   | ASK es útil cuando la interferencia no es un gran problema.                      |



#### 🔄 b. Frequency Shift Keying (FSK)

Utiliza una portadora analógica cuya **frecuencia varía** dependiendo del valor del bit digital.

Es decir, los bits **modulan la frecuencia** de la portadora:
- Bit 1 → frecuencia $f_1$​
- Bit 0 → frecuencia $f_0$
​
Fórmula típica:
$$s(t) = \begin{cases} A \cdot \cos(2\pi f_1 t), & \text{si el bit es 1} \\ A \cdot \cos(2\pi f_0 t), & \text{si el bit es 0} \end{cases}$$

Así, la **moduladora digital (la secuencia de bits)** determina **qué frecuencia usa la señal senoidal** (portadora analógica) en cada instante.

- La **amplitud** es constante

- Más resistente al ruido que ASK

- Requiere más ancho de banda

![[Pasted image 20250803124346.png]]

|Aplicación|Detalle técnico|
|---|---|
|**Modems antiguos (300–1200 bps)**|FSK fue usado en modems telefónicos pre-1990.|
|**Radiocomunicación de baja velocidad**|Comunicación entre dispositivos embebidos, sensores.|
|**Identificación por radiofrecuencia (RFID)**|Algunas etiquetas RFID utilizan FSK.|
|**Sistemas de telemetría y control industrial**|Por su simplicidad y robustez al ruido.|


#### 🔃 c. Phase Shift Keying (PSK)

La **fase de la portadora analógica** se modifica según los **valores de la señal digital**.

Los bits controlan **cuántos grados de fase** tiene la onda:
$$s(t) = A \cdot \cos(2\pi f t + \phi_i)$$

Donde:

- $\phi_i$​: fase asignada al bit o grupo de bits (por ejemplo, 0° para '00', 90° para '01', etc.)

- En **BPSK**, se usan solo dos fases (0° y 180°).

- En **QPSK**, se usan cuatro fases (0°, 90°, 180°, 270°) para codificar 2 bits por símbolo.

- La frecuencia y la amplitud de la señal se mantienen constantes

![[Pasted image 20250803124400.png]]

|Aplicación|Detalle técnico|
|---|---|
|**Wi-Fi (IEEE 802.11)**|Usa **BPSK y QPSK** en sus esquemas de modulación según la velocidad.|
|**Sistemas satelitales**|PSK es muy robusto al ruido → ideal para transmisión en banda ancha (DVB-S).|
|**Bluetooth**|Utiliza GFSK, pero versiones anteriores usaban formas de PSK para control.|
|**Radioaficionados digitales**|Modos digitales como PSK31 para transmisión de texto eficiente.|


#### 🔀 d. Quadrature Amplitude Modulation (QAM)

QAM es una **modulación compuesta** que combina:
- **Variación en amplitud** (como ASK) 
- **Variación en fase** (como PSK)

Se usan **dos portadoras senoidales ortogonales** (una en fase y otra en cuadratura), y los bits digitales determinan **qué amplitud y fase combinada** se usa en cada símbolo.

Fórmula base:
$$s(t) = I(t) \cdot \cos(2\pi f t) + Q(t) \cdot \sin(2\pi f t)$$

Donde:

- $I(t)$ y $Q(t)$ son funciones que dependen de los **bits digitales** y determinan la amplitud de cada componente.

- Cada combinación única de bits se representa como un **punto en el plano IQ** (constelación).

- Por eso, **QAM también usa una portadora analógica**, pero la **modulación digital actúa sobre dos parámetros** a la vez (amplitud y fase).

- Permite **modulaciones multibit** muy eficientes (como 16-QAM, 64-QAM, etc.).

- Permite alcanzar mayores velocidades de transmisión al aumentar la cantidad de bits por baudio, aunque es más susceptible a ruido. Requiere de receptores más sensibles y de mayor procesamiento.

![[Pasted image 20250803124644.png]]

|Aplicación|Detalle técnico|
|---|---|
|**Televisión digital (DVB-C)**|Utiliza QAM (16-QAM, 64-QAM, 256-QAM) para cable.|
|**Internet por cable (DOCSIS)**|Transmisión de datos en HFC, con 64-QAM o más.|
|**Wi-Fi (802.11n/ac/ax)**|Usa **QAM de hasta 1024 o 4096 niveles** en altas velocidades.|
|**4G/5G móvil (LTE, NR)**|Modulación adaptativa entre QPSK, 16-QAM, 64-QAM, 256-QAM según condiciones del canal.|


### 🧮 **¿Qué son los estados posibles?**

Los **estados posibles** en una modulación digital son **las diferentes combinaciones únicas de fase, frecuencia y/o amplitud** que puede adoptar un símbolo.

Cada **símbolo** representa varios bits, y los **estados posibles** son el total de **símbolos distintos** que se pueden transmitir.

#### 🧠 ¿Cómo los calculo?

Cuando tenés:

- **Tasa de transmisión en bits por segundo (bps):** $T_t$
    
- **Baudios (símbolos por segundo):** $B$
    

Usás esta relación:
$$\text{bits por símbolo} = \frac{T_T}{B}$$​

Y los **estados posibles** se calculan como:
$$M = 2^{\frac{T_T}{B}}$$



### 💾 **Modulación Portadora Digital a Moduladora Analógica**

Aquí, la **portadora** ya no es una onda senoidal continua como en AM/FM/PM, sino una **señal digital** (por ejemplo, una secuencia de pulsos). Lo que se hace es **modular sus características** (amplitud, duración, posición, etc.) para representar una señal analógica original.

Este tipo de modulación se usa comúnmente en sistemas de **digitalización de señales analógicas**, como en telefonía, audio, sensores, etc.


#### Ventajas y Desventajas

Debo tener sistemas sincrónicos, por eso deben tener una señal de reloj con tren de pulsos cuadrados o triangulares.

La frecuencia nos va a decir cuándo tomar la muestra, y debe cumplir el teorema del muestreo (Nyquist)

**Ventajas**

• Inmune al ruido

• Circuitos digitales sencillos

• Facilidad en reconocer un estado definido

• Señalización simple

• Control del canal junto con datos

• Encriptable, QoS (etiquetar datos para que otro sistema se dé cuenta de las prioridades), Monitoreo.

**Desventajas**

• Mayor BW - Nyquist

• Necesidad conversión A/D y D/A

• Sincronización



### 🔢 Tipos de Modulación con Portadora Digital

#### 1. **PAM – Pulse Amplitude Modulation**

> Modulación por amplitud de pulsos.

- La **amplitud de cada pulso digital** representa el valor instantáneo de la señal analógica.

- Es una técnica **analógica a digital** (aunque el resultado aún es una señal analógica en forma de pulsos).

- La señal analógica se **muestrea** periódicamente.

- Cada muestra se convierte en un pulso de **amplitud proporcional** a su valor.

Fórmula:
$$s(t) = \sum_{n=-\infty}^{\infty} m(nT_s) \cdot \delta(t - nT_s)$$

Donde:

- $m(nT_s)$: valor de la señal analógica en el instante de muestreo.

- $T_s$​: período de muestreo.


***📦 Uso típico:***

- Primer paso en sistemas PCM.

- Transmisión de audio o video en sistemas antiguos.

- Se envían **pulsos a intervalos regulares**, cuya **amplitud representa** el valor instantáneo de la señal analógica.

- Es una **etapa previa** en sistemas como PCM.

- Muy sensible al **ruido en amplitud**.



#### 2. **PDM – Pulse Duration Modulation**

> Modulación por duración de pulsos.

- También se llama **PWM – Pulse Width Modulation**.

- Todos los pulsos tienen la **misma amplitud**, pero su **duración (ancho)** varía proporcionalmente a la señal analógica.

- Cada valor de la señal moduladora se representa mediante un pulso de duración proporcional.

- Ideal para sistemas con componentes que responden a tiempo de activación (motores, fuentes de alimentación).



***📦 Uso típico:***

- Control de motores eléctricos.

- Electrónica de potencia.

- Audio digital (PWM en amplificadores clase D).



#### 3. **PPM – Pulse Position Modulation**

> Modulación por posición de pulsos.

- Pulsos de igual amplitud y duración, pero su **posición en el tiempo** cambia según la señal analógica.

- Cada valor de la señal se representa desplazando el pulso dentro de su ventana temporal.


***📦 Uso típico:***

- Comunicaciones ópticas.

- Infrarrojos (ej. controles remotos).

- Es más **resistente al ruido en amplitud**.




#### 4. **PCM – Pulse Code Modulation**

> Modulación por código de pulsos.

- Transforma una señal analógica en una **secuencia de palabras binarias** (digital puramente).

- La señal analógica es:
    1. **Muestreada** (según Nyquist),
        
    2. **Cuantificada** (discretización de valores),
        
    3. **Codificada** (en binario).
    

Fórmula para el número de bits por muestra:
$$\text{Bits por muestra} = \log_2(N)$$

Donde $N$ es el número de niveles de cuantificación.

***📦 Uso típico:***

- Telefonía digital (Ej: G.711)

- CD de audio

- Transmisión digital en redes




#### 5. **Delta Modulation**

> Variante simplificada de PCM.

Variante de PCM más simple: en lugar de codificar el valor completo de cada muestra, codifica si **sube o baja** respecto a la anterior.

- Genera una secuencia de bits (1 = sube, 0 = baja).
    
- Más eficiente en términos de ancho de banda.
    
- Puede sufrir **sobrecarga** si la señal varía rápido.
    

***📦 Uso típico:***

- Voz digital en sistemas de bajo ancho de banda.
    
- Codificadores de audio con baja complejidad.

- En lugar de enviar el valor completo de cada muestra, se envía **si sube o baja respecto a la anterior**.
    
- Requiere menos bits.
    
- Más eficiente, pero **sensible a variaciones rápidas**.



|Técnica|Parámetro modulado|Señal moduladora|Tipo de codificación|
|---|---|---|---|
|**PAM**|Amplitud del pulso|Analógica|Pulsos analógicos|
|**PDM**|Duración del pulso|Analógica|Pulsos analógicos|
|**PPM**|Posición del pulso|Analógica|Pulsos analógicos|
|**PCM**|Código binario completo|Analógica|Digital puro|
|**Delta**|Diferencia entre muestras|Analógica|Digital binario (1/0)|




### Modulación portadora digital a moduladora digital - Codificación de línea

Sirve para neutralizar el ruido (codificación Manchester). Lo usan los teclados de computadoras para evitar mandarle ruido a la pc.

#### 🔌 **Codificación en línea**

> _La codificación en línea consiste en representar los bits digitales mediante formas específicas de señal digital (1s y 0s), adaptadas al medio físico de transmisión._

- Se utiliza cuando la **portadora es digital** (por ejemplo, una línea de transmisión de impulsos eléctricos).
    
- Su función no es modular en amplitud/frecuencia/fase, sino **codificar directamente** los bits en formas de onda eléctricas.
    
- Elige una **convención temporal** para representar los bits, y puede incorporar:
    
    - Control de **nivel DC** (evitar corriente continua acumulada)
        
    - Facilitación de la **sincronización**
        
    - **Detección de errores** (en algunos casos)
        


### 🧩 Tipos principales de codificación en línea

#### 1. **NRZ – Non Return to Zero**

- El bit **1** se representa con un nivel alto; el **0**, con un nivel bajo (o viceversa).
    
- 🧾 Problema: largas secuencias iguales dificultan la sincronización.
    
- Variante **NRZ-I**: cambia de nivel solo cuando hay un '1'.
    



#### 2. **RZ – Return to Zero**

- Cada bit vuelve a 0 en la mitad del intervalo.
    
- Mejora la sincronización.
    
- Requiere mayor ancho de banda.
    



#### 3. **Manchester**

- Bit '1': transición de alto a bajo.
    
- Bit '0': transición de bajo a alto.
    
- 🧠 Ventaja: siempre hay transición → fácil sincronización.
    
- Utilizado en **Ethernet clásico (10Base-T)**.
    



#### 4. **Differential Manchester**

- Cada bit tiene al menos una transición.
    
- La presencia o ausencia de transición al inicio del bit determina su valor.
    
- Más robusto ante inversión de polaridad del cable.
    


#### 5. **AMI – Alternate Mark Inversion**

- '0' → nivel 0 (sin señal); '1' → alterna entre nivel positivo y negativo.
    
- Controla componente DC y facilita detección de errores.









- - -




# Códigos

### 🔠 ¿Qué es un código?

> _"Conjunto de reglas para representar símbolos o mensajes por medio de otros símbolos."_

Un **código** es un sistema para representar información (como letras, números, señales) en un **formato binario** o digital que sea **transmisible** y/o **procesable**.

Ejemplos cotidianos:

- ASCII (letras a bits)
    
- Morse (letras a puntos y rayas)
    
- Binario (números o símbolos a 0s y 1s)


### 🎯 ¿Por qué usamos códigos?

1. **Representación**: transformar datos a símbolos binarios.
    
2. **Protección**: detectar y/o corregir errores que ocurren durante la transmisión.
    



### 🧠 Propiedades deseables de un código

En el diseño y análisis de códigos, buscamos ciertas **propiedades clave** que garanticen eficiencia y confiabilidad:

- **No ambiguo**: Cada secuencia codificada debe representar **únicamente** un símbolo.
    
- **Único**: No debe haber dos símbolos distintos con el mismo código.
    
- **Eficiente**: Que use la menor cantidad posible de bits promedio.
    
- **Fácil de decodificar**: Que permita identificar rápidamente los límites de cada código.
    



### 🗂️ Clasificación de los códigos

#### 🔹 **1. Códigos sin detección de errores**

> Usados solo para **representar información**.

Ejemplos:

- **Binario natural**: representación directa de números.
    
- **BCD (Decimal codificado en binario)**: cada dígito decimal se representa con 4 bits.
    
- **Gray**: entre dos números consecutivos solo cambia **1 bit** → útil en electrónica digital.
    
- **ASCII**: para letras, números y símbolos del teclado.
    


#### 🔸 **2. Códigos con detección y corrección de errores**

> Además de representar, están diseñados para **detectar o corregir errores** de transmisión.

Se dividen en:

- **Códigos de detección**:
    
    - **Paridad**: bit extra para asegurar que el número total de 1s sea par/impar.
        
    - **VRC (Vertical Redundancy Check)**, **LRC (Longitudinal Redundancy Check)**.
        
    - **Checksum**.
        
- **Códigos de corrección**:
    
    - **Hamming**: permite detectar y corregir **1 bit** de error.
        
    - **Códigos CRC (Cyclic Redundancy Check)**: muy usados en redes (Ethernet, USB).
        



### 📌 Tabla resumen de clasificación

| Tipo de Código            | Función principal           | Ejemplos                  |
| ------------------------- | --------------------------- | ------------------------- |
| Sin detección de errores  | Representación pura         | Binario, BCD, ASCII, Gray |
| Con detección de errores  | Detectar errores            | Paridad, VRC, LRC         |
| Con corrección de errores | Detectar y corregir errores | Hamming, CRC              |

### Tipos de códigos

### 1️⃣ **Código en bloque**

- Es un código en el que **todos los símbolos codificados** tienen **la misma longitud** en bits.
    
- Ejemplo:  
    Si tenemos los símbolos $\{A, B, C\}$ y usamos:
    
    - $A = 00$
        
    - $B = 01$
        
    - $C = 10$
        → Cada código tiene **2 bits** → es un **código en bloque**.
        
- Ventaja: fácil de sincronizar, rápida decodificación.
    
- Desventaja: no siempre es eficiente si las probabilidades de los símbolos son muy desiguales.
    


### 2️⃣ **Código no singular**

- Un código es **no singular** si **cada símbolo** del alfabeto de la fuente tiene un **código distinto**.
    
- Esto garantiza que no haya **dos símbolos diferentes con el mismo código**.
    
- Ejemplo:
    
    - $A = 0$, $B = 10$, $C = 11$ → **No singular**
        
    - $A = 0$, $B = 0$, $C = 11$ → **Singular** (A y B tienen el mismo código)
        



### 3️⃣ **Código singular**

- Es lo contrario: **sí hay** al menos **dos símbolos distintos** que comparten el mismo código binario.
    
- Esto genera **ambigüedad total**, incluso en la codificación de un solo símbolo.
    
- Ejemplo:
    
    - $A = 0$, $B = 0$, $C = 1$ → código **singular**
        



### 4️⃣ **Código unívocamente decodificable**

- Incluso si el código **no es en bloque**, se puede decodificar **sin ambigüedad** en un mensaje completo.
    
- Esto significa que **ninguna secuencia de bits válida para un símbolo puede ser confundida con parte de otra secuencia**.
    
- Ejemplo:
    
    - $A = 0$, $B = 01$, $C = 011$ → ❌ **No es unívocamente decodificable**, porque “011” puede interpretarse como C o como A+B.
        
    - $A = 0$, $B = 10$, $C = 11$ → ✅ **Unívocamente decodificable**
        



### 5️⃣ **Código instantáneo**

- También llamado **prefijo**: **ningún código de un símbolo es prefijo del código de otro símbolo**.
    
- Esto garantiza que pueda decodificarse **en el momento exacto** que termina un símbolo, sin esperar bits adicionales.
    
- Todos los códigos instantáneos son unívocamente decodificables, pero no al revés.
    
- Ejemplo instantáneo:
    
    - $A = 0$, $B = 10$, $C = 110$ → ✅
        
- Ejemplo no instantáneo:
    
    - $A = 0$, $B = 01$, $C = 011$ → ❌ (A es prefijo de B y C)
        



### 6️⃣ **Código compacto**

- Es un código que **usa el menor número posible de bits promedio** para la longitud de código, dado el alfabeto y sus probabilidades.
    
- Ejemplo típico: **Código de Huffman**
    
- En un código compacto, la **longitud promedio $L$** está muy cerca del **límite teórico de la entropía HHH**:
    
    $$H \le L < H+1$$



## 📊 Resumen en tabla:

|Tipo de código|Característica principal|Ejemplo válido|Ejemplo no válido|
|---|---|---|---|
|**En bloque**|Todos los códigos misma longitud|00, 01, 10|0, 10, 110|
|**No singular**|Cada símbolo tiene un código distinto|0, 10, 11|0, 0, 11|
|**Singular**|Dos símbolos con el mismo código|0, 0, 1|—|
|**Unívocamente decodificable**|Mensajes completos se decodifican sin ambigüedad|0, 10, 11|0, 01, 011|
|**Instantáneo**|Ningún código es prefijo de otro|0, 10, 110|0, 01, 011|
|**Compacto**|Longitud promedio mínima según probabilidades|Huffman|Código aleatorio|



### 📌 ¿Qué es el método Huffman?

El **algoritmo de Huffman** es un método de **codificación óptima** (dentro de los códigos prefijo) que asigna **códigos binarios de distinta longitud** a cada símbolo, en función de su **probabilidad de aparición**.

🎯 **Objetivo:**  
Reducir la **longitud promedio del código** ($L$) lo más cerca posible de la **entropía** ($H$) de la fuente.



#### 📌 Características clave

- Es **un código instantáneo** (prefijo) → ningún código es prefijo de otro.
    
- Es **unívocamente decodificable**.
    
- Es **compacto** → no existe otro código prefijo con menor longitud promedio para esas probabilidades.
    
- **Longitudes más cortas** para los símbolos **más probables**.
    
- **Longitudes más largas** para los símbolos **menos probables**.
    



#### 📌 Procedimiento paso a paso

1. **Listar símbolos y probabilidades** de la fuente.
    
2. **Ordenar** de menor a mayor probabilidad.
    
3. **Combinar** los dos símbolos **menos probables en un nodo**, sumando sus probabilidades.
    
4. Repetir el paso anterior hasta quedar con un único nodo (árbol completo).
    
5. **Asignar** 0 y 1 a las ramas de cada unión (convención: izquierda 0, derecha 1).
    
6. Leer los códigos desde la raíz hasta cada símbolo.


> [!warning] IMPORTANTE
> Es importante **Combinar** los dos símbolos **menos probables en un nodo**




#### 📌 Ejemplo

***Fuente:***

| Símbolo | Probabilidad |
| ------- | ------------ |
| A       | 0.4          |
| B       | 0.3          |
| C       | 0.2          |
| D       | 0.1          |

***Paso 1: Ordenar (menor a mayor)***

D (0.1), C (0.2), B (0.3), A (0.4)


***Paso 2: Combinar los dos menores***

- C (0.2) + D (0.1) → nodo CD (0.3)

Lista:  
CD (0.3), B (0.3), A (0.4)


***Paso 3: Repetir***

- CD (0.3) + B (0.3) → nodo CDB (0.6)

Lista:  
CDB (0.6), A (0.4)


***Paso 4: Última unión***

- CDB (0.6) + A (0.4) → nodo raíz (1.0)


***Paso 5: Asignar bits***

```mathematica
           (1.0)
          /     \
       (0.6)     A:0.4
      /     \
   (0.3)     B:0.3
  /     \
D:0.1   C:0.2

```

Asignación de bits:

- Izquierda: 0
    
- Derecha: 1
    

Códigos:

- A = 1
    
- B = 01
    
- C = 001
    
- D = 000
    

![[Pasted image 20250730200007.png]]


### 📌 Cálculo de la longitud promedio

$$L = \sum p_i \cdot l_i$$$$L = (0.4 \cdot 1) + (0.3 \cdot 2) + (0.2 \cdot 3) + (0.1 \cdot 3) = 1.9 \, \text{bits/símbolo}$$

#### 📌 Relación con la entropía

$$H = -\sum p_i \log_2 p_i$$​$$H \approx 1.846 \, \text{bits/símbolo}$$$$E = \frac{H}{L} \approx 97.16\%$$

→ Es muy eficiente.



### 📌 Usos del código Huffman

- Compresión de datos (ZIP, GZIP, 7z)
    
- Codificación de imágenes (JPEG)
    
- Compresión de audio (MP3, AAC)
    
- Transmisiones digitales con compresión de fuente



### 📌 **Transmisión de códigos**

Es la forma en que los **bits que representan símbolos** (por ejemplo, en ASCII, Huffman, etc.) se envían por un **canal físico**.

La transmisión puede clasificarse principalmente por **cómo se envían los bits** y por **cómo se sincroniza el emisor con el receptor**.



### 📌 **Transmisión en paralelo**

- **Qué es:** Se envían **varios bits al mismo tiempo**, cada uno por un **conductor diferente**.
    
- Ejemplo: Un bus de 8 bits en un microprocesador (8 cables transmiten simultáneamente un byte).
    
- **Ventajas:**
    
    - Muy rápida (un ciclo transmite varios bits).
        
- **Desventajas:**
    
    - Necesita muchos conductores → más costosa.
        
    - Difícil de usar en largas distancias (problemas de sincronía y crosstalk).
        
- **Usos típicos:** Dentro de computadoras (buses de datos), impresoras antiguas con puerto paralelo (IEEE 1284).


> [!NOTE] Title
> Es muy viejo. Lo solían usar impresoras. Agarrabas 80 cables y en cada uno mandabas un bit. No servía para comunicaciones a distancia.



### 📌 **Transmisión en serie**

- **Qué es:** Los bits se envían **uno tras otro** por un solo canal o conductor.
    
- **Ventajas:**
    
    - Menos cables → más barata y sencilla.
        
    - Adecuada para largas distancias.
        
- **Desventajas:**
    
    - Más lenta que la paralela (a igualdad de tecnología), aunque en la práctica moderna con altas frecuencias puede superar a la paralela.
        
- **Usos típicos:** USB, Ethernet, RS-232, transmisión de datos por fibra óptica.

> [!NOTE] Title
> Sirve para comunicación a distancia. Se usó en los primeros mouse. Sirve para la tarjeta SUBE. En poco volumen de datos se usa transmisión en serie.



### 📌 **Transmisión asíncrona**

- **Qué es:** No hay un reloj común continuo entre emisor y receptor; la sincronización se realiza **por carácter o por palabra**.
    
- Cada bloque transmitido lleva:
    
    - **Bit de inicio** (_start bit_) → marca el comienzo.
        
    - **Bits de datos**.
        
    - **Bit(es) de parada** (_stop bits_) → marca el final.
        
    - Opcional: bit de paridad para control de errores.
        
- **Ventajas:**
    
    - Simple, no requiere sincronización continua.
        
    - Ideal para transmisiones intermitentes.
        
- **Desventajas:**
    
    - Sobrecarga de bits extra.
        
- **Ejemplo:** Comunicación serie RS-232, puertos COM antiguos.

> [!NOTE] Title
> Tiene bits de arranque, de parada y bits de fin. Se usa en terminales tipo dumb. Se le puede sumar un bit de paridad.



### 📌 **Transmisión síncrona**

- **Qué es:** Emisor y receptor comparten un **reloj común** o derivan la sincronía de la señal recibida.
    
- Se transmiten los bits **de forma continua**, sin bits de inicio/parada por cada carácter.
    
- La sincronización se puede mantener:
    
    - Por un canal de reloj dedicado.
        
    - Por técnicas de codificación en línea (ej. Manchester, 8B/10B) que permiten recuperar el reloj del flujo de datos.
        
- **Ventajas:**
    
    - Mayor eficiencia (no hay bits de inicio/parada por cada carácter).
        
    - Ideal para flujos continuos de datos.
        
- **Desventajas:**
    
    - Más compleja de implementar (requiere mantener sincronía).
        
- **Ejemplo:** Ethernet, USB 3.x, SPI.

> [!NOTE] Title
> Tengo que tener un canal que nos ponga en sincronismo. Es en general por bloques, y los caracteres se transmiten en forma continua. La sincronización entre el transmisor y el receptor se realiza mediante caracteres de sincronización. Se usa en terminales Smart. Los datos que ingresa el usuario se almacenan en la terminal. Cuando se completa la entrada, el usuario presiona enter y todos los datos se transmiten en un bloque.



## 📊 Comparativa rápida

|Tipo|Velocidad|Complejidad|Uso típico|
|---|---|---|---|
|Paralelo|Alta|Alta|Comunicación interna de hardware|
|Serie|Media/Alta|Baja|Redes, buses modernos|
|Asíncrono|Media|Baja|Transmisión intermitente|
|Síncrono|Alta|Media/Alta|Flujos de datos continuos|



### 📌 **Códigos de detección y corrección de errores**

Cuando transmitimos datos por un canal real, las señales pueden verse afectadas por **ruido, distorsión, interferencia**, etc. → Esto puede alterar bits.

Los **códigos de detección y corrección de errores** agregan **redundancia controlada** para que el receptor pueda:

- **Detectar** si hubo un error
    
- **Corregirlo** (en algunos casos) sin retransmisión
    



#### 🔍 a) **Códigos de detección**

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

### VRC (paridad simple)

**Qué es:** agregar **1 bit de paridad** al final de cada palabra (trama) para que el **número total de unos** sea **par** (paridad par) o **impar** (paridad impar).

**Cómo se calcula:**

- Paridad **par** → si la cantidad de 1s en los datos es impar, ponés el bit de paridad = 1 (así total queda par).
    
- Paridad **impar** → al revés.
    

**Qué detecta:**

- Detecta **cualquier número impar** de errores de bit (1, 3, 5, …).
    
- **No** detecta cuando hay un número **par** de errores (2, 4, …) dentro de la misma palabra.
    

**Uso típico:** barato, simple, se usa mucho combinado con otras técnicas.



### LRC (paridad longitudinal)

**Qué es:** pensar las tramas como una **matriz** de bits: juntás varias palabras del mismo largo, las apilás y calculás **paridad por columna**. Ese vector de paridades (una palabra extra) es el **LRC**.

**Qué detecta:**

- Detecta **muchos patrones** que VRC solo no detecta, porque mira **por columnas**.
    
- Si combinás **VRC + LRC** (paridad bidimensional), **detectás** cualquier error de **1 bit** y la gran mayoría de errores múltiples (incluso te permite **corregir** 1 bit si sabés fila y columna que fallaron).
    

**Limitación:** sigue siendo simple; no es tan fuerte como CRC para ráfagas largas de errores.



### CRC (Cyclic Redundancy Check)

**Idea clave:** tratar las palabras de bits como **polinomios sobre GF(2)** (coeficientes 0/1, sumas como XOR). Elegís un **polinomio generador** $g(x)$ de **grado $r$**. El **CRC** es el **resto** de dividir el polinomio del **mensaje extendido con $r$ ceros** por $g(x)$.

**Pasos en el emisor:**

1. Tenés el mensaje $M$ (bits).
    
2. Elegís $g(x)$ (por ejemplo, en tu ejercicio: $x^3 + x + 1$).
    
    - En bits se escribe con coeficientes del grado mayor al menor: $x^3+x+1 \Rightarrow 1\,0\,1\,1$ (o “1011”).
        
    - **Longitud de $g$** = grado + 1 ⇒ acá **4 bits**.
        
    - **Longitud del CRC** = **r** = 3 bits (porque grado=3).
        
3. Formás $M\cdot x^r$ (o lo mismo: **agregás $r$ ceros** al final del mensaje).
    
4. Hacés **división módulo-2** (XOR en lugar de restas) de $M x^r$ entre $g(x)$.
    
5. El **resto $R$** (de **3 bits** en este caso) es el **CRC**.
    
6. Enviás el **codeword** = **$M$ seguido de $R$**.
    

**Pasos en el receptor (lo que te piden):**

- Dividís la **trama recibida completa** (datos+CRC) **por el mismo $g(x)$** usando módulo-2.
    
- Si el **resto es 0**, el mensaje es **“libre de errores detectables por ese $g(x)$”**. Si **no es 0**, **hubo error**.
    

**Cómo dividir en módulo-2 (a mano):**

- Usás el “**long division**” pero con XOR.
    
- Alineás $g$ con el primer 1 del dividendo; si el bit líder es 1, **XOR** con $g$; bajás el siguiente bit y repetís.
    
- El **resto final** tiene **longitud < longitud de $g$** (acá 3 bits).

> [!note] 
> Bit lider = bit más significativo = bit más a la izquierda

**Por qué funciona:** el emisor construye una palabra **exactamente divisible** por $g(x)$. Si la transmisión cambia algún bit, esa divisibilidad casi siempre se rompe → resto ≠ 0.

**Capacidades de detección del CRC:**

- Detecta **todos los errores de 1 bit** si $g(x)$ tiene al menos dos términos (siempre).
    
- Detecta **muchos** errores de 2 bits (si $g(x)$ no divide $x^k+1$ para ciertos $k$).
    
- Detecta **todas las ráfagas de longitud ≤ r** (a lo sumo $r$ bits contiguos).
    
- Si $g(x)$ **tiene factor $(x+1)$** (equivale a **paridad incluida**, número de coeficientes 1 **par**), detecta **todos los errores con número impar de bits**.
    
    - En tu caso $g(x)=x^3+x+1$ → bits “1011” (tres unos, **impar**) ⇒ **no** contiene $(x+1)$; no garantiza detectar **todos** los errores de paridad impar (igual sigue siendo muy bueno).



#### 🔍 b) **Códigos de corrección**

- Permiten **detectar y corregir** errores sin pedir retransmisión.
    
- Usan más redundancia que los de detección.
    
- Ejemplos:
    
    - **Código de Hamming**
        
    - **Códigos Reed–Solomon**
        
    - **Turbo codes**, **LDPC** en telecomunicaciones modernas
        

**Idea básica:**

- Cada palabra transmitida es suficientemente distinta de las demás en términos de bits (distancia de Hamming) para que, si se recibe con 1 o 2 bits cambiados, se pueda identificar cuál era la palabra original.
    

### Código de Hamming y para qué se usa

El **código de Hamming** es un código lineal que **detecta y corrige errores** en transmisión/almacenamiento.

### 📌 **Distancia de Hamming**

La **distancia de Hamming** $d$ entre dos palabras binarias es el **número de bits en los que difieren**.

Ejemplo:

- Palabra 1: `101101`
    
- Palabra 2: `100001`
    
- Distancia de Hamming: $d = 2$ (difieren en la tercera y cuarta posición).
    

Te dice cómo medir la **distancia mínima** de un código $d_{min}$​ y cómo eso determina si podés detectar o corregir errores.

Para un código Hamming estándar:

- $d_{min} = 3$
    
- Eso implica que puede **corregir 1 error** y **detectar 2**.



#### 🧮 **Distancia mínima de Hamming** $d_{min}$

En un **código**, es la **distancia más pequeña** entre **cualquier par de palabras de código válidas**.

Esta es **clave** para saber cuántos errores puedo detectar o corregir:

- **Capacidad de detección**:
    $$\text{Puede detectar hasta } e \text{ errores si } d_{min} \ge e+1$$
    
- **Capacidad de corrección**:
    $$\text{Puede corregir hasta } t \text{ errores si } d_{min} \ge 2t+1$$
    
    donde $t = \lfloor \frac{d_{min} - 1}{2} \rfloor$

• Detección: d=k+1

• Corrección: d=2k+1



#### 📌 Ejemplo práctico:

Supongamos un código con:

$d_{min} = 3$

- Puede **detectar** hasta $e = 2$ errores
    
- Puede **corregir** hasta $t = 1$ error
    

Esto es precisamente lo que hace el **código de Hamming (7,4)**:

- Longitud: 7 bits (4 de datos, 3 de paridad)
    
- $d_{min} = 3$
    
- Detecta 2 errores, corrige 1.


## 📊 Resumen:

|Código|Redundancia|Detecta|Corrige|Ejemplo|
|---|---|---|---|---|
|Paridad simple|1 bit|1|0|UART|
|CRC|Varios bits|Muchos|0|Ethernet|
|Hamming (7,4)|3 bits|2|1|Memoria ECC|
|Reed–Solomon|Muchos bits|Muchos|Muchos|CDs, DVB|


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



**P1:** posiciones 1, 3, 5, 7, 9 → P1, 0, 1, 0, 0 → hay 1 uno → para que sea par, **P1 = 1**.

**P2:** posiciones 2, 3, 6, 7, 10 → P2, 0, 1, 0, 1 → hay 2 unos + P2 → para paridad par, **P2 = 0**.

**P4:** posiciones 4, 5, 6, 7 → P4, 1, 1, 0 → hay 2 unos → para paridad par, **P4 = 0**.

**P8:** posiciones 8, 9, 10 → P8, 0, 1 → hay 1 uno → para paridad par, **P8 = 1**.



### 4️⃣ Palabra final codificada

Sustituyendo los P calculados:

|Pos|1|2|3|4|5|6|7|8|9|10|
|---|---|---|---|---|---|---|---|---|---|---|
|Bit|1|0|0|0|1|1|0|1|0|1|

**Código Hamming (paridad par) = 1 0 0 0 1 1 0 1 0 1**



### 📌 Proceso general de decodificación (Hamming)

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


#### 🔹 Ejemplo rápido con tu palabra (paridad par)

Supongamos que codificamos 011001 y obtuvimos:

**1 0 0 0 1 1 0 1 0 1** (posiciones 1 a 10)

Ahora el receptor recibe:

**1 0 0 0 1 0 0 1 0 1** ← Se dañó el bit en la posición 6 (antes era 1, ahora es 0).


### 📌 Regla para ubicar los bits de paridad en Hamming

1. **Los bits de paridad se colocan en posiciones que son potencias de 2**  
    Es decir:
    
    $1,\ 2,\ 4,\ 8,\ 16,\ 32,\ \dots$
    
    (numerando las posiciones desde 1 empezando por la izquierda).
    
2. **Los demás lugares se llenan con bits de datos** del símbolo original, en orden.


#### 1️⃣ Verificación de paridades

- **P1** (pos 1, 3, 5, 7, 9): 1, 0, 1, 0, 0 → hay 2 unos → ✅ cumple paridad par (0 en el síndrome).
    
- **P2** (pos 2, 3, 6, 7, 10): 0, 0, 0, 0, 1 → hay 1 uno → ❌ no cumple (1 en el síndrome).
    
- **P4** (pos 4, 5, 6, 7): 0, 1, 0, 0 → hay 1 uno → ❌ no cumple (1 en el síndrome).
    
- **P8** (pos 8, 9, 10): 1, 0, 1 → hay 2 unos → ✅ cumple (0 en el síndrome).
    



#### 2️⃣ Formar el síndrome

El **síndrome** en el código Hamming es el resultado de **volver a calcular** esas paridades sobre la palabra recibida y comparar con los bits de paridad que vinieron en el mensaje.

- Síndrome = 0 → sin errores.
    
- Síndrome ≠ 0 → el número indica **posición del bit con error**.

**Importante que se debe ordenar de mayor a menos los bits de paridad**

P8 P4 P2 P1 = **0 1 1 0** (binario) = **6 en decimal**.



#### 3️⃣ Interpretar y corregir

El síndrome indica que el bit con error está en la **posición 6**.  
Corregimos: en vez de 0 debe ser 1.

Palabra corregida: **1 0 0 0 1 1 0 1 0 1**



#### 4️⃣ Recuperar los datos

Quitamos las posiciones de paridad (1, 2, 4, 8) → queda:  
0 1 1 0 0 1 ✅


📌 **Nota:**  
Si se usa **paridad impar**, el cálculo de cada paridad en el receptor es igual, pero la condición de “cumplir” cambia: debe haber un número **impar** de 1’s en cada grupo.



# Multiplexores 


### 📡 Multiplexación

La **multiplexación** es una técnica esencial en telecomunicaciones que permite **transmitir múltiples señales independientes** a través de un mismo medio físico (cable, fibra óptica, enlace de radio, etc.), **optimizando el uso del ancho de banda**.

En lugar de asignar un canal exclusivo para cada comunicación, la multiplexación organiza las señales para que compartan el medio, separándolas mediante diferentes criterios: **frecuencia**, **tiempo**, **longitud de onda** o **código**.

El proceso inverso, en el receptor, se denomina **demultiplexación**, y consiste en aislar la señal correspondiente a cada usuario.

> [!note] 
> Consiste en mandar más de una información (a través de canales de información) en un único medio.


### 🎯 Objetivos de la Multiplexación

- **Optimizar** el uso del canal disponible.
    
- **Reducir costos** al evitar la duplicación de infraestructura.
    
- **Permitir escalabilidad** en redes y sistemas de comunicación.


### Ancho de banda

- **En el dominio de la frecuencia:**  
    Es la **diferencia entre la frecuencia más alta y la más baja** que un canal puede transmitir correctamente.
    $$BW = f_{\text{máx}} - f_{\text{mín}}$$

- **En telecomunicaciones digitales:**  
    También puede referirse a la **tasa máxima de datos** (en bits por segundo) que puede transmitir un canal, según su ancho de banda en Hz y la relación señal/ruido (Ley de Shannon).


#### 🎯 Importancia

- **Más ancho de banda → más información por unidad de tiempo.**
    
- Determina la **calidad** y **velocidad** de la transmisión.
    
- Influye en el tipo de modulación y codificación que se puede utilizar.



#### 📍 Ejemplos

- Una línea telefónica tradicional: ancho de banda ≈ **4 kHz** → suficiente para voz humana.
    
- Wi-Fi 2.4 GHz: canales de **20 o 40 MHz**.
    
- Fibra óptica: anchos de banda de **decenas de GHz**, permitiendo velocidades de **varios Tbps**.




### Tipos de multiplexación

#### Multiplexación por División de Frecuencia (FDM)

- Cada canal se transmite en una banda de frecuencias diferente.
- Requiere filtros pasabajos y pasaaltos para separar las señales.     
- Muy utilizada en radio FM, TV analógica y sistemas telefónicos analógicos.

![[Pasted image 20250809135717.png]]

#### 🔍 Lo que pasa realmente en FDM

1. **Antes de multiplexar**
    
    - Tienes 12 canales de voz, cada uno ocupando **4 kHz de ancho de banda**.
        
    - Sin modulación, todos estarían “apilados” en el mismo rango (0–4 kHz) → se solaparían y sería imposible distinguirlos.
        
2. **Durante la multiplexación (FDM)**
    
    - A cada canal se le asigna una **portadora distinta** y se **modula** (por ejemplo, en AM o SSB).
        
    - Esto **traslada** la señal de cada canal a **distintas posiciones del espectro** (frecuencias centrales diferentes).
        
    - Ejemplo:
        
        - Canal 1 → centrado en 64 kHz
            
        - Canal 2 → centrado en 68 kHz
            
        - Canal 3 → centrado en 72 kHz
            
        - … así hasta cubrir de 60 a 108 kHz.
            
3. **Resultado final**
    
    - El grupo de 12 canales ocupa **48 kHz de ancho total**, pero **ya no están en el mismo rango de frecuencias**:
        
        - Cada canal sigue teniendo sus 4 kHz,
            
        - pero están “escalonados” en frecuencia para no pisarse.
            
4. **Demultiplexación en el receptor**
    
    - Se usan **filtros sintonizados** para aislar la banda de cada canal y llevarla de nuevo a su posición original (0–4 kHz) para que el oyente escuche la voz normal.

#### Banda de guarda 

En FDM, cada canal modulado está ubicado en un rango específico de frecuencias.  
Pero, para que no haya **interferencias** entre un canal y el siguiente, se deja un **pequeño espacio vacío** en el espectro entre ellos:

- A ese espacio se le llama **banda de guarda** (_guard band_).
    
- Funciona como una zona de “seguridad” para evitar que las señales “se mezclen” debido a imperfecciones en filtros o modulación

#### Canales de distinto ancho de banda

Si en un sistema FDM **los canales no tienen todos el mismo ancho**, pasa lo siguiente:

- Para simplificar el diseño y evitar interferencias, se les asigna **a todos el ancho del canal más grande** (más la banda de guarda).
    
- Esto significa que, aunque un canal requiera menos ancho, “desperdicia” espacio para poder alinearse con los demás.
    

📌 Ejemplo:

- Canal 1: 4 kHz
    
- Canal 2: 5 kHz
    
- Canal 3: 3 kHz  
    ➡ Todos se espacian como si midieran **5 kHz + banda de guarda**, para mantener la separación y alineación en el espectro.




### OFDM - Multiplexación por división de frecuencias ortogonal 

Se basa en la transformada directa de Fourier.

Trasforma el FDM. En vez de poner un ancho de banda con su frecuencia, la banda de guarda y el otro canal con su ancho de banda y frecuencia, puedo aplicarle a esas señales la transformada discreta de Fourier y calcular que la frecuencia de mayor energía dentro de mi canal calce justo en la posición en la que los vecinos no tienen señal.

![[Pasted image 20250809150859.png]]

>[!important] 
>Esto se usa para comunicaciones **DIGITALES** (la implementación es analógica pero los datos no)**.** FDM se usa para comunicaciones 100% analógicas.

Los módems usan esta técnica.



### Multiplexación por División de Longitud de Onda (WDM)

- Usada en fibra óptica. Cada señal se transmite con una longitud de onda distinta (color de luz distinto).

- Puede ser CWDM (coarse) o DWDM (dense) según la separación entre canales.

Es lo mismo que FDM pero cuando usás fibra óptica. Cuando estás en frecuencias tan altas como la velocidad de la luz, hacés referencia a la longitud de onda.

Multiplexás luz.

Cuando crean una fibra, el fabricante marca una zona llamada MARCA DE AGUA. Cualquier señal que vos pongas ahí, la fibra no la va a dejar pasar (atenuación total). Vos cuando comprás equipamiento lo hacés para mandar canales en determinadas zonas de transmisión de esa fibra óptica.

El equipamiento más barato está cerca de la marca de agua.



### Digitales 


### Multiplexación por División de Tiempo (TDM)

TDM se usa para datos y telefonía, para telefonía o solamente para datos.

Funciona ampliando la voz (convirtiéndola en digital) y metiéndolas en slot de tiempos.

Los estadounidenses tenían un sistema y los europeos otro. Para comunicarse, tenían que poner a un interlocutor en el medio.



### FHSS – Frequency Hoping Spread Spectrum

Sistema de multiplexación basado en tiempo.

Nos ponemos de acuerdo en ciertos saltos de frecuencia. Por ejemplo: en el tiempo 1, el mensaje se emite en la frecuencia f1, en el tiempo 2 en la frecuencia f6, y así. Se usa por motivos de seguridad. Consume mucho ancho de banda.

Si mando una sola comunicación estaría desperdiciando el sistema, por eso es que se envían varias comunicaciones a la vez.



### DSSS – Direct Secuence Spread Spectrum

Emisor y transmisor se ponen de acuerdo en un pseudo-ruido (señal analógica).

Cuando te quiero mandar un 1, mando ese ruido en fase. Cuando quiero mandar un 0 lo mando con fase cambiada.

Se puede mezclar con OFDM:

![[Pasted image 20250809151122.png]]

Lo usa el wifi (es half-duplex)



### Multiplexación por División de Tiempo Sincrónica (STDM)

Lo tienen los sistemas de celular.

La antena divide el tiempo entre la cantidad de usuarios. Mientras más usuarios, menos recibe cada uno, y viceversa, entre menos usuarios, más recibe cada uno.

La antena de teléfono censa cada vez que cambia de tiempo y se va adaptando en tiempo acorde a la cantidad de demanda que tenga.

El wifi no sabe hacer esto.











### a

### En frecuencia (FDM / OFDM / WDM / SCM)

**FDM (Frequency Division Multiplexing)**

- **Idea:** cada señal usa **una banda distinta** de frecuencias dentro del mismo medio; van **en paralelo**.
    
- **Señal típica:** **analógica bandapaso** (pero puede ser digital modulada).
    
- **Requiere:** **bandas de guarda** para que no se pisen.
    
- **Ejemplos:** radio AM/FM (cada emisora su canal), TV por cable analógica, enlaces microondas analógicos.
    

**OFDM (Orthogonal FDM)**

- **Idea:** muchas **subportadoras ortogonales** (espaciadas Δf = 1/Tu) que **se superponen sin interferir**.
    
- **Señal:** **digital** (QPSK/QAM por subportadora); usa **IFFT/FFT** y **prefijo cíclico**.
    
- **Ventajas:** robusto a multitrayecto; alta eficiencia.
    
- **Ejemplos:** Wi-Fi (802.11a/g/n/ac/ax), LTE/5G (downlink), DVB-T, ADSL/VDSL (DMT).
    

**OFDMA (multiusuario con OFDM)**

- **Idea:** las subportadoras (o grupos) se **reparten entre usuarios** simultáneamente.
    
- **Señal:** digital multiusuario.
    
- **Ejemplos:** LTE/5G (uplink/downlink), Wi-Fi 6/7 (RU).
    

**WDM (Wavelength Division Multiplexing)** – óptico

- **Idea:** cada canal es **una longitud de onda** distinta (colores) sobre **la misma fibra**.
    
- **Señal:** **óptica** continua modulada (digital o analógica).
    
- **Variantes:** **CWDM** (pocos canales separados en nm), **DWDM** (muchos, espaciados en GHz).
    
- **Ejemplos:** backbone de fibra 10/100/400G, DWDM C/L-band, PON con downstream/upstream en λ distintas.


***Tipos principales (por separación en frecuencia/longitud de onda)***

1. **CWDM (Coarse WDM, “gruesa”)**
    

- **Espaciado**: ~**20 nm** (p. ej. 1271, 1291, 1311… hasta ~1611 nm).
    
- **Canales**: hasta **18** máx. teórico (suele usarse 8–16).
    
- **Bandas**: O/E/S/C/L según el caso (mucho uso en metro/edificios).
    
- **Pros/Contras**: más **barato/simple**, **menos canales** y alcance menor que DWDM.
    

2. **DWDM (Dense WDM, “densa”)**
    

- **Espaciado**: **100/50/25/12.5 GHz** (en C/L-band, ITU-T G.694.1).
    
- **Canales**: **80–96+** típicos (o más con grids finos).
    
- **Uso**: **long-haul, core, backbone**, con amplificación **EDFA** y **ROADM**.
    
- **Pros/Contras**: **muchos canales** y alcance muy largo; mayor **complejidad/costo**.
    

> Regla rápida: **CWDM = barato/pocas λ**; **DWDM = muchos λ/alto rendimiento**.


**SCM (Subcarrier Multiplexing) / Radio-over-Fiber**

- **Idea:** varias **subportadoras RF** modulan la **intensidad óptica** simultáneamente.
    
- **Señal:** **RF analógica** transportada por fibra (o digital embebida).
    
- **Ejemplos:** CATV HFC analógico, distribución de RF celular por fibra (DAS).
    



### En tiempo (TDM / TDMA)

**TDM (Time Division Multiplexing)**

- **Idea:** las señales comparten el **mismo canal** pero en **turnos** (ranuras de tiempo).
    
- **Señal:** típicamente **digital**.
    
- **Variantes:**
    
    - **TDM síncrono:** cada canal tiene **su slot fijo** en cada trama, use o no datos.
        
    - **TDM estadístico (asíncrono):** asigna slots **según demanda** (mejor aprovechamiento).
        
- **Ejemplos:** **E1** (2048 kb/s): 32 timeslots de 64 kb/s (PCM), trama cada 125 μs; **T1** (1.544 Mb/s).
    

**TDMA (Time Division Multiple Access)**

- **Idea:** múltiples **usuarios** acceden en **tiempos** distintos (es TDM aplicado al acceso radio).
    
- **Señal:** digital; cada usuario tiene **su ráfaga**.
    
- **Ejemplos:** GSM, satélites TDMA, algunos sistemas PMR.
    

> **Clave de examen:** TDM multiplexa **flujos**; TDMA organiza el **acceso de usuarios** (conceptos hermanos, contextos distintos).



### En código (CDM / CDMA)

**CDM (Code Division Multiplexing) – CDMA**

- **Idea:** todos transmiten **a la vez y en la misma banda**, pero cada uno usa un **código de expansión** diferente (separación por **código**).
    
- **Señal:** **digital extendida en banda** (spread spectrum); detección por **correlación**.
    
- **Variantes:** **DSSS** (secuencia pseudoaleatoria), **FHSS** (salto en frecuencia).
    
- **Ejemplos:** 3G (IS-95/CDMA2000, WCDMA con Rake), **GPS** (C/A, P-code), 802.11b (DSSS).
    



### En espacio y polarización (SDM / MIMO / PDM)

**SDM (Space Division Multiplexing)**

- **Idea:** canales separados **espacialmente**.
    
- **Señal:** cualquiera; la separación es física.
    
- **Ejemplos:** varias **fibras** en paralelo; **multi-core fiber**; en radio, **sectores** o **celdas** distintas.
    

**MIMO (Multiple-Input Multiple-Output)** – radio

- **Idea:** varios **antenas** TX/RX explotan **multipath** para enviar **flujos simultáneos**.
    
- **Señal:** digital multicarrier (p.ej., OFDM) + **precodificación**/detección espacial.
    
- **Ejemplos:** Wi-Fi 4/5/6/7, LTE/5G.
    

**PDM (Polarization Division Multiplexing)** – óptico/coherente

- **Idea:** dos canales en **polarizaciones ortogonales** de la misma λ.
    
- **Señal:** óptica coherente (QPSK/QAM).
    
- **Ejemplos:** 100G/200G/400G coherente: **DP-QPSK**, **DP-16QAM**.
    



## Tabla “para memorizar”

|Técnica|Dimensión|Señal típica|Guardas/Claves|Ejemplos|
|---|---|---|---|---|
|**FDM**|Frecuencia|Analógica bandapaso|**Banda de guarda**|Radio AM/FM, microondas analógico|
|**OFDM**|Frecuencia (ortogonal)|Digital (QAM/QPSK)|Δf=1/Tu, **CP**|Wi-Fi, LTE/5G, DVB-T, xDSL|
|**WDM**|Long. de onda (óptica)|Óptica|Espaciado en nm/GHz|DWDM/CWDM, backbone fibra|
|**TDM**|Tiempo|Digital|Tramas/slots|E1/T1, multiplexores|
|**TDMA**|Tiempo (acceso)|Digital|Ráfagas por usuario|GSM, satélites|
|**CDMA**|Código|Digital spread|Códigos ortogonales/casi|3G, GPS, 802.11b|
|**SCM**|Subportadoras RF|Analógica RF|Linealidad|CATV HFC, RoF|
|**SDM/MIMO**|Espacio|Cualquiera|Antenas/multicore|Wi-Fi/LTE MIMO, multicore fiber|
|**PDM**|Polarización (óptica)|Óptica coherente|Rx coherente|DP-QPSK/DP-QAM|

### a




### Métodos de acceso

**Forma en la que varios usuarios o dispositivos comparten un mismo medio de transmisión** (cable, fibra, enlace de radio, etc.) **de manera ordenada**, evitando interferirse entre sí.

Es decir:

- Tenemos **un recurso limitado** (el canal de comunicación).
    
- Hay **muchos que quieren usarlo** al mismo tiempo.
    
- El método de acceso define **cómo se reparte ese recurso** entre todos para que la comunicación sea posible y eficiente.


## 🎯 Objetivos de un método de acceso

- **Evitar colisiones** (que dos usuarios transmitan a la vez en la misma porción del canal).
    
- **Optimizar el uso del ancho de banda** disponible.
    
- **Garantizar calidad de servicio** (QoS) según el tipo de tráfico: voz, datos, video, etc.
    
- **Permitir escalabilidad** (soportar más usuarios sin degradar excesivamente el servicio).


## 📍 Clasificación general

Los métodos de acceso más comunes se basan en **dividir el canal compartido** de distintas formas:

1. **En el tiempo** → TDMA (_Time Division Multiple Access_).
    
2. **En códigos** → CDMA (_Code Division Multiple Access_).
    
3. **En subportadoras ortogonales** → OFDMA (_Orthogonal Frequency Division Multiple Access_).


### 💡 Diferencia clave con **multiplexación**:

- **Multiplexación** → Combina señales para enviarlas por un canal. Puede ser entre señales de un mismo usuario o de varios, no importa si hay control de acceso o no.
    
- **Método de acceso** → Reglas y técnicas **para que varios usuarios accedan** a un mismo medio compartido de forma coordinada, evitando interferencias.


### Tipos de métodos de acceso

### ⏳ 1. TDMA – Time Division Multiple Access

**Qué es:**  
Método de acceso múltiple donde **varios usuarios comparten el mismo canal de frecuencia**, pero **en diferentes intervalos de tiempo**.

![[Pasted image 20250809151524.png]]

> [!example] 
> Un tiempo hablás vos, y un tiempo habla la persona que está al lado tuyo.

**Cómo funciona:**

- El tiempo se divide en **ranuras (time slots)**.
    
- A cada usuario se le asigna una o varias ranuras de tiempo de forma fija o dinámica.
    
- Cuando llega su turno, transmite; el resto del tiempo, espera.
    

**Ventajas:**

- Sencillo de implementar.
    
- No hay interferencia entre usuarios (si hay sincronización correcta).
    

**Desventajas:**

- Si un usuario no transmite, su tiempo se desperdicia (en la versión fija).
    
- Requiere sincronización muy precisa.
    

**Ejemplos:**

- GSM (2G).
    
- Telefonía digital TDM.




### 📶 2. OFDMA – Orthogonal Frequency Division Multiple Access

**Qué es:**  
Es la versión “multiusuario” del **OFDM**.  
Divide el canal en **muchas subportadoras ortogonales** y asigna **distintos grupos de subportadoras** a diferentes usuarios, simultáneamente.

> [!example] 
> En una frecuencia, mando multiplexación por tiempo.
> 
> Suele venir con TDMA. Mi equipo tiene una sola antena, y por eso, en una frecuencia, mando multiplexación por tiempo

**Cómo funciona:**

- El espectro se divide en decenas o cientos de subportadoras.
    
- Cada usuario recibe un conjunto exclusivo de subportadoras (y puede tener más de una si necesita más ancho).
    
- Los datos de todos viajan **al mismo tiempo y en frecuencias diferentes**, pero las subportadoras son ortogonales → no hay interferencia.
    

**Ventajas:**

- Alta eficiencia espectral.
    
- Flexibilidad para asignar recursos según la demanda.
    
- Robusto frente a multitrayecto y variaciones del canal.
    

**Desventajas:**

- Complejidad alta en la gestión y sincronización.
    

**Ejemplos:**

- LTE (4G).
    
- WiMAX.
    
- 5G NR (modo downlink).
    



### 🔑 3. CDMA – Code Division Multiple Access

**Qué es:**  
Método en el que **todos los usuarios transmiten al mismo tiempo y en el mismo ancho de banda**, pero cada uno con un **código único de expansión** que distingue sus datos.

> [!example] 
> Es como Direct Sequence, pero en vez de un pseudo-ruido ahora es un código que solo sabe la antena y el teléfono. El código está puesto adentro del chip.
> 
> En los servicios de roaming, las empresas se comparten la base de datos de códigos.


**Cómo funciona:**

- Cada bit de información se multiplica por un **código seudorrandom** de mayor frecuencia (spread spectrum).
    
- En el receptor, se usa el mismo código para “desexpandir” la señal y recuperar los datos.
    
- Los códigos están diseñados para ser ortogonales o tener baja correlación → permite separar señales superpuestas.
    

**Ventajas:**

- Muy robusto contra interferencias y escuchas.
    
- Permite más usuarios que FDMA/TDMA en el mismo ancho de banda.
    
- Resistente a multitrayecto.
    

**Desventajas:**

- Alta complejidad de implementación.
    
- Si hay demasiados usuarios, aumenta el ruido de fondo (“self-interference”).
    

**Ejemplos:**

- 3G (UMTS, CDMA2000).
    
- GPS (cada satélite tiene un código distinto).
    




📊 **Comparación rápida**

|Método|División principal|Simultaneidad|Ejemplo típico|
|---|---|---|---|
|**TDMA**|Tiempo|No (uno por turno)|GSM|
|**OFDMA**|Frecuencia (subportadoras ortogonales)|Sí|LTE, 5G|
|**CDMA**|Código|Sí|3G, GPS|
