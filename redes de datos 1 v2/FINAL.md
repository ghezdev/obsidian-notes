
# ✅ **📘 PARTE 1 — FUNDAMENTOS DE REDES Y COMUNICACIONES (Resumen Completo CCNA)**

Esta parte cubre **todo lo esencial** que el estudiante debe dominar de los fundamentos para aprobar el examen.

---

## 🔹 **1. ¿Qué es una red? Tipos y elementos**

### **Concepto**

Una red es un conjunto de dispositivos que intercambian datos.

### **Tipos principales**

- **LAN**: Red local dentro de un edificio. Rápida, privada.
    
- **WAN**: Conecta redes geográficamente distantes. Lenta, costosa.
    
- **WLAN**: LAN inalámbrica.
    
- **MAN**: Red metropolitana.
    
- **SAN**: Red de almacenamiento.
    

### **Componentes de una red**

- **Host** (PC, laptop, celular).
    
- **Switch** (Capa 2).
    
- **Router** (Capa 3).
    
- **Medios**: UTP, fibra, wireless.
    
- **Servicios**: DHCP, DNS, NAT, VPN.
    

---

## 🔹 **2. Modelo OSI y TCP/IP**

### **Modelo OSI (7 capas)**

1. **Física** → señales, cables, conectores
    
2. **Enlace de Datos** → tramas, MAC, switches
    
3. **Red** → IP, routers, paquetes
    
4. **Transporte** → TCP/UDP
    
5. **Sesión** → control de sesiones
    
6. **Presentación** → cifrado, formato
    
7. **Aplicación** → HTTP, DNS, FTP
    

### **Modelo TCP/IP (4 capas)**

- Acceso a la red
    
- Internet
    
- Transporte
    
- Aplicación
    

**OSPF, EIGRP → Capa 3**  
**TCP/UDP → Capa 4**  
**HTTP, DNS, DHCP → Capa 7**

> En el examen: te preguntan mucho qué hace cada capa y qué protocolo corresponde a qué capa.

---

## 🔹 **3. Encapsulación y PDU (Unidad de Datos de Protocolo)**

El proceso cuando un usuario envía datos:

Aplicación → Transporte → Red → Enlace → Física

| Capa       | Nombre de la PDU |
| ---------- | ---------------- |
| Aplicación | Datos            |
| Transporte | Segmento         |
| Red        | Paquete          |
| Enlace     | Trama            |
| Física     | Bits             |

Proceso inverso en el host de destino = **desencapsulación**.

> Muy preguntado: ¿en qué capa se encuentra un paquete? → Capa 3.

---

## 🔹 **4. Direccionamiento en redes: MAC, IPv4, IPv6**

### **MAC**

- 48 bits, hexadecimal.
    
- Única, grabada en el hardware.
    
- Usada por switches en Capa 2.
    

### **IPv4**

- 32 bits → formato decimal con puntos.
    
- Tipos:
    
    - Unicast → host específico
        
    - Broadcast → 255.255.255.255
        
    - Multicast → 224.0.0.0/4
        

### **IPv6**

- 128 bits, hexadecimal.
    
- Tipos:
    
    - **Global Unicast** (equivalente a pública)
        
    - **Link-local** (FE80::/10) → obligatoria para IPv6
        
    - **Loopback ::1**
        
    - **Multicast FF00::/8**
        

> En el examen suelen preguntar: “¿Cuál es una dirección link-local válida?” → FE80::/10.

---

## 🔹 **5. Subneteo IPv4 e IPv6 (conceptos clave para el examen)**

Aunque en esta parte no hacemos ejercicios, **los conceptos fundamentales son**:

### **Subred IPv4**

- Break de red = AND entre IP y máscara.
    
- Broadcast = último host.
    
- Hosts válidos = entre ambos extremos.
    

**Ejemplo rápido**  
Red: 192.168.10.0/24  
Máscara: /24 = 255.255.255.0  
Host válidos: .1 a .254  
Broadcast: .255

### **VLSM**

Permite crear subredes de tamaños diferentes para no desperdiciar IP.

### **IPv6**

Sin broadcast → usa multicast.  
Las subredes casi siempre son /64.

---

## 🔹 **6. Protocolos esenciales: ARP, ICMP, DHCP, DNS**

### **ARP (Address Resolution Protocol)**

- Convierte IP → MAC.
    
- Solo en IPv4.
    
- Muy frecuente en preguntas del examen.
    

### **ICMP**

- ping
    
- traceroute
    
- mensajes de error (host unreachable, TTL expired)
    

### **DHCP**

Proceso **DORA**:

1. **Discover**
    
2. **Offer**
    
3. **Request**
    
4. **ACK**
    

> Direcciones 169.254.x.x = fallo de DHCP (APIPA).

### **DNS**

Convierte **nombres ↔ direcciones IP**.

---

## 🔹 **7. TCP vs UDP**

### **TCP**

- Confiable
    
- Orientado a conexión
    
- Handshake de 3 pasos (SYN, SYN-ACK, ACK)
    
- Reenvío, control de flujo, ventanas
    

Ejemplos: HTTP, HTTPS, FTP, SMTP

### **UDP**

- No confiable
    
- Sin conexión
    
- Más rápido
    
- Sin reenvíos
    

Ejemplos: DNS consultas, VoIP, streaming.

> Pregunta típica: ¿Qué protocolo usar para baja latencia? → UDP.

---

## 🔹 **8. Rendimiento y parámetros clave**

- **Ancho de banda**: capacidad instalada.
    
- **Throughput**: lo real que se transmite.
    
- **Latencia**: tiempo que tarda en viajar un paquete.
    
- **Jitter**: variación en la latencia.
    
- **Pérdida de paquetes**: mala calidad o congestión.
    

---

## 🔹 **9. Ethernet y medios físicos**

- Cable UTP → categorías (5e, 6, 6a).
    
- Tipos de fibra → multimodo vs monomodo.
    
- Normalmente:
    
    - Router–PC → cable recto
        
    - Switch–PC → cable recto
        
    - Switch–Switch → cable cruzado
        
    - Pero hoy todo es **Auto-MDI/MDIX**.
        

### Trama Ethernet:

- MAC destino
    
- MAC origen
    
- Tipo/Longitud
    
- Datos
    
- FCS (CRC)
    

> Pregunta típica: “¿Qué campo detecta errores?” → FCS.

---

## 🔹 **10. Comandos básicos de diagnóstico**

- `ping` → conectividad
    
- `traceroute` / `tracert` → saltos
    
- `nslookup` → DNS
    
- `ipconfig` / `ifconfig`
    
- `show ip interface brief`
    
- `show mac address-table`
    

---


# ✅ **📘 PARTE 2 — SWITCHING, VLANs, TRUNKING Y REDUNDANCIA**

---

## 🔹 **1. Funcionamiento de un switch (Capa 2)**

### **Tabla MAC (CAM table)**

El switch aprende direcciones MAC observando la **dirección MAC de origen** de las tramas que entran por cada puerto.

- Si conoce la MAC destino → reenvía por un único puerto (unicast).
    
- Si NO la conoce → hace **flooding** por todos los puertos.
    
- Si la trama es broadcast o multicast → se envía por todos los puertos.
    

### **Envejecimiento**

Las entradas MAC se eliminan después de 300 segundos (aprox.), o cuando cambia la topología.

### **Switching interno**

- **Store-and-forward**: almacena toda la trama y verifica FCS → más seguro.
    
- **Cut-through**: reenvía rápidamente sin verificar → menos seguro.
    

---

## 🔹 **2. VLANs (Virtual LANs)**

### **¿Qué es una VLAN?**

Una red lógica dentro de un switch para separar dominios de broadcast.

### **Beneficios:**

- Más seguridad
    
- Menor congestión
    
- Segmentación de usuarios/departamentos
    
- Soporte para VoIP
    

### **Tipos de puertos**

- **Access port** → pertenece a una sola VLAN.
    
- **Trunk port** → transporta múltiples VLAN mediante etiquetado 802.1Q.
    

### **VLAN por defecto**

- VLAN 1 → nativa y de administración (no recomendado).
    
- Los ports nuevos = VLAN 1 por defecto.
    

### **VLAN nativa**

En los trunks, los frames sin etiqueta viajan en la VLAN nativa (por defecto VLAN 1).

> Pregunta típica: “Un mismatch de VLAN nativa puede generar fallos de tráfico o riesgos de seguridad.”

---

## 🔹 **3. Trunking – 802.1Q**

### **802.1Q**

Agrega una etiqueta de 4 bytes dentro de la trama Ethernet para transportar VLANs.

### **Comandos básicos**

```
switchport mode trunk
switchport trunk native vlan X
switchport trunk allowed vlan 10,20,30
```

### **Problemas comunes**

- VLAN no permitida en el trunk → no hay comunicación.
    
- VLAN nativa diferente → error, posible brecha de seguridad.
    
- El puerto no está en modo trunk.
    

---

## 🔹 **4. Inter-VLAN Routing**

Los hosts en VLANs distintas **no pueden comunicarse sin un router**.

### Métodos:

1. **Router-on-a-stick**
    
    - Un router con subinterfaces etiquetadas por VLAN
        
    - Conexión a un trunk del switch
        
2. **Switch multilayer (Capa 3)**
    
    - Interfaces VLAN (SVI)
        
    - `ip routing` habilitado en el switch
        

### Ejemplo Router-on-a-stick:

```
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
```

---

## 🔹 **5. STP — Spanning Tree Protocol**

STP evita **bucles de capa 2**, que causarían:

- Broadcast storms
    
- Tabla MAC inestable
    
- Caída de la red
    

### **Conceptos clave**

- **Root Bridge**: switch central elegido por prioridad + MAC.
    
- **Puertos en el root**:
    
    - Root port
        
    - Designated port
        
    - Blocking
        
- **Estados**:
    
    - Blocking
        
    - Listening
        
    - Learning
        
    - Forwarding
        

### **Tipos de STP**

- **STP (802.1D)** → lento
    
- **RSTP (802.1w)** → rápido
    
- **MSTP** → multiples instancias
    

> Cisco ama preguntar:  
> “¿Por qué STP pone un puerto en estado blocking?” → Para evitar loops.

---

## 🔹 **6. EtherChannel (LACP/PAgP)**

Agrupa múltiples enlaces físicos en uno lógico para:

- Más ancho de banda
    
- Redundancia
    
- Balanceo de carga
    

### **Protocolos**

- **LACP (IEEE 802.3ad)** → estándar
    
- **PAgP** → propietario Cisco
    
- **On** → sin negociación (peligroso si no coincide)
    

### Modos LACP:

- **active** ↔ negotiation
    
- **passive** ↔ responde
    
- Para formar EtherChannel:
    
    - active ↔ passive
        
    - active ↔ active
        

> Muy preguntado: “Para EtherChannel, todos los puertos deben tener la misma configuración (VLAN, velocidad, dúplex).”

---

## 🔹 **7. Redes redundantes y alta disponibilidad**

### **Redundancia**

La idea es tener **más de un camino** para evitar puntos únicos de falla.

Ejemplos:

- Dos switches core
    
- Dos uplinks
    
- Dos caminos entre switches
    
- EtherChannel
    

### **Herramientas para verificar conectividad**

- `show cdp neighbors` → ver dispositivos adjuntos
    
- `show interfaces trunk` → verificar trunks
    
- `show spanning-tree` → ver puertos bloqueados
    
- `show etherchannel summary` → verificar grupos
    

---

## 🔹 **8. Seguridad de Capa 2**

Los ataques más comunes:

- **MAC flooding**
    
- **DHCP spoofing**
    
- **VLAN hopping**
    
- **ARP spoofing**
    

### **Contramedidas (muy preguntadas en el examen)**

✔ **Port security**

```
switchport port-security
switchport port-security maximum 2
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

✔ **DHCP Snooping**

✔ **Dynamic ARP Inspection (DAI)**

✔ **BPDU Guard**  
Protege puertos access ante conexiones no autorizadas de switches.

✔ **Root Guard**  
Evita que switches no autorizados se conviertan en root.

---

## 🔹 **9. Troubleshooting de switches**

Preguntas típicas del examen:

- **PC no tiene red → revisar VLAN del puerto**
    
    - `show vlan brief`
        
- **No hay comunicación entre switches**
    
    - problema de trunk
        
    - VLAN no permitida
        
    - vlan nativa mismatch
        
- **STP bloqueando un puerto**
    
    - `show spanning-tree`
        
- **MAC no aparece**
    
    - cable suelto
        
    - otro puerto
        
    - la VLAN no existe o no está activa
        

---
Aquí tenés **LA PARTE 3 COMPLETA**, una de las más importantes del CCNA: **Routing, Subneteo, OSPF y NAT**.  
Esto representa aproximadamente **30–40% del examen**, así que prestale mucha atención.

---

# ✅ **📘 PARTE 3 — ROUTING, SUBNETEO, OSPF y NAT**

---

## 🔹 **1. Routing — Conceptos Fundamentales**

### **¿Qué es el enrutamiento?**

Proceso por el cual un router decide **a qué red enviar los paquetes** basándose en la **tabla de routing**.

### **Tipos de rutas**

- **Conectada directamente (C)**  
    → aparece cuando configurás una IP en la interfaz del router.
    
- **Local (L)**  
    → la IP asignada a la interfaz del router.
    
- **Estática (S)**  
    → agregadas manualmente.
    
- **Default (0.0.0.0/0)**  
    → ruta por defecto cuando no sabe adónde enviar un paquete.
    
- **Dinámicas (R, O, D)**  
    → aprendidas por protocolos de routing.
    

### **Tabla de enrutamiento**

```
show ip route
```

Campos principales:

- Código de origen (C, L, S, O, D, R…)
    
- Red destino
    
- Máscara
    
- Next-hop
    
- Interfaz de salida
    
- Distancia administrativa
    
- Métrica
    

### **Distancia administrativa (AD)**

Preferencia del origen de la ruta:

- Directamente conectada: **0**
    
- Estática: **1**
    
- OSPF: **110**
    
- RIP: **120**
    

> Pregunta típica: “¿Cuál ruta elige el router?” → La de **menor AD**, y si son iguales, la de **menor métrica**.

---

## 🔹 **2. Subneteo IPv4**

### **Objetivo**

Crear redes más pequeñas para:

- mejorar la seguridad,
    
- evitar broadcast innecesario,
    
- asignar direcciones eficientemente.
    

### **Conversiones clave**

- /24 = 255.255.255.0 → bloque 1
    
- /25 = 128 → bloque 128
    
- /26 = 192 → bloque 64
    
- /27 = 224 → bloque 32
    
- /28 = 240 → bloque 16
    
- /29 = 248 → bloque 8
    
- /30 = 252 → bloque 4
    

### **Pasos rápidos (método CCNA)**

1. Identificar máscara y bloque.
    
2. Encontrar red donde pertenece la IP.
    
3. Calcular:
    
    - IP de red
        
    - Broadcast
        
    - Host válidos
        

### **Ejemplo típico de examen**

IP: 192.168.1.70/27  
/27 = bloque 32  
Rangos:

- 0–31
    
- 32–63
    
- **64–95** ← pertenece aquí  
    → Red = 192.168.1.64  
    → Broadcast = 192.168.1.95  
    → Hosts válidos = 65–94
    

---

## 🔹 **3. Subneteo VLSM (Variable Length Subnet Mask)**

VLSM permite usar máscaras distintas dentro del mismo bloque, evitando desperdiciar IP.

### **Reglas clave**

- Ordenar redes de mayor a menor cantidad de hosts.
    
- Usar primero las subredes grandes.
    
- No superponer redes.
    

> Prácticamente siempre aparece un ejercicio de VLSM o una tabla para completar.

---

## 🔹 **4. IPv6 Routing**

### **Tipos de direcciones**

- **Global Unicast** → públicas, comienzan con 2 o 3
    
- **Link-local (FE80::/10)** → obligatorias
    
- **Loopback ::1**
    
- **Multicast FF00::/8**
    

### **Comandos básicos**

Ver interfaces:

```
show ipv6 interface brief
```

Habilitar IPv6 routing:

```
ipv6 unicast-routing
```

### **OSPFv3 / IPv6**

- Funciona por interfaz, no por red.
    
- Sin wildcard mask.
    

---

## 🔹 **5. Routing estático**

### **Ruta estática**

```
ip route <red> <máscara> <next-hop>
```

### **Ruta estática flotante**

Ruta estática con AD mayor para ser backup:

```
ip route 10.0.0.0 255.255.255.0 192.168.1.2 5
```

### **Ruta por defecto**

```
ip route 0.0.0.0 0.0.0.0 <next-hop>
```

> Pregunta típica: “¿Qué ruta usa un router cuando no tiene ninguna específica?” → la **default route**.

---

## 🔹 **6. OSPF (Open Shortest Path First)**

Uno de los temas más pesados del CCNA.  
Tipo de protocolo: **estado de enlace** → basado en costo (bandwidth).

### **Características**

- AD = **110**
    
- Algoritmo SPF (Dijkstra)
    
- Métrica = **coste** = 100,000,000 / bandwidth
    
- Se organiza en **áreas** (normalmente área 0)
    

### **Estados OSPF (muy preguntado)**

1. Down
    
2. Init
    
3. 2-Way
    
4. Exstart
    
5. Exchange
    
6. Loading
    
7. Full (adyacencia completa)
    

### **Router ID (RID)**

Prioridad:

1. Configurado manualmente → mayor prioridad
    
2. Loopback más alta
    
3. IP activa más alta
    

### **Network command**

```
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
```

### **LSDB (Link-State Database)**

Todos los routers del área deben tener la misma tabla → si no, no forman adyacencia.

---

## 🔹 **7. Implementación OSPF por interfaz (muy común en CCNA)**

En lugar de usar network:

```
interface g0/0
 ip ospf 1 area 0
```

---

## 🔹 **8. NAT (Network Address Translation)**

Permite que una red privada acceda a Internet usando IP públicas.

### **Tipos de NAT**

### **1. NAT estático**

Una IP privada = una IP pública

```
ip nat inside source static 192.168.1.10 200.1.1.10
```

### **2. NAT dinámico**

Usa un pool de direcciones públicas:

```
ip nat pool INTERNET 200.1.1.10 200.1.1.20 netmask 255.255.255.0
ip nat inside source list 1 pool INTERNET
```

### **3. PAT (NAT sobrecargado)**

Una IP pública para muchos dispositivos → más usado.

```
ip nat inside source list 1 interface g0/0 overload
```

### **Inside / Outside**

- inside local
    
- inside global
    
- outside local
    
- outside global
    

> Aparece SIEMPRE una pregunta comparando estos términos.

---

## 🔹 **9. Troubleshooting avanzado de routing**

### **Comandos esenciales**

- `show ip interface brief`
    
- `show ip route`
    
- `show ipv6 route`
    
- `show ip ospf neighbor`
    
- `show ip ospf interface`
    
- `debug ip ospf adj`
    
- `show ip nat translations`
    
- `show access-lists`
    

### **Errores típicos en el examen**

- Wildcard mask incorrecta
    
- OSPF sin misma área → no forman adyacencia
    
- NAT sin inside/outside
    
- Red no anunciada → no aparece en RIB
    
- IP fuera del rango VLSM
    
- Falta "ip routing" en multilayer switches
    

---

---

# ✅ **📘 PARTE 4 — SERVICIOS DE RED (DHCP, ACLs, Syslog, SNMP, NTP, QoS, FHRP)**

---

## 🔹 **1. DHCP (Dynamic Host Configuration Protocol)**

### **¿Qué hace?**

Asigna automáticamente:

- IP
    
- Máscara
    
- Gateway
    
- DNS
    

### **Proceso DORA (MUY IMPORTANTE)**

1. **Discover** → el cliente pide una IP (broadcast).
    
2. **Offer** → el servidor ofrece una IP.
    
3. **Request** → el cliente pide la IP ofrecida.
    
4. **ACK** → el servidor confirma.
    

### **Configuración del servidor DHCP en un router**

```
ip dhcp pool VENTAS
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8
```

### **Excluir IPs**

```
ip dhcp excluded-address 192.168.10.1 192.168.10.20
```

### **DHCP Relay (ip helper-address)**

Se usa cuando el servidor DHCP está en otra red:

```
interface VLAN10
 ip helper-address 192.168.99.5
```

### **Error típico en examen**

Dirección **169.254.x.x** → el cliente **NO contacta con DHCP**.

---

## 🔹 **2. ACLs (Access Control Lists)**

Permiten filtrar tráfico según:

- IP origen
    
- IP destino
    
- Puerto
    
- Protocolo (ICMP, TCP, UDP)
    

> ACLs SIEMPRE tienen un “deny any” implícito al final.

---

## 🟦 **ACL Estándar (1–99)**

Filtran **solo por IP origen**.

### Reglas:

- Colocar **cerca del destino** (para evitar bloquear demasiado tráfico).
    

### Ejemplo:

```
access-list 10 permit 192.168.1.0 0.0.0.255
interface g0/0
 ip access-group 10 in
```

---

## 🟩 **ACL Extendida (100–199)**

Filtran por:

- IP origen
    
- IP destino
    
- Puerto
    
- Protocolo
    

### Reglas:

- Colocar **cerca del origen** para reducir tráfico innecesario.
    

### Ejemplo:

```
access-list 100 permit tcp 192.168.10.0 0.0.0.255 host 192.168.20.10 eq 80
interface g0/1
 ip access-group 100 out
```

---

## 🟧 Wildcard Mask (inverso de la máscara)

Ejemplo:

- Máscara /24 = 255.255.255.0
    
- Wildcard = 0.0.0.255
    

> MUY preguntado: 0 = “debe coincidir”, 255 = “puede variar”.

---

## 🟥 Comandos de verificación

```
show access-lists
show running-config
show ip interface
```

---

## 🔹 **3. NAT (ya mencionado, pero aquí su papel como “servicio”)**

Tipos:

- NAT Estático
    
- NAT Dinámico
    
- PAT (muchos a uno)
    

Comandos de verificación:

```
show ip nat translations
show ip nat statistics
```

---

## 🔹 **4. Syslog — Registro de eventos**

Permite enviar logs a:

- consola
    
- buffer local
    
- servidor syslog
    
- sesiones VTY (con `terminal monitor`)
    

### **Niveles Syslog (0–7) — MUY PREGUNTADO**

0 – Emergencias  
1 – Alertas  
2 – Críticos  
3 – Errores  
4 – Advertencias  
5 – Notificaciones  
6 – Información  
7 – Debug

### **Habilitar timestamps**

```
service timestamps log datetime
```

---

## 🔹 **5. SNMP (Simple Network Management Protocol)**

Permite monitorear y gestionar dispositivos de red.

### **Componentes**

- **NMS** → software de gestión
    
- **Agentes** → routers/switches
    
- **MIB** → base de datos de objetos
    

### **Versiones**

- **v1/v2c** → comunidad (poco seguro)
    
- **v3** → autenticación y cifrado → recomendado
    

### Configuración básica:

```
snmp-server community public RO
snmp-server location Oficina1
snmp-server contact admin@example.com
```

---

## 🔹 **6. NTP (Network Time Protocol)**

Sincroniza la hora entre dispositivos.

### Comando:

```
ntp server 192.168.1.10
```

### Verificación:

```
show ntp status
```

¿Por qué es importante?  
→ Para logs correctos, correlación de eventos, seguridad.

---

## 🔹 **7. QoS (Quality of Service)**

Prioriza tráfico sensible:

- Voz
    
- Video
    
- Streaming
    

Conceptos básicos:

- **Clasificación** → identificar el tráfico.
    
- **Marcado** (DSCP, CoS).
    
- **Colas** → prioridad alta/normal/baja.
    

> Pregunta típica: “¿Qué tráfico debe tener la mayor prioridad?” → VoIP.

---

## 🔹 **8. FHRP (First Hop Redundancy Protocols)**

Permiten que dos routers actúen como un gateway redundante.

Tipos:

- **HSRP (Cisco)**
    
- **VRRP (estándar)**
    
- **GLBP (Cisco, balancea carga)**
    

### Ejemplo HSRP:

```
standby 1 ip 192.168.1.1
standby 1 priority 110
standby 1 preempt
```

### ¿Qué hace?

Dos routers comparten una IP virtual:

- Router activo
    
- Router en espera  
    → Si uno falla, el otro toma el rol automáticamente.
    

---

## 🔹 **9. Seguridad en servicios**

### **SSH**

```
ip domain-name red.local
crypto key generate rsa
ip ssh version 2
line vty 0 4
 transport input ssh
 login local
```

### **Contraseñas cifradas**

```
service password-encryption
```

### **Banners**

```
banner motd #Acceso no autorizado prohibido#
```

### **exec-timeout**

Evita sesiones abiertas en VTY o consola.

```
exec-timeout 5 0
```

---

## 🔹 **10. Troubleshooting de servicios**

### **Problemas comunes**

- DHCP no responde → clientes con IP 169.254.x.x
    
- DNS falla → ping a IP funciona pero a nombre NO
    
- ACL mal aplicada → tráfico bloqueado
    
- Syslog no muestra mensajes → falta terminal monitor
    
- SNMP no responde → comunidad incorrecta
    
- NTP incorrecto → logs desordenados
    
- NAT no traduce → no hay inside/outside o pool vacío
    

### **Comandos clave**

- `show ip dhcp binding`
    
- `debug ip dhcp server events`
    
- `show ip interface`
    
- `show ip nat translations`
    
- `show access-lists`
    
- `show snmp`
    

---

---

# ✅ **📘 PARTE 5 — ADMINISTRACIÓN, SEGURIDAD Y TROUBLESHOOTING GLOBAL (CCNA)**

---

## 🔹 **1. Administración básica de dispositivos Cisco**

### **Modos de operación**

- **User EXEC** → `>`
    
- **Privileged EXEC** → `#`
    
- **Global config** → `(config)#`
    
- **Interface config** → `(config-if)#`
    

### **Guardar configuración**

```
copy running-config startup-config
write memory
```

### **Ver configuraciones**

```
show running-config
show startup-config
show interfaces
```

### **Configurar banners**

```
banner motd #Acceso no autorizado prohibido#
```

---

## 🔹 **2. Hardening (endurecimiento) de dispositivos Cisco**

### **Proteger acceso remoto**

Habilitar SSH:

```
ip domain-name red.local
crypto key generate rsa
username admin secret cisco123
line vty 0 4
 login local
 transport input ssh
```

### **Cifrar contraseñas**

```
service password-encryption
```

### **timeout de inactividad (VTY o consola)**

```
exec-timeout 5 0
```

### **Desactivar servicios innecesarios**

- CDP en interfaces externas
    
- HTTP server desactivado
    
- No permitir Telnet
    

### **Seguridad de consola**

```
line console 0
 password cisco
 login
```

---

## 🔹 **3. Seguridad en switches — Capa 2**

### **Port Security (MUY PREGUNTADO)**

```
switchport port-security
switchport port-security maximum 2
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

Modos de violación:

- **protect** → descarta paquetes
    
- **restrict** → descarta + log
    
- **shutdown** → pone el puerto en err-disabled
    

### **DHCP Snooping**

Evita servidores DHCP falsos.  
Define puertos:

- trusted
    
- untrusted
    

### **Dynamic ARP Inspection (DAI)**

Evita ARP spoofing  
Requiere DHCP snooping configurado.

### **BPDU Guard**

Evita que un switch conectado a un puerto access participe en STP.

```
spanning-tree bpduguard enable
```

### **Root Guard**

Protege la elección del root bridge.

---

## 🔹 **4. Troubleshooting de conectividad (lo más importante del examen)**

Cisco ama meterte diagramas y preguntarte:  
“¿Dónde está el problema?”

### **Herramientas fundamentales**

#### 🔵 Ping

- Prueba Capa 3 (IP).
    
- `!` éxito, `.` timeout, `U` unreachable.
    

#### 🔵 traceroute / tracert

- Muestra los **saltos** que sigue un paquete.
    
- Si falla en un salto → problema ahí.
    

#### 🔵 nslookup

Prueba DNS:

- Si `ping 8.8.8.8` funciona pero `ping google.com` NO → problema de DNS.
    

#### 🔵 show ip interface brief

Verifica:

- IPs
    
- Estado de interfaces (up/down)
    

#### 🔵 show cdp neighbors

Verifica conectividad **Capa 2**.

#### 🔵 show spanning-tree

Verifica:

- puertos en blocking
    
- loops prevenidos
    

#### 🔵 show ip route

Verifica la tabla de rutas:

- Static
    
- Connected
    
- OSPF/RIP
    
- Default route
    

---

## 🔹 **5. Metodología de troubleshooting (Cisco)**

### **1. Identificar el problema**

- “No tengo Internet.”
    
- “No llego al gateway.”
    
- “DNS no resuelve.”
    

### **2. Recolectar información**

- `show run`
    
- `ping`
    
- `traceroute`
    
- `show interfaces`
    

### **3. Localizar la falla**

Preguntas clave:

- ¿Capa 1? cableado, velocidad, dúplex
    
- ¿Capa 2? VLAN, trunk, STP
    
- ¿Capa 3? IP, máscara, gateway, rutas
    

### **4. Probar solución**

- Cambiar IP
    
- Activar interfaz
    
- Agregar ruta
    
- Corregir VLAN
    

### **5. Verificar**

Probar nuevamente con ping/traceroute.

---

## 🔹 **6. Problemas típicos que Cisco pone en el examen**

### 🟧 **El cliente recibe IP 169.254.x.x**

→ El cliente NO recibe DHCP.  
Causas:

- No llega Discover
    
- Falta ip helper-address
    
- No hay servidor DHCP
    

### 🟧 **Ping a IP funciona, pero a dominio NO**

→ Falla DNS → usar `nslookup`.

### 🟧 **Dos PCs en la misma VLAN no se ven**

- El puerto está en VLAN incorrecta.
    
- La VLAN no existe en el switch.
    

### 🟧 **Switches no comunican VLANs**

→ TRUNK mal configurado:

- VLAN no permitida
    
- VLAN nativa distinta
    
- Puerto no está en trunk
    

### 🟧 **STP bloquea una interfaz**

Comando clave:

```
show spanning-tree
```

### 🟧 **OSPF no forma vecinos**

Causas:

- Distinta área
    
- Subred incorrecta en “network”
    
- Router IDs iguales
    
- Tipo de red distinto
    
- Interfaz apagada
    

### 🟧 **NAT no funciona**

Revisar:

- inside/outside
    
- ACL
    
- overload
    
- pool vacío
    

### 🟧 **ACL bloquea tráfico**

→ Orden incorrecto (top-down).  
→ Wildcard incorrecta.

---

## 🔹 **7. Redundancia y disponibilidad**

### **¿Por qué se usa redundancia?**

- Evitar puntos únicos de falla
    
- Mejorar uptime
    
- Balancear carga
    

### Métodos:

- STP
    
- EtherChannel
    
- FHRP (HSRP/VRRP/GLBP)
    
- Enlaces y routers duplicados
    

---

## 🔹 **8. Gestión y monitoreo**

### **Syslog**

Permite analizar eventos:

- Consola
    
- Buffer
    
- VTY (usar `terminal monitor`)
    
- Servidor externo
    

### **SNMP**

Monitoreo y estadísticas.

### **NetFlow**

Analiza flujos de tráfico (más avanzado).

---

## 🔹 **9. Comandos esenciales (lista rápida)**

### Diagnóstico

```
ping
traceroute
nslookup
show ip interface brief
show interfaces
show cdp neighbors
show spanning-tree
show ip route
show running-config
```

### Routing

```
ip route
ipv6 route
router ospf 1
network X.X.X.X X.X.X.X area 0
```

### VLANs y switches

```
show vlan brief
show interfaces trunk
switchport mode access/trunk
switchport access vlan X
```

### Seguridad

```
switchport port-security
service password-encryption
transport input ssh
exec-timeout X
```

### DHCP

```
ip dhcp pool X
ip helper-address X
```

### NAT

```
show ip nat translations
ip nat inside
ip nat outside
```

---

## 🔹 **10. Consejos finales para aprobar el examen CCNA**

### ✔ Practicá al menos 100 preguntas de CCNA

(yo puedo generarte un simulador cuando quieras)

### ✔ Saber subnetear sin calculadora

probablemente aparezcan 3–5 preguntas.

### ✔ Saber interpretar salidas de “show”

Cisco pone muchísimas preguntas visuales.

### ✔ Entender cómo se configura:

- SSH
    
- VLANs
    
- Trunks
    
- Inter-VLAN routing
    
- OSPF básico
    
- NAT overload
    
- ACL extendida
    

### ✔ Saber analizar diagramas

El examen está lleno de topologías pequeñas.
