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




# 🧩 **MÓDULO 11 – Direccionamiento IPv4 (ITN v7.0)**

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




# 🧩 **MÓDULO 12 – Direccionamiento IPv6 (ITN v7.0)**

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





# 🧩 **MÓDULO 13 – ICMP (ITN v7.0)**

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


