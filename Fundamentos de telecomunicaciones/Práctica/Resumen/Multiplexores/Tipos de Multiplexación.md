
# Multiplexación por División de Frecuencia (FDM)

- Cada canal se transmite en una banda de frecuencias diferente.

- Requiere filtros pasabajos y pasaaltos para separar las señales.     
- Muy utilizada en radio FM, TV analógica y sistemas telefónicos analógicos.

![[Pasted image 20250809135717.png]]

### 🔍 Lo que pasa realmente en FDM

1. **Antes de multiplexar**
    
    - Tienes 12 canales de voz, cada uno ocupando **4 kHz de ancho de banda**.
        
    - Sin modulación, todos estarían “apilados” en el mismo rango (0–4 kHz) → se solaparían y sería imposible distinguirlos.
        
2. **Durante la multiplexación (FDM)**
    
    - A cada canal se le asigna una **portadora distinta** y se **modula** (por ejemplo, en AM o SSB).
        
    - Esto **traslada** la señal de cada canal a **distintas posiciones del espectro** (frecuencias centrales diferentes).
        
    - Ejemplo:
        
        - Canal 1 → centrado en 64 kHz
            
        - Canal 2 → centrado en 68 kHz
            
        - Canal 3 → centrado en 72 kHz
            
        - … así hasta cubrir de 60 a 108 kHz.
            
3. **Resultado final**
    
    - El grupo de 12 canales ocupa **48 kHz de ancho total**, pero **ya no están en el mismo rango de frecuencias**:
        
        - Cada canal sigue teniendo sus 4 kHz,
            
        - pero están “escalonados” en frecuencia para no pisarse.
            
4. **Demultiplexación en el receptor**
    
    - Se usan **filtros sintonizados** para aislar la banda de cada canal y llevarla de nuevo a su posición original (0–4 kHz) para que el oyente escuche la voz normal.

### Banda de guarda 

En FDM, cada canal modulado está ubicado en un rango específico de frecuencias.  
Pero, para que no haya **interferencias** entre un canal y el siguiente, se deja un **pequeño espacio vacío** en el espectro entre ellos:

- A ese espacio se le llama **banda de guarda** (_guard band_).
    
- Funciona como una zona de “seguridad” para evitar que las señales “se mezclen” debido a imperfecciones en filtros o modulación

### Canales de distinto ancho de banda

Si en un sistema FDM **los canales no tienen todos el mismo ancho**, pasa lo siguiente:

- Para simplificar el diseño y evitar interferencias, se les asigna **a todos el ancho del canal más grande** (más la banda de guarda).
    
- Esto significa que, aunque un canal requiera menos ancho, “desperdicia” espacio para poder alinearse con los demás.
    

📌 Ejemplo:

- Canal 1: 4 kHz
    
- Canal 2: 5 kHz
    
- Canal 3: 3 kHz  
    ➡ Todos se espacian como si midieran **5 kHz + banda de guarda**, para mantener la separación y alineación en el espectro.

- - -

# OFDM - Multiplexación por división de frecuencias ortogonal 

Se basa en la transformada directa de Fourier.

Trasforma el FDM. En vez de poner un ancho de banda con su frecuencia, la banda de guarda y el otro canal con su ancho de banda y frecuencia, puedo aplicarle a esas señales la transformada discreta de Fourier y calcular que la frecuencia de mayor energía dentro de mi canal calce justo en la posición en la que los vecinos no tienen señal.

![[Pasted image 20250809150859.png]]

>[!important] 
>Esto se usa para comunicaciones **DIGITALES** (la implementación es analógica pero los datos no)**.** FDM se usa para comunicaciones 100% analógicas.

Los módems usan esta técnica.

- - -
# Multiplexación por División de Longitud de Onda (WDM)

- Usada en fibra óptica. Cada señal se transmite con una longitud de onda distinta (color de luz distinto).

- Puede ser CWDM (coarse) o DWDM (dense) según la separación entre canales.

Es lo mismo que FDM pero cuando usás fibra óptica. Cuando estás en frecuencias tan altas como la velocidad de la luz, hacés referencia a la longitud de onda.

Multiplexás luz.

Cuando crean una fibra, el fabricante marca una zona llamada MARCA DE AGUA. Cualquier señal que vos pongas ahí, la fibra no la va a dejar pasar (atenuación total). Vos cuando comprás equipamiento lo hacés para mandar canales en determinadas zonas de transmisión de esa fibra óptica.

El equipamiento más barato está cerca de la marca de agua.

- - -
# Digitales 


# Multiplexación por División de Tiempo (TDM)

TDM se usa para datos y telefonía, para telefonía o solamente para datos.

Funciona ampliando la voz (convirtiéndola en digital) y metiéndolas en slot de tiempos.

Los estadounidenses tenían un sistema y los europeos otro. Para comunicarse, tenían que poner a un interlocutor en el medio.

- - -

# FHSS – Frequency Hoping Spread Spectrum

Sistema de multiplexación basado en tiempo.

Nos ponemos de acuerdo en ciertos saltos de frecuencia. Por ejemplo: en el tiempo 1, el mensaje se emite en la frecuencia f1, en el tiempo 2 en la frecuencia f6, y así. Se usa por motivos de seguridad. Consume mucho ancho de banda.

Si mando una sola comunicación estaría desperdiciando el sistema, por eso es que se envían varias comunicaciones a la vez.

- - -

# DSSS – Direct Secuence Spread Spectrum

Emisor y transmisor se ponen de acuerdo en un pseudo-ruido (señal analógica).

Cuando te quiero mandar un 1, mando ese ruido en fase. Cuando quiero mandar un 0 lo mando con fase cambiada.

Se puede mezclar con OFDM:

![[Pasted image 20250809151122.png]]

Lo usa el wifi (es half-duplex)

- - -
# Multiplexación por División de Tiempo Sincrónica (STDM)

Lo tienen los sistemas de celular.

La antena divide el tiempo entre la cantidad de usuarios. Mientras más usuarios, menos recibe cada uno, y viceversa, entre menos usuarios, más recibe cada uno.

La antena de teléfono censa cada vez que cambia de tiempo y se va adaptando en tiempo acorde a la cantidad de demanda que tenga.

El wifi no sabe hacer esto.