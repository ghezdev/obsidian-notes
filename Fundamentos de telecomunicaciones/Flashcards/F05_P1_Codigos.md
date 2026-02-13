# F05 P1 - Códigos Parte 1

## ⚡ Flashcards Generadas (Telecom)

STARTI [Basic] ¿Qué es un código en telecomunicaciones? Back: Es un conjunto de reglas para representar símbolos o mensajes por medio de otros símbolos Tags: codigos <!--ID: 1767742736352--> ENDI
STARTI [Basic] ¿Cuáles son las dos funciones principales de los códigos? Back: Representación transformando datos a símbolos binarios y protección detectando o corrigiendo errores de transmisión Tags: codigos <!--ID: 1767742736354--> ENDI
STARTI [Basic] ¿Qué significa que un código sea no ambiguo? Back: Que cada secuencia codificada representa únicamente un símbolo sin ambigüedad Tags: codigos <!--ID: 1767742736355--> ENDI
STARTI [Basic] ¿Qué significa que un código sea único? Back: Que no hay dos símbolos distintos con el mismo código Tags: codigos <!--ID: 1767742736357--> ENDI
STARTI [Basic] ¿Qué es un código en bloque? Back: Es un código donde todos los símbolos codificados tienen la misma longitud en bits Tags: codigos <!--ID: 1767742736359--> ENDI
STARTI [Basic] ¿Qué ventaja tiene un código en bloque? Back: Es fácil de sincronizar y permite decodificación rápida Tags: codigos <!--ID: 1767742736361--> ENDI
STARTI [Basic] ¿Qué es un código no singular? Back: Es un código donde cada símbolo del alfabeto tiene un código distinto Tags: codigos <!--ID: 1767742736363--> ENDI
STARTI [Basic] ¿Qué es un código singular? Back: Es un código donde al menos dos símbolos distintos comparten el mismo código binario generando ambigüedad Tags: codigos <!--ID: 1767742736364--> ENDI
STARTI [Basic] ¿Qué es un código unívocamente decodificable? Back: Es un código donde los mensajes completos se pueden decodificar sin ambigüedad incluso si no es en bloque Tags: codigos <!--ID: 1767742736366--> ENDI
STARTI [Basic] ¿Qué es un código instantáneo? Back: Es un código prefijo donde ningún código de un símbolo es prefijo del código de otro símbolo Tags: codigos <!--ID: 1767742736368--> ENDI
STARTI [Basic] ¿Qué ventaja tiene un código instantáneo? Back: Permite decodificarse en el momento exacto que termina un símbolo sin esperar bits adicionales Tags: codigos <!--ID: 1767742736369--> ENDI
STARTI [Basic] ¿Qué es un código compacto? Back: Es un código que usa el menor número posible de bits promedio para la longitud de código dado el alfabeto y sus probabilidades Tags: codigos <!--ID: 1767742736371--> ENDI
STARTI [Basic] ¿Cómo se clasifican los códigos según su función? Back: En códigos sin detección de errores y códigos con detección y corrección de errores Tags: codigos <!--ID: 1767742736373--> ENDI
STARTI [Basic] ¿Qué es el código binario natural? Back: Es la representación directa de números en sistema binario Tags: codigos <!--ID: 1767742736374--> ENDI
STARTI [Basic] ¿Qué es el código BCD? Back: Es Decimal Codificado en Binario donde cada dígito decimal se representa con 4 bits Tags: codigos <!--ID: 1767742736376--> ENDI
STARTI [Basic] ¿Qué es el código Gray? Back: Es un código donde entre dos números consecutivos solo cambia 1 bit útil en electrónica digital Tags: codigos <!--ID: 1767742736378--> ENDI
STARTI [Basic] ¿Qué es el código ASCII? Back: Es un código para representar letras números y símbolos del teclado en formato binario Tags: codigos <!--ID: 1767742736379--> ENDI
STARTI [Basic] ¿Qué es un código de detección de errores? Back: Es un código que permite saber que hubo un error pero no lo corrige Tags: codigos <!--ID: 1767742736381--> ENDI
STARTI [Basic] ¿Qué es un bit de paridad? Back: Es un bit extra agregado para asegurar que el número total de unos sea par o impar Tags: codigos <!--ID: 1767742736383--> ENDI
STARTI [Basic] ¿Qué es la paridad par? Back: Es cuando el bit de paridad se ajusta para que el total de unos incluyendo el bit de paridad sea par Tags: codigos <!--ID: 1767742736384--> ENDI
STARTI [Basic] ¿Qué es la paridad impar? Back: Es cuando el bit de paridad se ajusta para que el total de unos incluyendo el bit de paridad sea impar Tags: codigos <!--ID: 1767742736386--> ENDI
STARTI [Basic] ¿Qué errores detecta el bit de paridad? Back: Detecta cualquier número impar de errores de bit 1 3 5 etc Tags: codigos <!--ID: 1767742736388--> ENDI
STARTI [Basic] ¿Qué errores no detecta el bit de paridad? Back: No detecta cuando hay un número par de errores 2 4 6 etc dentro de la misma palabra Tags: codigos <!--ID: 1767742736389--> ENDI
STARTI [Basic] ¿Qué es VRC? Back: Es Vertical Redundancy Check que agrega un bit de paridad en horizontal al final de cada palabra Tags: codigos <!--ID: 1767742736391--> ENDI
STARTI [Basic] ¿Qué es LRC? Back: Es Longitudinal Redundancy Check que agrega bits de paridad en vertical calculando paridad por columna Tags: codigos <!--ID: 1767742736392--> ENDI
STARTI [Basic] ¿Qué ventaja tiene combinar VRC y LRC? Back: Detecta cualquier error de 1 bit y la gran mayoría de errores múltiples permitiendo incluso corregir 1 bit Tags: codigos <!--ID: 1767742736394--> ENDI
STARTI [Basic] ¿Qué es CRC? Back: Es Cyclic Redundancy Check un método de detección de errores basado en división polinomial módulo 2 Tags: codigos <!--ID: 1767742736396--> ENDI
STARTI [Basic] ¿Por qué CRC es mejor que VRC y LRC juntos? Back: Por su mayor confiabilidad detectando el 100 por ciento de errores de igual o menor longitud del polinomio Tags: codigos <!--ID: 1767742736398--> ENDI
STARTI [Basic] ¿Cómo funciona CRC en el emisor? Back: Se agregan r ceros al mensaje se divide por el polinomio generador módulo 2 y el resto es el CRC Tags: codigos <!--ID: 1767742736399--> ENDI
STARTI [Basic] ¿Cómo funciona CRC en el receptor? Back: Se divide la trama recibida completa por el mismo polinomio generador si el resto es 0 no hay errores detectables Tags: codigos <!--ID: 1767742736401--> ENDI
STARTI [Basic] ¿Qué es un código de corrección de errores? Back: Es un código que permite detectar y corregir errores sin pedir retransmisión Tags: codigos <!--ID: 1767742736403--> ENDI
STARTI [Basic] ¿Qué es la distancia de Hamming? Back: Es el número de bits en los que difieren dos palabras binarias Tags: codigos <!--ID: 1767742736404--> ENDI
STARTI [Basic] ¿Qué es la distancia mínima de Hamming d_min? Back: Es la distancia más pequeña entre cualquier par de palabras de código válidas Tags: codigos <!--ID: 1767742736406--> ENDI
STARTI [Basic] ¿Cómo se relaciona d_min con la capacidad de detección? Back: Puede detectar hasta e errores si d_min mayor o igual a e más 1 Tags: codigos <!--ID: 1767742736407--> ENDI
STARTI [Basic] ¿Cómo se relaciona d_min con la capacidad de corrección? Back: Puede corregir hasta t errores si d_min mayor o igual a 2t más 1 Tags: codigos <!--ID: 1767742736409--> ENDI
STARTI [Basic] ¿Qué es el código de Hamming? Back: Es un código lineal que detecta y corrige errores en transmisión usando bits de paridad en posiciones de potencias de 2 Tags: codigos <!--ID: 1767742736411--> ENDI
STARTI [Basic] ¿Cuántos errores puede corregir el código de Hamming estándar? Back: Puede corregir 1 error y detectar 2 errores Tags: codigos <!--ID: 1767742736413--> ENDI
STARTI [Basic] ¿En qué posiciones se colocan los bits de paridad en Hamming? Back: En posiciones que son potencias de 2 es decir 1 2 4 8 16 32 etc Tags: codigos <!--ID: 1767742736414--> ENDI
STARTI [Basic] ¿Qué condición debe cumplirse para calcular cuántos bits de paridad usar en Hamming? Back: 2 elevado a p mayor o igual a m más p más 1 donde m son bits de datos y p bits de paridad Tags: codigos <!--ID: 1767742736416--> ENDI
STARTI [Basic] ¿Qué es el síndrome en la decodificación de Hamming? Back: Es el resultado de volver a calcular las paridades sobre la palabra recibida indicando la posición del bit con error Tags: codigos <!--ID: 1767742736418--> ENDI
STARTI [Basic] ¿Qué significa que el síndrome sea 0000 en Hamming? Back: Significa que no hay errores detectables Tags: codigos <!--ID: 1767742736420--> ENDI
STARTI [Basic] ¿Cómo se ordena el síndrome en Hamming para encontrar la posición del error? Back: Se ordena de mayor a menor los bits de paridad P8 P4 P2 P1 Tags: codigos <!--ID: 1767742736421--> ENDI

