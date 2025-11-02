TEORICOS: Responda las siguientes preguntas, justificando las respuestas:

1.    ¿Qué variables debe considerar para establecer el **tamaño de una antena**? Justifique los conceptos de las **unidades relevantes** para el cálculo de la misma.  

> El tamaño de la antena es igual a longitud de onda sobre 2 = $\lambda / 2$. Para obtener la longitud de onda, se podría obtener con la división entre velocidad y frecuencia = $\lambda = v / f$.

2.    Explique con la **ayuda de un gráfico** como se propaga la información dentro de una Fibra Óptica. Describa los **tipos de fibra** que conoce, y sus ventajas y desventajas. Considere **todos los elementos** que intervienen en dicho sistema.

> La información de una fibra óptica viaja a través del núcleo, que está compuesto por fibras de vidrio, otros componentes que tiene la fibra optica es una revestimiento y una cubierta. Las ventajas de la fibra optica es que tiene muy poca atenuacion, puede transmitir a largas distancias, desventajas es que es dificil de manipular. Existe la fibra monomodo y multimodo, monomodo es una fibra optica de un punto a otro punto, sirve para largas distancias, la multimodo es de un punto a varios puntos, permite comunicarse con varios dispositivos a la vez y soporta poca distancia

3.    Explique la técnica de **multiplexación CDM** y para qué **resulta necesaria**. De **al menos un ejemplo** de utilización de la misma.  
  
> La multiplexación CDM es la multiplexación por división de código, todos transmiten la información a la vez pero con un código de expansión único, se suele usar en GPS, es una técnica que permite compartir varias señales en un mismo canal de comunicación. 


4.    **Ordene** – justificando la respuesta - a los siguientes **dispositivos**, según la **cantidad de dominios de colisión** que poseen:

-           Switch de 48 puertos

-           Bridge

-           Hub de 8 puertos

-           Hub de 24 puertos

- **Hub / Repetidor (Capa 1)** → **1 solo** dominio de colisión sin importar cuántos puertos tenga.  
    (Todos comparten el mismo medio; si dos hablan a la vez, chocan.)
    
- **Bridge / Switch (Capa 2)** → **1 dominio de colisión por puerto** (segmentan el medio).
    
    - En la práctica hoy todo va **full-duplex** y ya no hay colisiones, pero académicamente se cuenta así.
        
    - Un **bridge** clásico es de **2 puertos** ⇒ 2 dominios.
        
- **Router (Capa 3)** → **1 dominio de colisión por interfaz** (además separa dominios de broadcast).

## Otros equipos que te pueden aparecer

- **Repeater**: 1 dominio (igual que hub).
    
- **Router / Firewall L3**: N dominios (uno por interfaz), además separa **broadcast**.
    
- **AP Wi-Fi**: todos los clientes en el **mismo canal** y celda comparten un dominio de contención (no hay CSMA/CD, sino CSMA/CA).
    
- **Medios coaxiales antiguos (10Base2/5)**: todo el bus es **1** dominio.

> Switch 
> Bridge
> Hub de 8
> Hub de 24

5.    ¿Por qué es necesario, en algunos casos, **modular una señal cuadrada** para transmitirla? ¿Conoce **técnicas** que lo hagan posible? ¿Cómo funcionan?  
  
> Para que viaje en largas distancias, rápido y que el ancho de banda sea mínimo. Existe FSK, PSK.
> FSK: Modifica la frecuencia de la portadora analógica según los valores digitales. Cuando la señal cuadrada es 1, la frecuencia aumenta, cuando es 0, disminuye
> PSK: Modifica la fase de la portadora analógica según los valores digitales

6.    Explique detalladamente el concepto de **distancia entre códigos,** qué **se puede definir** a partir del mismo y para qué resulta útil.

> La distancia entre códigos, es la distancia mínima de hamming, determina cuantos bits difieren entre ámbos. Es útil porque me sirve para saber cuantos errores puedo detectar y corregir. 


7.    **Salvavidas**: ¿Conocés algún tema en detalle del que quieras escribir? (Beneficia solamente a la teoría)

> Existen 3 tipos de satélites geo estacionarios, LEO, MEO, GEO.
> LEO: Satélite de baja órbita, es el que menos latencia tiene pero el que menos abarca
> MEO: Satélite de media óribta, tiene más latencia que LEO y abarca más 
> GEO: Satélite de órbita global, tiene una latencia aproximada de 250ms y con 3 satélites GEO es capaz de abarcar todo el planeta.

PRÁCTICOS:

1.    Se transmite a **57600 bps** con un modem de **3600 baudios**.

Graficar los estados de la señal modulada en un diagrama de amplitudes y fases, suponiendo un modem QAM de 2 amplitudes y uno PSK.

> Tasa de transmisión = T = 57600 bps 
> Baud = 3600 baudps
> 
> Bits/Simbolo = 57600 bps / 3600 baudps = 16 bits/simbolo 
> 
> La cantidad de bits por símbolo hace que la cantidad de estados sea muy grande como para graficarlo. Pero el gráfico de QAM debe tener 2 anillos y el PSK debe tener 1 solo.

2.    Se desea enviar el **símbolo** **101101001010**, aplicando algún método de **detección de errores**.

Agregar el **CRC**, sabiendo que el **polinomio generador es P(x) = x3 + x2 +** **x**

> ![[Pasted image 20250820114203.png]]

3.    Determinar el **nivel de ruido** (expresado el **W o alguno de sus submúltiplos**) que deberá soportar el medio, si:

·         La **distancia** entre ambos es **3 km**

·         La línea de comunicación tiene una **atenuación** de **6 dB/km**

·         Del equipo transmisor sale una señal de **80 mw**

·         Al equipo receptor llega una señal de **0.1 mW**

>L = 3km
>At = 6 dB/km
>Px = 80mw
>Rx = 0.1mw
>N = ?
>
>Px - At - N = Rx - Media 
>
>Px_W = 80mw * 10^-3 W = 0.08W => Px_dB = 10 * log_10(0.08) = -10.969 dB
>
>At_dB = 6dB/km * 3km = 18dB
>
>Rx_W = 0.1mw * 10^-3 W = 0.0001W => Rx_dB = 10 * log_10(0.0001W) = -40 dB
>
>-10.969 dB - 18 dB - N = -40 dB - 0 dB
>-28,969 dB - N = -40 dB
>- N = -40 dB + 28.969 dB
>- N = -11.031 dB
>  N = 11.031 dB
>  
>  W = 10^(11.031/10) = 12.679


4.    Deseamos enviar un **archivo de 100 símbolos**, con el siguiente alfabeto fuente y sus frecuencias de aparición:

|   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|
|**Símbolo**|**A**|**B**|**C**|**D**|**E**|**F**|**G**|**H**|
|**Probabilidad**|0.18|0.07|0.06|x|0.08|x|0.06|0.13|

a.    Calcular el **tamaño que ocupará el archivo** si se utiliza un **código bloque** binario.

b.    **Ídem anterior**, pero con un **código compacto** óptimo.

c.     Calcular el **porcentaje de compresión** obtenido.

> a) Cantidad de bits máximos que se pueden tener con 8 símbolos es igual a log_2(8) = 3 bits / simbolo => si hay 100 símbolos => 3 bits/simbolo * 100 símbolos = 300 bits => el archivo va a pesar 300 bits 
> 
> b) Aplicando huffman