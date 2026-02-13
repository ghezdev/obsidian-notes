# F02 - Teoría de la Información

## ⚡ Flashcards Generadas (Telecom)

STARTI [Basic] ¿Qué es la información desde el punto de vista de la teoría de la información? Back: Es una medida de la reducción de incertidumbre en el receptor al recibir un mensaje Tags: teoria_informacion <!--ID: 1767742736565--> ENDI
STARTI [Basic] ¿Cómo se calcula la cantidad de información I(x) asociada a un mensaje? Back: I(x) = -log₂ P(x) donde P(x) es la probabilidad de ocurrencia del mensaje Tags: teoria_informacion <!--ID: 1767742736567--> ENDI
STARTI [Basic] ¿Por qué se usa logaritmo en base 2 para medir información? Back: Porque en comunicaciones digitales trabajamos con bits, que es un sistema binario Tags: teoria_informacion <!--ID: 1767742736569--> ENDI
STARTI [Basic] ¿Qué es una fuente de memoria nula? Back: Es una fuente que emite símbolos de manera independiente entre sí, sin memoria de los símbolos anteriores Tags: teoria_informacion <!--ID: 1767742736571--> ENDI
STARTI [Basic] ¿Qué mide la entropía de una fuente de información? Back: Mide la incertidumbre promedio de una fuente, es decir cuánta información en promedio produce un símbolo emitido Tags: teoria_informacion <!--ID: 1767742736572--> ENDI
STARTI [Basic] ¿Cuál es la fórmula de la entropía H(X)? Back: H(X) = -Σ P(xi) · log₂ P(xi) para todos los símbolos posibles Tags: teoria_informacion <!--ID: 1767742736574--> ENDI
STARTI [Basic] ¿Cuándo se alcanza la entropía máxima en una fuente? Back: Cuando todos los símbolos son equiprobables, es decir cuando P(xi) = 1/n para todos los símbolos Tags: teoria_informacion <!--ID: 1767742736576--> ENDI
STARTI [Basic] ¿Cuál es el valor de la entropía máxima para n símbolos equiprobables? Back: H = log₂(n) bits por símbolo Tags: teoria_informacion <!--ID: 1767742736578--> ENDI
STARTI [Basic] ¿Cuándo la entropía es mínima? Back: Cuando un símbolo tiene probabilidad cercana a 1 y los demás a 0, en cuyo caso H = 0 Tags: teoria_informacion <!--ID: 1767742736580--> ENDI
STARTI [Basic] ¿Qué es la tasa de información? Back: Mide cuántos bits útiles por segundo se transmiten sin contar errores ni redundancias, es una medida teórica Tags: teoria_informacion <!--ID: 1767742736582--> ENDI
STARTI [Basic] ¿Cómo se calcula la tasa de información? Back: T = H/t donde H es la entropía en bits por símbolo y t es el tiempo en segundos por símbolo Tags: teoria_informacion <!--ID: 1767742736584--> ENDI
STARTI [Basic] ¿Qué diferencia existe entre tasa de información y velocidad de transmisión? Back: La tasa de información mide bits útiles sin redundancia, mientras que la velocidad de transmisión cuenta todos los bits incluyendo redundancias Tags: teoria_informacion <!--ID: 1767742736586--> ENDI
STARTI [Basic] ¿Qué es un baudio? Back: Es una unidad que representa la cantidad de símbolos transmitidos por segundo en un sistema de comunicación digital Tags: teoria_informacion <!--ID: 1767742736588--> ENDI
STARTI [Basic] ¿Cómo se relaciona la tasa de transmisión con los baudios? Back: Tt = B · k donde B son los baudios y k es la cantidad de bits por símbolo Tags: teoria_informacion <!--ID: 1767742736590--> ENDI
STARTI [Basic] ¿Qué es la redundancia en un código? Back: Mide el exceso de codificación respecto al ideal, cuando todos los símbolos transmiten la máxima información posible Tags: teoria_informacion <!--ID: 1767742736591--> ENDI
STARTI [Basic] ¿Cómo se calcula la eficiencia de codificación? Back: E = H/L donde H es la entropía y L es la longitud media del código en bits por símbolo Tags: teoria_informacion <!--ID: 1767742736593--> ENDI
STARTI [Basic] ¿Cómo se relaciona la redundancia con la eficiencia? Back: R = 1 - E, es decir la redundancia es el complemento de la eficiencia Tags: teoria_informacion <!--ID: 1767742736595--> ENDI
STARTI [Basic] ¿Qué es un canal de comunicación? Back: Es el medio por el cual viaja la información desde un emisor hasta un receptor Tags: teoria_informacion <!--ID: 1767742736596--> ENDI
STARTI [Basic] ¿Cuáles son los componentes del modelo de comunicación de Shannon? Back: Fuente, codificador, canal, decodificador y receptor Tags: teoria_informacion <!--ID: 1767742736598--> ENDI
STARTI [Basic] ¿Qué es un canal sin ruido? Back: Es un canal teórico ideal donde la información llega perfecta sin errores ni perturbaciones Tags: teoria_informacion <!--ID: 1767742736600--> ENDI
STARTI [Basic] ¿Qué es un canal binario simétrico? Back: Es un canal que transmite bits 0 o 1 con una probabilidad de error p constante Tags: teoria_informacion <!--ID: 1767742736602--> ENDI
STARTI [Basic] ¿Qué establece el teorema de Shannon-Hartley? Back: Establece la capacidad máxima de un canal C = B · log₂(1 + S/N) donde B es el ancho de banda y S/N es la relación señal-ruido Tags: teoria_informacion <!--ID: 1767742736603--> ENDI
STARTI [Basic] ¿Qué parámetros se pueden modificar para aumentar la capacidad de un canal según Shannon-Hartley? Back: El ancho de banda B y la relación señal-ruido S/N Tags: teoria_informacion <!--ID: 1767742736605--> ENDI
STARTI [Basic] ¿Qué es la relación señal-ruido S/N? Back: Es la comparación entre la potencia de la señal y la potencia del ruido, expresada como razón lineal Tags: teoria_informacion <!--ID: 1767742736606--> ENDI
STARTI [Basic] ¿Cómo se expresa la relación señal-ruido en decibeles? Back: SNR_dB = 10 · log₁₀(S/N) Tags: teoria_informacion <!--ID: 1767742736608--> ENDI
STARTI [Basic] ¿Cómo se convierte SNR de decibeles a razón lineal? Back: S/N = 10^(SNR_dB/10) Tags: teoria_informacion <!--ID: 1767742736609--> ENDI
STARTI [Basic] ¿Qué es un decibel? Back: Es una expresión logarítmica que indica una relación de potencias o tensiones eléctricas, representando un valor con respecto a otro de referencia Tags: teoria_informacion <!--ID: 1767742736611--> ENDI
STARTI [Basic] ¿Cómo se calcula un valor en decibeles? Back: dB = 10 · log₁₀(P₁/P₀) donde P₁ es la potencia medida y P₀ es la potencia de referencia Tags: teoria_informacion <!--ID: 1767742736613--> ENDI
STARTI [Basic] ¿Qué es dBm? Back: Es una unidad de potencia donde la referencia es 1 miliwatt, es decir P₀ = 1 mW Tags: teoria_informacion <!--ID: 1767742736614--> ENDI
STARTI [Basic] ¿Qué es el efecto umbral en modulaciones digitales? Back: Es el fenómeno donde a partir de cierto S/N no mejora la relación de error, el receptor necesita un mínimo SNR para diferenciar símbolos Tags: teoria_informacion <!--ID: 1767742736616--> ENDI
STARTI [Basic] ¿Qué es la comunicación simplex? Back: Es una comunicación unidireccional donde un dispositivo transmite siempre y el otro recibe siempre Tags: teoria_informacion <!--ID: 1767742736619--> ENDI
STARTI [Basic] ¿Qué es la comunicación half-duplex? Back: Es una comunicación bidireccional pero no simultánea, los dispositivos alternan turnos para transmitir o recibir Tags: teoria_informacion <!--ID: 1767742736621--> ENDI
STARTI [Basic] ¿Qué es la comunicación full-duplex? Back: Es una comunicación bidireccional simultánea donde ambos dispositivos pueden transmitir y recibir al mismo tiempo Tags: teoria_informacion <!--ID: 1767742736623--> ENDI
STARTI [Basic] ¿Qué ventaja tiene la transmisión full-duplex sobre half-duplex? Back: Permite comunicación fluida y simultánea, ideal para servicios interactivos en tiempo real Tags: teoria_informacion <!--ID: 1767742736625--> ENDI
STARTI [Basic] ¿Qué desventaja tiene la comunicación simplex? Back: Falta de retroalimentación, no se pueden detectar errores en tiempo real Tags: teoria_informacion <!--ID: 1767742736626--> ENDI

