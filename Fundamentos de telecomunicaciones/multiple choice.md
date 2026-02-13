
## **1. Entropía e información**

Una fuente sin memoria tiene 8 símbolos equiprobables. ¿Cuál es su entropía?

A) 2 bits/símbolo  
B) 3 bits/símbolo  
C) 8 bits/símbolo  
D) Depende de la velocidad de transmisión

RTA: Sum(log_2(8)) = 3 bits/simbolo => B

---

## **2. Baudios, bits y estados**

Un sistema transmite a **9600 bps** usando **2400 baudios**. ¿Cuántos estados posibles tiene la modulación?

A) 2  
B) 4  
C) 8  
D) 16

RTA: M = 2^k con k = bits/simbolo & baudio = simbolo/seg => 9600 bits/seg / 2400 baudios (simb/seg) = 4 => B

---

## **3. Capacidad de canal (Shannon)**

Según el teorema de Shannon–Hartley, ¿cuál es el **factor más costoso de modificar** para aumentar la capacidad de un canal?

A) La codificación  
B) El ancho de banda  
C) La relación señal/ruido  
D) El tipo de modulación

RTA: B

---

## **4. Decibeles**

¿Cuál de las siguientes operaciones es **correcta**?

A) dBm + dBm  
B) dB + dB  
C) dBm + dB  
D) dBm × dB

RTA: C

---

## **5. Señales y espectro**

¿Por qué una señal cuadrada tiene ancho de banda teóricamente infinito?

A) Porque es digital  
B) Porque tiene amplitud constante  
C) Porque contiene infinitos armónicos  
D) Porque no es periódica

RTA: C

---

## **6. Teorema de Nyquist**

Si una señal analógica tiene frecuencia máxima de **4 kHz**, ¿cuál es la frecuencia mínima de muestreo?

A) 4 kHz  
B) 6 kHz  
C) 8 kHz  
D) 16 kHz

RTA: f_min_muestreo > 2 x f_max => f_min_muestreo = 8khz => C

---

## **7. Modulación**

¿Cuál de las siguientes modulaciones **varía simultáneamente amplitud y fase**?

A) PSK  
B) FSK  
C) ASK  
D) QAM

RTA: D

---

## **8. Códigos**

¿Cuál de las siguientes afirmaciones sobre el **código de Huffman** es correcta?

A) Es un código en bloque  
B) Siempre tiene longitud fija  
C) Es instantáneo y óptimo  
D) Permite corregir errores

RTA: A

---

## **9. Detección y corrección de errores**

El código de Hamming estándar tiene distancia mínima:

A) 1  
B) 2  
C) 3  
D) 4

RTA: 1 (Realmente no sé)

---

## **10. Modelo OSI y propagación**

¿En qué capa del modelo OSI se realiza la **detección de errores a nivel de trama**?

A) Física  
B) Enlace de datos  
C) Red  
D) Transporte

RTA: La trama se trabaja en la capa de enlace de datos. Pero la capa de transporte es la que se asegura que todo llegue bien, así que estoy medio confundido. Mi respuesta es la B

---

## **11. Información vs entropía**

¿Cuál es la diferencia correcta entre **información** y **entropía**?

A) Ambas miden bits por segundo  
B) La información mide una fuente, la entropía un símbolo  
C) La información mide un símbolo, la entropía una fuente  
D) Son conceptos equivalentes

RTA: C

---

## **12. Redundancia**

Si una fuente tiene **H = 2 bits/símbolo** y se codifica con una longitud media **L = 3 bits/símbolo**, la redundancia es:

A) 33 %  
B) 50 %  
C) 66 %  
D) 1 bit

RTA: A

---

## **13. Capacidad sin ruido**

La fórmula de Nyquist **sin ruido** indica que la capacidad del canal depende de:

A) Solo del ancho de banda  
B) Del ancho de banda y la SNR  
C) Del ancho de banda y la cantidad de niveles  
D) Solo del tipo de modulación

RTA: C

---

## **14. Señales**

¿Cuál de las siguientes señales **NO** es determinística?

A) Senoidal  
B) Cuadrada ideal  
C) Triangular periódica  
D) Ruido térmico

RTA: D, aunque no sé bien a qué se refiere que NO sea determinística

---

## **15. Análisis espectral**

Si el primer armónico de una señal digital está en **200 kHz**, ¿dónde están los dos siguientes armónicos?

A) 300 kHz y 400 kHz  
B) 400 kHz y 600 kHz  
C) 600 kHz y 800 kHz  
D) 600 kHz y 1000 kHz

RTA: No sé

---

## **16. Modulación FM**

¿Cuál es una característica correcta de la modulación FM?

A) La amplitud varía con la señal  
B) La fase es constante  
C) La frecuencia varía con la señal  
D) Es sensible al ruido de amplitud

RTA: C

---

## **17. Codificación de línea**

¿Por qué Manchester tiene mejor sincronización que NRZ?

A) Usa más potencia  
B) Tiene componente DC  
C) Tiene una transición por bit  
D) Ocupa menos ancho de banda

RTA: D, aunque no sé que es DC

---

## **18. CRC**

¿Por qué el CRC es más confiable que el bit de paridad?

A) Usa más bits  
B) Detecta errores múltiples  
C) Corrige errores  
D) No agrega redundancia

RTA: B

---

## **19. Transmisión**

¿Por qué la transmisión síncrona es más eficiente que la asíncrona?

A) Usa menos voltaje  
B) No necesita reloj  
C) No usa bits de inicio y parada  
D) Usa menos ancho de banda

RTA: C

---

## **20. Multiplexación vs acceso**

¿Cuál es la diferencia correcta entre **multiplexación** y **método de acceso**?

A) Son sinónimos  
B) La multiplexación es analógica y el acceso digital  
C) La multiplexación combina señales, el acceso reparte el medio  
D) El acceso solo se usa en radio

RTA: C

- - -

## **21. Entropía y fuente**

Una fuente sin memoria tiene 4 símbolos con probabilidades:  
P(A)=0,5 ; P(B)=0,25 ; P(C)=0,125 ; P(D)=0,125.  
¿Cuál de las siguientes afirmaciones es correcta?

A) La entropía es máxima  
B) La entropía es menor que log₂(4)  
C) La entropía vale exactamente 2 bits/símbolo  
D) La entropía depende de la velocidad de transmisión

RTA: B

---

## **22. Longitud media y eficiencia**

Un código tiene longitud media **L = 3,2 bits/símbolo** y la entropía de la fuente es **H = 2,6 bits/símbolo**.  
¿Cuál de las siguientes afirmaciones es correcta?

A) El código no puede ser Huffman  
B) El código es imposible  
C) La eficiencia es mayor al 80 %  
D) La redundancia es mayor a 1 bit/símbolo

RTA: C

---

## **23. Shannon vs Nyquist**

¿Cuál de las siguientes afirmaciones es correcta respecto a **Shannon–Hartley y Nyquist**?

A) Nyquist siempre da mayor capacidad que Shannon  
B) Shannon no considera ruido  
C) Nyquist supone canal ideal sin ruido  
D) Ambos dependen de la SNR

RTA: C

---

## **24. Decibeles (conceptual)**

Un sistema tiene:

- Potencia transmitida: 10 dBm
    
- Atenuación del canal: 13 dB
    
- Ganancia de antena: 6 dBi
    

¿Cuál de las siguientes expresiones representa correctamente la potencia recibida?

A) 10 − 13 − 6 dBm  
B) 10 + 13 − 6 dBm  
C) 10 − 13 + 6 dBm  
D) 10 + 13 + 6 dBm

RTA: C

---

## **25. Señales y ancho de banda**

Una señal digital ideal se transmite por un canal con ancho de banda limitado.  
¿Cuál es el **primer efecto** que aparece al reducir el ancho de banda?

A) Atenuación  
B) Ruido térmico  
C) Distorsión por pérdida de armónicos  
D) Interferencia electromagnética

RTA: Realmente no sé, supongo que la C

---

## **26. Muestreo**

Se muestrea una señal analógica a una frecuencia menor que la de Nyquist.  
¿Cuál de las siguientes consecuencias es correcta?

A) La señal pierde amplitud  
B) Aparece distorsión por retardo  
C) Se produce aliasing  
D) Se reduce la SNR

RTA: C

---

## **27. Modulación**

Un módem QAM aumenta la cantidad de bits por símbolo manteniendo constante el ancho de banda.  
¿Cuál es el principal costo de esta decisión?

A) Mayor complejidad del receptor  
B) Mayor ancho de banda  
C) Menor eficiencia espectral  
D) Menor velocidad de transmisión

RTA: Realmente no sé

---

## **28. Códigos**

¿Cuál de las siguientes afirmaciones sobre códigos es correcta?

A) Todo código compacto es instantáneo  
B) Todo código instantáneo es compacto  
C) Todo código unívocamente decodificable es instantáneo  
D) Un código Huffman siempre tiene longitud fija

RTA: C

---

## **29. Hamming**

El código de Hamming estándar puede:

A) Detectar un error y corregir dos  
B) Detectar y corregir un error  
C) Detectar dos errores y corregir uno  
D) Detectar y corregir errores múltiples

RTA: C

---

## **30. OSI y encapsulamiento**

Durante el proceso de encapsulamiento en el modelo OSI:

A) Cada capa elimina información de la anterior  
B) Cada capa agrega su propio encabezado  
C) Solo las capas inferiores agregan redundancia  
D) El tamaño del mensaje permanece constante

RTA: B


- - -

## **31. Entropía y codificación**

Una fuente sin memoria tiene entropía **H = 3,7 bits/símbolo**.  
¿Cuál de las siguientes afirmaciones es correcta respecto a cualquier codificación posible?

A) Puede codificarse con longitud media menor a 3 bits  
B) No puede codificarse con longitud media menor a 3,7 bits  
C) Siempre puede codificarse con longitud media igual a 3 bits  
D) La longitud media no depende de la entropía

RTA: B

---

## **32. Tasa, velocidad y baudios**

Un sistema transmite símbolos a **2000 baudios** usando una modulación de **32 estados**.  
¿Cuál de las siguientes afirmaciones es correcta?

A) La velocidad es 10 kbps  
B) La velocidad es 8 kbps  
C) La velocidad es 5 kbps  
D) La velocidad depende del ancho de banda

RTA: 2^K = 32 => K=T_t / baudios => A

---

## **33. Shannon–Hartley (conceptual)**

Si se duplica el ancho de banda de un canal y se mantiene constante la SNR, la capacidad del canal:

A) Se duplica  
B) Se cuadruplica  
C) Aumenta linealmente con B  
D) Aumenta logarítmicamente con la SNR

RTA: A

---

## **34. dB y potencias**

¿Cuál de las siguientes situaciones **no** puede resolverse correctamente usando solo decibeles (sin pasar a lineal)?

A) Sumar atenuaciones de varios tramos  
B) Calcular potencia de salida con ganancia conocida  
C) Calcular la SNR lineal para Shannon  
D) Comparar pérdidas entre dos enlaces

RTA: D

---

## **35. Espectro y distorsión**

Una señal digital transmitida por un canal con ancho de banda limitado presenta intersímbolo.  
¿Cuál es la causa principal?

A) Ruido térmico  
B) Atenuación uniforme  
C) Diferente atenuación de armónicos  
D) Interferencia electromagnética externa

RTA: no sé que es intersimbolo, pero creo que es la D

---

## **36. Muestreo y PAM**

Luego del muestreo ideal de una señal analógica se obtiene una señal PAM.  
¿Cuál es una característica correcta de esta señal?

A) Discreta en tiempo y en amplitud  
B) Continua en tiempo y en amplitud  
C) Discreta en tiempo y continua en amplitud  
D) Continua en tiempo y discreta en amplitud

RTA: no sé realmente, creo que A

---

## **37. Modulación y eficiencia**

Al aumentar el número de niveles de una modulación QAM:

A) Disminuye la eficiencia espectral  
B) Aumenta la robustez al ruido  
C) Aumenta la cantidad de bits por símbolo  
D) Disminuye la velocidad de transmisión

RTA: C

---

## **38. Códigos y detección**

¿Cuál de los siguientes códigos es **exclusivamente** de detección de errores y no de corrección?

A) Hamming  
B) Paridad simple  
C) Código Gray  
D) Huffman

RTA: C

---

## **39. Multiplexación vs acceso**

¿Cuál de los siguientes pares está correctamente asociado?

A) TDMA – multiplexación en frecuencia  
B) OFDMA – método de acceso  
C) WDM – método de acceso  
D) CDMA – multiplexación temporal

RTA: B

---

## **40. Propagación**

La propagación ionosférica es más adecuada para:

A) Frecuencias muy altas (microondas)  
B) Enlaces de línea de vista  
C) Frecuencias medias y altas en HF  
D) Comunicaciones satelitales GEO

RTA: C

- - -

## **41. Entropía y fuente**

Una fuente tiene entropía **H = 0 bits/símbolo**.  
¿Cuál de las siguientes situaciones es consistente con ese valor?

A) Dos símbolos equiprobables  
B) Un símbolo con probabilidad 1  
C) Una fuente con ruido  
D) Una fuente con memoria

RTA: B

---

## **42. Longitud media**

¿Cuál de las siguientes afirmaciones es correcta respecto a la longitud media **L** de un código?

A) Siempre es mayor que la entropía  
B) Puede ser menor que la entropía  
C) Es independiente de las probabilidades  
D) Solo depende del número de símbolos

RTA: A

---

## **43. Capacidad de canal**

Según Shannon–Hartley, si se mantiene constante el ancho de banda y se aumenta la potencia de señal indefinidamente:

A) La capacidad crece linealmente  
B) La capacidad crece sin límite  
C) La capacidad crece logarítmicamente  
D) La capacidad no cambia

RTA: C

---

## **44. Decibeles y referencias**

¿Cuál de las siguientes unidades es una **potencia absoluta**?

A) dB  
B) dBi  
C) dBm  
D) dBd

RTA: A

---

## **45. Señales**

Una señal periódica no senoidal ideal:

A) Tiene un único componente espectral  
B) Tiene ancho de banda finito  
C) Puede descomponerse en infinitas senoidales  
D) No puede analizarse en frecuencia

RTA: C

---

## **46. Ancho de banda**

¿Cuál es la relación correcta entre ancho de banda y velocidad de transmisión?

A) Son magnitudes equivalentes  
B) El ancho de banda limita la velocidad máxima  
C) La velocidad define el ancho de banda  
D) No están relacionadas

RTA: B

---

## **47. Modulación**

¿Cuál de las siguientes modulaciones **no** modifica ningún parámetro de la portadora de forma continua?

A) AM  
B) FM  
C) PM  
D) ASK

RTA: NO SÉ, CREO QUE D

---

## **48. Codificación de línea**

¿Cuál es el principal problema de NRZ en largas secuencias de bits iguales?

A) Alto consumo de potencia  
B) Falta de sincronización  
C) Exceso de ancho de banda  
D) Dificultad de decodificación

RTA: B

---

## **49. Errores**

Un código tiene distancia mínima **d = 4**.  
¿Qué puede garantizar este código?

A) Detectar hasta 3 errores  
B) Corregir hasta 2 errores  
C) Detectar 4 errores y corregir 1  
D) Corregir 1 error y detectar 2

RTA: No me acuerdo cual era la formula para saber esto, creo que es la A

---

## **50. OSI**

¿Cuál de las siguientes funciones **NO** corresponde a la capa de transporte?

A) Control de flujo extremo a extremo  
B) Corrección de errores extremo a extremo  
C) Direccionamiento lógico  
D) Segmentación de datos

RTA: C