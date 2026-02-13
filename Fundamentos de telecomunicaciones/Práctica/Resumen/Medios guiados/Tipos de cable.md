## Cable trenzado

El **cable de par trenzado** está formado por **dos conductores de cobre aislados** que se **trenzan helicoidalmente** entre sí.  
Ese trenzado reduce la **interferencia electromagnética (EMI)** y la **diafonía** (crosstalk) entre pares, ya que cada conductor induce señales opuestas que tienden a cancelarse.

![[Pasted image 20250809171843.png]]

> [!note] 
> Trenzo los cables para evitar ruido de crosstalk

---

## 🛠 2. Tipos de cable trenzado

Se dividen según la presencia o no de blindaje:

### **UTP (Unshielded Twisted Pair)**

- Sin blindaje adicional.
    
- Ligero, económico y fácil de instalar.
    
- Más susceptible al ruido electromagnético.
    
- Muy usado en redes Ethernet (Cat5e, Cat6, Cat6a…).
    

### **STP (Shielded Twisted Pair)**

- Cada par tiene una pantalla metálica.
    
- Mejor protección contra interferencias.
    
- Más caro y menos flexible que el UTP.
    

### **FTP (Foiled Twisted Pair)**

- Todos los pares están envueltos en una única lámina de aluminio.
    
- Protección intermedia entre UTP y STP.

> [!note] 
> UTP: No es blindado, es decir, no tiene protección contra los ruidos electromagnéticos. Son viejos, su ancho de banda trabaja en 250MHz. (no tiene aislación)
> 
> FTP: igual a UTP pero blindados con una mezcla de plástico y aluminio. (aislación media)
> 
> STP: igual a UTP pero con un papel aluminio que va conectado a tierra. (aislación full)

---

## ⚙ 3. Ventajas

- Bajo costo y fácil instalación.
    
- Flexibilidad y ligereza.
    
- Compatible con muchas tecnologías (Ethernet, telefonía, etc.).
    

## ⚠ 5. Desventajas

- Menor alcance que la fibra óptica.
    
- Más susceptible al ruido que el coaxial o la fibra (sobre todo el UTP).

***Cable multipar:*** Conjunto de hilos de cobre agrupados por pares y trenzados.

***Atenuación***: Cada cable tiene su atenuación basada en la frecuencia
![[Pasted image 20250809172355.png]]

## 📏 3. Categorías (estándares de rendimiento)

La **TIA/EIA** define categorías según la frecuencia máxima y velocidad soportada:

|Categoría|Frecuencia máx.|Velocidad típica|
|---|---|---|
|Cat5e|100 MHz|1 Gbps|
|Cat6|250 MHz|1–10 Gbps (distancias cortas)|
|Cat6a|500 MHz|10 Gbps|
|Cat7|600 MHz|10 Gbps (blindado)|
|Cat8|2000 MHz|25–40 Gbps|

- - -

# Cable coaxial

![[Pasted image 20250809172632.png]]

• Es utilizado para transmitir señales analógicas y digitales.

• Debido a su blindaje, es menos susceptible a interferencias y crosstalk que el par trenzado.

• Esto le permite alcanzar mayores anchos de banda. El típico de un cable coaxial es aproximadamente de 1Ghz (un Gigahertz).

• De esta manera, se evidencia que es superior al par trenzado ya que puede alcanzar, de manera eficiente, anchos de banda más elevados y, por lo tanto, mayores tasas de transmisión.

Nació para transmitir en largas distancias

## Divisores y atenuadores de los cables coaxial:

Entra 100%, sale 50% y 50%

![[Pasted image 20250809172729.png]]

*Cabe aclarar que todos los dispositivos tienen una ligera pérdida.*

## Tipos 

![[Pasted image 20250809172752.png]]
El RG6 es el mejor, pero es el más caro

*(Los cables coaxil son más fáciles de implementar que la fibra óptica)*


- - -

# Fibra óptica 

- La fibra óptica transmite señales mediante **luz** en lugar de electricidad.
    
- Está hecha de **vidrio o plástico** muy puro.
    
- Funciona con el principio de la **reflexión interna total**: la luz queda atrapada dentro del núcleo y viaja largas distancias con muy poca pérdida.

### 🔹 Estructura de la fibra

- **Núcleo:** por donde viaja la luz (vidrio de mayor índice de refracción).
    
- **Revestimiento (cladding):** vidrio de menor índice de refracción → provoca reflexión interna total.
    
- **Recubrimiento protector:** plástico que protege de golpes, humedad y microcurvaturas.


### 🔹 Tipos de fibra

- **Monomodo (SMF):**
    
    - Núcleo muy delgado (≈ 9 µm).
        
    - Solo permite un modo de propagación.
        
    - Para largas distancias (decenas o cientos de km).
        
    - Se usa con láseres.
        
- **Multimodo (MMF):**
    
    - Núcleo más ancho (50 o 62,5 µm).
        
    - Varios modos de propagación.
        
    - Más barata, pero con más **dispersión modal** → útil solo en distancias cortas (hasta unos cientos de metros).
        
    - Se usa con LED.


👉 Imagen mental: como un cable con “capas”, siendo el núcleo el camino de la luz.

Funciona gracias a la ley de Snell. Cuando un haz de luz pasa de un medio a otro, sufre cambios. Depende del ángulo de incidencia de ese haz de luz.

Cuando el ángulo de incidencia se hace mayor que el ángulo crítico, se produce la reflexión.

![[Pasted image 20250809172831.png]]

Así funciona la fibra óptica. La fibra óptica es un medio hecho de vidrio, donde voy a insertar un modo (haz de luz) con un determinado ángulo para quedarme en una reflexión interna total.

Para poder hacer reflexión interna necesito de dos medios, el primero es donde inserto la luz (núcleo) y el segundo es otra estructura de vidrio (cladding).

Al vidrio la cubro con plástico para que el interior no interfiera.

Le agrego además un refuerzo físico para que el vidrio no se rompa.

## Ventajas 

▪ Menor tamaño y menor peso

▪ Baja atenuación

▪ Mayor espacio entre repetidores

▪ Aislamiento electromagnético

• No es vulnerable a interferencia , ruido por impulsos ni crosstalk.

• Previene el eavesdropping (escucha de líneas).

▪ La reflexión total interna puede ocurrir en cualquier medio transparente con un índice de refracción mayor que el índice del medio que lo rodea.

• Inmunidad al ruido, la única sería la luz externa, que es bloqueada por el recubrimiento opaco exterior.

• Menor atenuación de la señal, la distancia de transmisión es mayor que en los otros medios guiados.

• Ancho de banda mayor, además el ancho de banda no está limitado por el medio en sí, sino por la tecnología empleada.

▪ Menor precio (fibra vs cable, degradación de señal, repetidores)

_Cono de aceptación:_ *es el ángulo respecto al centro del core en que los modos de luz tienen que entrar para que el efecto de Snell se replique y la fibra funcione.*

## Desventajas 

• Costo: es caro debido a que cualquier impureza en el núcleo podría interrumpir la señal.

• Instalación/Mantenimiento: las uniones deben ser perfectas para permitir la comunicación.

• Fragilidad: la fibra de cristal se rompe más fácilmente que un cable metálico.

## Tipos 

### Fibra de índice escalonado

Multimodo. La información de los haces puede llegar en distinto orden, y esto puede generar muchos problemas. Sufre atenuación. Por eso se usa con distancias cortas.

### Fibra de índice gradual 

Multimodo. ahora el core no tiene un índice definido de reflexión a lo largo de todo el diámetro, sino que va variando a medida que me acerco al cladding. Esto hace que todos los modos se junten en algún momento, logrando que lleguen al mismo tiempo. De igual forma se usa para distancias cortas y bajas capacidades. Sirve para cableado vertical.

### Fibra monomodo

Se reduce la sección del núcleo. Solo puedo mandar la luz con un láser. (Con los multimodos de podía también con luz led). El láser solo manda una frecuencia de luz, pero si vida útil es muy baja, y por eso es caro. Estos tipos de fibra se usan para un cableo submarino.

Mandamos datos digitales sobre una luz. Si le cambio la frecuencia a una luz cambia de color. La fase de una luz no se puede cambiar. Por lo tanto, lo único que puedo cambiar es la amplitud, o sea, la intensidad de la luz. Decimos entonces que cuando modulamos una fibra óptica, lo hacemos en ASK.

_Receptores:_ *son aparatos fotosensibles que reciben la luz.*


## Atenuación 

![[Pasted image 20250809173153.png]]

