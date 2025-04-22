  

## Gestión de entrada / salida

  

![[image.png]]

  

### Tipos de entrada / salida

  

![[image 1.png]]

  

Ti

![[image 2.png]]

  

  

- Gestión de Entrada / Salida  
    a) Tipos básicos de E/S  
    b) Concepto de controladores de E/S . Explicar cuál es su función y aclarar si se  
    encuentran dentro o fuera del núcleo.  
    

  

1. Según el tipo de memoria  
    Según el tipo de operación:  
    - Programada: La cpu controla directamente todas las operaciones de e/s, programando las transferencias de datos entre la memoria y los dispositivos periféricos  
    - Por interrupciones: La CPU inicia una operación de E/S y luego continúa con otras tareas. Cuando la operación de E/S se completa, el dispositivo genera una interrupción para notificar a la CPU.  
    - Por DMA: Un controlador de DMA (Direct Memory Access) gestiona las transferencias de datos entre la memoria y los dispositivos periféricos, liberando a la CPU de estas tareas.  
    - Procesadores de E/S: