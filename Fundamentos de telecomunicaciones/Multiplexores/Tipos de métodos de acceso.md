## ⏳ 1. **TDMA – Time Division Multiple Access**

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

---

## 📶 2. **OFDMA – Orthogonal Frequency Division Multiple Access**

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
    

---

## 🔑 3. **CDMA – Code Division Multiple Access**

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
    

---

📊 **Comparación rápida**

|Método|División principal|Simultaneidad|Ejemplo típico|
|---|---|---|---|
|**TDMA**|Tiempo|No (uno por turno)|GSM|
|**OFDMA**|Frecuencia (subportadoras ortogonales)|Sí|LTE, 5G|
|**CDMA**|Código|Sí|3G, GPS|
