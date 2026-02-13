# F05 P2 - Códigos Parte 2

## ⚡ Flashcards Generadas (Telecom)

STARTI [Basic] ¿Qué es el método de Huffman? Back: Es un algoritmo de codificación óptima que asigna códigos binarios de distinta longitud a cada símbolo según su probabilidad de aparición Tags: codigos_huffman <!--ID: 1767742736278--> ENDI
STARTI [Basic] ¿Cuál es el objetivo del código de Huffman? Back: Reducir la longitud promedio del código L lo más cerca posible de la entropía H de la fuente Tags: codigos_huffman <!--ID: 1767742736280--> ENDI
STARTI [Basic] ¿Qué característica tiene el código de Huffman? Back: Es un código instantáneo prefijo donde ningún código es prefijo de otro Tags: codigos_huffman <!--ID: 1767742736282--> ENDI
STARTI [Basic] ¿Es el código de Huffman unívocamente decodificable? Back: Sí es unívocamente decodificable y además es compacto Tags: codigos_huffman <!--ID: 1767742736284--> ENDI
STARTI [Basic] ¿Qué símbolos tienen códigos más cortos en Huffman? Back: Los símbolos más probables tienen longitudes más cortas Tags: codigos_huffman <!--ID: 1767742736286--> ENDI
STARTI [Basic] ¿Qué símbolos tienen códigos más largos en Huffman? Back: Los símbolos menos probables tienen longitudes más largas Tags: codigos_huffman <!--ID: 1767742736288--> ENDI
STARTI [Basic] ¿Cuál es el primer paso del algoritmo de Huffman? Back: Listar símbolos y probabilidades de la fuente Tags: codigos_huffman <!--ID: 1767742736289--> ENDI
STARTI [Basic] ¿Cómo se ordenan los símbolos en Huffman? Back: Se ordenan de menor a mayor probabilidad Tags: codigos_huffman <!--ID: 1767742736291--> ENDI
STARTI [Basic] ¿Qué símbolos se combinan en cada paso de Huffman? Back: Se combinan los dos símbolos menos probables en un nodo sumando sus probabilidades Tags: codigos_huffman <!--ID: 1767742736293--> ENDI
STARTI [Basic] ¿Cuándo termina el algoritmo de Huffman? Back: Cuando queda un único nodo raíz con probabilidad 1 Tags: codigos_huffman <!--ID: 1767742736294--> ENDI
STARTI [Basic] ¿Cómo se asignan los bits en el árbol de Huffman? Back: Se asignan 0 y 1 a las ramas de cada unión típicamente izquierda 0 derecha 1 Tags: codigos_huffman <!--ID: 1767742736296--> ENDI
STARTI [Basic] ¿Cómo se leen los códigos en Huffman? Back: Se leen desde la raíz hasta cada símbolo siguiendo las ramas Tags: codigos_huffman <!--ID: 1767742736298--> ENDI
STARTI [Basic] ¿Cómo se calcula la longitud promedio en Huffman? Back: L = Σ pi · li donde pi es la probabilidad y li es la longitud del código del símbolo i Tags: codigos_huffman <!--ID: 1767742736300--> ENDI
STARTI [Basic] ¿Cuál es la relación entre entropía y longitud promedio en Huffman? Back: H menor o igual a L menor que H más 1 Tags: codigos_huffman <!--ID: 1767742736301--> ENDI
STARTI [Basic] ¿Qué usos tiene el código de Huffman? Back: Compresión de datos ZIP GZIP 7z codificación de imágenes JPEG compresión de audio MP3 AAC Tags: codigos_huffman <!--ID: 1767742736303--> ENDI
STARTI [Basic] ¿Qué es la transmisión de códigos? Back: Es la forma en que los bits que representan símbolos se envían por un canal físico Tags: transmision_codigos <!--ID: 1767742736305--> ENDI
STARTI [Basic] ¿Qué es la transmisión en paralelo? Back: Se envían varios bits al mismo tiempo cada uno por un conductor diferente Tags: transmision_codigos <!--ID: 1767742736307--> ENDI
STARTI [Basic] ¿Qué ventaja tiene la transmisión en paralelo? Back: Es muy rápida un ciclo transmite varios bits Tags: transmision_codigos <!--ID: 1767742736309--> ENDI
STARTI [Basic] ¿Qué desventaja tiene la transmisión en paralelo? Back: Necesita muchos conductores más costosa y difícil de usar en largas distancias Tags: transmision_codigos <!--ID: 1767742736310--> ENDI
STARTI [Basic] ¿Qué es la transmisión en serie? Back: Los bits se envían uno tras otro por un solo canal o conductor Tags: transmision_codigos <!--ID: 1767742736312--> ENDI
STARTI [Basic] ¿Qué ventaja tiene la transmisión en serie? Back: Menos cables más barata y adecuada para largas distancias Tags: transmision_codigos <!--ID: 1767742736314--> ENDI
STARTI [Basic] ¿Qué es la transmisión asíncrona? Back: No hay un reloj común continuo la sincronización se realiza por carácter o por palabra Tags: transmision_codigos <!--ID: 1767742736316--> ENDI
STARTI [Basic] ¿Qué bits adicionales tiene la transmisión asíncrona? Back: Bit de inicio start bit bits de datos bit de parada stop bits y opcional bit de paridad Tags: transmision_codigos <!--ID: 1767742736318--> ENDI
STARTI [Basic] ¿Qué ventaja tiene la transmisión asíncrona? Back: Simple no requiere sincronización continua ideal para transmisiones intermitentes Tags: transmision_codigos <!--ID: 1767742736320--> ENDI
STARTI [Basic] ¿Qué desventaja tiene la transmisión asíncrona? Back: Sobrecarga de bits extra por cada carácter Tags: transmision_codigos <!--ID: 1767742736322--> ENDI
STARTI [Basic] ¿Qué es la transmisión síncrona? Back: Emisor y receptor comparten un reloj común o derivan la sincronía de la señal recibida Tags: transmision_codigos <!--ID: 1767742736324--> ENDI
STARTI [Basic] ¿Qué ventaja tiene la transmisión síncrona? Back: Mayor eficiencia no hay bits de inicio parada por cada carácter ideal para flujos continuos Tags: transmision_codigos <!--ID: 1767742736326--> ENDI
STARTI [Basic] ¿Qué desventaja tiene la transmisión síncrona? Back: Más compleja de implementar requiere mantener sincronía Tags: transmision_codigos <!--ID: 1767742736328--> ENDI
STARTI [Basic] ¿Qué es un protocolo orientado a carácter? Back: Usa caracteres especiales del código de control ASCII u otro para marcar el inicio y fin de una trama Tags: protocolos_comunicacion <!--ID: 1767742736330--> ENDI
STARTI [Basic] ¿Qué caracteres de control usa un protocolo orientado a carácter? Back: STX Start of Text para inicio y ETX End of Text para fin Tags: protocolos_comunicacion <!--ID: 1767742736331--> ENDI
STARTI [Basic] ¿Qué problema tiene un protocolo orientado a carácter? Back: Si el carácter especial aparece dentro de los datos el receptor podría interpretarlo como fin de trama por error Tags: protocolos_comunicacion <!--ID: 1767742736333--> ENDI
STARTI [Basic] ¿Qué es un protocolo orientado a bit? Back: No usa caracteres especiales sino secuencias de bits únicas para marcar el inicio y fin de la trama Tags: protocolos_comunicacion <!--ID: 1767742736335--> ENDI
STARTI [Basic] ¿Qué ventaja tiene un protocolo orientado a bit? Back: Independencia del código de caracteres sirve para cualquier tipo de datos binarios Tags: protocolos_comunicacion <!--ID: 1767742736337--> ENDI
STARTI [Basic] ¿Qué problema tiene un protocolo orientado a bit? Back: La secuencia de inicio fin podría aparecer dentro de los datos Tags: protocolos_comunicacion <!--ID: 1767742736339--> ENDI
STARTI [Basic] ¿Cómo se soluciona el problema de secuencias especiales en protocolos orientados a bit? Back: Usando bit stuffing inserción de bits de relleno Tags: protocolos_comunicacion <!--ID: 1767742736341--> ENDI
STARTI [Basic] ¿Qué ventaja tiene un protocolo orientado a bit sobre uno orientado a carácter? Back: Mayor aprovechamiento del ancho de banda menor redundancia y detección de errores sofisticadas Tags: protocolos_comunicacion <!--ID: 1767742736343--> ENDI
STARTI [Basic] ¿Por qué tiene sentido aplicar un código de corrección de errores en un protocolo orientado a bit? Back: Porque los protocolos orientados a bit transmiten flujos continuos donde los errores pueden propagarse Tags: protocolos_comunicacion <!--ID: 1767742736345--> ENDI
STARTI [Basic] ¿Por qué tiene sentido aplicar un código de detección de errores en un protocolo orientado a bit? Back: Porque permite detectar errores sin retransmitir todo el flujo mejorando la eficiencia Tags: protocolos_comunicacion <!--ID: 1767742736347--> ENDI
STARTI [Basic] ¿Qué es el bit stuffing? Back: Es la inserción de bits de relleno para evitar que la secuencia de inicio fin aparezca dentro de los datos Tags: protocolos_comunicacion <!--ID: 1767742736348--> ENDI
STARTI [Basic] ¿Qué diferencia hay entre protocolos orientados a carácter y bit en términos de eficiencia? Back: Los orientados a bit aprovechan mejor el ancho de banda por la independencia del alfabeto y menor redundancia Tags: protocolos_comunicacion <!--ID: 1767742736350--> ENDI

