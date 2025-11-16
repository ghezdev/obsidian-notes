[Presentación](https://uadeeduar.sharepoint.com/:p:/r/sites/Section_539616/_layouts/15/Doc.aspx?sourcedoc=%7B495B7225-5AEC-4105-8C81-F1B0B76638E6%7D&file=ITN_Module_1.pptx&action=edit&mobileredirect=true)


# Componentes de red

## Roles de host

**Computadora**: Host o dispositivo final 

**Servidor**: Computadoras que proporcionan información a dispositivos finales 
- Servidores de correo electrónico 
- Servidores web 
- Servidores de archivos 

**Clientes**: Equipos que envían solicitudes a los servidores para recuperar información
- Página web desde un servidor web
- Correo electrónico desde un servidor de correo electrónico

![[Pasted image 20250804181912.png]]

Una computadora es cliente si solicita información.

Una computadora es servidor si brinda servicios.

- - -

## Punto a punto 

Es posible que un dispositivo sea un cliente y un servidor en una red Punto a Punto. Este tipo de diseño de red **solo se recomienda para redes muy pequeñas**. ​

**Ventajas y desventajas**

![[Pasted image 20250804182202.png]]

**Esta red no es escalable**

- - -

## Dispositivos finales 

Un terminal es el punto donde un mensaje se origina o se recibe. Los datos se originan con un dispositivo final, fluyen por la red y llegan a un dispositivo final.​

![[Pasted image 20250804193307.png]]

**Switch**: Rectángulos con doble flecha. Dispositivo de acceso donde conecto los Hosts
**Router**: Circulos con una X. Normalmente no tienen dispositivos finales conectados pero podrían tenerlo. Elemento que va a tomar decisiones que va a saber qué hacer con los mensajes, hacia donde se dirigen. Sirven para conectar redes

**Una red es un conjunto de routers y switches**

- - -

## Dispositivos de red intermedios 

Un dispositivo intermediario interconecta dispositivos finales. Los ejemplos incluyen switches, puntos de acceso inalámbrico, routers y firewalls.​

La gestión de los datos a medida que fluyen a través de una red también es la función de un dispositivo intermediario, que incluye:​

- Volver a generar y transmitir las señales de datos.​
    
- Mantener información sobre qué vías existen en la red.​
    
- Notificar a otros dispositivos los errores y las fallas de comunicación.​

![[Pasted image 20250804194337.png]]


- - -

## Medios de red

La comunicación a través de una red se efectúa a través de un medio que permite que un mensaje viaje desde el origen hacia el destino. ​


### Tipos de medios 

- **Inalámbrica** (medios no guiados) Mayor comodidad
	- Wifi
- **Alambrada** (medios guiados) Mayor seguridad y velocidad
	- Cobre
		- Coaxil
		- Par de cobre
	- Fibra óptica 
		- Fibras monomodo
		- Fibras multimodo


![[Pasted image 20250804194446.png]]

- - -

# Representaciones de red y topologías 

Los diagramas de red, con frecuencia, denominados diagramas de topología, utilizan símbolos para representar los dispositivos dentro de la red.​

Los términos importantes a conocer incluyen:​

- Tarjeta de interfaz de red (NIC)​
    
- Puerto físico​
    
- Interfaz​

Nota: A menudo, los términos puerto e interfaz se usan indistintamente​


![[Pasted image 20250804195522.png]]

**Topología lógica**: dibujos donde se diagrama qué dispositivos se conectan entre sí

**Topología física**: el laburo hecho a mano

> [!NOTE]
> Puertos, interfaz, placa de red, NIC, es todo lo mismo

- - -

## Diagramas de topología

Los diagramas de topología física ilustran la ubicación física de los dispositivos intermedios y la instalación de cables.​

![[Pasted image 20250804195812.png]]


Los diagramas de topología lógica ilustran dispositivos, puertos y el esquema de direccionamiento de la red.​

![[Pasted image 20250804195835.png]]

- - -

# Tipos comunes de redes

## Redes de muchos tamaños 

- Las redes domésticas pequeñas conectan algunas computadoras entre sí y con Internet.​
    
- Las oficinas pequeñas y las oficinas en el hogar permiten que una computadora dentro de una oficina en el hogar o una oficina remota se conecte a una red corporativa.​
    
- Las redes medianas a grandes incluyen muchos lugares con cientos o miles de computadoras interconectadas.​
    
- Redes mundiales: conecta cientos de millones de computadoras en todo el mundo, como Internet​

![[Pasted image 20250804200153.png]]

**SOHO**: small ofice, home office

- - -

## LANs y WANs

Las infraestructuras de red pueden variar en gran medida en términos de:​

- El tamaño del área que abarcan.​
    
- La cantidad de usuarios conectados.​
    
- La cantidad y los tipos de servicios disponibles.​
    
- El área de responsabilidad​
​

Los dos tipos de redes más comunes son los siguientes: ​

- Red de área local (LAN): aquellas donde estan los dispositivos finales
    
- Red de área amplia (WAN): aquellas donde se conecta entre LANs


![[Pasted image 20250804200445.png]]


Una LAN es una infraestructura de la red que abarca un área geográfica pequeña. ​

![[Pasted image 20250804200908.png]]

Una WAN es una infraestructura de la red que abarca un área geográfica extensa.​

​![[Pasted image 20250804200917.png]]

![[Pasted image 20250804200927.png]]

Las redes WAN son administradas por proveedores

> [!NOTE]
> Antes se dividían por ubicación geográfica debido a que se usaba el cobre, y el cobre tiene una atenuación luego de los 100m. Ahora con la fibra óptica ya no está bien dividir por ubicación geográfica

- - -

## Internet 

Internet es una colección mundial de LAN y WAN interconectadas. ​

- Las redes LAN se conectan entre sí mediante redes WAN.​
    
- Las WAN pueden usar cables de cobre, cables de fibra óptica y transmisiones inalámbricas.​
    

Internet no pertenece a una persona o un grupo **_MENTIRA_**. Los siguientes grupos se desarrollaron para ayudar a mantener la estructura en Internet:​

- IETF​
    
- ICANN​
    
- IAB​

Pensar que los routers de capa 3 son switches

![[Pasted image 20250804201132.png]]

- - -

## Intranets y Extranets

Una intranet es una colección privada de LAN y WAN internas de una organización que debe ser accesible solo para los miembros de la organización u otros con autorización.​

Una organización puede utilizar una red extranet para proporcionar un acceso seguro a su red por parte de personas que trabajan para otra organización y que necesitan tener acceso a sus datos en su red.​

![[Pasted image 20250804201408.png]]


- - -

# Conexiones de internet 

## Tecnologías de acceso a internet 

Hay muchas formas de conectar usuarios y organizaciones a Internet:​

- Los servicios más utilizados para los usuarios domésticos y las oficinas pequeñas incluyen banda ancha por cable, banda ancha por línea de suscriptor digital (DSL), redes WAN inalámbricas y servicios móviles.​
    
- Las organizaciones necesitan conexiones más rápidas para admitir los teléfonos IP, las videoconferencias y el almacenamiento del centro de datos.​
    
- Por lo general, los proveedores de servicios (SP) son quienes proporcionan interconexiones de nivel empresarial y pueden incluir DSL empresarial, líneas arrendadas y red Metro Ethernet.​

- - -

## Home and Small Office Conexiones de Internet​

![[Pasted image 20250804205343.png]]

![[Pasted image 20250804205356.png]]

- - -

## Conexiones a internet para usuarios corporativas 

Las conexiones empresariales corporativas pueden requerir:​

- Mayor ancho de banda ​
    
- Conexiones dedicadas​
    
- Servicios gestionados ​

![[Pasted image 20250804211353.png]]

![[Pasted image 20250804211405.png]]

- - -

## La red convergente 

Antes de las redes convergentes, una organización habría sido cableada por separado para el teléfono, el vídeo y los datos. Cada una de estas redes usaría diferentes tecnologías para transportar la señal. ​

Cada una de estas tecnologías utilizaría un conjunto diferente de reglas y estándares.​

![[Pasted image 20250804211555.png]]


Las redes de datos convergentes transportan múltiples servicios en un enlace que incluyen: ​

- Datos ​
    
- Voz​
    
- Video​
    

Las redes convergentes pueden entregar datos, voz y video a través de la misma infraestructura de red. La infraestructura de la red utiliza el mismo conjunto de reglas y normas.​

​
![[Pasted image 20250804211756.png]]


- - -

# Redes confiables 

## Arquitectura de red

La arquitectura de red se refiere a las tecnologías que admiten la infraestructura que mueve los datos a través de la red.​

Existen cuatro características básicas que las arquitecturas subyacentes deben abordar para cumplir con las expectativas del usuario:​

- Tolerancia a fallas​: ante la falla de un elemento, la red puede seguir o no funcionando
    
- Escalabilidad​: la posibilidad de escalar la tecnología
    
- Calidad de servicio (QoS)​
    
- Seguridad​


![[Pasted image 20250804212027.png]]


- - -

## Tolerancia de fallas 

Una red con tolerancia a fallas disminuye el impacto de una falla al limitar la cantidad de dispositivos afectados. Para la tolerancia a fallas, se necesitan varias rutas.​

Las redes confiables proporcionan redundancia al implementar una red de paquetes conmutados:​

- La conmutación por paquetes divide el tráfico en paquetes que se enrutan a través de una red. ​
    
- En teoría, cada paquete puede tomar una ruta diferente hacia el destino.​
    

Esto no es posible con las redes conmutadas por circuitos que establecen circuitos dedicados.​

![[Pasted image 20250804212604.png]]

La máxima disponibilidad que puede tener una red es de 99,99999.

- - -

## Escalabilidad

Una red escalable puede expandirse fácil y rápidamente para admitir nuevos usuarios y nuevas aplicaciones sin afectar el rendimiento de los servicios de los usuarios actuales.​

Los diseñadores de redes siguen normas y protocolos aceptados para hacer que las redes sean escalables.​

![[Pasted image 20250804213008.png]]

- - -

## Calidad de servicio 

Las transmisiones de voz y vídeo en vivo requieren mayores expectativas para los servicios que se proporcionan. ​

¿Alguna vez miró un vídeo en vivo con interrupciones y pausas constantes? Esto sucede cuando existe una mayor demanda de ancho de banda que la que hay disponible y la QoS no está configurada.​

- La calidad de servicio (QoS) es el principal mecanismo que se utiliza para garantizar la entrega confiable de contenido a todos los usuarios. ​
    
- Con la implementación de una política de QoS, el router puede administrar más fácilmente el flujo del tráfico de voz y de datos.​

![[Pasted image 20250804213039.png]]

- - -

## Seguridad de la red 

Existen dos tipos principales de seguridad de la red que se deben abordar: ​

- Seguridad de la infraestructura de la red​
    
- Seguridad física de los dispositivos de red​
    
- Prevenir el acceso no autorizado a los dispositivos​
    
- Seguridad de la información​
    
- Protección de la información o de los datos transmitidos a través de la red​
    

Tres objetivos de seguridad de la red:​

- Confidencialidad: solo los destinatarios deseados pueden leer los datos​
    
- Integridad: garantía de que los datos no se alteraron durante la transmisión​
    
- Disponibilidad: garantía del acceso confiable y oportuno a los datos por parte de los usuarios autorizados​

![[Pasted image 20250804213113.png]]

- - -

# Tendencias de red (no va a entrar en el examen)

- - -

Ejercicio de CCNA1 packet tracer 1.0.5 Packet Tracer - Logical and Physical Mode Exploration.pka

![[Pasted image 20250804213746.png]]

Topología física


![[Pasted image 20250804213801.png]]

Área de trabajo 

![[Pasted image 20250804213841.png]]

Confirmar si realizaste todo bien

![[Pasted image 20250804213918.png]]

Tareas a realizar 

​


> [!NOTE]
> Primer parcial de CISCO corresponde al módulo Examen de punto de control de la página de CISCO.

​