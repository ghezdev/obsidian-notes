
# Unidad 1

### **1.2 Componentes de red**

- **Dispositivos finales (hosts):** generan o reciben datos.  
    Ejemplos: PC, teléfonos, impresoras, cámaras IP.
    
- **Servidores:** proveen información y servicios (web, correo, archivos).
    
- **Clientes:** solicitan servicios a los servidores.
    
- **Redes punto a punto (P2P):** cada dispositivo puede actuar como cliente y servidor. Solo recomendadas en redes pequeñas.
    
- **Dispositivos intermedios:** interconecta dispositivos finales. Gestionan y mueven datos en la red.  
    Ejemplos: switches, routers, APs, firewalls.
    
- **Medios de red:** el camino físico por donde viajan los datos 
	- cobre, utiliza impulsos eléctricos
	- fibra, utiliza pulsos de luz 
	- inalámbrico, utiliza modulación de frecuencias específicas de ondas electromagnéticas
    

---

### **1.3 Representaciones de red y topologías**

- Los **diagramas de topología (o de red)** usan símbolos (NIC, **puerto físico**, **interfaz**) para representar la red. _Nota: “puerto” e “interfaz” pueden usarse como sinónimos en el material._
    
- **Topología física:** ubicación de equipos y cableado. 

- **Topología lógica:** dispositivos, puertos y **esquema de direccionamiento** (cómo fluye la info).

> [!note] 
> NIC significa Network Interface Card (Tarjeta de Interfaz de Red)

---

### **1.4 Tipos comunes de redes**

- **Según tamaño:**
    
    - Hogar/pequeña oficina (SOHO).
        
    - Medianas y grandes (oficinas, empresas).
        
    - Globales (Internet).
        
- **LAN (Local Area Network):** red local en un área geográfica pequeña.
    
- **WAN (Wide Area Network):** interconecta LANs en áreas extensas.
    
- **Internet:** red mundial de LAN y WAN interconectadas, mantenida por organizaciones como **IETF, ICANN e IAB**.
    
- **Intranet:** red privada de una organización.
    
- **Extranet:** acceso controlado a la red de una organización por parte de usuarios externos autorizados.
    

---

### **1.5 Conexiones de Internet**

Las redes convergentes pueden entregar datos, voz y video a través de la misma infraestructura de red.   

---

### **1.6 Conexiones de red confiables**

- Una red debe garantizar:
    
    - **Tolerancia a fallas:** usar redundancia (ej. enlaces y equipos duplicados).
        
    - **Escalabilidad:** crecer sin perder rendimiento.
        
    - **Calidad de servicio (QoS):** priorización de tráfico sensible (voz, video).
        
    - **Seguridad:** proteger datos y dispositivos de accesos no autorizados.


- - -

- - -

# Unidad 2

### **2.1 Acceso a Cisco IOS**

- **Cisco IOS (Internetwork Operating System):** sistema operativo de los dispositivos Cisco.
    
- Componentes de un sistema:
    
    - **Shell:** interfaz (CLI o GUI) que permite al usuario interactuar.
        
    - **Kernel:** comunica hardware ↔ software.
        
    - **Hardware:** la parte física del dispositivo.
        
- **Acceso a IOS:**
    
    - **Consola:** acceso físico para configuración inicial.
        
    - **SSH (Secure Shell):** conexión remota segura (recomendado) a través de una interfaz virtual.
        
    - **Telnet:** conexión remota insegura (envía datos en texto claro).  

---

### **2.2 Navegación del IOS**

- **Modos de comando principales:**
    
    - **Modo EXEC de usuario (`>`):** solo monitoreo básico.
        
    - **Modo EXEC privilegiado (`#`):** acceso total a comandos.
        
- **Modos de configuración:**
    
    - **Global (config)#** → configuración general del dispositivo.
        
    - **Línea (config-line)#** → acceso a consola, SSH, Telnet.
        
    - **Interfaz (config-if)#** → configuración de puertos e interfaces.
        
- Para moverse entre modos se usan comandos como:
    
    - `enable` → entrar a EXEC privilegiado.
        
    - `configure terminal` → entrar a modo global.
        
    - `exit` → salir hacia atrás

    - `end` / `Ctrl+Z` → salir a EXEC privilegiado.

	- `line … / interface … / line console 0` → entrar a submodos o a configuración de línea        

---

### **2.3 Estructura de los comandos**

- Un comando IOS se compone de:
    
    - **Palabras clave:** parámetros fijos del sistema (`ip address`).
        
    - **Argumentos:** valores definidos por el usuario (`192.168.1.1`).

![[Pasted image 20250831131652.png]]


- **Ayudas de IOS:**
    
    - `?` → muestra comandos disponibles.
        
    - `comando ?` → muestra parámetros posibles para un comando.
        
    - `Tab` → autocompleta.
        
    - Mensajes de error ayudan a corregir sintaxis.
        

---

### 2.4 Configuración básica de dispositivos

**1. Nombres de host**

- Primer paso: poner **un nombre único** al equipo (`hostname`) y seguir la guía de nomenclatura (empieza/termina con letra o dígito, sin espacios, <64 chars, solo letras/números/guiones). Para volver al predeterminado: `no hostname`.
    

**2. Endurecimiento mínimo (contraseñas y banner)**

- **Proteger acceso local por consola**:
    
    ```
    line console 0
    password <clave>
    login
    ```
    
- **Proteger modo EXEC privilegiado**:  
    `enable secret <clave>` (encripta la clave del modo privilegiado).
    
- **Proteger acceso remoto (líneas VTY 0–15)** para Telnet/SSH:
    
    ```
    line vty 0 15
    password <clave>
    login
    ```
    
    (Los switches Cisco suelen tener hasta **16 líneas VTY**.)
    
- **Cifrar contraseñas en texto claro** (running/startup):  
    `service password-encryption` + verificación con `show running-config`.
    
- **Banner legal (MOTD)** para advertir accesos no autorizados:  
    `banner motd #<mensaje>#` (el `#` es el **delimitador**).
    

> Nota de los apuntes: **evitar contraseñas débiles**; usar 8+ caracteres, mezcla de tipos, no repetir entre dispositivos.


- - -

### 2.5 Guardar las configuraciones

> **Flash:** almacena IOS y archivos. No pierde su contenido cuando el dispositivo está apagado

**Dónde se guarda la configuración**

- **startup-config** (NVRAM): lo que el dispositivo **usa al arrancar**.
    
- **running-config** (RAM): la **configuración actual** (volátil).
    
- Guardar cambios: `copy running-config startup-config`.
    

**Volver atrás si te equivocaste**

- Si **NO** guardaste:
    
    - borra comandos puntuales **o** `reload` (corta el servicio un momento).
        
- Si **SÍ** guardaste:
    
    - `erase startup-config` y luego `reload`.
        

**Respaldar a texto (log de sesión)**

- En el emulador (PuTTY/TeraTerm): habilitar **session logging** y ejecutar `show running-config`/`show startup-config`; queda todo en un archivo (p.ej. _MySwitchLogs_).
    

---

### 2.6 Puertos e interfaces / Direcciones

> Las comunicaciones de red dependen de las interfaces de los dispositivos para usuarios finales

> Las direcciones IP es el principal medio para permitir que los dispositivos se ubiquen entre sí

- Las **interfaces/puertos** y el **medio** (cobre, fibra, coaxial, inalámbrico) determinan 
	- distancia 
	- entorno, 
	- velocidad/capacidad 
	- costo del enlace.
    
- **Direcciones IPv4**: 
	- “notación decimal con puntos” entre 0 y 255
	- 32 bits
	- Ej: 192.168.1.10

- **Máscara de subred IPv4:**
	- determina la subred particular a la que pertenece el dispositivo
	- “notación decimal con puntos” entre 0 y 255
	- 32 bits
	- separa **red/host**;
	- Ej: 255.255.255.0

- **Puerta de enlace predeterminada / Default Gateway:** 
	- “notación decimal con puntos” entre 0 y 255
	- 32 bits
	- es la IP del router para salir a otras redes (e Internet).
	- Ej: 192.168.1.1
    
- **Direcciones IPv6**: 128 bits en **hex** (32 dígitos), grupos separados por `:`
    

---

### 2.7 Configuración de direcciones IP (host y switch)

**En hosts (Windows)**

- **Manual (IPv4)**: Panel de control → Centro de redes → Cambiar configuración del adaptador → Propiedades de **TCP/IPv4** → configurar **IP/máscara/puerta/DNS**.
    
- **Automática (DHCP)**: misma ruta, marcar “**Obtener una dirección IP automáticamente**” y “**DNS automáticamente**”.
    
- Nota: para **IPv6**, el material menciona **DHCPv6** y **SLAAC**.
    

**En el switch (SVI para administración remota)**

- **Configurar SVI** (normalmente `Vlan1`) con **IP y máscara** y habilitarla:
    
    ```
    interface vlan 1
    ip address <ip> <mask>
    no shutdown 
    ```
    
- En el propio módulo 2 se remarca que, para administrar remotamente, además debes definir **puerta de enlace predeterminada** del switch junto con IP/máscara.



# Unidad 3
## 3.1 El Reglamento (reglas de comunicación)

- **Idea clave:** no alcanza con “estar conectados”; **emisor, receptor y medio** deben **ponerse de acuerdo en cómo** se comunican (formato, turnos, confirmaciones, etc.). Eso lo fijan los **protocolos**, que son las “reglas del juego”.

- **Reglas que deben cumplir todo protocolo:**
	- Existencia de emisor y receptor 
	- Existencia de idioma o gramática común 
	- Velocidad y momento de carga 
	- Requisitos de confirmación
    
- **Requisitos que todo protocolo debe contemplar:**  
    - **codificación** (cómo convertir datos a señales y volver a interpretarlos)
    - **formato/encapsulamiento** (estructura del mensaje)
    - **tamaño** (cuánto puede medir)
    - **temporización** (control de flujo, tiempos de espera, método de acceso al medio)
    - **opciones de entrega** (unicast o unidifusion/multicast o multidifusion/broadcast o difusión).

> [!note] 
> Reglas que rijen las colisiones, cuando más de un dispositivo envía tráfico al mismos tiempo y los mensajes se dañan
> Protocolos proactivos: evitan colisiones.
> Protocolos reactivos: establecen metodos de recuperación después de que se produzca la colisión


> [!note] 
> **Unicast**: Comunicación **uno a uno**. Un dispositivo le habla directamente a otro.
> **Broadcast**: Comunicación **uno a todos** (en la misma red). Un dispositivo envía un mensaje y todos los equipos en esa red lo reciben.
> **Multicast**: Comunicación **uno a varios (grupo específico)**. El emisor manda un mensaje y solo los que se unieron a ese grupo lo reciben.

   
- **Notas finas de entrega:** en **IPv4** existe **broadcast**; en **IPv6** no (se usa **multicast** y más adelante se verá **anycast**).
    
- **Ejemplo rápido:** “página web”. El cliente debe hablar el mismo **formato** (HTTP), respetar **tamaños** (MTU/MSS), **temporización** (timeouts/turnos) y usar la **opción de entrega** adecuada (unicast al servidor).
    

---

## 3.2 Protocolos (qué son y cómo se usan)

- **Qué son:** reglas comunes que los dispositivos implementan en **software**, **hardware** o ambos; cada protocolo tiene **función** y **formato** definidos.
    
- **Interacción:** en una red real **conviven múltiples protocolos**, cada uno se ocupa de “su parte” y se **encadena** con los demás (capas).

Ejemplos de protocolos de internet: 
- HTTP 
- TCP 
- IP
- Ethernet

---

## 3.3 Suites de protocolos (trabajar en capas)

- **Qué es una suite:** **conjunto de protocolos** que funcionan coordinados y **en capas** (las **superiores** tratan la app; las **inferiores** mueven bits y dan servicios a las de arriba) para realizar una función de comunicación
    
- **Principales suites:** **TCP/IP** (la de Internet, mantenida por la **IETF**), **OSI** (modelo de referencia de ISO/UIT), y suites históricas **AppleTalk** y **Novell NetWare**.
    
- **Dónde operan los protocolos en TCP/IP:** **Aplicación, Transporte, Internet**; en acceso a red, lo más común son **Ethernet** y **WLAN**.
    
- **Ejemplo visual del curso:** servidor web **encapsula** y envía la página; el cliente **desencapsula** para que la vea el navegador.

![[Pasted image 20250914001753.png]]

---

**NO CREO QUE TOME ESTO**
## 3.4 Organizaciones de estándares (quién define las reglas)

- **Ecosistema Internet/TCP-IP:** **ISOC** (visión global), **IAB** (arquitectura/estándares), **IETF** (desarrolla/mantiene tecnologías de Internet y TCP/IP), **IRTF** (investigación a largo plazo).
    
- **Gestión de nombres/direcciones:** **ICANN** coordina y **IANA** administra **IP, DNS e identificadores** de protocolo.
    

---

## 3.5 Modelos de referencia (por qué “en capas”)

- **Para qué sirve un modelo en capas (OSI, TCP/IP):** facilita **diseño de protocolos**, **interoperabilidad** entre fabricantes, **aisla cambios** tecnológicos de una capa para no romper las demás y da un **lenguaje común** para describir funciones.

Modelo OSI 

![[Pasted image 20250914002257.png]]

Modelo TCP/IP

![[Pasted image 20250914002311.png]]

- **Comparación OSI ↔ TCP/IP:** OSI **detalla** lo que TCP/IP agrupa (p. ej., acceso a la red y aplicación), y explica que **capas 1–2 (OSI)** tratan acceso al medio y envío físico.

---

## 3.6 Encapsulamiento de datos (cómo viaja “de verdad”)

- **Segmentación:** dividir mensajes en **segmentos**, acelerando el envío y hace la retransmisión **más eficiente** (solo se reenvía lo perdido).

- **Multiplexación:** entrelazar flujos segmentados

- **Secuenciación de mensajes:** proceso de numerar los segmentos para que el mensaje pueda volver a ensamblarse en el destino. **TCP** es el responsable de numerar (**secuencia**) para rearmar en destino.

- **Encapsulación:** proceso descendente en el que los protocolos agregan su información a los datos

- **Desencapsulación:** se hace a meidad que se mueven hacia arriba en la pila. Cuando una capa completa su proceso, esa capa elimina su encabezado y lo pasa al siguiente nivel
    
- **PDU por capa:** cada etapa **agrega su propio encabezado**; el curso nombra las **PDU** conforme a TCP/IP (datos/segmento/paquete/trama/bits).

![[Pasted image 20250914003004.png]]


- - -

## 3.7 Acceso a los datos

La **Capa 2 (MAC)** y **Capa 3 (IP)** trabajan en equipo para que un dato salga del origen y llegue al destino.

La capa 2 cambia el dato de origen y destino salto a salto y las otras **se mantienen** extremo a extremo.

### 1) Rol de cada direccionamiento

- **Direcciones IP (L3):** IP **origen** e **IP destino** identifican extremos y llevan el **paquete** hasta el dispositivo final (misma red o remota). Además, la IP tiene **parte de red/prefijo** y **parte de host/ID de interfaz**.
    
- **Direcciones MAC (L2):** sirven para mover la **trama** **solo dentro de un enlace** (local al segmento). En cada tramo hay una **MAC origen** (la NIC que envía) y una **MAC destino** (la NIC del siguiente salto).
    

### 2) Caso A — Dispositivos en la **misma red**

- Si origen y destino comparten la **misma porción de red**, la trama Ethernet usa **la MAC real del host destino**; la **MAC origen** es la del iniciador en ese enlace.
    

### 3) Caso B — Destino en **red remota**

- El host **no** puede enviar directo a la MAC del destino: envía al **router puerta de enlace (DGW)**. Capa 3 entrega a Capa 2 la **IP de la DGW** para armar la trama hacia ese router.
    
- **Salto 1:** MAC **origen = NIC del host**, MAC **destino = NIC del router (DGW)**.
    
- **Salto 2 y siguientes:** cada router **desencapsula** la trama, mantiene el **paquete IP** y **re-encapsula** con **nuevas MAC** hacia el próximo salto.
    
- **Dato clave:** el **paquete IP no se modifica** durante el camino; lo que **cambia** en cada enlace es la **trama/MAC**.
    

### 4) Idea final (lo que te piden saber)

- **L3 (IP)**: guía **extremo-a-extremo** (IP origen/destino permanecen). **L2 (MAC)**: entrega **salto-a-salto** (MAC cambia en cada enlace). Si el destino es remoto, **primera trama → DGW**; luego cada router rehace la trama para el siguiente tramo.


- - -

# Unidad 4

## 4.1 Propósito de la capa física

- Antes de cualquier comunicación, el dispositivo debe **conectarse físicamente** (cableado o inalámbrico) mediante su **NIC**; no todas las conexiones rinden igual.
    
- La capa física **transporta bits**: toma la **trama de Capa 2**, la **codifica** en señales y la envía por el medio; el siguiente equipo **recibe bits**, vuelve a **encapsular la trama** y decide su reenvío.
    

## 4.2 Características de la capa física

- Los **estándares** cubren tres áreas: **componentes físicos**, **codificación** y **señalización** (qué hardware/medios y conectores se usan; cómo se representa la secuencia de bits; y cómo se “pinta” un 0/1 en el medio).
    
- **Codificación**: convierte bits en patrones **reconocibles** (ej.: **Manchester**, **4B/5B**, **8B/10B**).
    
- **Señalización** según el medio: **eléctrica** (cobre), **luz** (fibra), **radio/microondas** (inalámbrico).
    
- **Ancho de banda**: capacidad (cuántos **bits/s** puede transportar el medio); depende del medio, la tecnología y **las leyes físicas**.

- **Capacidad de transferencia útil:** medida de datos utilizables transferidos durante un período de tiempo determinado. $Goodput = Rendimiento - sobrecarga\ de\ tráfico$

## 4.3 Medios de **cobre** (visión general)

- Ventajas: 
	- **económico**
	- fácil de instalar
	- baja resistencia al flujo de corriente eléctrica 

- **Limitaciones**: 
	- **Atenuación** (a mayor longitud, menor señal)
	- **EMI/RFI** e **interferencia entre pares** (**crosstalk**). 

**Mitigación**: respetar **longitudes máximas**, usar **blindaje/conexión a tierra** y **pares trenzados**.
    
- **Tipos**:
    
    - **UTP** (más común, termina en **RJ-45**). La **cubierta** protege; los **pares trenzados** reducen interferencias.
        
    - **STP** (mejor contra ruido, **más caro/difícil**); agrega **blindajes** por par y general; también usa **RJ-45**.
        
    - **Coaxial** (malla/lamina + dieléctrico + conductor): hoy típico en **antenas** y **Internet por cable** en el cliente.
        

## 4.4 **Cableado UTP** (propiedades y estándares)

- **Propiedades**: cuatro **pares** trenzados **sin blindaje** dentro de una funda; limita diafonía por **cancelación** (polaridad opuesta en cada par) y por **distintos giros por par**.
    
- **Estándares TIA/EIA-568**: definen **tipos/longitudes**, **conectores**, **terminaciones** y **pruebas**; categorías **Cat3**, **Cat5/5e**, **Cat6**; conector **RJ-45** y **terminación correcta** (directo/cruzado).

- Host a host, cable cruzado
  Host a dispositivo de red, cable directo.

## 4.5 **Fibra óptica** (propiedades, tipos y conectores)

- Codifica bits como **pulsos de luz** que viajan por un **núcleo de vidrio** con **pérdida mínima**.

- Menos económico que UTP. 
- Menos susceptible a la atenuación e inmune al EMI/RFI
    
- **Tipos**:
    
    - **Monomodo (SMF)**: **núcleo muy pequeño**, usa **láser** (más costoso), **larga distancia**.
        
    - **Multimodo (MMF)**: **núcleo mayor**, usa **LED**; varias trayectorias → **dispersión** mayor; típico hasta **10 Gbps/550 m**.
        
- **Conectores** comunes: **ST**, **SC**, **LC** (simplex/dúplex). **Jumpers**/patch cords SM o MM; **colores**: **amarillo** (SM), **naranja/aqua** (MM).
    
- **Uso típico**: **troncales/backbone** de alto tráfico, **punto a punto** entre salas de distribución y **entre edificios** en campus.
    

## 4.6 **Medios inalámbricos** (propiedades, límites y WLAN)

- Transportan **señales electromagnéticas** (RF/microondas), maximizan **movilidad**, pero sufren **limitaciones de cobertura** y **seguridad**; en **medio compartido** operan **semidúplex** y muchos usuarios reducen **ancho de banda por usuario**.
    
- **Estándares** (física + enlace): **Wi-Fi (802.11)**, **Bluetooth (802.15)**, **WiMAX (802.16)**, **Zigbee (802.15.4)**.
    
- **WLAN**: requiere **AP** (concentra inalámbrico y lo une a la red de cobre) y **NIC inalámbricas** en los hosts; **asegurar compatibilidad** y **políticas de seguridad**.

- - -

# Unidad 5
## 5.1 Sistema de **numeración binaria** (base 2)

- **Qué es y por qué importa:** las computadoras y equipos de red “piensan” en **bits (0/1)**. **IPv4** se representa internamente en **32 bits** divididos en **4 octetos** de **8 bits** (luego lo vemos como “decimal punteado” para humanos).
    
- **Notación posicional:** el valor de cada bit depende de su **posición** (128,64,32,16,8,4,2,1 en un octeto).
    
- **Convertir binario → decimal (ejemplo real de un IPv4):**  
    `11000000.10101000.00001011.00001010` → **192.168.11.10** (sumando los valores posicionales en cada octeto).
    
- **Convertir decimal → binario (mecánica que pide el curso):**  
    Partís en 128 y vas restando: si el número ≥ valor posicional, ponés **1** y restás; si no, **0** (seguís con 64, 32, …, 1).
    
    - **Ejemplo:** 168 → **10101000** (128=1, 64=0, 32=1, 16=0, 8=1, 4=0, 2=0, 1=0).
        
- **Idea clave que recalca el módulo:** **routers y PCs entienden binario; nosotros trabajamos en decimal**, por eso hay que dominar ambas vistas.
    

---

## 5.2 Sistema **hexadecimal** (base 16)

- **Qué es y dónde se usa:** base **16** con dígitos **0–9** y **A–F**; es compacto (cada **4 bits** ≡ **1** dígito hex). Se usa para **IPv6** y **direcciones MAC**.
    
- **IPv6 en hex:** tiene **128 bits**, por eso se escribe con **32 dígitos hex** agrupados en **8 “hextetos”** (cada grupo = 16 bits).
    
- **Decimal → Hex (método del curso):**
    
    1. Pasás a **binario de 8 bits**.
        
    2. Agrupás en **nibbles** (grupos de 4).
        
    3. Cada nibble → su **dígito hex**.
        
    
    - **Ejemplo:** 168 → bin `10101000` → `1010` `1000` → **A8**.
        
- **Hex → Decimal (método del curso):**
    
    1. Cada dígito hex → **4 bits**.
        
    2. Reagrupás en 8 bits (si hace falta).
        
    3. Ese binario → **decimal**.
        
    
    - **Ejemplo:** **D2** → `1101 0010` → `11100010` (agrupado) → **210**.


- - -

# Unidad 6
## 6.1 Propósito de la capa de enlace de datos

- **Qué hace:** conecta lógicamente **NIC ↔ NIC** entre dispositivos finales, **encapsula** paquetes de Capa 3 (**IPv4/IPv6**) en **tramas** de Capa 2, y realiza **detección de errores** para descartar tramas corruptas.
    
- **Subcapas IEEE 802:**
    
    - **LLC (802.2):** puentea **software** de capas superiores con **hardware** inferior.
        
    - **MAC (802.3/802.11/802.15):** **encapsulación** y **acceso al medio**.
        
- **Qué pasa en cada salto (router):** recibe **trama**, la **desencapsula** para ver el **paquete IP**, la **vuelve a encapsular** según el siguiente medio y la **reenvía** al siguiente segmento.
    
- **Quién define estándares:** IEEE, **ITU**, **ISO**, **ANSI**.
    

> **Para qué te sirve:** entender que Capa 2 es la “**fábrica de tramas**” y el **portero del cable/aire**: decide **cómo** se envía por cada enlace y **cuándo** puede hablar cada NIC.

---

## 6.2 Topologías

### Físicas vs lógicas

- **Física:** cómo están **cableados/conectados** los equipos.
    
- **Lógica:** cómo **fluye** el tráfico (interfaces, **IP** y reglas de reenvío).
    

### WAN (físicas típicas)

- **Punto a punto:** un **enlace dedicado** entre dos nodos; protocolos simples (no comparten medio).
    
- **Hub-and-spoke:** un **sitio central** enlaza varias sucursales (estrella).
    
- **Malla:** **alta disponibilidad**; cada sitio conecta con todos (más enlaces).
    

### LAN (físicas típicas)

- **Estrella / estrella extendida:** lo más común; **fácil de instalar**, **escalable** y **fácil de diagnosticar**.
    
- Heredadas: **bus** y **anillo** (hoy casi sólo históricas).
    

### Dúplex y acceso al medio

- **Semidúplex:** un equipo **envía o recibe** (no ambos); típico en **WLAN** o hubs antiguos.
    
- **Dúplex completo:** **envío/recepción simultáneos**; **switches** actuales operan así.
    
- **Métodos de acceso (cuando hay contención):**
    
    - **CSMA/CD** (Ethernet heredada, semidúplex): si colisiona, **detecta**, **espera aleatorio** y **retransmite**.
        
    - **CSMA/CA** (802.11): **previene** colisiones indicando la **duración** prevista; los demás **esperan**.
        
    - **Acceso controlado** (determinista, p. ej., **Token Ring**, **ARCNET**).
        

> **Para qué te sirve:** identificar **cómo se organiza** la red (física/lógica), qué **método de acceso** aplica y **por qué** en switches modernos **no** usamos CSMA/CD.

---

## 6.3 **Trama** del enlace de datos

- **Estructura mínima:** **encabezado + datos + tráiler** (**FCS/CRC**); los **campos** cambian según el **protocolo** de Capa 2 (Ethernet, 802.11, PPP, etc.).
    
- **Direcciones de Capa 2 (MAC):** están en el **encabezado**, sirven **solo localmente** en el **enlace** y se **actualizan en cada salto**.
    
- **Protocolos según medio/topología:**
    
    - **LAN:** **Ethernet (802.3)**, **WLAN (802.11)**.
        
    - **WAN:** **PPP**, **HDLC**, **Frame Relay** (histórico). Cada uno trae su propio **control de acceso al medio**.
        

> **Para qué te sirve:** leer una trama (qué **campos** miran los equipos), y comprender que la **trama cambia** de enlace en enlace, pero el **paquete IP** (Capa 3) **permanece** igual durante todo el recorrido. (Esto lo verás reforzado en 3.7/Unidad 3 y en Unidad 9 con **ARP/ND**).


- - -

# Unidad 7
## 7.1 Tramas de Ethernet

- **Dónde opera y quién norma:** Ethernet trabaja en **capa de enlace** y **capa física**; se apoya en **IEEE 802.2 (LLC)** y **IEEE 802.3 (MAC)**. La LLC identifica el protocolo de red (IPv4/IPv6) y la MAC encapsula y controla el acceso al medio.
    
- **Qué lleva la trama:** **MAC origen/destino**, **datos** y **FCS** para **detección de errores**. (Encapsulado MAC = estructura de trama + direccionamiento + FCS).
    
- **Acceso al medio hoy:** en switches **full-duplex** **no** se usa **CSMA/CD** (eso era para bus/hubs semidúplex heredados).
    

**Qué te deja:** identificar campos clave de la trama y ubicar a LLC/MAC, entendiendo por qué **no hay CSMA/CD** en redes conmutadas actuales.

---

## 7.2 Dirección MAC de Ethernet

- **Formato:** **48 bits**, escritos como **12 hex** (6 bytes). Es la **identidad L2** de la NIC.
    
- **Unicast / Broadcast / Multicast:** las MAC multicast típicas mapean a **01-00-5E** (si el payload es IPv4) y **33-33** (si es IPv6). Broadcast se inunda en la LAN; multicast se inunda salvo que el switch tenga **snooping** configurado.
    

**Qué te deja:** leer una MAC, distinguir **unicast/broadcast/multicast** y relacionar multicast IP con su **MAC de grupo**.

---

## 7.3 La tabla de direcciones MAC (CAM) y el comportamiento del switch

- **Base del switching L2:** el switch **decide solo con MAC** (no “mira” el protocolo dentro de los datos). Al encender, su **tabla MAC** está **vacía** (también llamada **CAM**).
    
- **Aprendizaje:** toma la **MAC origen** y la **asocia** al **puerto de entrada**; **refresca** el temporizador y, por defecto, las entradas **caducan** (~**5 min**).
    
- **Reenvío / Inundación / Filtrado:**
    
    - Si la **MAC destino** está en tabla → **reenvía** solo a ese puerto (**filtra** el resto).
        
    - Si **no** está → **inunda** por todos menos el de entrada (**unknown unicast flood**).
        
    - **Broadcast** y **multicast** → también se **inundan**. Con el tiempo, al **llenarse** la tabla, el switch **filtra** más e **inunda** menos.
        

**Qué te deja:** explicar el ciclo **learn → lookup → forward/flood → age** y predecir qué hará el switch según conozca o no la MAC destino.

---

## 7.4 Velocidades del switch y métodos de reenvío

- **Métodos de conmutación:**
    
    - **Store-and-Forward:** recibe la **trama completa**, valida **FCS** y recién **reenvía** (mayor integridad; **necesario** para **QoS** en redes convergentes).
        
    - **Cut-Through:** empieza a reenviar al leer la **MAC destino** (menor latencia, **no** verifica FCS).
        
    - **Fragment-Free:** lee los **primeros 64 bytes** para evitar propagar tramas con colisiones/errores típicos del inicio.
        
- **Búferes y conmutación asimétrica:** el switch **almacena** tramas si el puerto de salida está ocupado o a otra velocidad (útil p. ej. para **puerto de servidor** con más ancho de banda).
    
- **Velocidad/Dúplex/Autonegociación:** hay que **hacer coincidir** velocidad y **dúplex** en ambos extremos; **Gigabit** es **solo full-duplex**. **Desajuste de dúplex** es causa común de bajo rendimiento; mejor práctica: **full-duplex** en ambos.
    
- **Auto-MDIX:** elimina la preocupación de usar cable **directo o cruzado** (el puerto se adapta).
    

**Qué te deja:** elegir **método de switching** (latencia vs integridad/QoS), entender **buffers/asimetría**, y evitar **problemas de dúplex/velocidad** en enlaces.



- - -

