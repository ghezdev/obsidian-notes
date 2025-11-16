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


# 3) Configurar las **PCs** (SLAAC)

Como el ejercicio dice “establecer los cuatro hosts para **configurar automáticamente** con direcciones IPv6”:

En **cada PC** de cada LAN:

1. Abre **Desktop → IP Configuration**.
    
2. En la sección **IPv6**, selecciona **Auto Config**.
    

Listo: los routers enviarán **RA** y las PCs obtendrán automáticamente su dirección **GUA**, la **link-local** y el **gateway**.

_(Si te piden estático, usa por ejemplo `2001:db8:acad:00c8::10/64` con gateway `2001:db8:acad:00c8::1`, etc.)_



- - -
- - -


## 🧩 1️⃣ **Verifica la conexión física (cables y LEDs)**

Antes de probar pings o comandos:

- Asegúrate de que **cada cable esté bien conectado** (usa los puertos correctos).
    
- Los **LEDs deben estar en verde**:
    
    - Verde sólido = enlace activo.
        
    - Naranja = negociando (espera unos segundos).
        
    - Apagado = sin conexión.
        

Si ves rojo o apagado:  
👉 revisa que hayas usado el **tipo correcto de cable**:

|Tipo de conexión|Cable|
|---|---|
|PC ↔ Switch|Cable **Straight-through**|
|Switch ↔ Router|**Straight-through**|
|Router ↔ Router (interfaces seriales)|**Cable serial DCE/DTE**|
|Switch ↔ Switch (antiguos)|**Crossover** _(Packet Tracer los autoajusta si son modernos)_|

---

## 🧩 2️⃣ **Verifica el estado de las interfaces**

En los routers y switches:

```bash
show ip interface brief
```

Verás algo como:

```
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     10.0.0.1        YES manual up                    up
Serial0/0/0            209.165.200.1   YES manual up                    up
```

👉 Deben aparecer **“up/up”** (estado físico y lógico activo).  
Si ves **“administratively down”**, ejecuta en esa interfaz:

```bash
Router(config-if)# no shutdown
```

---

## 🧩 3️⃣ **Prueba conectividad local (entre PC y su gateway)**

Desde una **PC**, abre:  
**Desktop → Command Prompt**, y escribe:

```bash
ping <IP del gateway>
```

Por ejemplo:

```bash
ping 192.168.1.1
```

✅ Si responde → la conexión física + IP está bien.  
❌ Si no → revisa:

- Que la PC tenga la **IP y máscara correctas**.
    
- Que el **default gateway** sea la IP del router.
    
- Que el cable esté conectado al switch correcto.
    

---

## 🧩 4️⃣ **Prueba conectividad entre redes (enrutamiento)**

Si tu router tiene varias subredes, prueba **ping entre PCs de redes diferentes**:

```bash
ping <IP de PC en otra red>
```

✅ Si responde → el **router está enrutando correctamente**.  
❌ Si no responde:

- Asegúrate de que el **router tenga IPs configuradas en cada interfaz**.
    
- Verifica que **IPv4 routing esté activo** (en routers Cisco está por defecto).
    
- Si son varios routers, revisa si hay **rutas estáticas o dinámicas configuradas.**
    

---

## 🧩 5️⃣ **Verifica las tablas de enrutamiento**

En routers:

```bash
show ip route
```

Verás algo como:

```
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
C    10.0.0.0/30 is directly connected, Serial0/0/0
S    192.168.2.0/24 [1/0] via 10.0.0.2
```

👉 “C” = Conectado directamente  
👉 “S” = Ruta estática  
👉 “D”, “O”, “R” = Protocolos dinámicos (EIGRP, OSPF, RIP)

Si no ves una red que deberías alcanzar → falta ruta.

---

## 🧩 6️⃣ **Verifica direcciones IPv6 (si usas IPv6)**

Usa:

```bash
show ipv6 interface brief
```

Y prueba conectividad con:

```bash
ping ipv6 <dirección destino>
```

Ejemplo:

```bash
ping ipv6 2001:db8:acad:1::10
```

---

## 🧩 7️⃣ **Usa la herramienta de simulación (modo Simulation)**

En Packet Tracer, abajo a la derecha, cambia de **Realtime → Simulation**.

Luego:

1. Envía un **ping** desde una PC.
    
2. Mira cómo se mueven los “paquetes” entre los dispositivos.
    
3. Puedes hacer clic en cada uno para ver si se envió, recibió o falló, y en qué capa.
    

👉 Es excelente para entender **dónde se rompe la comunicación** (capa física, IP, o enrutamiento).

---

## 🧠 8️⃣ **Comprobaciones adicionales útiles**

|Comando|Función|
|---|---|
|`show running-config`|Ver toda la configuración actual|
|`show interfaces`|Detalles completos de cada interfaz|
|`show arp`|Ver la tabla ARP (vincula IP ↔ MAC)|
|`show mac address-table`|En switches, ver qué MAC están aprendidas|
|`show cdp neighbors`|Ver qué dispositivos Cisco están conectados directamente|

---

## ✅ En resumen (checklist rápido)

|Paso|Qué revisar|Comando / Herramienta|
|---|---|---|
|1️⃣|Cables correctos y LEDs verdes|Visual|
|2️⃣|Interfaces activas (up/up)|`show ip interface brief`|
|3️⃣|Ping entre PC y router local|`ping <gateway>`|
|4️⃣|Ping entre redes distintas|`ping <PC otra red>`|
|5️⃣|Tabla de rutas correcta|`show ip route`|
|6️⃣|IPv6 configurado correctamente|`show ipv6 interface brief`|
|7️⃣|Simulación de paquetes|Modo “Simulation”|
|8️⃣|Verificación general|`show running-config`, `show arp`, `show mac address-table`|

---

¿Querés que te diga **cómo hacer una verificación completa paso a paso en Packet Tracer** con ejemplos reales de comandos (por ejemplo: ping → show route → debug ip icmp)? Así podrías detectar fallos como si fueras un técnico de red.


`ip route {ip de la ruta destino} {mascara del destino} {ip del router}` Comando para que dos routers se puedan comunicar entre sí



Excelente pregunta 👏 — justo esa diferencia (usar **dos routers en lugar de uno**) es un tema clave en **topologías jerárquicas** y **diseño de redes reales**.  
Tu imagen muestra una red **dividida geográficamente y por función**, con un router en **Buenos Aires (R_BsAs)** y otro en **Pinamar (R_Pinamar)**.  
Vamos a analizar qué cambia técnica y conceptualmente 👇

---

## 🧩 1️⃣ **Distribución del tráfico y segmentación geográfica**

Con **un solo router**, toda la red dependería de un único punto de conexión:

- Todo el tráfico (de todas las sedes y VLANs) pasaría por él.
    
- Habría más carga de procesamiento y posibles cuellos de botella.
    

Con **dos routers**:

- Cada **zona o campus** (BsAs y Pinamar) maneja su **propio tráfico local**.
    
- Solo se **envía tráfico entre routers** cuando se necesita acceder a otra red (por ejemplo, un servidor o un alumno en otra sede).
    

👉 Esto reduce la carga en cada router y mejora el rendimiento general.

---

## 🧭 2️⃣ **Enrutamiento entre sedes (WAN o interconexión)**

Con dos routers se crea una **red WAN** (enlace entre routers).  
Esto permite que cada uno:

- **Administre sus propias subredes locales** (LANs, switches, PCs).
    
- **Envíe tráfico remoto** al otro router mediante una ruta estática o un protocolo dinámico.
    

Por ejemplo:

|Origen|Red local|Ruta hacia destino remoto|
|---|---|---|
|R_BsAs|20.0.0.0/21, 20.0.8.0/25, 20.0.9.0/25|Enviar vía **R_Pinamar**|
|R_Pinamar|20.0.8.128/25, 20.0.9.128/28|Enviar vía **R_BsAs**|

➡️ El enlace entre routers (línea roja) permite que ambos **compartan rutas**.

---

## 🧠 3️⃣ **Mayor escalabilidad**

- Si tu red crece (nuevos edificios o sedes), simplemente agregas otro router y una nueva subred.
    
- Con un solo router central, las conexiones físicas se multiplican y se vuelve inmanejable.
    

👉 Dos routers permiten una **topología jerárquica**:  
**Core (interconexión)** ↔ **Distribución (routers locales)** ↔ **Acceso (switches)**.

---

## 🛡️ 4️⃣ **Seguridad y segmentación del tráfico**

Cada router puede:

- Tener **políticas de acceso diferentes** (ACLs) según la ubicación.
    
- Controlar **qué tráfico pasa** entre redes.
    
- Aplicar **filtrado o NAT** en los límites.
    

Por ejemplo:

- R_Pinamar podría filtrar acceso al **servidor IT**.
    
- R_BsAs podría permitir solo tráfico de gestión hacia esa red.
    

---

## ⚙️ 5️⃣ **Resiliencia (tolerancia a fallos)**

Con **dos routers**, si uno falla, el otro **sigue operando su propia sede**.  
Con un solo router, **toda la red cae** si ese router se apaga o se desconecta.

En redes reales, se suelen conectar los routers entre sí con **rutas redundantes o enlaces de respaldo** (para alta disponibilidad).

---

## 🌐 6️⃣ **Resumen comparativo**

|Característica|Un router|Dos routers|
|---|---|---|
|**Topología**|Centralizada|Distribuida / jerárquica|
|**Escalabilidad**|Limitada|Alta (se agregan routers por sede)|
|**Enrutamiento**|Interno solamente|Interno + WAN entre sedes|
|**Tolerancia a fallos**|Baja|Media / Alta|
|**Seguridad**|Global (todo pasa por el mismo equipo)|Local y por segmento|
|**Rendimiento**|Carga en un solo equipo|Carga distribuida|
|**Distancia física**|Ideal para una LAN|Ideal para varias ubicaciones o campus|

---

## 📘 En tu diagrama:

- **R_BsAs** concentra las redes de **Lima, Libertad y Belgrano** (sedes locales).
    
- **R_Pinamar** maneja **Alumnos e IT** (otra sede o datacenter).
    
- El enlace rojo es la **conexión WAN** (por serial o fibra simulada).
    
- Cada router **enruta entre sus LANs locales** y **usa el otro router como salida hacia las redes remotas.**
    

---

## 🧠 Ejemplo de configuración de rutas estáticas entre ambos routers

En **R_BsAs**:

```bash
ip route 20.0.8.128 255.255.255.128 <IP hacia R_Pinamar>
ip route 20.0.9.128 255.255.255.240 <IP hacia R_Pinamar>
```

En **R_Pinamar**:

```bash
ip route 20.0.0.0 255.255.248.0 <IP hacia R_BsAs>
ip route 20.0.9.0 255.255.255.128 <IP hacia R_BsAs>
```

De ese modo, los routers se “conocen” mutuamente las redes de cada lado.

---

¿Querés que te muestre **cómo se configuraría paso a paso el enlace entre ambos routers (R_BsAs ↔ R_Pinamar)** con IPs, rutas y comandos, para que puedas probarlo en Packet Tracer?



Excelente 👏 — esa es una pregunta muy práctica.  
Vamos por partes para que entiendas exactamente **qué hace** `copy running-config sftp` y **cómo hacer un backup completo** en Packet Tracer.

---

## 🧩 1. Qué significa `copy running-config sftp`

Este comando copia la **configuración activa del router o switch** (la “running-config”) hacia un **servidor remoto** usando el protocolo **SFTP (Secure File Transfer Protocol)**.

👉 En otras palabras:

> “Envía mi configuración actual por SFTP a un servidor remoto para guardarla como copia de seguridad”.

---

## ⚙️ 2. Qué copia exactamente

- La **running-config**, es decir:
    
    - Todas las configuraciones que hiciste y están **en memoria RAM**.
        
    - Incluye interfaces, contraseñas, rutas, VLANs, etc.
        
- No copia:
    
    - La **startup-config** (la que está en NVRAM).
        
    - Archivos adicionales (por ejemplo, IOS, certificados, etc.).
        

Si querés guardar lo que el router carga al iniciar, deberías copiar también la **startup-config**.

---

## 🧠 3. Diferencia entre running y startup config

|Configuración|Dónde se guarda|Cuándo se usa|Se pierde al apagar|
|---|---|---|---|
|`running-config`|RAM|Inmediatamente|✅ Sí|
|`startup-config`|NVRAM|Al iniciar el dispositivo|❌ No|

Entonces, si querés guardar los cambios actuales para que no se pierdan al apagar el router:

```bash
copy running-config startup-config
```

Y si querés hacer backup remoto:

```bash
copy startup-config sftp
```

(es más útil que guardar solo la running-config).

---

## 📦 4. Cómo hacer un **backup de todo en un solo lugar**

### Opción A – Guardar cada configuración por SFTP o TFTP

1. **Configurar un servidor SFTP o TFTP** en tu topología (lo agregás desde _End Devices → Server_).
    
2. Configurás su dirección IP.
    
3. En cada router o switch, ejecutás:
    
    ```bash
    copy startup-config sftp
    ```
    
    o
    
    ```bash
    copy running-config sftp
    ```
    
4. Ingresás:
    
    - Dirección IP del servidor
        
    - Nombre de usuario / contraseña
        
    - Nombre del archivo de destino
        

Así vas guardando cada config en el mismo servidor central (por ejemplo, “router1.cfg”, “switch2.cfg”, etc.).

---

### Opción B – Usar el servidor TFTP integrado de Packet Tracer (más fácil)

1. Colocás un **Server** desde la paleta.
    
2. Le configurás una IP (por ejemplo `192.168.1.100`).
    
3. Entrás en el router y hacés:
    
    ```bash
    copy startup-config tftp
    ```
    
4. Ingresás la IP del servidor (`192.168.1.100`).
    
5. Te pedirá el nombre del archivo → escribí algo como `R1-backup.cfg`.
    

💾 Todo quedará almacenado en la carpeta de archivos del servidor dentro de Packet Tracer.

---

### 🧰 5. Comando general de backup recomendado

```bash
copy startup-config tftp
```

o (más seguro pero requiere login)

```bash
copy startup-config sftp
```

Así tendrás **todas las configuraciones de tus routers y switches** guardadas en un solo servidor central dentro del simulador.

---

¿Querés que te muestre paso a paso (con direcciones IP, comandos y pantallazo conceptual) cómo armar ese servidor TFTP o SFTP y guardar los backups automáticamente?