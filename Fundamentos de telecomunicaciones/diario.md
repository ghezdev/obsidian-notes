# Plan de Estudio - Examen Final Fundamentos de Telecomunicaciones
## 20 días de estudio + 5 días de simulacros

---

## DÍA 1: TEORÍA DE LA INFORMACIÓN - Fundamentos

### 1.1. Concepto de información y cantidad de información
- Definición de información como reducción de incertidumbre
- Fórmula: I(x) = -log₂ P(x)
- Unidad: bits
- Interpretación: eventos menos probables aportan más información

### 1.2. Fuente de memoria nula
- Definición: símbolos independientes entre sí
- Ejemplos prácticos
- Relación con entropía

### 1.3. Entropía de una fuente
- Fórmula: H(X) = -Σ P(xᵢ) · log₂ P(xᵢ)
- Entropía mínima (H = 0): un símbolo con probabilidad cercana a 1
- Entropía máxima: símbolos equiprobables, H = log₂(n)
- Interpretación: incertidumbre promedio

**Preguntas teóricas:**
1. ¿Qué significa que una fuente tenga entropía máxima?
2. ¿Cómo se ve afectada la entropía si los símbolos no son equiprobables?
3. ¿Cuál es la diferencia entre información de un símbolo y entropía de una fuente?
4. ¿Qué características tiene la entropía cuando todos los símbolos tienen igual probabilidad?

**Ejercicios prácticos:**
1. Calcular la entropía de una fuente con 4 símbolos equiprobables.
2. Dada una fuente con símbolos A, B, C con probabilidades 0.5, 0.3, 0.2 respectivamente, calcular la entropía.
3. Una fuente tiene 8 símbolos equiprobables. Calcular su entropía y explicar qué significa el resultado.

---

## DÍA 2: TEORÍA DE LA INFORMACIÓN - Tasa y Velocidad

### 2.1. Tasa de información
- Fórmula: T = H/t (bits/símbolo / seg/símbolo)
- Diferencia con velocidad de transmisión
- Mide bits útiles sin contar redundancias

### 2.2. Velocidad de transmisión
- Mide bits por segundo incluyendo redundancias
- Relación con tasa de información

### 2.3. Baudio
- Definición: símbolos por segundo
- Fórmula: B = Tₜ/k donde k = log₂(M)
- Diferencia con bps

### 2.4. Eficiencia y Redundancia
- Eficiencia: E = T/Tₜ o E = H/L
- Redundancia: R = 1 - E
- Redundancia en bits: L - H
- Redundancia por entropía: R = (H₀ - H)/H₀

**Preguntas teóricas:**
1. ¿Cuál es la diferencia entre tasa de información y velocidad de transmisión?
2. ¿Qué es un baudio y cómo se relaciona con los bits por segundo?
3. ¿Cómo se calcula la eficiencia de un código?
4. ¿Qué significa que un código tenga alta redundancia?

**Ejercicios prácticos:**
1. Calcular la cantidad de bits de información y redundancia si: tasa de información = 400 kbps, duración de cada bit = 2 μseg, cantidad total de bits = 40.
2. Si una fuente tiene entropía de 2.5 bits/símbolo y se codifica con longitud media de 3 bits/símbolo, calcular eficiencia y redundancia.
3. Se transmite a 9.6 Kbps con un módem de 2400 bauds. Calcular la cantidad de bits por símbolo y estados posibles.

---

## DÍA 3: CANAL DE COMUNICACIÓN Y TEOREMA DE SHANNON-HARTLEY

### 3.1. Concepto de canal de comunicación
- Definición y componentes del modelo de Shannon
- Tipos de canales (sin ruido, con ruido, binario simétrico, continuo)

### 3.2. Capacidad del canal
- Teorema de Shannon-Hartley: C = B · log₂(1 + S/N)
- Parámetros: ancho de banda (B) y relación señal/ruido (S/N)
- Límite teórico máximo

### 3.3. Relación señal/ruido (SNR)
- Definición: S/N = P_señal / P_ruido
- Conversión a dB: SNR_dB = 10 · log₁₀(S/N)
- Conversión de dB a lineal: S/N = 10^(SNR_dB/10)

### 3.4. Factores modificables y no modificables
- Modificables: ancho de banda, relación señal/ruido
- No modificables: ruido térmico natural, límites regulatorios

**Preguntas teóricas:**
1. Según el teorema de Shannon-Hartley, ¿qué parámetros puede modificar para aumentar la capacidad de un canal?
2. ¿Qué significa que la capacidad del canal sea un límite teórico?
3. ¿Cómo se relaciona la relación señal/ruido con la capacidad del canal?
4. ¿Por qué no se puede eliminar completamente el ruido térmico?

**Ejercicios prácticos:**
1. Calcular la capacidad de un canal con ancho de banda de 2 MHz y relación señal/ruido de 30 dB.
2. Si un canal tiene capacidad de 2.4 Mbps y relación señal/ruido de 36 dB, calcular su ancho de banda.
3. Calcular la capacidad de un canal telefónico (3.1 kHz) con relación señal/ruido de 50 dB.

---

## DÍA 4: DECIBELES Y CONVERSIONES DE POTENCIA

### 4.1. Concepto de decibel
- Definición: dB = 10 · log₁₀(P₁/P₀)
- Unidad logarítmica para comparar potencias
- Ventajas del uso de dB

### 4.2. Unidades derivadas
- dBm: referencia a 1 mW (P_dBm = 10·log₁₀(P_mW))
- dBW: referencia a 1 W
- Conversiones entre unidades

### 4.3. Operaciones con decibeles
- Suma y resta de dB (multiplicación y división en lineal)
- Regla: dBm ± dB = dBm

### 4.4. Atenuación y ganancia
- Atenuación: pérdida de potencia (valores negativos o positivos según convención)
- Ganancia: aumento de potencia
- Cálculo de potencia de salida

**Preguntas teóricas:**
1. ¿Por qué se usan decibeles en lugar de valores lineales?
2. ¿Cuál es la diferencia entre dB, dBm y dBW?
3. ¿Cómo se calcula la potencia de salida si conozco la potencia de entrada y la atenuación?
4. ¿Qué significa una atenuación de -3 dB?

**Ejercicios prácticos:**
1. Convertir 100 mW a dBm y a dBW.
2. Calcular la potencia de salida de una línea de transmisión de 1000 metros donde la atenuación del cable coaxial es de 5 dB/100 metros y la potencia del transmisor es de 10 W.
3. Dado un canal con atenuación de 0.8 dB/100 metros, longitud de 1200 metros, potencia de entrada de 160 mW y sensibilidad del receptor de -10 dBm, calcular la potencia mínima del transmisor y expresarla en mW.

---

## DÍA 5: SEÑALES - Conceptos Fundamentales

### 5.1. Definición y clasificación de señales
- Señal analógica vs digital
- Señal binaria vs multinivel
- Señal periódica vs no periódica
- Señal determinística vs aleatoria

### 5.2. Parámetros característicos de señales
- Amplitud (A)
- Frecuencia (f) y período (T = 1/f)
- Fase (φ)
- Relación entre parámetros

### 5.3. Señal senoidal
- Ecuación: s(t) = A · sin(2πft + φ)
- Análisis en dominio del tiempo
- Espectro espectral (una sola frecuencia)

### 5.4. Velocidad de propagación y longitud de onda
- Velocidad: v = c = 3×10⁸ m/s (en vacío)
- Longitud de onda: λ = v/f
- Relación: v = λ · f

**Preguntas teóricas:**
1. ¿Cuáles son los elementos que caracterizan a las señales?
2. ¿Qué diferencia hay entre una señal analógica y una digital?
3. ¿De los 3 parámetros característicos de la señal, cuáles pueden observarse en el dominio de la frecuencia y cuáles en el dominio del tiempo?
4. ¿Cómo se relacionan la frecuencia, la longitud de onda y la velocidad de propagación?

**Ejercicios prácticos:**
1. Dada una señal de 150 MHz, calcular la longitud de onda y la distancia recorrida en 5 períodos.
2. Determinar la frecuencia central de la banda MF y calcular la longitud de onda correspondiente.
3. Si una señal tiene frecuencia de 100 MHz, calcular su período y longitud de onda en el vacío.

---

## DÍA 6: SEÑALES - Análisis Espectral y Señal Cuadrada

### 6.1. Análisis espectral
- Teorema de Fourier
- Dominio del tiempo vs dominio de la frecuencia
- Descomposición en armónicos

### 6.2. Ancho de banda
- Definición: B = f_max - f_min
- Ancho de banda absoluto vs relativo
- Relación con capacidad de transmisión

### 6.3. Señal cuadrada
- Características: transiciones abruptas
- Descomposición en serie de Fourier
- Armónicos impares: f₀, 3f₀, 5f₀, ...
- Ancho de banda teóricamente infinito

### 6.4. Efectos del ancho de banda limitado
- Distorsión de señales cuadradas
- Filtrado de armónicos
- Relación con el teorema de Nyquist

**Preguntas teóricas:**
1. ¿Por qué una señal cuadrada tiene ancho de banda teóricamente infinito?
2. ¿Cómo se modifican las amplitudes de los armónicos en una señal cuadrada?
3. ¿Qué sucede si el primer armónico de una señal digital se ubica en 200 kHz? ¿En qué frecuencias se ubican los próximos dos armónicos?
4. ¿Cómo afecta a una señal ser transmitida por un medio a medida que su ancho de banda disminuye?

**Ejercicios prácticos:**
1. Si una señal cuadrada tiene frecuencia fundamental de 1 MHz, indicar las frecuencias de los primeros 5 armónicos y cómo se modifican sus amplitudes.
2. Calcular el ancho de banda mínimo necesario para transmitir una señal cuadrada de 500 kHz con distorsión aceptable (considerando hasta el 5º armónico).
3. Dada una señal digital con primer armónico en 200 kHz, calcular las frecuencias de los próximos dos armónicos.

---

## DÍA 7: PROBLEMAS DE LAS SEÑALES

### 7.1. Atenuación
- Definición: pérdida de potencia con la distancia
- Dependencia del medio y frecuencia
- Medición en dB/km

### 7.2. Ruido
- Ruido térmico (Johnson-Nyquist): N = k·T·B
- Ruido de intermodulación
- Crosstalk (diafonía)
- Ruido por impulsos

### 7.3. Distorsión por retardo
- Retardo de grupo
- Diferentes frecuencias viajan a diferentes velocidades
- Efectos en señales complejas

### 7.4. Factores evitables y no evitables
- Evitables: crosstalk (mejorando apantallamiento), interferencia (filtros)
- No evitables: ruido térmico, atenuación (inherente al medio)

**Preguntas teóricas:**
1. ¿Cuáles son los factores que afectan a las señales y no pueden ser evitados?
2. ¿Qué es el ruido por impulso y cómo se diferencia del ruido térmico?
3. Si se transmite una señal a través de un par de cables de cobre ya instalado, ¿qué factores pueden ser evitados y cómo?
4. ¿Qué es la distorsión por retardo y cómo afecta a las señales?

**Ejercicios prácticos:**
1. Calcular la potencia recibida si la potencia transmitida es de 20 dBm, la atenuación es de 2 dB/km y la distancia es de 5 km.
2. Determinar el ruido máximo (en mW) que puede afectar a un sistema con: Pin = 160 mW, atenuación = 0.4 dB/100m, longitud = 3 km, sensibilidad = -10 dBm.
3. Si un cable tiene atenuación de 1.5 dB/km a 1 MHz, calcular la potencia de salida para una entrada de 10 mW después de 2 km.

---

## DÍA 8: ANCHO DE BANDA DE NYQUIST

### 8.1. Teorema de Nyquist (sin ruido)
- Fórmula: C = 2·B·log₂(L)
- Donde L es el número de niveles
- Capacidad máxima sin ruido

### 8.2. Muestreo de señales analógicas
- Frecuencia de Nyquist: f_s ≥ 2·f_max
- Teorema del muestreo
- Aliasing si no se cumple

### 8.3. Señal PAM (Pulse Amplitude Modulation)
- Resultado del muestreo
- Señal discreta en tiempo, continua en amplitud

### 8.4. Relación con modulación digital
- Niveles de modulación
- Bits por símbolo: k = log₂(M)

**Preguntas teóricas:**
1. ¿Cuál es el ancho de banda según la fórmula de Nyquist (sin ruido)?
2. ¿Qué sucede si muestreamos una señal a una frecuencia menor que el doble de su frecuencia máxima?
3. ¿Cómo se relaciona el teorema de Nyquist con el proceso de digitalización?
4. Explique brevemente cómo se realiza el proceso de muestreo de una señal analógica que da como resultado una señal PAM.

**Ejercicios prácticos:**
1. Calcular la capacidad máxima de un canal sin ruido con ancho de banda de 4 kHz y 8 niveles de modulación.
2. ¿Cuál es la frecuencia de muestreo mínima para una señal analógica con frecuencia máxima de 3.4 kHz?
3. Si un sistema usa 16 niveles de modulación y tiene ancho de banda de 1 MHz, calcular la capacidad máxima según Nyquist.

---

## DÍA 9: MODULACIÓN - Conceptos y Clasificación

### 9.1. Definición de modulación
- Técnica para adaptar señales para transmisión
- Componentes: moduladora, portadora, modulada
- Proceso de demodulación

### 9.2. Objetivos de la modulación
- Transmitir a largas distancias
- Adaptar la señal al canal
- Multiplexar varias señales
- Reducir tamaño de antenas
- Permitir detección eficiente

### 9.3. Clasificación de modulaciones
- Portadora analógica + Moduladora analógica: AM, FM, PM
- Portadora analógica + Moduladora digital: ASK, FSK, PSK, QAM
- Portadora digital + Moduladora analógica: PAM, PDM, PPM, PCM, Delta
- Portadora digital + Moduladora digital: Codificación de línea

### 9.4. Estados posibles y constelación
- Definición: combinaciones únicas de fase/frecuencia/amplitud
- Cálculo: M = 2^k donde k = bits por símbolo
- Diagrama de constelación

**Preguntas teóricas:**
1. ¿Cuáles son los objetivos de la modulación?
2. ¿Cómo se clasifican las modulaciones según el tipo de portadora y moduladora?
3. ¿Qué es una constelación en modulación?
4. ¿Qué son los estados posibles y cómo se calculan?

**Ejercicios prácticos:**
1. Se transmite a 7.200 bps con un módem PSK de 2.400 baudios. Calcular la cantidad de estados y graficar la constelación.
2. Se transmite a 12 Mbps con un módem QAM de 3 Mbaudios con 2 amplitudes diferentes. Calcular estados y graficar la constelación.
3. Si un módem transmite a 28.8 kbps con 9.6 kbaudios, calcular bits por símbolo y estados posibles.

---

## DÍA 10: MODULACIÓN - Portadora Analógica

### 10.1. AM (Amplitud Modulada)
- Modifica la amplitud de la portadora
- Frecuencia y fase constantes
- Uso: radio AM, transmisión analógica

### 10.2. FM (Frecuencia Modulada)
- Modifica la frecuencia de la portadora
- Amplitud constante
- Uso: radio FM, audio de alta calidad

### 10.3. PM (Fase Modulada)
- Modifica la fase de la portadora
- Relacionada con FM
- Uso: modulaciones digitales (PSK)

### 10.4. ASK, FSK, PSK (Modulaciones digitales con portadora analógica)
- ASK: modulación en amplitud para datos digitales
- FSK: modulación en frecuencia para datos digitales
- PSK: modulación en fase para datos digitales
- Características y usos de cada una

**Preguntas teóricas:**
1. ¿Cuáles son las características principales de las modulaciones con portadora analógica?
2. ¿En qué se diferencia AM de FM?
3. ¿Cuáles de las siguientes afirmaciones identifican a la modulación FSK?
4. ¿Qué es QAM y cómo se diferencia de PSK?

**Ejercicios prácticos:**
1. Se transmite a 9.6 Kbps con un módem de 2400 bauds. Calcular la cantidad de estados posibles y graficar la constelación para un módem QAM con 2 amplitudes.
2. Se desean transmitir 4 bits a través de un módem de 9600 bauds modulando en PSK. Determinar la tasa en bits por segundo y la cantidad de estados.
3. Explicar mediante gráficos cómo QAM aumenta la velocidad de transmisión al aumentar los bits por baudio.

---

## DÍA 11: MODULACIÓN - Portadora Digital

### 11.1. PAM (Pulse Amplitude Modulation)
- Modulación de amplitud de pulsos
- Resultado del muestreo
- Múltiples niveles de amplitud

### 11.2. PCM (Pulse Code Modulation)
- Proceso completo: muestreo, cuantización, codificación
- Conversión analógica-digital estándar
- Uso: telefonía digital, audio digital

### 11.3. PDM y PPM
- PDM: modulación de duración de pulsos
- PPM: modulación de posición de pulsos
- Aplicaciones específicas

### 11.4. Delta Modulation
- Modulación diferencial
- Ventajas y desventajas
- Comparación con PCM

**Preguntas teóricas:**
1. ¿Cuáles son las características principales de las modulaciones con portadora digital?
2. ¿En qué consiste el proceso de digitalización de una señal analógica?
3. ¿Qué diferencia hay entre PAM y PCM?
4. Indique si es correcto: "La señal discreta obtenida luego del muestreo es del tipo PAM."

**Ejercicios prácticos:**
1. Explicar el proceso completo de conversión de una señal analógica a digital usando PCM.
2. Comparar las ventajas y desventajas de PCM vs Delta Modulation.
3. Si se muestrea una señal de voz (0-4 kHz) a 8 kHz y se cuantiza a 8 bits, calcular la tasa de bits resultante.

---

## DÍA 12: CODIFICACIÓN DE LÍNEA

### 12.1. Concepto de codificación de línea
- Representación de bits digitales como señales eléctricas
- Objetivos: sincronización, control de DC, detección de errores

### 12.2. NRZ (Non Return to Zero)
- Características: sin retorno a cero
- Ventajas y desventajas
- Problemas de sincronización

### 12.3. RZ (Return to Zero)
- Características: retorno a cero en cada bit
- Mejor sincronización que NRZ
- Mayor ancho de banda

### 12.4. Manchester y Differential Manchester
- Manchester: transición en medio de cada bit
- Differential Manchester: transición al inicio si bit = 0
- Auto-sincronización
- Uso en Ethernet

### 12.5. AMI (Alternate Mark Inversion)
- Alternancia de polaridad para '1'
- Control de componente DC
- Uso en telefonía

**Preguntas teóricas:**
1. ¿Qué es la codificación en línea y cuál es su objetivo principal?
2. ¿Cuál es la diferencia entre NRZ y Manchester?
3. ¿Por qué Manchester es mejor para sincronización que NRZ?
4. ¿Qué ventajas tiene AMI sobre otras codificaciones?

**Ejercicios prácticos:**
1. Codificar la secuencia 1011010 usando: a) NRZ, b) Manchester, c) AMI.
2. Comparar el ancho de banda necesario para transmitir 1 Mbps usando NRZ vs Manchester.
3. Explicar por qué Differential Manchester es más robusto ante inversión de polaridad del cable.

---

## DÍA 13: CÓDIGOS - Sin Detección de Errores

### 13.1. Concepto de código
- Definición: conjunto de reglas para representar símbolos
- Propiedades deseables: no ambiguo, único, eficiente, fácil de decodificar

### 13.2. Código en bloque
- Todos los símbolos con misma longitud
- Ventajas: fácil sincronización
- Desventajas: puede ser ineficiente

### 13.3. Códigos básicos
- Binario natural
- BCD (Binary Coded Decimal)
- Código Gray
- ASCII

### 13.4. Tipos de códigos según propiedades
- No singular vs singular
- Unívocamente decodificable
- Código instantáneo (prefijo)
- Código compacto

**Preguntas teóricas:**
1. ¿Qué propiedades debe tener un código para ser útil?
2. ¿Cuál es la diferencia entre código en bloque y código no en bloque?
3. ¿Qué es un código instantáneo?
4. ¿Qué significa que un código sea unívocamente decodificable?

**Ejercicios prácticos:**
1. Determinar si el siguiente código es instantáneo: A=0, B=01, C=011, D=111.
2. Si se desea codificar 4 símbolos en bloque, ¿cuántos bits se necesitan como mínimo?
3. Dada una fuente con 32 símbolos equiprobables, calcular la longitud mínima de un código en bloque.

---

## DÍA 14: CÓDIGO DE HUFFMAN

### 14.1. Algoritmo de Huffman
- Objetivo: codificación óptima (código compacto)
- Características: código instantáneo, unívocamente decodificable
- Asignación según probabilidades

### 14.2. Procedimiento paso a paso
1. Listar símbolos y probabilidades
2. Ordenar de menor a mayor probabilidad
3. Combinar los dos menos probables
4. Repetir hasta formar árbol completo
5. Asignar bits (0 izquierda, 1 derecha)
6. Leer códigos desde raíz

### 14.3. Cálculo de longitud media
- Fórmula: L = Σ pᵢ · lᵢ
- Relación con entropía: H ≤ L < H+1
- Eficiencia: E = H/L

### 14.4. Ventajas y aplicaciones
- Compresión de datos
- Codificación de imágenes y audio
- Transmisiones digitales

**Preguntas teóricas:**
1. ¿Cómo funciona el algoritmo de Huffman?
2. ¿Por qué Huffman es un código compacto?
3. ¿Cuál es la relación entre la entropía y la longitud media en Huffman?
4. Indique cuál es correcta: "El algoritmo de Huffman permite obtener un código con alta eficiencia."

**Ejercicios prácticos:**
1. Construir un código de Huffman para una fuente con símbolos A(0.4), B(0.3), C(0.2), D(0.1). Calcular longitud media, entropía, eficiencia y redundancia.
2. Calcular la eficiencia y redundancia de una fuente con probabilidades: A(x), B(0.20), C(0.04), D(0.07), E(0.08), F(0.08), G(x), H(0.13), si se codifica con Huffman.
3. Una fuente sin memoria tiene 4 símbolos con P(a)=0.45, P(b)=0.25, P(c)=P(d). Construir código Huffman y comprobar la relación entre entropía y longitud media.

---

## DÍA 15: CÓDIGOS DE DETECCIÓN DE ERRORES

### 15.1. Concepto y necesidad
- Errores en transmisión: ruido, distorsión, interferencia
- Redundancia controlada para detectar errores
- Diferencia entre detección y corrección

### 15.2. Bit de paridad
- Paridad par e impar
- Detección de un error
- Limitaciones

### 15.3. VRC y LRC
- VRC: Vertical Redundancy Check (paridad horizontal)
- LRC: Longitudinal Redundancy Check (paridad vertical)
- Uso combinado

### 15.4. CRC (Cyclic Redundancy Check)
- Método de división polinomial
- Muy confiable: detecta 100% de errores ≤ longitud del polinomio
- Uso: Ethernet, USB, protocolos de red
- Procedimiento: división módulo 2

**Preguntas teóricas:**
1. ¿Por qué tiene sentido aplicar un código de detección de errores en un protocolo orientado al bit?
2. ¿Cuál es la diferencia entre VRC, LRC y CRC?
3. ¿Por qué CRC es mejor que paridad simple?
4. ¿Qué errores puede detectar un CRC de grado n?

**Ejercicios prácticos:**
1. Verificar si el código 1101011011110 es correcto, sabiendo que fue generado por el polinomio x⁴ + x + 1.
2. Agregar el CRC al símbolo 110111010100, sabiendo que el polinomio generador es P(x) = x⁴ + x³ + 1.
3. Un equipo receptor recibe 1011001101100 codificado con CRC cuyo polinomio es x³ + x² + 1. Determinar si es correcto o contiene errores.

---

## DÍA 16: CÓDIGO DE HAMMING

### 16.1. Concepto de Hamming
- Código de corrección de errores
- Detecta 2 errores, corrige 1 error
- Distancia mínima: d_min = 3

### 16.2. Distancia de Hamming
- Definición: número de bits en que difieren dos palabras
- Distancia mínima del código
- Relación con capacidad de detección/corrección

### 16.3. Codificación con Hamming
- Determinar bits de paridad: 2^p ≥ m + p + 1
- Posiciones de paridad: potencias de 2 (1, 2, 4, 8, ...)
- Cálculo de cada bit de paridad según grupos
- Paridad par vs impar

### 16.4. Decodificación con Hamming
- Verificar paridades en recepción
- Formar síndrome (orden: P8 P4 P2 P1)
- Síndrome = 0 → sin errores
- Síndrome ≠ 0 → posición del error
- Corregir y extraer datos

**Preguntas teóricas:**
1. ¿Cuáles de las siguientes afirmaciones identifican al método de Hamming?
2. ¿Qué es la distancia de Hamming y cómo se relaciona con la capacidad de corrección?
3. ¿Por qué los bits de paridad se colocan en posiciones que son potencias de 2?
4. ¿Cómo funciona el proceso de decodificación en Hamming?

**Ejercicios prácticos:**
1. Codificar, con paridad par, el símbolo 0110011 aplicando Hamming.
2. Decodificar, con paridad impar, el símbolo 1110010010 determinando si hubo errores.
3. Obtener el código Hamming a emitir para el mensaje "111110" (con paridad par).

---

## DÍA 17: TRANSMISIÓN DE CÓDIGOS

### 17.1. Transmisión en paralelo vs serie
- Paralelo: varios bits simultáneos por conductores diferentes
- Serie: bits uno tras otro por un solo canal
- Ventajas y desventajas de cada una

### 17.2. Transmisión asíncrona
- Sin reloj común continuo
- Bits de inicio y parada por carácter
- Uso: RS-232, terminales "dumb"
- Sobrecarga de bits

### 17.3. Transmisión síncrona
- Reloj común o recuperado de la señal
- Transmisión continua sin bits de inicio/parada
- Mayor eficiencia
- Uso: Ethernet, USB, terminales "smart"

### 17.4. Comparación y aplicaciones
- Cuándo usar cada método
- Eficiencia comparativa
- Sincronización en cada caso

**Preguntas teóricas:**
1. Explique en qué consiste la transmisión sincrónica. ¿Qué ventajas presenta respecto de la transmisión asincrónica?
2. ¿Cuál es la diferencia entre transmisión en paralelo y en serie?
3. ¿Por qué la transmisión síncrona es más eficiente que la asíncrona?
4. ¿En qué casos se usa transmisión asíncrona?

**Ejercicios prácticos:**
1. Calcular la eficiencia de transmisión asíncrona si cada carácter tiene 8 bits de datos, 1 bit de inicio y 2 bits de parada.
2. Comparar el tiempo de transmisión de 1000 bytes usando transmisión serie a 9600 bps vs paralela de 8 bits a 1200 bps por línea.
3. Si se transmite en forma síncrona un bloque de 1024 bytes con overhead de 16 bytes, calcular la eficiencia.

---

## DÍA 18: MULTIPLEXACIÓN

### 18.1. Concepto de multiplexación
- Combinar múltiples señales en un solo canal
- Multiplexor y demultiplexor
- Objetivos: aprovechar ancho de banda, reducir costos

### 18.2. FDM (Frequency Division Multiplexing)
- División por frecuencias
- Cada canal en banda diferente
- Banda de guarda entre canales
- Uso: radio AM/FM, TV analógica

### 18.3. TDM (Time Division Multiplexing)
- División por tiempo
- Slots de tiempo para cada canal
- TDM síncrono vs estadístico
- Uso: E1, T1, telefonía digital

### 18.4. WDM (Wavelength Division Multiplexing)
- División por longitud de onda (fibra óptica)
- CWDM vs DWDM
- Uso: backbone de fibra óptica

### 18.5. OFDM (Orthogonal Frequency Division Multiplexing)
- Subportadoras ortogonales
- Uso en comunicaciones digitales
- Ventajas: eficiencia espectral, robustez

**Preguntas teóricas:**
1. ¿Cuál es la diferencia entre FDM y TDM?
2. ¿Qué es la banda de guarda en FDM y por qué es necesaria?
3. ¿En qué se diferencia OFDM de FDM?
4. ¿Cuándo se usa WDM en lugar de FDM?

**Ejercicios prácticos:**
1. Si se multiplexan 12 canales de voz de 4 kHz cada uno usando FDM con banda de guarda de 1 kHz, calcular el ancho de banda total necesario.
2. En un sistema TDM, si cada canal tiene 64 kbps y hay 32 canales, calcular la tasa total de transmisión.
3. Explicar cómo funciona OFDM y por qué es más eficiente que FDM tradicional.

---

## DÍA 19: MÉTODOS DE ACCESO

### 19.1. Concepto de método de acceso
- Forma de compartir un medio entre múltiples usuarios
- Diferencia con multiplexación
- Objetivos: evitar colisiones, optimizar ancho de banda

### 19.2. TDMA (Time Division Multiple Access)
- División por tiempo entre usuarios
- Ranuras de tiempo asignadas
- Ventajas y desventajas
- Ejemplos: GSM, telefonía digital

### 19.3. CDMA (Code Division Multiple Access)
- División por códigos
- Todos transmiten simultáneamente
- Códigos ortogonales
- Ejemplos: 3G, GPS

### 19.4. OFDMA (Orthogonal Frequency Division Multiple Access)
- División por subportadoras ortogonales
- Asignación dinámica de recursos
- Ejemplos: LTE, 5G, WiMAX

### 19.5. Comparación de métodos
- Ventajas y desventajas de cada uno
- Aplicaciones típicas
- Eficiencia espectral

**Preguntas teóricas:**
1. ¿Cuál es la diferencia entre multiplexación y método de acceso?
2. ¿Cómo funciona TDMA y qué ventajas tiene?
3. ¿En qué se diferencia CDMA de TDMA?
4. ¿Por qué OFDMA es usado en LTE y 5G?

**Ejercicios prácticos:**
1. Comparar la capacidad de un sistema TDMA vs CDMA con el mismo ancho de banda y número de usuarios.
2. Explicar cómo OFDMA permite asignar recursos dinámicamente según la demanda.
3. Si un sistema CDMA tiene 10 usuarios activos, ¿cómo afecta esto al rendimiento?

---

## DÍA 20: MEDIOS DE TRANSMISIÓN

### 20.1. Medios guiados
- Par trenzado: características, categorías, usos
- Cable coaxial: estructura, ventajas, aplicaciones
- Fibra óptica: monomodo vs multimodo, ventajas

### 20.2. Medios no guiados
- Antenas y propagación
- Espectro radioeléctrico
- Tipos de propagación: terrestre, espacial, directa
- Horizonte radioeléctrico

### 20.3. Características de medios
- Atenuación
- Ancho de banda
- Interferencia electromagnética
- Costo y seguridad

### 20.4. Cálculos de antenas
- Longitud de antena: λ/2, λ/4
- PIRE (Potencia Isotrópica Radiada Equivalente)
- Fórmula: PIRE = Pt - Lc + Ga

**Preguntas teóricas:**
1. Describa las características principales de un medio guiado vs no guiado.
2. ¿Cuál es la diferencia entre fibra monomodo y multimodo?
3. ¿Qué medio utilizaría para interconectar dos edificios de un campus universitario en la misma manzana?
4. ¿Cuáles son los tipos de propagación según la frecuencia?

**Ejercicios prácticos:**
1. Calcular los posibles dipolos para una antena que debe transmitir una señal de 150 MHz.
2. Calcular PIRE si: Pt = 20 dBm, pérdidas del cable = 3 dB, ganancia de antena = 15 dBi.
3. Determinar el tiempo que tarda un bit en ir y venir desde Buenos Aires hasta un datacenter en Bahía Blanca usando un satélite MEO a 22500 km.

---

## DÍA 21: SATÉLITES

### 21.1. Tipos de satélites según órbita
- LEO (Low Earth Orbit): baja latencia, menor cobertura
- MEO (Medium Earth Orbit): latencia media, mayor cobertura
- GEO (Geosynchronous/Geostationary): latencia ~250 ms, cobertura global con 3 satélites

### 21.2. Satélites geosincrónicos y geoestacionarios
- Geosincrónico: mismo período que rotación terrestre
- Geoestacionario: además está sobre el ecuador en órbita circular
- Características y aplicaciones

### 21.3. Constelaciones de satélites
- Necesidad de múltiples satélites para cobertura continua
- Handover entre satélites
- Ejemplos: Starlink, Iridium

### 21.4. Cálculos de latencia
- Distancia = 2 × altura de órbita (ida y vuelta)
- Tiempo = distancia / velocidad de la luz
- Aplicaciones según latencia requerida

**Preguntas teóricas:**
1. Describa las características principales de un satélite LEO y qué servicios pueden brindarse.
2. ¿Cuántos satélites GEO se necesitan para cubrir todo el planeta?
3. ¿Cuál es la diferencia entre satélite geosincrónico y geoestacionario?
4. ¿Por qué se necesitan constelaciones de satélites LEO?

**Ejercicios prácticos:**
1. Determinar el tiempo que tarda un bit en ir y venir usando un satélite MEO ubicado a 22500 km.
2. Si se utiliza un satélite GEO para acceder a un datacenter ubicado en San Francisco (15.000 km), calcular la demora para 10 consultas y respuestas.
3. Comparar la latencia de un satélite LEO (altura 500 km) vs GEO (altura 35786 km) para una comunicación.

---

## DÍA 22: MODELO OSI

### 22.1. Arquitectura del modelo OSI
- 7 capas: Física, Enlace, Red, Transporte, Sesión, Presentación, Aplicación
- Propósito: estandarizar comunicaciones de red
- Encapsulamiento y desencapsulamiento

### 22.2. Capa 1 - Física
- Transmisión de bits a través del medio
- Especificaciones eléctricas, mecánicas
- PDU: bit

### 22.3. Capa 2 - Enlace de Datos
- Direccionamiento físico (MAC)
- Control de acceso al medio
- Detección de errores
- PDU: trama (frame)
- Dispositivos: switches

### 22.4. Capa 3 - Red
- Enrutamiento y direccionamiento lógico (IP)
- Fragmentación de paquetes
- PDU: paquete (packet)
- Dispositivos: routers

### 22.5. Capas superiores (4-7)
- Transporte: control de flujo, corrección de errores end-to-end
- Sesión: gestión de sesiones
- Presentación: traducción, compresión, encriptación
- Aplicación: servicios de red a aplicaciones

### 22.6. Encapsulamiento
- Proceso de agregar headers en cada capa
- Introduce redundancia
- PDU diferente en cada capa

**Preguntas teóricas:**
1. Explique las funciones de las capas 2 y 3 del modelo OSI y dé ejemplos de protocolos.
2. ¿Por qué el encapsulamiento introduce redundancia en los paquetes del modelo OSI?
3. ¿En qué capa actúan los switches y en cuál los routers?
4. ¿Cuál es la PDU en cada capa del modelo OSI?

**Ejercicios prácticos:**
1. Explicar el proceso de encapsulamiento desde la capa de aplicación hasta la capa física para enviar un mensaje HTTP.
2. Identificar en qué capa del modelo OSI actúa cada uno de los siguientes dispositivos: switch, router, hub, firewall L3.
3. Calcular el overhead total si un paquete de 1000 bytes pasa por las 7 capas del modelo OSI, asumiendo headers de 20 bytes por capa.

---

## DÍA 23: ESTÁNDARES Y PROPAGACIÓN

### 23.1. Estándares de iure vs de facto
- De iure: aprobados formalmente por organismos internacionales
- De facto: ampliamente utilizados pero sin aprobación formal
- Ventajas y desventajas de cada uno

### 23.2. Propagación de ondas electromagnéticas
- Onda terrestre: frecuencias medias y bajas, sigue curvatura de la Tierra
- Onda espacial: frecuencias altas, rebote en ionosfera
- Onda directa: frecuencias muy altas, línea recta

### 23.3. Propagación ionosférica
- Cómo funciona el rebote en la ionosfera
- Efectos del día y la noche
- Frecuencias que pueden usar este tipo de propagación

### 23.4. Horizonte radioeléctrico
- Fórmula: D = 4.14 × √H (km)
- Zona de Fresnel
- Importancia para enlaces de microondas

**Preguntas teóricas:**
1. Indique si la Tecnología Y corresponde a un estándar de facto o de iure. Justifique.
2. Explique cómo funciona la propagación ionosférica.
3. ¿Cuáles son las ventajas y desventajas de usar un estándar de facto?
4. ¿A qué se le llama horizonte radioeléctrico y cómo se calcula?

**Ejercicios prácticos:**
1. Calcular el horizonte radioeléctrico para una antena ubicada a 81 metros de altura.
2. Si un enlace tiene una antena en una torre de 81 m y otra en una de 64 m, ¿logra cubrir más de 200 km? Justificar.
3. Explicar por qué durante el día la ionosfera permite rebotes de ciertas frecuencias.

---

## DÍA 24: REPASO GENERAL Y CASOS INTEGRADOS

### 24.1. Repaso de fórmulas clave
- Entropía: H = -Σ P(xᵢ) · log₂ P(xᵢ)
- Shannon-Hartley: C = B · log₂(1 + S/N)
- Nyquist: C = 2·B·log₂(L)
- Tasa de información = H/t, t = tiempo
- Baudio: B = Tₜ/k
- Eficiencia: E = H/L
- Longitud de onda: λ = v/f
- PIRE: PIRE = Pt - Lc + Ga
- Distancia = 2 × altura de órbita (ida y vuelta); Tiempo = distancia / velocidad de la luz
- Velocidad de la luz = 3\*10^8 
- Relacion Longitud de simbolos con entropia = H ≤ L < H + 1
- Estados posibles M = 2^k con k = T_t / Baudios
- Prx​=Ptx​−At​−N​
- Longitud de antena: λ/2, λ/4
- Velocidad de transmision = T_t = Baudios \* log_2(M)

### 24.2. Conversiones importantes
- dB a lineal: P = 10^(dB/10)
- Lineal a dB: dB = 10·log₁₀(P)
- dBm a mW: P_mW = 10^(dBm/10)
- mW a dBm: dBm = 10·log₁₀(P_mW)

### 24.3. Resolución de problemas integrados
- Combinar múltiples conceptos
- Identificar qué fórmula usar
- Verificar unidades y conversiones

### 24.4. Errores com unes a evitar
- Confundir tasa de información con velocidad de transmisión
- No convertir dB a lineal antes de usar en Shannon
- Olvidar unidades o hacer conversiones incorrectas
- Confundir baudios con bps

**Preguntas teóricas:**
1. ¿Cuál es el factor más costoso de modificar para aumentar la capacidad de un canal?
2. Si tiene una señal digital donde su primer armónico se ubica en 200 kHz, ¿en qué frecuencias se ubican los próximos dos armónicos?
3. ¿Cómo se puede reducir el tiempo de respuesta en una comunicación satelital?
4. ¿Qué sucede con la entropía de una fuente cuando los símbolos son equiprobables?

**Ejercicios prácticos:**
1. Problema integrado: Calcular la capacidad de un canal, luego determinar cuántos estados necesita una modulación para alcanzarla, y finalmente calcular la eficiencia de codificación.
2. Problema integrado: Dada una fuente, calcular entropía, construir código Huffman, calcular eficiencia, y determinar si es posible usar código en bloque.
3. Problema integrado: Calcular potencia mínima del transmisor considerando atenuación, ruido, y sensibilidad del receptor, expresando todo en las unidades correctas.

---

## DÍAS 25-29: SIMULACROS DE EXÁMENES

### Estrategia para los 5 días de simulacros:
- **Día 25-26**: Resolver 2-3 exámenes completos de años anteriores
- **Día 27**: Revisar errores y temas débiles identificados
- **Día 28**: Resolver 2 exámenes más con tiempo limitado
- **Día 29**: Repaso final de fórmulas y conceptos clave

### Formato de cada simulacro:
1. **Parte teórica** (60-90 min):
   - 5-6 preguntas teóricas que requieren justificación
   - Cubrir todos los temas principales
   
2. **Parte práctica** (90-120 min):
   - 4-5 ejercicios de cálculo
   - Incluir: entropía/Huffman, Hamming, CRC, modulación, capacidad de canal, decibeles/atenuación

### Checklist antes del examen real:
- [ ] Conocer todas las fórmulas de memoria
- [ ] Saber convertir entre dB, dBm, mW, W
- [ ] Dominar el algoritmo de Huffman
- [ ] Saber codificar y decodificar Hamming
- [ ] Poder calcular CRC
- [ ] Entender constelaciones de modulación
- [ ] Saber calcular capacidad de canal (Shannon y Nyquist)
- [ ] Dominar cálculos de atenuación y potencia
- [ ] Conocer características de satélites
- [ ] Entender modelo OSI y funciones de cada capa

---

## RECURSOS ADICIONALES PARA ESTUDIO

### Archivos de referencia en tu proyecto:
- `Resumen/PREVIO.md` - Resumen completo de todos los temas
- `Guia de estudio/Examenes/Examenes.md` - Exámenes de práctica
- `Flashcards/` - Tarjetas de repaso por tema
- `Resumen/` - Notas detalladas por tema específico

### Tiempo sugerido por día:
- **Estudio de conceptos**: 2-3 horas
- **Resolución de ejercicios**: 1-2 horas
- **Repaso y flashcards**: 30 minutos

### Consejos finales:
1. **Practica cálculos diariamente** - La práctica hace al maestro
2. **No memorices sin entender** - Comprende el "por qué" de cada fórmula
3. **Resuelve exámenes completos** - Acostúmbrate al formato y tiempo
4. **Revisa tus errores** - Aprende de cada equivocación
5. **Mantén un formulario** - Ten todas las fórmulas en un lugar accesible
6. **Estudia en voz alta** - Explicar conceptos ayuda a fijarlos
7. **Haz pausas** - El descanso es importante para la retención

¡Éxitos en tu examen! 🚀