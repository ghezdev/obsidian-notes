### Portadora analógica a Moduladora digital

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

- - -

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

- - -
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

- - -
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
