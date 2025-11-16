# **MÓDULO 8 – Capa de Red (ITN v7.0)**

### **8.1 Características de la Capa de Red**

#### 📘 Propósito:

La **capa de red (Capa 3 del modelo OSI)** permite que los dispositivos **intercambien datos entre redes diferentes**.  
Su protocolo principal es **IP (Internet Protocol)**, tanto en **versión 4 (IPv4)** como en **versión 6 (IPv6)**

#### 🔹 Funciones básicas:

1. **Direccionamiento de terminales:**
    
    - Cada dispositivo tiene una **dirección lógica (IP)**.
        
    - Ejemplo: El PC A (192.168.1.10) envía datos al servidor B (10.0.0.2).  
        La capa de red usa esas direcciones IP para encontrar la mejor ruta.
        
2. **Encapsulamiento:**
    
    - La capa de red **recibe un segmento** de la capa de transporte (TCP/UDP) y lo **encapsula en un paquete IP**.
        
    - Este paquete incluye las **direcciones IP de origen y destino**.
        
3. **Enrutamiento (routing):**
    
    - Los **routers** deciden **qué camino** sigue el paquete hasta llegar a destino.
        
    - Esto se basa en **tablas de enrutamiento**.
        
4. **Desencapsulamiento:**
    
    - Cuando el paquete llega al destino, se **extrae la información** y se pasa al nivel superior (transporte).
        

---

### **8.2 Encapsulación IP**

#### 🔹 Concepto:

- IP **no modifica el segmento** de transporte (por ejemplo TCP o UDP), solo lo envuelve en un **paquete IP**.
    
- Los **routers examinan el encabezado IP** en cada salto (cada router que atraviesa la red).
    

#### 🔹 Características clave de IP:

- **Sin conexión (Connectionless):**  
    IP **no establece una sesión previa** con el destino.  
    Ejemplo: Enviar una carta sin asegurarte de que la persona esté en casa.  
    No hay mensajes de “confirmación” ni control de flujo.
    
- **Mejor esfuerzo (Best Effort):**  
    IP **no garantiza** que el paquete llegue o que llegue en orden.  
    Si un paquete se pierde, IP **no lo reenvía**. Esa tarea la hace TCP.
    
- **Independencia de medios:**  
    IP **funciona sobre cualquier tipo de red**: cobre, fibra, Wi-Fi, etc.  
    No le importa el tipo de medio ni la tecnología física.
    

---

### **8.3 Fragmentación y MTU (Unidad de Transmisión Máxima)**

#### 🔹 MTU (Maximum Transmission Unit):

- Es **el tamaño máximo de paquete** que puede enviarse a través de una interfaz de red sin fragmentar.
    
- Por ejemplo:
    
    - Ethernet estándar: **1500 bytes**.
        
    - WAN PPPoE: **1492 bytes**.
        

#### 🔹 Fragmentación:

- Si el paquete IP **es más grande que la MTU**, IPv4 **puede dividirlo en fragmentos**.
    
- Cada fragmento viaja como un paquete independiente con su propio encabezado IP.
    

⚠️ **IPv6 NO permite fragmentación** por los routers intermedios; solo el host origen puede fragmentar antes de enviar.

#### 🧠 Ejemplo:

Si un router pasa de una red Ethernet (MTU 1500) a una WAN con MTU 600, el paquete IPv4 se **fragmenta en partes más pequeñas**.  
Esto **aumenta la latencia**, ya que cada fragmento se procesa individualmente.

---

### **8.4 Características del Protocolo IP (Resumen general)**

|Propiedad|Descripción|
|---|---|
|**No confiable**|IP no verifica si los datos llegaron o se corrompieron.|
|**Sin conexión**|No hay comunicación previa antes de enviar datos.|
|**Mejor esfuerzo**|No hay reenvíos ni control de errores.|
|**Independiente de medios**|Funciona sobre cualquier red física.|
|**Encapsulación**|Toma segmentos y los coloca dentro de paquetes IP.|
|**Enrutamiento**|Selecciona la mejor ruta para el envío.|

---

### **8.5 Encabezado IPv4**

#### 🔹 Estructura básica:

El **encabezado IPv4** tiene **20 a 60 bytes**, dependiendo de los campos opcionales.  
Contiene **campos esenciales** para el envío del paquete.

#### 🔹 Campos importantes:

|Campo|Función|
|---|---|
|**Versión (4 bits)**|Identifica la versión del protocolo (4 para IPv4).|
|**Longitud del encabezado (IHL)**|Tamaño del encabezado IP.|
|**Longitud total**|Tamaño total del paquete (datos + encabezado).|
|**Identificación, banderas, desplazamiento de fragmentos**|Usados para la fragmentación.|
|**TTL (Time To Live)**|Límite de saltos. Se reduce en cada router; si llega a 0, se descarta el paquete.|
|**Protocolo**|Indica el protocolo de capa 4 (6 = TCP, 17 = UDP).|
|**Suma de comprobación del encabezado**|Verifica errores en el encabezado.|
|**Dirección IP de origen y destino**|Indican quién envía y quién recibe.|

---

### **8.6 Encabezado IPv6 (Introducción breve)**

Aunque se detalla más en el **módulo 12**, aquí se menciona que:

- IPv6 **simplifica el encabezado** (tamaño fijo de 40 bytes).
    
- **Elimina campos innecesarios** como checksum y fragmentación.
    
- Añade nuevos campos para **rendimiento y seguridad**, como el “Flow Label”.
    

---

### 💡 **Resumen general de la Unidad 8**

| Concepto clave              | Explicación corta                                   |
| --------------------------- | --------------------------------------------------- |
| **Capa 3 (Red)**            | Mueve paquetes entre redes diferentes.              |
| **Protocolos principales**  | IPv4 e IPv6.                                        |
| **Encapsulación**           | IP mete el segmento (TCP/UDP) dentro de un paquete. |
| **Routing**                 | Selecciona el mejor camino mediante routers.        |
| **Best Effort**             | IP no garantiza entrega.                            |
| **Sin conexión**            | No establece sesión previa.                         |
| **Independencia de medios** | IP trabaja sobre cualquier red física.              |
| **MTU y fragmentación**     | IPv4 puede fragmentar; IPv6 no.                     |
| **TTL**                     | Evita bucles infinitos en los routers.              |


# **MÓDULO 9 – Resolución de Direcciones (ITN v7.0)**

## 🧠 **9.1 Direcciones MAC e IP**

Cada dispositivo en una red tiene **dos direcciones diferentes pero complementarias**:

| Tipo de dirección | Capa OSI                 | Función                                                             | Ejemplo             |
| ----------------- | ------------------------ | ------------------------------------------------------------------- | ------------------- |
| **MAC**           | Capa 2 (Enlace de datos) | Identifica un dispositivo dentro de la misma red local (NIC a NIC). | `00:1A:2B:3C:4D:5E` |
| **IP**            | Capa 3 (Red)             | Identifica el dispositivo de forma lógica en una red.               | `192.168.1.10`      |

### 🔹 **Destino en la misma red**

Si el **dispositivo de destino está en la misma red local**, se envía directamente a su **dirección MAC**.

#### Ejemplo:

- PC1 → IP: 192.168.10.5
    
- PC2 → IP: 192.168.10.8  
    Ambos están en la red **192.168.10.0/24**.  
    ➡️ PC1 enviará su **trama Ethernet directamente a la MAC de PC2.**
    

### 🔹 **Destino en una red remota**

Si el **destino está en otra red**, el paquete **debe salir por la puerta de enlace predeterminada** (router).

- PC1 (192.168.10.5) quiere comunicarse con Server (10.0.0.10).
    
- El router tiene la IP **192.168.10.1** (gateway).  
    ➡️ La trama se envía **a la MAC del router**, no a la del servidor.
    

| Campo       | Valor                             |
| ----------- | --------------------------------- |
| IP destino  | 10.0.0.10                         |
| MAC destino | MAC del router (puerta de enlace) |

### 🔹 **Protocolos utilizados para resolver direcciones**

| Protocolo                             | Función                                      | Versión de IP |
| ------------------------------------- | -------------------------------------------- | ------------- |
| **ARP (Address Resolution Protocol)** | Asocia una IP a una dirección MAC (IPv4).    | IPv4          |
| **ICMPv6 Neighbor Discovery (ND)**    | Hace la misma función que ARP, pero en IPv6. | IPv6          |

---

## ⚙️ **9.2 ARP (Address Resolution Protocol)**

### 📘 **Descripción general**

ARP se usa cuando un dispositivo conoce la **dirección IP** del destino, pero **no su dirección MAC**.  
Sirve para “traducir” la IP a una dirección física.

---

### 🔹 **Funciones principales de ARP**

1. **Resolver direcciones IPv4 → MAC**
    
    - Encuentra la dirección MAC asociada a una IP.
        
2. **Mantener una tabla ARP**
    
    - Guarda temporalmente las asociaciones IP–MAC aprendidas.
        
    - Esta tabla evita tener que enviar solicitudes ARP cada vez.
        

---

### 🔹 **Cómo funciona ARP paso a paso**

#### Ejemplo:

PC1 (192.168.10.5) quiere enviar datos a PC2 (192.168.10.8).

1. **PC1 busca en su tabla ARP** la dirección MAC correspondiente a 192.168.10.8.
    
    - Si la encuentra ✅, la usa directamente.
        
    - Si no la encuentra ❌, pasa al paso 2.
        
2. **PC1 envía una solicitud ARP (ARP Request)**:
    
    - Mensaje tipo **broadcast** (a todas las MAC de la red):  
        “¿Quién tiene la IP 192.168.10.8? Respóndeme con tu MAC.”
        
3. **PC2 responde (ARP Reply)** con su dirección MAC:
    
    - “192.168.10.8 soy yo, mi MAC es 00:11:22:33:44:55.”
        
4. **PC1 guarda la información en su tabla ARP**:
    
    - `192.168.10.8 → 00:11:22:33:44:55`
        
5. A partir de ahora, PC1 puede enviar tramas directamente a esa MAC.
    

---

### 🔹 **Estructura del mensaje ARP**

| Tipo de mensaje                 | Descripción                                                                           |
| ------------------------------- | ------------------------------------------------------------------------------------- |
| **Solicitud ARP (ARP Request)** | Pregunta quién tiene una IP específica. Se envía por broadcast (`FF:FF:FF:FF:FF:FF`). |
| **Respuesta ARP (ARP Reply)**   | El dispositivo con esa IP responde con su dirección MAC. Se envía por unicast.        |

---

### 🔹 **Tabla ARP**

- Cada dispositivo tiene una **tabla ARP** que almacena los pares IP ↔ MAC.
    
- Las entradas son **temporales** (tienen un tiempo de expiración).
    
- En Cisco y Windows, se pueden ver con:
    
    - Cisco: `show ip arp`
        
    - Windows: `arp -a`
        

#### Ejemplo:

| Dirección IP | Dirección MAC     | Tipo     |
| ------------ | ----------------- | -------- |
| 192.168.10.8 | 00:11:22:33:44:55 | Dinámica |
| 192.168.10.1 | 00:AA:BB:CC:DD:EE | Dinámica |

---

### 🔹 **Eliminación de entradas ARP**

- Las entradas **caducan después de un tiempo** determinado (depende del sistema operativo).
    
- También se pueden **borrar manualmente** si se sospecha de errores o cambios de red.
    

---

## 🌐 **9.3 Resolución en IPv6 – ICMPv6 y NDP**

En IPv6 **no se usa ARP**.  
El protocolo **ICMPv6 (Internet Control Message Protocol for IPv6)** realiza las mismas funciones mediante el **Neighbor Discovery Protocol (NDP)**.

### 🔹 **Funciones de ICMPv6 ND**

1. **Solicitar dirección MAC de otro dispositivo** (equivalente a ARP).
    
    - Usa mensajes de:
        
        - **Neighbor Solicitation (NS)**
            
        - **Neighbor Advertisement (NA)**
            
2. **Detección de routers y prefijos**:
    
    - Los routers IPv6 envían periódicamente:
        
        - **Router Advertisement (RA)** → anuncia su presencia y prefijos de red.
            
    - Los hosts pueden enviar:
        
        - **Router Solicitation (RS)** → piden información de routers.
            
3. **Detección de direcciones duplicadas (DAD)**:
    
    - Antes de usar una IP, el host envía una solicitud NS para asegurarse de que nadie más la tenga.
        
4. **Mensajes de redireccionamiento:**
    
    - Permiten informar al host de una mejor ruta para llegar a un destino.
        

---

### 📊 **Comparación ARP vs ICMPv6 ND**

| Característica                      | IPv4 (ARP)      | IPv6 (ICMPv6 ND)                                       |
| ----------------------------------- | --------------- | ------------------------------------------------------ |
| Protocolo usado                     | ARP             | ICMPv6                                                 |
| Tipo de mensajes                    | Request / Reply | Solicitation / Advertisement                           |
| Broadcast                           | Sí              | No (usa multicast, más eficiente)                      |
| Detección de routers                | No              | Sí                                                     |
| Detección de direcciones duplicadas | No              | Sí                                                     |
| Seguridad                           | Ninguna         | Incluye opciones para autenticación y seguridad (SEND) |

---

## 🧠 **Resumen general del Módulo 9**

| Concepto                   | Explicación                                                        |
| -------------------------- | ------------------------------------------------------------------ |
| **Dirección MAC**          | Física, capa 2, identifica una NIC.                                |
| **Dirección IP**           | Lógica, capa 3, identifica un host en una red.                     |
| **Misma red**              | Se usa la MAC del destino.                                         |
| **Red remota**             | Se usa la MAC de la puerta de enlace.                              |
| **ARP (IPv4)**             | Traduce IP → MAC. Guarda la información en una tabla.              |
| **Tabla ARP**              | Contiene pares IP/MAC, es temporal.                                |
| **ICMPv6 ND (IPv6)**       | Reemplaza a ARP. Usa mensajes NS, NA, RS, RA.                      |
| **Broadcast vs Multicast** | ARP usa broadcast (ineficiente), ND usa multicast (más eficiente). |

---

### 🧩 **Ejemplo final completo**

PC1 quiere comunicarse con el servidor 10.0.0.5:

1. PC1 detecta que **10.0.0.5 no está en su red local**.
    
2. Envía los datos al **router (gateway)**.
    
3. Si no conoce la MAC del router, **usa ARP** para descubrirla.
    
4. Una vez resuelto, envía la trama a la **MAC del router**, pero con **IP destino = 10.0.0.5**.
    
5. El router reenvía el paquete hacia la red destino.


# **MÓDULO 10 – Configuración básica del router (ITN v7.0)**

Este módulo enseña:

- Cómo acceder y configurar un router Cisco.
    
- Cómo activar sus interfaces.
    
- Cómo aplicar contraseñas y guardar la configuración.
    

---

## 🧠 **10.1 Configuración inicial del router**

### 📘 **Propósito**

Antes de que un router pueda enrutar tráfico, **debe configurarse** correctamente:

- Asignar nombre al dispositivo.
    
- Establecer contraseñas de acceso.
    
- Cifrar contraseñas.
    
- Configurar mensajes legales.
    
- Guardar la configuración.
    

---

### 🔹 **Pasos básicos de configuración (en orden)**

1. **Configurar el nombre del router:**
    
    `Router(config)# hostname R1`
    
    → Esto cambia el nombre del dispositivo (útil para identificarlo en la red).
    
2. **Proteger el modo EXEC privilegiado (enable):**
    
    `R1(config)# enable secret class`
    
    - `enable secret` crea una contraseña **encriptada** para el modo privilegiado (#).
        
    - Es más segura que `enable password`.
        
3. **Proteger el acceso a la consola:**
    
    ```
    R1(config)# line console 0
    R1(config-line)# password cisco
    R1(config-line)# login
    R1(config-line)# exit
    ```
    
    - Define una contraseña para acceder físicamente al router mediante consola.
        
4. **Proteger el acceso remoto (líneas VTY – Telnet/SSH):**
    
    ```
    R1(config)# line vty 0 4
    R1(config-line)# password cisco
    R1(config-line)# login
    R1(config-line)# exit
    ```
    
    - Configura una contraseña para conexiones remotas (hasta 5 sesiones simultáneas: 0–4).
        
5. **Cifrar todas las contraseñas del archivo de configuración:**
    
    `R1(config)# service password-encryption`
    
    - Aplica un **cifrado débil** (pero evita ver contraseñas en texto claro con `show running-config`).
        
6. **Mostrar mensaje legal (banner):**
    
    `R1(config)# banner motd #Acceso no autorizado prohibido#`
    
    - **MOTD (Message of the Day)** = mensaje de advertencia que aparece al acceder al router.  
        Ejemplo: “⚠️ Access unauthorized users is prohibited.”
        
7. **Guardar la configuración:**
    
    `R1# copy running-config startup-config`
    
    - Guarda la configuración actual (`running-config`) en la memoria NVRAM (`startup-config`).
        
    - Si no lo haces, se pierde al reiniciar.
        

---

### 📋 **Resumen rápido del flujo de configuración**

|Paso|Comando clave|Propósito|
|---|---|---|
|1|`hostname`|Identificar el router|
|2|`enable secret`|Proteger el modo privilegiado|
|3|`line console 0`|Proteger acceso por consola|
|4|`line vty 0 4`|Proteger acceso remoto|
|5|`service password-encryption`|Cifrar contraseñas|
|6|`banner motd`|Mostrar mensaje de advertencia|
|7|`copy run start`|Guardar configuración|

---

## ⚙️ **10.2 Configurar interfaces del router**

El router **conecta diferentes redes**, por lo que cada interfaz necesita una **dirección IP** (y opcionalmente una IPv6).

---

### 🔹 **Pasos para configurar una interfaz**

1. **Entrar a la interfaz:**
    
    `R1(config)# interface gigabitEthernet 0/0/0`
    
2. **(Opcional) Agregar una descripción:**
    
    `R1(config-if)# description Link to LAN`
    
    - Sirve como nota administrativa.
        
3. **Asignar dirección IPv4:**
    
    `R1(config-if)# ip address 192.168.10.1 255.255.255.0`
    
4. **Asignar dirección IPv6 (si aplica):**
    
    `R1(config-if)# ipv6 address 2001:db8:acad:10::1/64`
    
5. **Activar la interfaz (por defecto están apagadas):**
    
    `R1(config-if)# no shutdown`
    
    - ⚠️ Si olvidas este comando, la interfaz permanece **administrativamente inactiva**.
        
6. **Salir del modo interfaz:**
    
    `R1(config-if)# exit`
    

---

### 💡 **Ejemplo completo: configuración de dos interfaces**

#### Ejemplo: Router R1 conectado a una LAN y a otro router (R2)

**Configuración de la interfaz LAN:**

```
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# description Link to LAN
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
```

**Configuración de la interfaz WAN:**

```
R1(config)# interface gigabitEthernet 0/0/1
R1(config-if)# description Link to R2
R1(config-if)# ip address 209.165.200.225 255.255.255.252
R1(config-if)# no shutdown
R1(config-if)# exit
```

**Salida esperada del router:**

```
%LINK-3-UPDOWN: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
```

---

### 🔹 **Verificación de la configuración**

|Comando|Función|
|---|---|
|`show ip interface brief`|Muestra las interfaces, su IP y su estado (up/down).|
|`show running-config`|Muestra la configuración actual.|
|`show ip route`|Muestra la tabla de enrutamiento.|
|`ping <dirección>`|Verifica conectividad.|
|`traceroute <dirección>`|Muestra la ruta que siguen los paquetes.|

#### Ejemplo de salida:

```
R1# show ip interface brief
Interface              IP-Address      OK? Method  Status  Protocol
GigabitEthernet0/0/0   192.168.10.1    YES manual  up      up
GigabitEthernet0/0/1   209.165.200.225 YES manual  up      up
```

---

### ⚠️ **Estados importantes de interfaz**

|Estado|Significado|
|---|---|
|**up / up**|Funcional ✅|
|**up / down**|Problema de capa 2 (posible cable o switch) ⚠️|
|**administratively down**|No activada (`no shutdown` faltante) ❌|

---

### 🔹 **Guardado y recuperación de configuraciones**

|Acción|Comando|
|---|---|
|Guardar config actual|`copy running-config startup-config`|
|Ver config guardada|`show startup-config`|
|Borrar config de arranque|`erase startup-config`|
|Reiniciar el router|`reload`|

---

## 💡 **Consejo para el examen**

Siempre sigue este flujo cuando configures un router desde cero:

1. Entra por consola.
    
2. Activa el modo privilegiado con `enable`.
    
3. Entra al modo de configuración global con `configure terminal`.
    
4. Aplica los pasos básicos (hostname, passwords, banner, etc.).
    
5. Configura las interfaces y activa con `no shutdown`.
    
6. Guarda la configuración.
    

💬 **Truco mnemotécnico:**  
👉 **HPPBING** = Hostname – Passwords – Password encryption – Banner – Interfaces – No shutdown – Guardar.

---

## 🧠 **Resumen general del Módulo 10**

|Tema|Concepto clave|
|---|---|
|**Propósito del router**|Conectar redes diferentes y dirigir tráfico (enrutamiento).|
|**Modos IOS**|Usuario (>) → Privilegiado (#) → Configuración global (config)# → Submodos (line, interface).|
|**Contraseñas**|`enable secret`, `line console 0`, `line vty 0 4`.|
|**Cifrado**|`service password-encryption`.|
|**Mensaje legal**|`banner motd`.|
|**Guardar config**|`copy running-config startup-config`.|
|**Configurar interfaz**|`interface`, `ip address`, `no shutdown`.|
|**Verificación**|`show ip interface brief`, `ping`, `show run`.|

---

### 🧩 **Ejemplo completo (Resumen visual)**

```
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# enable secret class
R1(config)# line console 0
R1(config-line)# password cisco
R1(config-line)# login
R1(config-line)# exit
R1(config)# line vty 0 4
R1(config-line)# password cisco
R1(config-line)# login
R1(config)# service password-encryption
R1(config)# banner motd #Acceso no autorizado#
R1(config)# interface g0/0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# no shutdown
R1(config)# end
R1# copy run start
```




# **MÓDULO 11 – Direccionamiento IPv4 (ITN v7.0)**

---

## 🧠 **11.1 Estructura de direcciones IPv4**

### 📘 **Concepto general**

Una **dirección IPv4**:

- Tiene **32 bits** (4 octetos de 8 bits cada uno).
    
- Se representa en **notación decimal punteada** (por ejemplo: `192.168.10.5`).
    
- Cada bit puede ser **0 o 1**.
    
- Se divide en dos partes:
    
    - **Porción de red** 🕸️ → Identifica a qué red pertenece.
        
    - **Porción de host** 💻 → Identifica al dispositivo dentro de esa red.
        

---

### 🔹 **Máscara de subred**

Para saber dónde termina la red y dónde empieza el host, usamos la **máscara de subred**.

#### Ejemplo:

```
IP:      192.168.10.5
Máscara: 255.255.255.0
```

👉 En binario:

```
IP:      11000000.10101000.00001010.00000101
Máscara: 11111111.11111111.11111111.00000000
```

- Los **1s** indican la **porción de red**.
    
- Los **0s** indican la **porción de host**.
    

📍 En este caso, los **primeros 24 bits (255.255.255)** son de red, y los **últimos 8 bits** son para hosts.

---

### 🔹 **Operación AND (ANDing)**

La **operación lógica AND** se usa para determinar la **dirección de red** a la que pertenece una IP.  
Regla:

```
1 AND 1 = 1  
1 AND 0 = 0  
0 AND 1 = 0  
0 AND 0 = 0
```

#### Ejemplo:

```
IP:      192.168.10.5 → 11000000.10101000.00001010.00000101
Máscara: 255.255.255.0 → 11111111.11111111.11111111.00000000
Resultado:               11000000.10101000.00001010.00000000
```

Resultado: **192.168.10.0** → Dirección de red ✅

---

### 🔹 **Longitud de prefijo (/n)**

En lugar de escribir la máscara completa, se puede usar **notación de prefijo**:

- `255.255.255.0` = `/24`
    
- `255.255.0.0` = `/16`
    
- `255.0.0.0` = `/8`
    

💡 Ejemplo:

```
192.168.10.5/24  →  Red: 192.168.10.0
```

---

## 📦 **11.2 Direcciones de red, host y broadcast**

Cada red IPv4 tiene **tres tipos de direcciones**:

|Tipo de dirección|Descripción|Ejemplo (Red /24)|
|---|---|---|
|**Dirección de red**|Identifica la red (no se asigna a ningún host).|`192.168.10.0`|
|**Direcciones de host**|Identifican dispositivos dentro de la red.|`192.168.10.1` – `192.168.10.254`|
|**Dirección de broadcast**|Se usa para enviar mensajes a todos los hosts de la red.|`192.168.10.255`|

🧠 **Fórmulas útiles:**

- **Cantidad de hosts por red:**  
    ( 2^{n} - 2 )  
    donde _n_ = cantidad de bits de host.  
    Ejemplo: /24 → 8 bits → ( 2^8 - 2 = 254 ) hosts.
    
- **Cantidad de subredes:**  
    ( 2^{n} )  
    donde _n_ = bits tomados para subred.
    

---

## 🌐 **11.3 Tipos de direcciones IPv4**

IPv4 tiene distintos **tipos y clases** de direcciones según su uso.

---

### 🔹 **Clases de direcciones (A, B, C)**

|Clase|Rango de 1er octeto|Máscara por defecto|Nº Máximo de Hosts|
|---|---|---|---|
|**A**|1 – 126|255.0.0.0 (/8)|16 millones|
|**B**|128 – 191|255.255.0.0 (/16)|65 mil|
|**C**|192 – 223|255.255.255.0 (/24)|254|
|**D**|224 – 239|Multicast|—|
|**E**|240 – 255|Experimental|—|

💡 **Nota:**  
127.x.x.x está reservado para **loopback (autoprueba)** → más abajo se explica.

---

### 🔹 **Tipos según propósito**

|Tipo|Rango / Descripción|
|---|---|
|**Pública**|Enrutables en Internet. Asignadas por **IANA** y los **ISP**.|
|**Privada**|Uso interno (no se enrutan en Internet). Definidas en RFC 1918.|
|**Loopback**|127.0.0.0/8 (por ejemplo 127.0.0.1) → prueba local TCP/IP.|
|**Link-local (APIPA)**|169.254.0.0/16 → usada cuando no hay DHCP disponible.|
|**Broadcast**|Última dirección de la red.|
|**Multicast**|224.0.0.0 – 239.255.255.255 → grupos especiales de comunicación.|

---

### 🔹 **Rangos privados definidos en RFC 1918**

|Clase|Rango privado|Máscara por defecto|
|---|---|---|
|A|10.0.0.0 – 10.255.255.255|/8|
|B|172.16.0.0 – 172.31.255.255|/12|
|C|192.168.0.0 – 192.168.255.255|/16|

💡 Se utilizan en redes domésticas y empresariales.  
Ejemplo típico: `192.168.1.0/24`

---

## 🔁 **11.4 NAT – Traducción de direcciones**

Cuando las direcciones privadas necesitan comunicarse con Internet, se usa **NAT (Network Address Translation)**.

- **Función:** Traducir una IP privada (no enrutable) en una IP pública (enrutable).
    
- **Ubicación:** En el **router perimetral** o el **firewall**.
    

#### Ejemplo:

```
PC (192.168.1.10) → Router NAT (200.100.50.2) → Internet
```

El router reemplaza la IP privada con su IP pública antes de enviar el paquete.

💡 **Tipos de NAT (en módulos avanzados):**

- Estática (una a una)
    
- Dinámica (pool de direcciones)
    
- PAT (varios hosts comparten una IP pública)
    

---

## 🔍 **11.5 Tipos de comunicación IPv4**

|Tipo|Descripción|Ejemplo|
|---|---|---|
|**Unicast**|Comunicación uno a uno (host a host).|PC → Servidor|
|**Broadcast**|Uno a todos en la red local.|Router envía DHCP offer|
|**Multicast**|Uno a varios (solo los que pertenecen al grupo).|Streaming, videoconferencia|

💡 IPv6 **no usa broadcast**, solo **unicast y multicast** (y anycast).

---

## 🧠 **Ejemplo completo**

**Red:** 192.168.10.0/24  
**Máscara:** 255.255.255.0

|Tipo|Dirección|Descripción|
|---|---|---|
|Dirección de red|192.168.10.0|Identifica la red|
|Primer host|192.168.10.1|Router o servidor|
|Último host|192.168.10.254|Último dispositivo|
|Broadcast|192.168.10.255|Mensaje a todos los hosts|

**Cantidad de hosts:**  
( 2^8 - 2 = 254 )

---

## 🧩 **11.6 Comandos útiles (Cisco IOS)**

|Comando|Descripción|
|---|---|
|`show ip interface brief`|Verifica las IP configuradas en las interfaces.|
|`show running-config`|Muestra configuración actual.|
|`ping <IP>`|Verifica conectividad con otro host.|
|`show ip route`|Muestra la tabla de enrutamiento.|

---

## 📘 **Resumen general del Módulo 11**

|Concepto|Descripción|
|---|---|
|**IPv4**|Dirección de 32 bits, dividida en 4 octetos.|
|**Máscara de subred**|Determina red y host.|
|**ANDing**|Identifica la dirección de red.|
|**Notación /n**|Indica número de bits de red.|
|**Dirección de red**|Identifica la red (no asignable).|
|**Dirección de broadcast**|Envía a todos los hosts de la red.|
|**Privadas (RFC 1918)**|10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16|
|**Públicas**|Asignadas globalmente y enrutables.|
|**Loopback (127.0.0.1)**|Prueba TCP/IP local.|
|**Link-local (169.254.x.x)**|IP automática sin DHCP.|
|**NAT**|Traduce direcciones privadas ↔ públicas.|
|**Unicast / Broadcast / Multicast**|Tipos de entrega de paquetes.|

---

### 💡 **Ejemplo final para practicar**

> Dada la IP **172.16.20.130/20**, determina:
> 
> - Máscara: 255.255.240.0
>     
> - Red: 172.16.16.0
>     
> - Broadcast: 172.16.31.255
>     
> - Primer host: 172.16.16.1
>     
> - Último host: 172.16.31.254
>     
> - Hosts: ( 2^{12} - 2 = 4094 )
>     




# **MÓDULO 12 – Direccionamiento IPv6 (ITN v7.0)**

---

## 🧠 **12.1 Problemas de IPv4 y necesidad de IPv6**

### 📘 **Motivación principal**

IPv4 tiene solo **4.3 mil millones de direcciones posibles (2³²)**, pero ya no son suficientes para todos los dispositivos conectados (IoT, móviles, etc.).

Por eso nació **IPv6**, que tiene **128 bits**, ofreciendo:  
👉 ( 2^{128} ) direcciones posibles  
(≈ 340 _undecillones_ de direcciones — prácticamente infinitas).

---

### 🔹 **Limitaciones de IPv4 que IPv6 soluciona:**

|Problema IPv4|Solución en IPv6|
|---|---|
|Escasez de direcciones|Espacio de 128 bits, ¡muchísimo más amplio!|
|NAT (traducción de direcciones)|IPv6 permite comunicación directa (end-to-end).|
|Fragmentación ineficiente|IPv6 no permite fragmentación intermedia (solo en el origen).|
|Configuración manual o DHCP necesaria|IPv6 permite **autoconfiguración automática (SLAAC)**.|
|Broadcast (que genera congestión)|Eliminado; usa **multicast** y **anycast**.|
|Seguridad opcional|IPv6 incluye **IPsec por defecto**.|

---

### 🔹 **Coexistencia IPv4 ↔ IPv6**

IPv4 y IPv6 **convivirán por años**, por lo tanto se usan mecanismos de **transición**:

|Técnica|Descripción|
|---|---|
|**Dual Stack**|El dispositivo usa **ambos protocolos (IPv4 e IPv6)** simultáneamente.|
|**Tunneling**|Encapsula paquetes IPv6 dentro de IPv4 para atravesar redes que no lo soportan.|
|**Translation (NAT64)**|Traduce direcciones IPv6 ↔ IPv4, para permitir comunicación entre ambos mundos.|

💡 **Objetivo final:** Migrar a **IPv6 nativo**, sin necesidad de túneles o traducciones.

---

## 🌐 **12.2 Representación de direcciones IPv6**

### 📘 **Estructura general**

- Una dirección IPv6 tiene **128 bits** divididos en **8 grupos de 16 bits** (4 dígitos hexadecimales cada uno).
    
- Se representa en **hexadecimal** (base 16).
    
- Los grupos se separan con **dos puntos (:)**.
    

#### Ejemplo:

```
2001:0db8:0000:1111:0000:0000:0000:0200
```

👉 Es igual que:

```
2001:db8:0:1111:0:0:0:200
```

Cada grupo (llamado **hexteto**) representa 16 bits.

---

### 🔹 **Reglas para simplificar direcciones IPv6**

#### ✅ **Regla 1 – Omitir ceros iniciales**

Se pueden eliminar los ceros **al inicio de cada grupo**:

```
01ab → 1ab
09f0 → 9f0
0a00 → a00
00ab → ab
```

📌 _Solo los ceros al inicio, no los del final._

#### ✅ **Regla 2 – Usar “::” para grupos de ceros consecutivos**

Los ceros contiguos pueden reemplazarse con `::`, pero **solo una vez por dirección**.

Ejemplo:

```
2001:0db8:0000:0000:0000:0000:0000:0001
→ 2001:db8::1
```

Otro ejemplo:

```
2001:0db8:abcd:0000:0000:0000:0000:0001
→ 2001:db8:abcd::1
```

📛 **Error común:** No se puede usar “::” dos veces (causa ambigüedad).

---

### 🔹 **Tipos de notaciones**

|Notación|Ejemplo|Uso|
|---|---|---|
|**Completa**|2001:0db8:0000:1111:0000:0000:0000:0200|Formal|
|**Simplificada**|2001:db8:0:1111::200|Habitual|
|**Con prefijo**|2001:db8:0:1111::200/64|Incluye longitud de red|

---

## 📏 **12.3 Longitud de prefijo IPv6**

- Similar al `/24` de IPv4.
    
- Indica cuántos bits pertenecen a la **porción de red**.
    
- Puede variar de `/0` a `/128`.
    

🧠 **Recomendación estándar:** `/64`  
Esto deja **64 bits para el ID de interfaz** (host) y **64 bits para la red**.

---

### 💡 **SLAAC (Stateless Address Auto Configuration)**

Permite que un host IPv6 **genere su propia dirección automáticamente**, combinando:

1. El **prefijo de red** anunciado por el router (RA).
    
2. Un **ID de interfaz** (generalmente derivado de la MAC del dispositivo).
    

Ejemplo:

- Prefijo del router: `2001:db8:acad:1::/64`
    
- ID generado por la PC: `::abcd:12ff:fe34:5678`
    
- Dirección final: `2001:db8:acad:1::abcd:12ff:fe34:5678`
    

---

## 🧩 **12.4 Tipos de direcciones IPv6**

IPv6 no tiene broadcast, pero sí tres grandes tipos de direcciones:

|Tipo|Descripción|Ejemplo|
|---|---|---|
|**Unicast**|Identifica una interfaz única. Comunicación uno a uno.|`2001:db8:acad::1`|
|**Multicast**|Identifica un grupo de dispositivos. Comunicación uno a muchos.|`ff02::1` (todos los nodos)|
|**Anycast**|Dirección compartida por varios dispositivos; el paquete va al **más cercano**.|(depende de la configuración)|

---

### 🔹 **Tipos de direcciones Unicast IPv6**

|Tipo|Prefijo|Uso|
|---|---|---|
|**Global Unicast (GUA)**|`2000::/3`|Direcciones **públicas**, equivalentes a las IPv4 públicas. Enrutables globalmente.|
|**Link-Local (LLA)**|`fe80::/10`|Direcciones **automáticas** válidas solo en el enlace local. No son enrutables.|
|**Unique Local (ULA)**|`fc00::/7` – `fd00::/8`|Equivalentes a las IPv4 **privadas** (RFC 4193). Se usan dentro de organizaciones.|
|**Loopback**|`::1`|Equivalente a 127.0.0.1 (prueba local).|
|**Unspecified**|`::`|“Sin dirección” – usada al inicializar interfaces.|

---

### 🧠 **Comparación IPv4 vs IPv6**

|Característica|IPv4|IPv6|
|---|---|---|
|Longitud|32 bits|128 bits|
|Notación|Decimal punteada|Hexadecimal con “:”|
|NAT|Necesario|No necesario|
|Fragmentación|Por routers|Solo origen|
|Broadcast|Sí|No (usa multicast)|
|Autoconfiguración|DHCP o manual|SLAAC o DHCPv6|
|Seguridad (IPsec)|Opcional|Integrada|
|Cabecera|Variable, más pesada|Fija (40 bytes), más simple|
|Tamaño de red recomendado|/24|/64|

---

## 🧪 **12.5 Ejemplos prácticos**

### Ejemplo 1: Dirección IPv6 global

```
2001:0db8:acad:0001:0000:0000:0000:0001
→ 2001:db8:acad:1::1/64
```

- Prefijo de red: `2001:db8:acad:1::/64`
    
- ID de interfaz: `::1`
    

### Ejemplo 2: Dirección link-local

Generada automáticamente:

```
fe80::a00:27ff:fe8c:4d2/64
```

Solo válida en la red local.

### Ejemplo 3: Multicast

```
ff02::1 → Todos los nodos locales  
ff02::2 → Todos los routers locales
```

---

## 📘 **Resumen general del Módulo 12**

|Concepto|Descripción|
|---|---|
|**Tamaño IPv6**|128 bits (8 grupos de 16 bits en hex).|
|**Ventajas**|Más direcciones, sin NAT, mejor seguridad, autoconfiguración.|
|**Coexistencia**|Dual Stack, Tunneling, NAT64.|
|**Reglas de escritura**|Omitir ceros iniciales y usar `::` una vez.|
|**Prefijo /64**|Recomendado; 64 bits red + 64 bits host.|
|**SLAAC**|Autoconfiguración sin servidor DHCP.|
|**Unicast Global**|Enrutables globalmente (`2000::/3`).|
|**Link-Local**|Automáticas (`fe80::/10`).|
|**Unique Local (ULA)**|Privadas (`fc00::/7`).|
|**Loopback**|`::1` – prueba local.|
|**Multicast**|`ff00::/8` – comunicación uno a muchos.|
|**Anycast**|Mismo prefijo en varios nodos; el más cercano responde.|

---

## 🌍 **Ejemplo de coexistencia IPv4 e IPv6 en un router**

```bash
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 enable
R1(config-if)# no shutdown
```

🔹 Este router ahora tiene **Dual Stack**, puede comunicarse tanto con redes IPv4 como IPv6.





# **MÓDULO 13 – ICMP (ITN v7.0)**

---

## 🧠 **13.1 Introducción a ICMP**

### 📘 **¿Qué es ICMP?**

El **Internet Control Message Protocol (ICMP)** es un protocolo de **mensajería y control** usado por IPv4 e IPv6 para **informar errores o estados** relacionados con la entrega de paquetes IP.

No se usa para enviar datos de usuario, sino para **notificar problemas en la red** (por ejemplo, host inalcanzable o tiempo excedido).

|Versión IP|Protocolo asociado|
|---|---|
|**IPv4**|ICMPv4|
|**IPv6**|ICMPv6|

💡 **Ejemplo:**  
Si un router no puede entregar un paquete porque el destino no existe, enviará un mensaje ICMP al origen avisando del problema.

---

### 🔹 **Funciones principales de ICMP**

1. **Diagnóstico:**
    
    - Herramientas como `ping` y `traceroute` usan ICMP para comprobar conectividad.
        
2. **Notificación de errores:**
    
    - Informa si un paquete no se pudo entregar o si el tiempo de vida (TTL) se agotó.
        
3. **Control de red (en IPv6):**
    
    - ICMPv6 incluye funciones adicionales como detección de vecinos, routers y configuración automática.
        

---

### ⚠️ **Nota de seguridad**

Los mensajes ICMPv4 pueden ser **restringidos o bloqueados** por seguridad, ya que un atacante puede usarlos para reconocimiento de red (ping sweep).

---

## 🌐 **13.2 Mensajes ICMPv4**

### 📘 **Estructura general**

Los mensajes ICMPv4 son **encapsulados dentro de un paquete IP** y tienen:

- **Código de tipo de mensaje**
    
- **Código de causa**
    
- **Datos adicionales** (como parte del encabezado IP original)
    

---

### 🔹 **Tipos de mensajes ICMPv4 más comunes**

|Tipo de mensaje|Descripción|Uso|
|---|---|---|
|**Echo Request / Echo Reply**|Prueba la conectividad entre dos hosts.|Usado por **ping**.|
|**Destination Unreachable**|Informa que el destino o servicio no está disponible.|Error de entrega.|
|**Time Exceeded**|Indica que el TTL del paquete llegó a cero.|Usado por **traceroute**.|
|**Redirect**|Indica que hay una mejor ruta disponible.|Optimización del enrutamiento local.|

---

### 💡 **Ejemplo: Ping (ICMP Echo)**

1. El **host origen** envía un **Echo Request** (solicitud de eco).
    
2. El **host destino** responde con un **Echo Reply** (respuesta de eco).
    
3. Si la respuesta llega, hay **conectividad**; si no, hay un problema en la ruta.
    

#### Ejemplo en Windows o Cisco:

```bash
ping 192.168.1.1
```

Salida típica:

```
Reply from 192.168.1.1: bytes=32 time<1ms TTL=64
```

---

### 🔹 **Destination Unreachable (Destino inalcanzable)**

Cuando un router o dispositivo no puede entregar un paquete, devuelve un mensaje ICMPv4 con un **código de error**.

|Código|Significado|
|---|---|
|0|Red inalcanzable|
|1|Host inalcanzable|
|2|Protocolo inalcanzable|
|3|Puerto inalcanzable|

📘 Ejemplo:

- Si haces `ping` a un host que no existe, recibirás “**Host unreachable**”.
    

---

### 🔹 **Time Exceeded (Tiempo excedido)**

- Cada paquete IP tiene un campo **TTL (Time To Live)** que se reduce en cada salto de router.
    
- Si llega a 0, el router **descarta el paquete** y envía un mensaje ICMP “**Time Exceeded**”.
    

🧠 Esta función es la base del comando **traceroute**:

- Envía paquetes con TTL incremental para descubrir **por qué routers pasa el tráfico**.
    

---

## 🌐 **13.3 ICMPv6**

IPv6 utiliza **ICMPv6**, una versión **mejorada y ampliada** de ICMPv4.  
Además de las funciones de error y diagnóstico, ICMPv6 es esencial para que IPv6 **funcione correctamente**.

---

### 🔹 **Funciones de ICMPv6**

|Tipo de mensaje|Propósito|
|---|---|
|**Error messages**|Informan sobre errores de entrega (similar a ICMPv4).|
|**Informational messages**|Usados para diagnóstico (Echo Request/Reply).|
|**Neighbor Discovery (ND)**|Sustituye a ARP en IPv6.|
|**Router Discovery**|Permite a los hosts encontrar routers y configurar su dirección.|

---

### 🔹 **Mensajes ICMPv6 más importantes**

|Tipo de mensaje|Descripción|
|---|---|
|**Echo Request / Echo Reply**|Igual que en ICMPv4.|
|**Destination Unreachable**|Indica que el destino o servicio no está disponible.|
|**Time Exceeded**|TTL (ahora “Hop Limit”) alcanzó 0.|
|**Router Solicitation (RS)**|Los hosts preguntan por routers disponibles.|
|**Router Advertisement (RA)**|Los routers anuncian su presencia y prefijos de red.|
|**Neighbor Solicitation (NS)**|Similar a ARP Request: busca la MAC de un vecino.|
|**Neighbor Advertisement (NA)**|Similar a ARP Reply: responde con la MAC.|
|**Redirect**|Indica una mejor ruta para un destino.|

---

### 💡 **Ejemplo: Autoconfiguración con ICMPv6**

Cuando un host IPv6 se conecta a una red:

1. Envía un **Router Solicitation (RS)** preguntando por un router.
    
2. El router responde con un **Router Advertisement (RA)**:
    
    - Prefijo de red.
        
    - Parámetros de red.
        
3. El host usa esa información para **autoconfigurarse (SLAAC)**.
    
4. Luego envía un **Neighbor Solicitation (NS)** para verificar que su dirección no esté duplicada.
    

---

### 🔹 **Códigos ICMPv6 – Destino inalcanzable**

|Código|Descripción|
|---|---|
|0|No hay ruta hacia el destino|
|1|Comunicación prohibida (firewall)|
|2|Más allá del alcance de la dirección origen|
|3|Dirección inalcanzable|
|4|Puerto inalcanzable|

---

## 🧠 **13.4 ICMP en herramientas de red**

|Herramienta|Función|Protocolos usados|
|---|---|---|
|**Ping**|Comprueba la conectividad entre dispositivos.|ICMPv4/v6 Echo Request & Reply|
|**Traceroute**|Muestra los routers intermedios hasta el destino.|ICMPv4/v6 Time Exceeded|
|**Neighbor Discovery (IPv6)**|Descubre routers y vecinos locales.|ICMPv6 ND (RS, RA, NS, NA)|

---

## 🧩 **13.5 Ejemplo de funcionamiento**

### 🧱 Escenario:

- PC1: 192.168.1.10
    
- Router: 192.168.1.1
    
- Servidor: 10.0.0.10
    

#### Paso a paso:

1. PC1 hace `ping 10.0.0.10`.
    
2. El router recibe el paquete, lo enruta hacia la red 10.0.0.0.
    
3. Si el servidor responde, PC1 recibe un **Echo Reply** ✅.
    
4. Si no hay ruta, el router envía un **ICMP Destination Unreachable** ❌.
    
5. Si el paquete se pierde en la ruta, puede recibirse un **Time Exceeded**.
    

---

## 🧾 **13.6 ICMPv4 vs ICMPv6**

|Característica|ICMPv4|ICMPv6|
|---|---|---|
|Diagnóstico (ping, traceroute)|✅|✅|
|Notificación de errores|✅|✅|
|Detección de vecinos|❌ (usa ARP)|✅ (ND)|
|Descubrimiento de routers|❌|✅ (RA/RS)|
|Detección de direcciones duplicadas|❌|✅ (NS)|
|Broadcast|Sí|No (usa multicast)|
|Seguridad integrada|No|Sí (IPsec obligatorio)|

---

## 📘 **Resumen general del Módulo 13**

|Concepto|Descripción|
|---|---|
|**ICMP**|Protocolo de control y diagnóstico usado con IP.|
|**ICMPv4**|Para IPv4: echo, time exceeded, destination unreachable.|
|**ICMPv6**|Para IPv6: además, descubrimiento de routers y vecinos.|
|**Ping**|Usa mensajes Echo Request y Echo Reply.|
|**Traceroute**|Usa mensajes Time Exceeded para mostrar los saltos.|
|**Destination Unreachable**|Informa que el destino no pudo alcanzarse.|
|**Neighbor Discovery (ND)**|Sustituye ARP en IPv6.|
|**Mensajes RS/RA/NS/NA**|Permiten autoconfiguración y comunicación entre dispositivos IPv6.|

---

### 💡 **Ejemplo visual de ICMPv6 en acción**

|Paso|Mensaje ICMPv6|Función|
|---|---|---|
|1|RS (Router Solicitation)|El host busca routers en la red.|
|2|RA (Router Advertisement)|El router responde con prefijos y configuración.|
|3|NS (Neighbor Solicitation)|El host verifica si su IP está en uso.|
|4|NA (Neighbor Advertisement)|Un vecino responde con su dirección MAC.|

---

En resumen, **ICMP** es el “sistema nervioso” de la red IP — no transporta datos, pero **permite que la red se comunique sobre sí misma**.  
Sin ICMP, no podríamos diagnosticar ni detectar errores fácilmente. ⚡



# **MÓDULO 14 – Capa de Transporte (ITN v7.0)**

---

## 🧠 **14.1 Función de la capa de transporte**

### 📘 **Propósito general**

La **Capa de Transporte (Capa 4 del modelo OSI)** se encarga de **proporcionar comunicación lógica** entre las aplicaciones que se ejecutan en diferentes hosts.  
Actúa como **puente entre la capa de aplicación y las capas inferiores** (red, enlace y física).

---

### 🔹 **Funciones principales**

1. **Seguimiento de conversaciones individuales**
    
    - Cada aplicación (por ejemplo, un navegador o una app de correo) puede tener **varias conversaciones simultáneas**.
        
    - La capa de transporte **identifica cada sesión** usando **números de puerto**.
        
2. **Segmentación y reensamblado de datos**
    
    - Divide los datos de la aplicación en **segmentos más pequeños** para su transmisión.
        
    - En el destino, los vuelve a **reconstruir en el orden correcto**.
        
3. **Multiplexación**
    
    - Permite que múltiples aplicaciones usen la red al mismo tiempo, compartiendo el mismo canal.
        
4. **Control de flujo**
    
    - Regula la cantidad de datos que se envían para evitar congestión en el receptor.
        
5. **Control de errores (solo en TCP)**
    
    - Detecta y retransmite segmentos perdidos o dañados.
        

---

### 💡 **Ejemplo**

Cuando abres YouTube y a la vez navegas en otra pestaña, la capa de transporte usa distintos **puertos** para que las dos conexiones puedan coexistir sin interferirse:

- HTTP (YouTube) → puerto 80 o 443 (TCP)
    
- DNS → puerto 53 (UDP)
    

---

## 🌍 **14.2 Protocolos de la capa de transporte**

Los **dos protocolos principales** son:

|Protocolo|Tipo|Características principales|
|---|---|---|
|**TCP (Transmission Control Protocol)**|Orientado a la conexión|Confiable, ordenado, con control de flujo y errores.|
|**UDP (User Datagram Protocol)**|No orientado a la conexión|Rápido, sin confiabilidad ni control de flujo.|

---

## ⚙️ **14.3 TCP (Transmission Control Protocol)**

### 📘 **Propósito**

TCP ofrece una **comunicación confiable y ordenada** entre dos dispositivos.  
Es usado cuando es **importante que los datos lleguen correctamente y en orden**.

Ejemplos de aplicaciones que usan TCP:

- HTTP / HTTPS
    
- FTP
    
- SMTP (correo)
    
- SSH
    

---

### 🔹 **Características principales de TCP**

|Característica|Descripción|
|---|---|
|**Orientado a conexión**|Antes de enviar datos, se establece una sesión entre emisor y receptor.|
|**Fiable**|Reenvía los datos si se pierden.|
|**Ordenado**|Los datos llegan en el mismo orden en que fueron enviados.|
|**Control de flujo**|Ajusta la velocidad de transmisión según la capacidad del receptor.|
|**Control de congestión**|Reduce la velocidad si hay saturación en la red.|
|**Con estado**|Mantiene información sobre la sesión activa.|

---

### 🔹 **Establecimiento de la conexión: el _Three-Way Handshake_**

TCP usa un **proceso de tres pasos** para iniciar una conexión confiable:

|Paso|Acción|Bandera TCP|
|---|---|---|
|1️⃣|El cliente envía un segmento de sincronización|**SYN**|
|2️⃣|El servidor responde confirmando la sincronización|**SYN + ACK**|
|3️⃣|El cliente confirma la respuesta|**ACK**|

💡 Después de este intercambio, ambos lados están sincronizados y pueden comenzar a enviar datos.

---

### 🔹 **Terminación de la conexión**

Para cerrar la sesión, TCP realiza un intercambio de **cuatro pasos (four-way termination)**:

1. Cliente envía **FIN**
    
2. Servidor responde **ACK**
    
3. Servidor envía **FIN**
    
4. Cliente responde **ACK**
    

Así se garantiza que **ningún dato quede sin entregar**.

---

### 🔹 **Control de flujo y confiabilidad**

TCP usa los siguientes mecanismos:

|Mecanismo|Descripción|
|---|---|
|**ACK (Acknowledgment)**|El receptor confirma la recepción de segmentos.|
|**Ventana deslizante (Windowing)**|Permite enviar varios segmentos antes de requerir confirmación.|
|**Número de secuencia**|Cada byte tiene un número para mantener el orden correcto.|
|**Retransmisión**|Si no se recibe un ACK, el segmento se reenvía.|

💡 **Ejemplo:**  
Si un archivo grande se envía por TCP, los datos se dividen en segmentos y cada uno se numera.  
Si el segmento 3 no llega, el receptor no lo confirma y el emisor lo retransmite.

---

### 🔹 **Encabezado TCP (campos principales)**

|Campo|Descripción|
|---|---|
|**Puerto de origen / destino**|Identifican las aplicaciones comunicándose.|
|**Número de secuencia**|Ordena los bytes enviados.|
|**Número de acuse (ACK)**|Confirma los datos recibidos.|
|**Banderas (SYN, ACK, FIN, RST, PSH, URG)**|Controlan el flujo de la sesión.|
|**Ventana**|Controla cuántos bytes se pueden enviar sin confirmar.|
|**Checksum**|Detecta errores en el encabezado.|

---

## ⚡ **14.4 UDP (User Datagram Protocol)**

### 📘 **Propósito**

UDP ofrece una **comunicación rápida y sin conexión**.  
No garantiza la entrega ni el orden, pero tiene **menos sobrecarga**, ideal para aplicaciones **en tiempo real**.

Ejemplos de uso:

- Video en streaming 🎥
    
- VoIP (llamadas) ☎️
    
- Juegos en línea 🎮
    
- DNS y DHCP
    

---

### 🔹 **Características principales de UDP**

|Característica|Descripción|
|---|---|
|**Sin conexión**|No establece sesión previa.|
|**No confiable**|No hay confirmaciones ni retransmisión.|
|**Sin control de flujo**|Envía datos sin esperar al receptor.|
|**Ligero y rápido**|Menor sobrecarga que TCP.|
|**Usa puertos**|Identifica las aplicaciones como TCP.|

💡 UDP se usa cuando **la velocidad es más importante que la confiabilidad**.  
Por ejemplo, si se pierde un par de fotogramas en un video en vivo, no pasa nada.

---

### 🔹 **Encabezado UDP**

El encabezado UDP es **simple y corto (8 bytes)** con solo **4 campos**:

|Campo|Descripción|
|---|---|
|**Puerto de origen**|Puerto del emisor.|
|**Puerto de destino**|Puerto del receptor.|
|**Longitud**|Tamaño del segmento UDP.|
|**Checksum**|Verifica errores básicos.|

---

### 🔹 **Comparación TCP vs UDP**

|Característica|**TCP**|**UDP**|
|---|---|---|
|Tipo de conexión|Orientado a conexión|Sin conexión|
|Confiabilidad|Alta (usa ACKs y retransmisión)|Baja (sin confirmación)|
|Orden|Garantizado|No garantizado|
|Control de flujo|Sí|No|
|Velocidad|Más lento|Más rápido|
|Tamaño del encabezado|20 bytes|8 bytes|
|Aplicaciones típicas|HTTP, FTP, SSH, correo|DNS, DHCP, streaming, VoIP|

---

## 📦 **14.5 Puertos y multiplexación**

### 📘 **Puertos**

Los **números de puerto** permiten identificar qué aplicación usa una conexión.

|Tipo de puerto|Rango|Uso|
|---|---|---|
|**Bien conocidos**|0 – 1023|Asignados a servicios estándar (HTTP, FTP, etc.)|
|**Registrados**|1024 – 49151|Usados por aplicaciones de terceros.|
|**Dinámicos / privados**|49152 – 65535|Asignados temporalmente por el sistema operativo.|

💡 **Ejemplo:**  
Cuando haces una petición web:

- Tu PC usa un puerto origen aleatorio (por ejemplo, 56789).
    
- El servidor escucha en el puerto destino 80 (HTTP).
    

---

### 🔹 **Ejemplo de puertos comunes**

|Servicio|Protocolo|Puerto|
|---|---|---|
|HTTP|TCP|80|
|HTTPS|TCP|443|
|FTP|TCP|21|
|DNS|UDP|53|
|DHCP|UDP|67 (servidor) / 68 (cliente)|
|SMTP|TCP|25|
|SSH|TCP|22|

---

## 🧠 **14.6 Ejemplo práctico**

Imagina que un cliente descarga un archivo desde un servidor web:

1. El cliente abre el navegador → Capa de aplicación (HTTP).
    
2. La capa de transporte asigna:
    
    - Puerto origen aleatorio.
        
    - Puerto destino 80.
        
3. Se establece conexión TCP (handshake).
    
4. El archivo se divide en **segmentos TCP** numerados y enviados.
    
5. El servidor responde con ACKs confirmando la recepción.
    
6. Al finalizar, ambas partes cierran la sesión (FIN → ACK → FIN → ACK).
    

---

## 📘 **Resumen general del Módulo 14**

|Concepto|Descripción|
|---|---|
|**Capa de transporte**|Administra las comunicaciones entre aplicaciones.|
|**Segmentación / Reensamblado**|Divide datos y los reordena al recibir.|
|**Multiplexación**|Permite múltiples aplicaciones simultáneas.|
|**TCP**|Confiable, ordenado, orientado a conexión.|
|**UDP**|No confiable, rápido, sin conexión.|
|**Puertos**|Identifican aplicaciones (0–65535).|
|**Handshake (TCP)**|3 pasos: SYN → SYN-ACK → ACK.|
|**Control de flujo y congestión**|Regulan la velocidad de envío (solo TCP).|
|**Encabezado UDP**|8 bytes, simple y rápido.|
|**Aplicaciones comunes TCP/UDP**|HTTP, DNS, FTP, DHCP, VoIP, etc.|

---

### 💡 **Resumen visual TCP vs UDP**

|Característica|TCP|UDP|
|---|---|---|
|Conexión|Orientada|No orientada|
|Fiabilidad|Alta|Baja|
|Reenvío|Sí|No|
|Orden|Garantizado|No|
|Velocidad|Más lenta|Más rápida|
|Ejemplos|Web, correo, FTP|Streaming, VoIP, DNS|






# **MÓDULO 15 – Capa de Aplicación (ITN v7.0)**

---

## 🧠 **15.1 Función de la capa de aplicación**

### 📘 **Propósito general**

La **Capa de Aplicación (Capa 7 del modelo OSI)** es la que **interactúa directamente con el usuario** o con las aplicaciones del sistema operativo.

No se encarga de mover datos físicamente, sino de:

- Proporcionar **servicios de red a las aplicaciones**.
    
- Interpretar los datos que llegan desde la red.
    
- Formatear la información para que las aplicaciones puedan entenderla.
    

💡 Es la interfaz entre el **usuario final y la red**.

---

### 🔹 **Tres capas del modelo TCP/IP superior (comparación)**

|Modelo OSI|Modelo TCP/IP|Descripción|
|---|---|---|
|Aplicación|Aplicación|Interactúa con el software del usuario (HTTP, DNS).|
|Presentación|Aplicación|Formatea los datos (codificación, compresión, cifrado).|
|Sesión|Aplicación|Administra las sesiones de comunicación.|

👉 En TCP/IP, estas tres capas del modelo OSI se **combinan en una sola capa de Aplicación**.

---

## 💬 **15.2 Modelos de comunicación: Cliente/Servidor y P2P**

---

### ⚙️ **Modelo Cliente/Servidor**

#### 📘 **Concepto**

Un **servidor** proporciona servicios (archivos, correo, web, etc.), y un **cliente** los solicita.

#### 💡 **Ejemplo:**

- Cliente: Navegador web → solicita una página.
    
- Servidor: Apache o Nginx → envía la página web.
    

|Rol|Función|
|---|---|
|**Cliente**|Inicia la comunicación y solicita datos.|
|**Servidor**|Espera solicitudes y responde.|

🧠 Ejemplos de servicios cliente-servidor:

- **HTTP/HTTPS:** Navegación web
    
- **FTP:** Transferencia de archivos
    
- **SMTP/POP3/IMAP:** Correo electrónico
    
- **DNS:** Resolución de nombres
    

📍 Los **servidores** suelen tener **IP fija**, mientras que los clientes suelen recibir una IP dinámica.

---

### ⚙️ **Modelo Peer-to-Peer (P2P)**

#### 📘 **Concepto**

En el modelo **P2P**, **todos los dispositivos (peers)** actúan como **clientes y servidores a la vez**.  
No hay un servidor central.

#### 💡 **Ejemplo:**

- Dos PCs comparten archivos directamente por una red local o internet.
    
- Plataformas como **BitTorrent** usan este modelo.
    

|Ventajas|Desventajas|
|---|---|
|Fácil de configurar.|Menor seguridad.|
|No requiere servidor central.|Difícil de administrar en redes grandes.|
|Eficiente para compartir archivos.|Menor rendimiento con muchos usuarios.|

---

## 🌍 **15.3 Protocolos comunes de la capa de aplicación**

La capa de aplicación incluye **protocolos que permiten a los usuarios acceder a servicios de red**.

---

### 🔹 **1. HTTP y HTTPS – Navegación web**

|Protocolo|Puerto|Descripción|
|---|---|---|
|**HTTP (Hypertext Transfer Protocol)**|80|Transfiere páginas web entre cliente y servidor.|
|**HTTPS (HTTP Secure)**|443|Igual que HTTP, pero usa **TLS/SSL** para cifrar la comunicación.|

#### Ejemplo:

```
Cliente:  GET /index.html HTTP/1.1
Servidor: 200 OK
```

📘 HTTP funciona en modelo **cliente-servidor**, donde el navegador es el cliente y el servidor web responde a las peticiones.

---

### 🔹 **2. DNS – Resolución de nombres**

|Puerto|Protocolo|Descripción|
|---|---|---|
|53|UDP (a veces TCP)|Traduce nombres de dominio a direcciones IP.|

#### Ejemplo:

```
www.google.com → 142.250.64.78
```

💡 Sin DNS, los usuarios tendrían que recordar direcciones IP numéricas en lugar de nombres.

---

### 🔹 **3. DHCP – Asignación automática de IP**

|Puerto|Protocolo|Descripción|
|---|---|---|
|67 (servidor) / 68 (cliente)|UDP|Asigna automáticamente IPs, máscara, gateway y DNS.|

#### Proceso **DORA**:

1. **Discover:** Cliente busca servidores DHCP.
    
2. **Offer:** Servidor ofrece una IP.
    
3. **Request:** Cliente solicita esa IP.
    
4. **Acknowledge:** Servidor confirma y asigna la IP.
    

💡 DHCP simplifica la administración de redes grandes, evitando configuraciones manuales.

---

### 🔹 **4. FTP – Transferencia de archivos**

|Puerto|Protocolo|Descripción|
|---|---|---|
|21|TCP|Transfiere archivos entre cliente y servidor.|

- Requiere autenticación (usuario y contraseña).
    
- Soporta transferencia en ambos sentidos (upload/download).
    
- **FTP Seguro (FTPS/SFTP)** añade cifrado para proteger las credenciales y los datos.
    

📘 Ejemplo de uso:

```bash
ftp ftp.cisco.com
```

---

### 🔹 **5. Correo electrónico: SMTP, POP3, IMAP**

|Protocolo|Puerto|Descripción|
|---|---|---|
|**SMTP (Simple Mail Transfer Protocol)**|25 (envío)|Envía correos entre servidores o desde cliente a servidor.|
|**POP3 (Post Office Protocol v3)**|110|Descarga los correos del servidor y los elimina.|
|**IMAP (Internet Message Access Protocol)**|143|Permite leer correos directamente desde el servidor (no los borra).|

💡 **Diferencia clave:**

- POP3 → descarga y borra los mensajes.
    
- IMAP → mantiene los mensajes en el servidor (ideal para usar en varios dispositivos).
    

---

### 🔹 **6. SMB y AFP – Compartición de archivos**

|Protocolo|Uso|Plataforma|
|---|---|---|
|**SMB (Server Message Block)**|Comparte archivos e impresoras.|Windows|
|**AFP (Apple Filing Protocol)**|Compartición de archivos.|macOS|

---

### 🔹 **7. SSH y Telnet – Acceso remoto**

|Protocolo|Puerto|Descripción|
|---|---|---|
|**SSH (Secure Shell)**|22|Acceso remoto cifrado a dispositivos.|
|**Telnet**|23|Acceso remoto **sin cifrar** (no recomendado).|

💡 SSH es la **versión segura de Telnet** y se usa para administrar routers y switches.

Ejemplo:

```bash
ssh admin@192.168.1.1
```

---

## 💡 **15.4 Funciones comunes de la capa de aplicación**

|Función|Descripción|
|---|---|
|**Codificación de datos**|Convierte los datos en un formato estándar (ASCII, Unicode, etc.).|
|**Compresión**|Reduce el tamaño de los datos transmitidos.|
|**Cifrado**|Protege los datos durante la transmisión (ej: HTTPS).|
|**Control de sesión**|Mantiene la conexión activa entre cliente y servidor.|

---

## ⚙️ **15.5 Ejemplo de flujo completo (HTTP + DNS + TCP/IP)**

1. El usuario escribe `www.cisco.com` en el navegador.
    
2. **DNS** traduce el nombre a una IP.
    
3. El navegador (cliente HTTP) abre una **conexión TCP (puerto 80 o 443)** con el servidor web.
    
4. El servidor responde y envía la página solicitada.
    
5. El usuario recibe y visualiza la página.
    

📍 Aquí intervienen todas las capas:

- Aplicación → HTTP, DNS
    
- Transporte → TCP
    
- Red → IP
    
- Enlace → Ethernet/Wi-Fi
    

---

## 📘 **15.6 Capa de aplicación en IPv6**

Los mismos protocolos funcionan sobre IPv6, sin cambios importantes.  
Ejemplo:

- HTTP puede usar `http://[2001:db8::1]/index.html`
    
- DNS también soporta registros **AAAA** para direcciones IPv6.
    

---

## 🧠 **Resumen general del Módulo 15**

|Protocolo|Función|Puerto|Tipo|
|---|---|---|---|
|**HTTP / HTTPS**|Web|80 / 443|TCP|
|**DNS**|Resolución de nombres|53|UDP / TCP|
|**DHCP**|Asignación de IP|67 / 68|UDP|
|**FTP / SFTP**|Transferencia de archivos|21|TCP|
|**SMTP**|Envío de correo|25|TCP|
|**POP3 / IMAP**|Recepción de correo|110 / 143|TCP|
|**SSH / Telnet**|Acceso remoto|22 / 23|TCP|
|**SMB / AFP**|Compartición de archivos|445 / 548|TCP|
|**NTP**|Sincronización de hora|123|UDP|

---

## 🧩 **15.7 Resumen visual: Cliente/Servidor vs P2P**

|Característica|Cliente/Servidor|P2P|
|---|---|---|
|Control|Centralizado (servidor)|Distribuido|
|Seguridad|Alta (control central)|Menor (sin control)|
|Escalabilidad|Limitada por el servidor|Muy alta|
|Ejemplos|Web, correo, FTP|BitTorrent, eMule|

---

### 💡 **Ejemplo práctico final**

**Escenario:**  
Una PC se conecta a Internet y abre `www.google.com`.

1. **DHCP** asigna una IP a la PC.
    
2. **DNS** resuelve el nombre `www.google.com`.
    
3. **TCP (puerto 443)** establece conexión con el servidor HTTPS.
    
4. **HTTP/HTTPS** transfiere la página.
    
5. El usuario ve el contenido en su navegador.
    

✅ Todo ese proceso ocurre gracias a los **protocolos de la capa de aplicación**.

---

## 📘 **Resumen Final**

|Concepto clave|Descripción|
|---|---|
|**Capa de Aplicación**|Interfaz entre el usuario y la red.|
|**Protocolos más usados**|HTTP, DNS, DHCP, FTP, SMTP, POP3, IMAP, SSH.|
|**Modelo Cliente/Servidor**|Servidor presta servicios; cliente los solicita.|
|**Modelo P2P**|Todos los nodos son iguales.|
|**DHCP (DORA)**|Discover, Offer, Request, Acknowledge.|
|**DNS**|Traduce nombres ↔ IP.|
|**Puertos**|Identifican servicios (HTTP 80, HTTPS 443, DNS 53, etc.).|
|**Seguridad**|HTTPS y SSH ofrecen cifrado.|

---

¿Quieres que sigamos con la **Unidad 16 (Seguridad de red)**?  
Esa te enseña sobre **amenazas, vulnerabilidades, tipos de ataques y medidas de protección**, muy frecuente en parciales.




# **MÓDULO 16 – Fundamentos de Seguridad de Red (ITN v7.0)**

---

## 🧠 **16.1 Conceptos básicos de seguridad de red**

### 📘 **Propósito**

La seguridad de red consiste en **proteger la red, sus dispositivos y datos** frente a accesos no autorizados, ataques o daños.

La idea es mantener tres principios fundamentales conocidos como la **Tríada CIA**:

|Principio|Descripción|Ejemplo|
|---|---|---|
|**Confidencialidad**|Solo usuarios autorizados acceden a la información.|Cifrado de datos (HTTPS, VPN).|
|**Integridad**|Los datos no deben ser alterados sin autorización.|Sumas de comprobación (hashing).|
|**Disponibilidad**|Los recursos deben estar accesibles para los usuarios válidos.|Redundancia, backups, firewalls.|

---

### 🔹 **Amenazas comunes en una red**

1. **Acceso no autorizado**
    
    - Intrusos acceden a información o sistemas sin permiso.
        
2. **Interrupción del servicio**
    
    - Causar que los sistemas dejen de funcionar (ataques DoS).
        
3. **Robo de información**
    
    - Copiar o interceptar datos confidenciales (credenciales, correos, etc.).
        
4. **Daños físicos o lógicos**
    
    - Destruir o modificar archivos, servidores o dispositivos.
        

---

### 💡 **Ejemplo:**

Un atacante podría interceptar los datos de una conexión HTTP (sin cifrar) y ver contraseñas o mensajes enviados → se compromete la **confidencialidad**.

---

## 🔐 **16.2 Tipos de vulnerabilidades**

Las **vulnerabilidades** son **debilidades** que pueden ser explotadas por amenazas.  
Pueden clasificarse según su origen:

|Tipo de vulnerabilidad|Descripción|Ejemplo|
|---|---|---|
|**Tecnológica**|Errores o fallos en el software o hardware.|Sistema operativo desactualizado.|
|**De configuración**|Mala configuración de dispositivos.|Router con contraseña “admin123”.|
|**De políticas de seguridad**|Falta de reglas claras o de cumplimiento.|Usuarios que comparten contraseñas.|
|**Humanas**|Errores o engaños a usuarios.|Phishing, ingeniería social.|

📍 **Cualquier red es tan segura como su punto más débil.**

---

### 🔹 **Amenazas físicas vs lógicas**

|Tipo|Ejemplo|Contramedida|
|---|---|---|
|**Física**|Robo de equipos, incendios, humedad.|Controles de acceso, alarmas, UPS.|
|**Lógica**|Virus, ataques remotos, contraseñas débiles.|Antivirus, firewalls, autenticación.|

---

## 💣 **16.3 Tipos de ataques comunes**

Los ataques a redes pueden clasificarse según su **objetivo** o **método**:

---

### 🔹 **1. Ataques de reconocimiento (reconnaissance)**

El atacante busca **información sobre la red** (IP, puertos, servicios, etc.).

Ejemplo:

- Escaneo de puertos con herramientas como **Nmap**.
    
- Consultas DNS o SNMP para obtener información.
    

**Contramedidas:**

- Firewalls y filtrado de puertos.
    
- Desactivar servicios innecesarios.
    

---

### 🔹 **2. Ataques de acceso (access attacks)**

El atacante intenta **acceder a recursos no autorizados**.

Ejemplos:

- **Robo de contraseñas** (fuerza bruta, diccionario).
    
- **Explotación de vulnerabilidades** en sistemas o routers.
    
- **Phishing** o **ingeniería social**.
    

**Contramedidas:**

- Autenticación fuerte.
    
- Políticas de contraseñas.
    
- Cifrado de datos.
    

---

### 🔹 **3. Ataques de denegación de servicio (DoS y DDoS)**

Buscan **saturar la red o un servidor** para que no pueda atender usuarios legítimos.

- **DoS (Denial of Service):** desde un solo origen.
    
- **DDoS (Distributed DoS):** desde muchos equipos (botnets).
    

💡 Ejemplo:  
Un ataque DDoS puede enviar millones de solicitudes falsas a un servidor web, dejándolo fuera de servicio.

**Contramedidas:**

- Firewalls y sistemas de detección (IDS/IPS).
    
- Filtrado de tráfico y balanceadores de carga.
    

---

### 🔹 **4. Ataques de malware**

El atacante introduce **software malicioso** para dañar o controlar dispositivos.

|Tipo|Descripción|
|---|---|
|**Virus**|Se adjunta a un archivo y se propaga al ejecutarlo.|
|**Gusano (worm)**|Se propaga automáticamente por la red.|
|**Troyano**|Finge ser un programa legítimo.|
|**Spyware**|Espía la actividad del usuario.|
|**Ransomware**|Cifra los datos y exige rescate.|

**Contramedidas:**

- Antivirus actualizado.
    
- No abrir archivos sospechosos.
    
- Copias de seguridad regulares.
    

---

### 🔹 **5. Ataques de intermediario (Man-in-the-Middle – MITM)**

El atacante **intercepta y modifica la comunicación** entre dos dispositivos.

Ejemplo:

- Capturar tráfico entre cliente y servidor en una red Wi-Fi pública.
    

**Contramedidas:**

- Cifrado (HTTPS, VPN, SSH).
    
- No usar redes públicas sin protección.
    

---

### 🔹 **6. Ataques de suplantación (Spoofing)**

El atacante **finge ser otro dispositivo o usuario**.

Tipos:

- **IP spoofing:** falsifica dirección IP.
    
- **MAC spoofing:** cambia la dirección MAC.
    
- **Email spoofing:** falsifica direcciones de correo.
    

**Contramedidas:**

- Filtrado de direcciones.
    
- Autenticación.
    
- Políticas de correo seguras (SPF, DKIM).
    

---

## ⚙️ **16.4 Seguridad en dispositivos de red**

Los dispositivos de red (routers, switches, APs) deben configurarse correctamente para evitar accesos no autorizados.

---

### 🔹 **Buenas prácticas de seguridad en routers y switches**

1. **Cambiar contraseñas por defecto**
    
    ```bash
    Router(config)# enable secret <clave_segura>
    Router(config)# line vty 0 4
    Router(config-line)# password <clave_segura>
    ```
    
2. **Usar acceso remoto seguro (SSH, no Telnet)**
    
    ```bash
    Router(config)# ip domain-name red.local
    Router(config)# crypto key generate rsa
    Router(config)# line vty 0 4
    Router(config-line)# transport input ssh
    ```
    
3. **Cifrar contraseñas**
    
    ```bash
    Router(config)# service password-encryption
    ```
    
4. **Deshabilitar servicios innecesarios**  
    Ejemplo: HTTP, CDP o SNMP si no se usan.
    
5. **Configurar banners de advertencia**
    
    ```bash
    Router(config)# banner motd #Acceso no autorizado prohibido#
    ```
    
6. **Guardar la configuración**
    
    ```bash
    Router# copy running-config startup-config
    ```
    

---

### 💡 **Seguridad física**

- Guardar los equipos en **salas cerradas** y con **control de acceso**.
    
- Usar **UPS (alimentación ininterrumpida)**.
    
- Evitar exposición a polvo, humedad o calor.
    

---

## 🧱 **16.5 Protección de datos y usuarios**

### 🔹 **Métodos de autenticación**

Verifican la identidad del usuario.

|Tipo|Descripción|Ejemplo|
|---|---|---|
|**Contraseña**|Más común, pero débil si es simple.|Login de red.|
|**Autenticación de dos factores (2FA)**|Combina contraseña + código o huella.|Google Authenticator.|
|**Certificados digitales**|Usados en HTTPS y VPNs.|SSL/TLS.|

---

### 🔹 **Cifrado**

Protege los datos durante la transmisión o almacenamiento.

|Tipo|Ejemplo|Uso|
|---|---|---|
|**Simétrico**|AES, DES|Misma clave para cifrar/descifrar.|
|**Asimétrico**|RSA|Clave pública y privada.|
|**Hashing**|SHA-256, MD5|Verifica integridad, no se puede revertir.|

💡 **HTTPS, SSH y VPNs** usan cifrado para garantizar la confidencialidad.

---

## 🧠 **16.6 Herramientas y tecnologías de seguridad**

|Herramienta / Tecnología|Función|
|---|---|
|**Firewall**|Filtra tráfico permitido o bloqueado.|
|**IDS / IPS**|Detecta (IDS) o bloquea (IPS) ataques.|
|**Antivirus / Antimalware**|Protege contra programas maliciosos.|
|**VPN (Virtual Private Network)**|Crea un canal seguro sobre Internet.|
|**ACL (Access Control List)**|Define qué tráfico puede entrar o salir de una interfaz.|
|**Backup y redundancia**|Evitan pérdida de datos y mejoran disponibilidad.|

---

## 📘 **16.7 Seguridad del usuario final**

El **usuario** suele ser el eslabón más débil.  
Por eso, se aplican medidas de **concientización y políticas de seguridad**:

|Recomendación|Ejemplo|
|---|---|
|**Usar contraseñas seguras**|Mínimo 8 caracteres, mezcla de símbolos.|
|**Actualizar software**|Parchear vulnerabilidades.|
|**Evitar sitios o correos sospechosos**|Protección contra phishing.|
|**Usar antivirus y cortafuegos personales**|Protección básica.|
|**Bloquear sesiones inactivas**|Evitar accesos no autorizados.|

---

## 💡 **16.8 Ejemplo de política de seguridad**

**Objetivo:** proteger los recursos de una red escolar o empresarial.

1. Todos los usuarios deben autenticarse.
    
2. Contraseñas deben cambiarse cada 90 días.
    
3. El acceso remoto solo por SSH o VPN.
    
4. Se bloquean sitios maliciosos o inapropiados.
    
5. Se realizan respaldos semanales.
    
6. Solo el personal autorizado puede modificar equipos de red.
    

---

## 📘 **Resumen general del Módulo 16**

|Concepto|Descripción|
|---|---|
|**Seguridad de red**|Protección de datos, dispositivos y usuarios.|
|**Tríada CIA**|Confidencialidad, Integridad, Disponibilidad.|
|**Amenazas comunes**|Malware, DoS, spoofing, phishing, MITM.|
|**Vulnerabilidades**|Tecnológicas, de configuración, humanas.|
|**Ataques**|Reconocimiento, acceso, DoS, malware, MITM.|
|**Dispositivos seguros**|Contraseñas, SSH, cifrado, banners, backups.|
|**Herramientas**|Firewall, IDS/IPS, VPN, antivirus.|
|**Autenticación y cifrado**|Contraseñas, 2FA, RSA, AES, SSL/TLS.|
|**Seguridad física**|Acceso controlado, UPS, entorno seguro.|

---

### 💡 **Resumen visual: Capa de seguridad en acción**

|Capa|Ejemplo de medida|
|---|---|
|**Física**|Control de acceso, cámaras.|
|**Red**|Firewalls, ACLs, IDS/IPS.|
|**Transporte**|SSL/TLS (HTTPS, SSH).|
|**Aplicación**|Autenticación, antivirus, políticas.|
|**Usuario**|Capacitación y concientización.|

---

¿Quieres que sigamos con la **Unidad 17 (Construir una red pequeña)**?  
Esa es la última del parcial y reúne **todos los conceptos anteriores** (IP, routers, protocolos y seguridad) para **diseñar una red funcional real**.





# **MÓDULO 17 – Construir una red pequeña (ITN v7.0)**

---

## 🧠 **17.1 Dispositivos de una red pequeña**

### 📘 **Concepto general**

Una **red pequeña** es aquella que conecta **un número limitado de dispositivos** (normalmente de 5 a 50), y suele tener **una única conexión WAN** hacia Internet (por DSL, fibra o cable).

Estas redes deben ser:

- **Eficientes**
    
- **Seguras**
    
- **Fáciles de administrar**
    

🧠 En este tipo de redes, **un solo técnico o administrador** suele encargarse de la instalación, mantenimiento y soporte.

---

### 🔹 **Componentes de una red pequeña**

|Tipo de dispositivo|Función|
|---|---|
|**Dispositivos finales**|Computadoras, impresoras, cámaras IP, teléfonos VoIP.|
|**Dispositivos intermedios**|Switches, routers, puntos de acceso inalámbrico.|
|**Servidores**|DHCP, DNS, correo, archivos, web.|
|**Medios de conexión**|Cables UTP, fibra óptica o redes Wi-Fi.|
|**Conexión WAN**|Acceso a Internet (ISP mediante router o módem).|

---

### 🔹 **Topologías de red pequeñas**

Las redes pequeñas suelen usar topologías **en estrella** o **mixtas**, donde todos los dispositivos se conectan a un **switch central** o **router inalámbrico**.

📘 Imagen sugerida (ver diapositiva):  
_Topología de una red pequeña con router, switch y PC._

---

## ⚙️ **17.1.1 Selección de dispositivos**

Cuando se diseña una red pequeña, se deben considerar varios **factores técnicos y económicos**.

|Factor|Descripción|
|---|---|
|**Costo**|El presupuesto influye en el tipo de equipo (doméstico o empresarial).|
|**Velocidad y tipo de puertos**|Determina la capacidad de la red (Fast Ethernet, Gigabit, etc.).|
|**Capacidad de expansión**|Permite agregar más usuarios o dispositivos en el futuro.|
|**Características del sistema operativo del dispositivo**|Ejemplo: IOS de Cisco con funciones avanzadas de seguridad, QoS, VLANs.|

💡 **Ejemplo:**  
En una empresa pequeña (10 PCs y 2 impresoras), un **switch de 24 puertos** y un **router con Wi-Fi y DHCP** puede ser suficiente.

---

## 🌐 **17.1.2 Asignación de direcciones IP**

### 📘 **Importancia**

Antes de implementar una red, se debe crear un **plan de direccionamiento IP** bien organizado.  
Esto facilita la **administración**, la **resolución de problemas** y la **seguridad**.

---

### 🔹 **Pasos para crear un esquema de direccionamiento**

1. **Identificar los dispositivos finales**
    
    - PCs, impresoras, cámaras, servidores, puntos de acceso.
        
2. **Definir las redes o subredes**
    
    - Ejemplo:
        
        - VLAN 10 – Administración
            
        - VLAN 20 – Ventas
            
        - VLAN 30 – Visitantes
            
3. **Asignar direcciones IP por tipo de dispositivo**
    
    - Ejemplo:
        
        |Dispositivo|IP ejemplo|
        |---|---|
        |Router|192.168.1.1|
        |Servidor|192.168.1.10|
        |Impresora|192.168.1.20|
        |PC Usuario|192.168.1.100–150|
        
4. **Planificar rangos DHCP**
    
    - Para hosts dinámicos (PCs, móviles).
        
    - Ejemplo: `192.168.1.100 - 192.168.1.200`
        
5. **Documentar la red**
    
    - Registrar qué IP tiene cada dispositivo y a qué VLAN pertenece.
        

📘 Imagen sugerida: _Ejemplo de tabla de direccionamiento IP._

---

## 🔁 **17.1.3 Redundancia en redes pequeñas**

Aunque las redes pequeñas suelen tener pocos dispositivos, **la redundancia** mejora la **confiabilidad** y **disponibilidad**.

|Tipo de redundancia|Ejemplo|
|---|---|
|**Equipos duplicados**|Dos routers o switches principales.|
|**Enlaces duplicados**|Dos conexiones WAN o dos cables entre switches.|
|**Energía**|UPS o fuentes redundantes.|

💡 Esto ayuda a evitar que un **único punto de falla** deje sin servicio a toda la red.

---

## 🚦 **17.1.4 Administración del tráfico y QoS**

### 📘 **Objetivo**

Optimizar el rendimiento y priorizar los datos más importantes, especialmente los **servicios en tiempo real** (voz, video, conferencias).

### 🔹 **QoS (Quality of Service)**

Permite que el router o switch **clasifique el tráfico** y le dé prioridad según su tipo.

|Nivel de prioridad|Tipo de tráfico|Ejemplo|
|---|---|---|
|**Alta**|Voz, videollamadas|VoIP, Webex|
|**Media**|Navegación y correo|HTTP, SMTP|
|**Baja**|Descargas o actualizaciones|FTP, actualizaciones Windows|

📘 Los routers Cisco tienen **cuatro colas de prioridad**, y la **alta prioridad se vacía primero**.

---

## 💻 **17.2 Aplicaciones y protocolos en redes pequeñas**

Después del diseño físico y lógico, una red necesita **aplicaciones y protocolos** que le den funcionalidad.

---

### 🔹 **Aplicaciones comunes**

Las empresas pequeñas suelen usar aplicaciones locales y en la nube:

|Tipo de aplicación|Ejemplo|
|---|---|
|**Correo electrónico**|Gmail, Outlook, servidores SMTP/IMAP.|
|**Navegación web**|HTTP/HTTPS.|
|**Archivos compartidos**|Servidores SMB, Google Drive.|
|**Videoconferencia**|Webex, Zoom, Meet.|
|**Gestión**|ERP, bases de datos.|

---

### 🔹 **Protocolos de red más usados**

|Protocolo|Función|Descripción|
|---|---|---|
|**HTTP / HTTPS**|Web|Transferencia de páginas web.|
|**SMTP / POP3 / IMAP**|Correo|Envío y recepción de correos electrónicos.|
|**FTP / SFTP**|Archivos|Transferencia de archivos cliente-servidor.|
|**DNS**|Nombres|Traduce nombres a IP.|
|**DHCP**|Configuración|Asigna IPs automáticamente.|
|**SSH / Telnet**|Administración|Acceso remoto (SSH seguro).|

💡 **Importante:**  
Muchas empresas exigen usar las **versiones seguras** de los protocolos:

- **HTTPS** en lugar de HTTP
    
- **SFTP** en lugar de FTP
    
- **SSH** en lugar de Telnet
    

---

## 🎙️ **17.2.1 Aplicaciones de voz y video**

Cada vez más redes pequeñas integran servicios de **telefonía IP y videoconferencia**.

Para que estos funcionen bien:

- La infraestructura debe soportar **ancho de banda suficiente**.
    
- Se debe implementar **QoS** para priorizar tráfico en tiempo real.
    

|Requisito|Explicación|
|---|---|
|**Capacidad de red adecuada**|Switches Gigabit, routers modernos.|
|**QoS configurado**|Priorizar paquetes de voz/video.|
|**Latencia baja**|< 150 ms para llamadas claras.|

---

## 🔒 **17.3 Seguridad en redes pequeñas**

La seguridad sigue siendo esencial, incluso en redes pequeñas.

---

### 🔹 **Buenas prácticas básicas**

1. **Cambiar contraseñas por defecto.**
    
2. **Actualizar firmware y software de routers/switches.**
    
3. **Desactivar servicios innecesarios.**
    
4. **Habilitar SSH en lugar de Telnet.**
    
5. **Usar cifrado WPA3 en redes Wi-Fi.**
    
6. **Configurar un firewall o ACLs.**
    
7. **Hacer respaldos regulares.**
    
8. **Aplicar banners de advertencia:**
    
    ```bash
    Router(config)# banner motd #Acceso no autorizado prohibido#
    ```
    

---

### 🔹 **Seguridad inalámbrica**

|Tipo|Descripción|
|---|---|
|**WPA2/WPA3**|Cifrado fuerte en Wi-Fi.|
|**SSID oculto**|No se muestra el nombre de la red.|
|**MAC Filtering**|Solo ciertos dispositivos pueden conectarse.|

---

## 🧩 **17.4 Solución de problemas en redes pequeñas**

Los problemas pueden deberse a **errores físicos, de configuración o lógicos**.

### 🔹 **Metodología de diagnóstico**

1. **Identificar el problema**
    
    - “No hay conexión”, “No imprime”, etc.
        
2. **Recolectar información**
    
    - IP del equipo, ping, cableado, configuración.
        
3. **Probar conectividad (ping y traceroute)**
    
    - `ping 192.168.1.1` → prueba conexión local.
        
    - `ping 8.8.8.8` → prueba Internet.
        
    - `traceroute 8.8.8.8` → rastrea la ruta de red.
        
4. **Verificar configuración**
    
    - `show ip interface brief`
        
    - `show running-config`
        
5. **Reiniciar o reemplazar hardware si es necesario.**
    

---

### 🔹 **Herramientas de diagnóstico**

|Herramienta|Función|
|---|---|
|**ping**|Comprueba conectividad.|
|**traceroute**|Muestra el camino de los paquetes.|
|**ipconfig / ifconfig**|Muestra la configuración IP.|
|**show commands (Cisco)**|Verificación en routers/switches.|
|**Packet Tracer**|Simula redes para práctica y pruebas.|

---

## 📘 **17.5 Resumen general del Módulo 17**

|Tema|Descripción|
|---|---|
|**Diseño de red pequeña**|Plan simple, dispositivos adecuados, IP bien asignadas.|
|**Dispositivos principales**|Router, switch, AP, PCs, servidores.|
|**Direcciones IP**|Planificación clara y documentada.|
|**Redundancia**|Equipos o enlaces duplicados para evitar fallas.|
|**QoS**|Priorización del tráfico de voz y video.|
|**Protocolos esenciales**|HTTP, DNS, DHCP, SSH, FTP, SMTP, IMAP.|
|**Seguridad básica**|Contraseñas, SSH, WPA3, firewall, actualizaciones.|
|**Solución de problemas**|Ping, traceroute, comandos de verificación.|
|**Administrador de red**|Planifica, protege y optimiza la red.|

---

### 💡 **Resumen visual: ejemplo de red pequeña**

```
                 Internet (ISP)
                      |
                [Router con DHCP]
                      |
          ---------------------------
          |           |            |
        [Switch]   [AP Wi-Fi]   [Servidor]
          |
    --------------------------
    |    |    |     |        |
   PC1  PC2  Impresora  Teléfono IP
```

- El **router** asigna IPs mediante **DHCP** y actúa como **gateway**.
    
- El **switch** conecta los dispositivos por cable.
    
- El **AP Wi-Fi** permite acceso inalámbrico seguro.
    
- **QoS** da prioridad a la voz sobre el tráfico normal.
    
- **Firewall** protege el perímetro.
    

---

## 🧠 **Resumen final (clave para examen)**

|Concepto|Punto clave|
|---|---|
|**Diseño de red pequeña**|Sencillo, funcional, seguro.|
|**Plan IP**|Bien documentado.|
|**Redundancia**|Evita puntos únicos de falla.|
|**QoS**|Prioriza tráfico de voz/video.|
|**Protocolos esenciales**|HTTP, DNS, DHCP, SSH, SMTP.|
|**Seguridad**|Contraseñas seguras, SSH, WPA3, firewall.|
|**Solución de problemas**|Ping, traceroute, show commands.|

---

✅ **En resumen:**  
La **Unidad 17** integra todo lo aprendido — te enseña a **diseñar, configurar, proteger y mantener** una red pequeña, aplicando los principios de **direccionamiento IP, protocolos, QoS y seguridad**.

---

¿Quieres que te prepare un **mapa conceptual general del Módulo 8 al 17** (como repaso visual para el examen)?  
Puedo hacerlo con diagramas o en formato esquemático resumen.


- - -
- - - -
- - - 

# Practica 

### 🔍 **1. Ver todas las interfaces y su estado**

```bash
show ip interface brief
```

Muestra un resumen con:

- Nombre de la interfaz (`GigabitEthernet0/0/0`, `Serial0/0/0`, etc.)
    
- Dirección IP asignada
    
- Estado de línea y protocolo (up/down)
    

**Ejemplo:**

```
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     209.165.200.225 YES manual up                    up
Serial0/0/0            unassigned      YES unset  administratively down down
```

---

### 🌐 **2. Ver configuración completa (incluye gateway y IPs)**

```bash
show running-config
```

Muestra toda la configuración actual del router, incluyendo:

- Nombre del router
    
- Contraseñas
    
- Configuración de interfaces con IP y descripción
    
- Gateway por defecto (si está configurado con `ip route 0.0.0.0 0.0.0.0`)
    

**Ejemplo de salida:**

```
Router# show running-config
hostname R1
!
interface GigabitEthernet0/0
 description Link to LAN
 ip address 192.168.10.1 255.255.255.0
 no shutdown
!
ip route 0.0.0.0 0.0.0.0 209.165.200.226
```

👉 Esa última línea (`ip route 0.0.0.0 0.0.0.0 ...`) indica el **gateway predeterminado**.

---

### 🔗 **3. Ver tabla de rutas**

```bash
show ip route
```

Muestra las rutas conocidas por el router y la puerta de enlace predeterminada (si la hay).

**Ejemplo:**

```
Router# show ip route
Gateway of last resort is 209.165.200.226 to network 0.0.0.0
```

Esto indica cuál es el **default gateway**.

---

### 🧠 **4. Ver tabla ARP (si quieres saber con qué está conectado)**

```bash
show ip arp
```

Lista los dispositivos conectados directamente al router y sus direcciones MAC e IP.

---

### 💬 **5. Ver descripción de las interfaces (si las documentaste)**

```bash
show interfaces description
```

Muestra una vista rápida de las conexiones y etiquetas como:

```
R1# show interfaces description
Interface              Status         Protocol  Description
Gi0/0                  up             up        Link to LAN
Gi0/1                  up             up        Link to R2
```

---

### ✅ **Resumen rápido de comandos útiles**

|Objetivo|Comando|
|---|---|
|Ver IPs y estado|`show ip interface brief`|
|Ver configuración completa|`show running-config`|
|Ver gateway por defecto|`show ip route`|
|Ver dispositivos conectados|`show ip arp`|
|Ver descripciones de interfaces|`show interfaces description`|

---

## ⚙️ **Configuración completa de R1**

### 1️⃣ Configurar el nombre del router

```bash
Router> enable
Router# configure terminal
Router(config)# hostname R1
```

---

### 2️⃣ Desactivar la búsqueda de DNS

(Evita que el router intente resolver nombres si escribes mal un comando)

```bash
R1(config)# no ip domain-lookup
```

---

### 3️⃣ Asignar contraseñas

```bash
R1(config)# enable secret Cisconepa55        ← modo EXEC privilegiado
R1(config)# line console 0
R1(config-line)# password Cisconepa55
R1(config-line)# login
R1(config-line)# exit
```

---

### 4️⃣ Establecer requisito de longitud mínima de contraseñas

```bash
R1(config)# security passwords min-length 10
```

---

### 5️⃣ Cifrar todas las contraseñas

```bash
R1(config)# service password-encryption
```

---

### 6️⃣ Crear un banner de advertencia

(Must include “Warning” como dice la consigna)

```bash
R1(config)# banner motd #Warning: Accesso no autorizado está prohibido#
```

---

### 7️⃣ Configurar interfaces Gigabit Ethernet (según tu direccionamiento)

_(Ejemplo usando la subred 192.168.0.0/25 para Personal)_

```bash
R1(config)# interface g0/0
R1(config-if)# description Conexión a S1 - Personal
R1(config-if)# ip address 192.168.0.1 255.255.255.128
R1(config-if)# no shutdown
R1(config-if)# exit
```

(Si tienes más interfaces, repite para G0/1, G0/2, etc. con sus subredes correspondientes)

---

### 8️⃣ Configurar SSH (según indica tu guía)

1. **Asignar dominio**
    
    ```bash
    R1(config)# ip domain-name CCNA-lab.com
    ```
    
2. **Generar claves RSA**
    
    ```bash
    R1(config)# crypto key generate rsa
    How many bits in the modulus [512]: 1024
    ```
    
3. **Crear usuario local**
    
    ```bash
    R1(config)# username Admin1 privilege 15 secret Admin1pa55
    ```
    
4. **Habilitar SSH en las líneas VTY**
    
    ```bash
    R1(config)# line vty 0 4
    R1(config-line)# transport input ssh
    R1(config-line)# login local
    R1(config-line)# exec-timeout 5 0       ← cierra sesión tras 5 min de inactividad
    R1(config-line)# exit
    ```
    

---

### 9️⃣ Configurar bloqueo por intentos fallidos

```bash
R1(config)# login block-for 180 attempts 4 within 120
```

👉 Esto bloquea el acceso durante **3 minutos (180 segundos)** si alguien falla 4 intentos en 2 minutos.

---

### 🔟 Configurar timeout en la consola

(para cerrar sesión tras 5 minutos de inactividad)

```bash
R1(config)# line console 0
R1(config-line)# exec-timeout 5 0
R1(config-line)# exit
```

---

### ✅ 11️⃣ Guardar configuración

```bash
R1# copy running-config startup-config
Destination filename [startup-config]? <Enter>
```

---

## 🧾 **Resumen de configuración**

|Objetivo|Comando principal|
|---|---|
|Nombre del router|`hostname R1`|
|Desactivar DNS|`no ip domain-lookup`|
|Contraseña enable|`enable secret Cisconepa55`|
|Contraseña consola|`line console 0 → password Cisconepa55`|
|Mínimo de caracteres|`security passwords min-length 10`|
|Cifrar contraseñas|`service password-encryption`|
|Banner de advertencia|`banner motd #Warning...#`|
|Clave SSH|`crypto key generate rsa 1024`|
|Usuario admin|`username Admin1 privilege 15 secret Admin1pa55`|
|Acceso SSH|`line vty 0 4 → transport input ssh`|
|Bloqueo por intentos fallidos|`login block-for 180 attempts 4 within 120`|
|Timeout de sesión|`exec-timeout 5 0`|

`ipv6 unicast-routing` Comando para permitir que el router reenvíe paquetes ipv6

`ipv6 addres {ip v6} link-local` Comando para configurar la dirección ipv6 link-local

`no ipv6 address 2001:db8:1:5::1/64` Comando para eliminar la ip configurada 
