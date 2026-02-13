## 1️⃣ **Código Baudot**

- Uno de los primeros códigos de transmisión de texto.
    
- Usa **5 bits por carácter** → permite representar 25=322^5 = 3225=32 combinaciones. *insuficientes para representar 26 letras + 10 números*
    
- Originalmente se usaba en **telegrafía** y teletipos.
    
- Para cubrir todas las letras y símbolos, emplea un sistema de **shift**:
    
    - **Letras**: un conjunto de 32 símbolos
        
    - **Figuras**: otro conjunto (números, signos de puntuación)
        
- No incluye control de errores, era simple y rápido para la época.

- 4 códigos especiales para SP, CR, LF & blank

- Es CÓDIGO SINGULAR

**Problemas:**

- Requiere códigos especiales para cambiar el set de caracteres.

- No posee minúsculas, y tiene pocos caracteres especiales.

- No posee mecanismo de detección de errores.

- Los caracteres no están en orden por su valor binario.

- Diseñado para transmisión de datos, no para procesamiento.


---

## 2️⃣ **Código Baudot Internacional** (ITA2 – International Telegraph Alphabet No. 2)

- Agrega un 6to bit para paridad

- Versión estandarizada del **Baudot** por la **CCITT** (actual UIT-T).
    
- También de **5 bits**, pero con distribución adaptada para mayor compatibilidad entre equipos.
    
- Usado en teletipos, telex, radiotelegrafía.
    
- Velocidad típica: 50 baudios.
    
- Aún utiliza **shift de letras/figuras** para ampliar el alfabeto.
    

---

## 3️⃣ **Códigos BCD** (Binary Coded Decimal)

- Código de 4 o 6 bits

- Codifican **cada dígito decimal** en **su equivalente binario de 4 bits**. => 2^4 = 16 caracteres (4 bits) o 2^6 = 64 caracteres (6 bits)
    
- Ejemplo:
    
    - Decimal: 5 → BCD: 0101
        
    - Decimal: 27 → BCD: 0010 0111
        
- Se usan mucho en electrónica digital y sistemas que manejan datos numéricos (cajeros automáticos, relojes digitales).
    
- Variantes: **8421 BCD** (la más común), **Excess-3**, **BCD empaquetado**.

- Era el utilizado en las tarjetas perforada

---

## 4️⃣ **Código ASCII** (American Standard Code for Information Interchange)

- Longitud fija: **7 bits** (128 caracteres), a menudo almacenado en 8 bits (el bit extra se usa para paridad o extensión). => 2^7 = 128 caracteres diferentes
    
- Incluye:
    
    - Letras mayúsculas y minúsculas
        
    - Dígitos 0–9
        
    - Símbolos de puntuación
        
    - Caracteres de control (ENTER, ESC, etc.)
        
- Ampliación **ASCII extendido**: 8 bits → 256 caracteres (incluye acentos y símbolos gráficos).
	- Usado para procesamiento y almacenamiento de información.
	
	- Permite caracteres internacionales.
    

---

## 5️⃣ **Código EBCDIC** (Extended Binary Coded Decimal Interchange Code)

- Desarrollado por IBM.
    
- Longitud fija: **8 bits**.
    
- Organizado de forma distinta al ASCII (incompatible directamente).
    
- Muy usado en mainframes y sistemas heredados de IBM.
    
- Menos común hoy, pero todavía presente en entornos bancarios y corporativos antiguos.

- Es una extensión del código propietario BCD de 6 bits

- 2^8=256 diferentes caracteres.

---

## 6️⃣ **Código Unicode**

- Estándar moderno que busca **representar todos los caracteres de todos los idiomas**.
    
- Longitudes variables:
    
    - UTF-8: 1 a 4 bytes por carácter
        
    - UTF-16: 2 o 4 bytes
        
    - UTF-32: 4 bytes fijos
        
- Incluye alfabetos latinos, cirílico, chino, japonés, emojis, símbolos técnicos, etc.
    
- Es **compatible con ASCII** en UTF-8 (los primeros 128 caracteres son idénticos).
    

---

## 📊 Resumen comparativo

| Código               | Bits por carácter       | Caracteres posibles | Uso principal                         |
| -------------------- | ----------------------- | ------------------- | ------------------------------------- |
| Baudot               | 5                       | 32 (con shift: más) | Telegrafía                            |
| Baudot Internacional | 6 (5 datos + 1 paridad) | 32 (shift)          | Telex, teletipos                      |
| BCD                  | 4/6 por dígito          | 10 dígitos          | Datos numéricos en sistemas digitales |
| ASCII                | 8 (7 datis + 1 paridad) | 128 (256 extendido) | Texto en inglés y símbolos básicos    |
| EBCDIC               | 9 (8 datos + 1 paridad) | 256                 | Mainframes IBM                        |
| Unicode (UTF-8)      | 8 a 32                  | +1 millón           | Representación global de caracteres   |