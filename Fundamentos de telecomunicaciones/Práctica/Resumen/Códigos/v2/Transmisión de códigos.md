## 📌 1. **Transmisión de códigos**

Es la forma en que los **bits que representan símbolos** (por ejemplo, en ASCII, Huffman, etc.) se envían por un **canal físico**.

La transmisión puede clasificarse principalmente por **cómo se envían los bits** y por **cómo se sincroniza el emisor con el receptor**.

---

## 📌 2. **Transmisión en paralelo**

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


---

## 📌 3. **Transmisión en serie**

- **Qué es:** Los bits se envían **uno tras otro** por un solo canal o conductor.
    
- **Ventajas:**
    
    - Menos cables → más barata y sencilla.
        
    - Adecuada para largas distancias.
        
- **Desventajas:**
    
    - Más lenta que la paralela (a igualdad de tecnología), aunque en la práctica moderna con altas frecuencias puede superar a la paralela.
        
- **Usos típicos:** USB, Ethernet, RS-232, transmisión de datos por fibra óptica.

> [!NOTE] Title
> Sirve para comunicación a distancia. Se usó en los primeros mouse. Sirve para la tarjeta SUBE. En poco volumen de datos se usa transmisión en serie.

---

## 📌 4. **Transmisión asíncrona**

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

---

## 📌 5. **Transmisión síncrona**

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

---

## 📊 Comparativa rápida

|Tipo|Velocidad|Complejidad|Uso típico|
|---|---|---|---|
|Paralelo|Alta|Alta|Comunicación interna de hardware|
|Serie|Media/Alta|Baja|Redes, buses modernos|
|Asíncrono|Media|Baja|Transmisión intermitente|
|Síncrono|Alta|Media/Alta|Flujos de datos continuos|
