# Acceso a Cisco IOS 

## Sistema operativo

***IOS***: Sistema operativo de Cisco 

- **Shell** - La interfaz de usuario que permite a los usuarios solicitar tareas específicas del equipo. Estas solicitudes se pueden realizar a través de las interfaces CLI o GUI.
    
- **Kernel** - Establece la comunicación entre el hardware y el software de una computadora y administra el uso de los recursos de hardware para cumplir los requisitos del software.
    
- **Hardware** - La parte física de una computadora, incluida la electrónica subyacente.

![[Pasted image 20250811185024.png]]


## GUI 

- Una GUI permite al usuario interactuar con el sistema utilizando un entorno de iconos gráficos, menús y ventanas.
    
- Una GUI es más fácil de usar y requiere menos conocimiento de la estructura de comandos subyacente que controla el sistema.
    
- Ejemplos de estos son: Windows, macOS, Linux KDE, Apple iOS y Android.
    
- Las GUI también pueden fallar, colapsar o simplemente no operar como se les indica. Por eso, se suele acceder a los dispositivos de red mediante una CLI.


## Métodos de acceso 

***Forma Local***
- **Puerto de consola**: Puerto físico para conectarse al SO


***Forma Remota***
- **Telnet**: Protocolo por dececto, viejo, que establece una conexión remota insegura por línea de comandos. Toda la info va por texto plano.
- **SSH**: Otro protocolo que no viene por defecto, hay que verificar si soporta ssh (encriptación). Establece una conexión remote por CLI 


- - -

# Navegación del IOS 

Configuración para conectarse a la terminal
- 9600
- 8
- n
- 1
- n

Para pasar del modo usuario `>` al modo privilegiado `#`, el comando es: `enable`
Al revés: `exit` o `end`

Con `end` voy dos saltos para atrás.

`ctrl+mayus+6` interrumpe algún comando que se haya quedado trabado. 

`?` documentación del resto de comandos 

Modo de configuración global `(config)#`: `configure terminal`

Modo configuracion comando de linea: `line terminal 0`

# Estructura de los comandos 

![[Pasted image 20250811205640.png]]

***Archivo de configuración: Running config*** → Startup config



- - -
# Configuración básica de dispositivos 

Ponerle nombre a los switchs:

- Comenzar con una letra 
- No contener espacios 
- Finalizar con una letra o dígito 
- Menos de 64 caracteres 
- solo Letras, digitos o guiones 

para volver las cosas por defecto, poner ante todo comando `no`

para ejecutar cualquier comando desde cualquier parte: `do`

# Guardar las configuraciones 


# Puertos y direcciones 


# Configuraciones de direcciones IP  