# Diagrama de Flujo de Datos (DFD)

- Nos ayuda a modelar cómo diferentes entidades interactúan con un sistema o una aplicación.
- Se puede ver diferentes niveles de detalle

> [!NOTE]
> Hay que saber las 4-5 macroactividades

![[Pasted image 20250508195652.png]]

- entre entidades externas no pueden dialogar
- una entidad externa no puede dialogar con un archivo si no es a través de un proceso
- un archivo no puede dialogar con otro archivo no es a través de un proceso

![[Pasted image 20250508205521.png]]

![[Pasted image 20250508195727.png]]
![[Pasted image 20250508195740.png]]

![[Pasted image 20250508195757.png]]

![[Pasted image 20250508195813.png]]

![[Pasted image 20250508195819.png]]

![[Pasted image 20250508195831.png]]


# Diagrama de contexto

- Es una visión general de un sistema o una aplicación

![[Pasted image 20250508200734.png]]


## Nivel 0 - Diagrama de contexto


## asdasdasd

 1. Detectar necesidad
 2. Elegir proveedor
 3. Generar/Enviar órden de compra 
 4. Recepción de productos o servicios


## Nivel 1

![[Pasted image 20250508211233.png]]

Traer hecho para el 15/05 el diagrama de contexto 0 y 1 el sistema de biblioteca de uade


# Diagrama de Transición de Estados

- Se utilizan para describir el comportamiento de un sistema, representan los diferentes estados que puede adquirir una clase, como representarla a diferentes etapas de su vida
- El estado de un objeto se puede caracterizar por el valor de uno o varios de los atributos de su clase, además el estado de un objeto también se puede caracterizar por la existencia de un enlace con otro objeto
- !! Representar cómo cambia de estados un objeto del cual yo quiero analizar o estudiar

![[Pasted image 20250508211747.png]]

## Ejemplo

![[Pasted image 20250508211927.png]]


> [!NOTE] Nota
> Los diagramas pueden no tener estado final


## Tabla de transición de estados

|     | Estado      | Transición    | Estado final |
| --- | ----------- | ------------- | ------------ |
| 0   | Desemplado  | Contratar     | Trabajando   |
| 1   | Trabajando  | Perder empleo | Desempleado  |
| 2   | Trabajando  | Jubilarse     | Jubilado     |
| 3   | Desempleado | Jubilarse     | Jubilado     |
