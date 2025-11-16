$$Requerimiento \neq Requisito$$

**Requerimiento**: la necesidad del cliente 

**Requisito**: es la necesidad traducida con un formato más cercano para poder empezar a aplicarse 

# Requisitos 

## Características 

Los requisitos deben cumplir con: 

- **Correctos**: Representa realmente lo que el cliente necesita, no debe ser ambiguo, es decir, que sea super claro
- **Completo**: No falta información relevante 
- **Consistente**: No contradice otros requisitos 
- **No ambiguo**: Deben ser interpretados de una sola forma 
- **Verificable**: es posible comprobarlo mediante pruebas o revisiones, es decir, que se debe aclarar al menos de forma indirecta cómo probarlo “el sistema debe responder a las solicitudes en menos de 2 segundos”
- **Realista / factible**: puede implementarse con los recursos y tecnología disponibles 
- **Necesario**: Contribuye a alcanzar los objetivos del sistema 
- **Trazable**: puede rastrearse desde su origen hasta su implementación

## Clasificación 

- **Requisitos de negocio**: expresan objetivos de alto nivel de la organización o justificación del proyecto, definen por qué se construye el sistema. No describen qué hara el sistema, sino qué valor de negocio se espera lograr
- **Requisitos funcionales:** Describen las funcionalidades o servicios que el sistema debe ofrecer. Responde a la pregunta “¿Qué debe hacer el sistema?”
	- ***De comportamiento del sistema***: Funcionalidades que el sistema debe proporcionar. Qué acciones puede realizar el usuario o el sistema 
	- ***De reglas de negocio***: Lógica o condiciones propias del negocio que deben cumplirse. Refleja procesos u obligaciones propias del dominio. 
	- ***De interfaz funcional***: Funciones de interacción con otros sistemas 
	- ***Datos/Información***: Qué datos maneja la función (altas, bajas, consultas, validaciones)
	- ***Excepciones y errores***: Comportamiento esperado ante fallos o casos límite
- **Requisitos no funcionales:**
	- ***Escalabilidad***: Capacidad para crecer en usuarios, datos, transacciones
	- ***Compatibilidad***: Funcionamiento en diferentes plataformas o entornos 
	- ***Mantenibilidad***: Facilidad de mantenimiento, modularidad y documentación
	- ***Interoperabilidad***: Capacidad para comunicarse con otros sistemas 
	- ***Internacionalización***: Idiomas, monedas, formatos regionales 
	- ***Observabilidad***: Logs, métricas, trazas
	- Rendimiento 
	- Seguridad 
	- Usabilidad 
	- Disponibilidad: 
- **Requisitos de dominio:** Especificaciones que dependen del contexto particular de la organización, la industria o el entorno normativo
	- ***Normativas***: cumplimiento de leyes, normas o estándares
	- ***Procesos del negocio***: reglas o flujos específicos del negocio 
	- ***Del sector***: Estándares específicos del rubro
- ***Requisitos de restricciones de diseño***: Limitaciones impuestas sobre cómo debe desarrollarse el sistema 
	- ***Tecnologicas***: Plataformas, lenguajes, herramientas obligatorias 
	- ***De interfaz técnica***: Protocolos, APIs, estándares de comunicación
	- Organizacionales
	- Contrato
- **Requisitos nivel de abstracción**
	- ***Requisito de usuario***: Lenguaje natural, visión desde el usuario/cliente 
	- ***Requisito del sistema***: Versión técnica detallada, dirigida al equipo de desarrollo 
- **Requisitos prioridad**
	- ***Esencial***: SI no se cumple, el sistema fracasa 
	- ***Deseable***: Aporta valor pero no es crítico
	- ***Opcional***: Solo se implementa si hay tiempo o recursos extra



# Objetivo, límite y alcance 

$$\text{Alcance del producto} \neq \text{Alcance del proyecto}$$

- El cumplimiento del **alcance del producto** es medido **contra los requisitos**
- El **alcance del proyecto** es medido **contra la planificación**

> [!note] 
> Esto habla sobre cómo mido si x cosa se realizó o no 

## Alcance del producto 

Responde a la pregunta: **¿el sistema cumple con los requisitos?**
Describe qué características y funciones debe tener el producto o servicio o resultado de qué se va a entregar

Producto = lo que se entrega

**Ejemplo:** SIstema de pedidos, inventario y facturación


## Alcance del proyecto

Responde a la pregunta: **¿Se ejecutó todo lo que yo planée o planifiqué?**
Incluye todo el trabajo que se debe realizar para entregar el producto con sus características definidas (planificación, tareas recursos, cronogramas, entregable intermedios)

Proyecto = trabajo necesario para entregar el producto 

**Ejemplo:** todo el trabajo para desarrollar e implementar ese sistema 


# Gestión de los requisitos 

Es el conjunto de actividades para 
- Capturar 
- Documentar 
- Priorizar 
- Validar 
- Controlar los cambios 
- Mantener trazabilidad 

> [!note] 
> En la ppt hay ejemplos 


# Ciclo de vida de los requisitos 

1. **Elicitación* de requisitos**
2. **Análisis de requisitos.** *Refinar, detectar incosistencias, priorizar*
3. **Especificación de Requisitos.** *Documentar requisitos en un SRS (Software Requirements Specification)*
4. **Validación y verificación de requisitos**. *Asegurar que los requisitos cumplen con lo que el cliente necesita*
5. **Gestión del cambio y trazabilidad.** *Seguir requisitos a lo largo del desarrollo y evolución del sistema* 

**Esto va en loop**

Elicitación*: Recolectar requisitos mediante entrevistas, talleres, encuestas, observación



# S.M.A.R.T.

lo mismo de si1


# Matriz misuno 

Herramienta que permite relacionar la necesidad del cliente (**QUÉ**) con los requisitos técnicos o características de calidad (**CÓMO**) que satisfacen esas necesidades


# Casa de calidad 

Representación gráfica con forma de casa. Habitaciones: 

1. La voz del cliente 
2. Requisitos técnicos 
3. Relaciones entre requisito del cliente y técnico 
4. Percepción de la competencia 
5. Características de la competencia 
6. Correlaciones entre las características técnicas 
7. Peso de las especificaciones 
8. Representación gráfica de las especificaciones 


