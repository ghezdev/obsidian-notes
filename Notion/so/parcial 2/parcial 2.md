  

## Gestión de memoria

  

La reubicación e intercambio se aplican a los modelos para gestión de la memoria, con o sin abstracción, donde para el caso de sin abstracción, si se trata de un unico o varios espacios de direccionamiento independiente

  

Técnicas en los modelos de abstracción:

- Intercambio
- Paginación

  

El objetivo de estas técnicas es la de mover algo hacia otro lugar nivel inferior y viceversa con el objetivo de abstraer la memoria del sistema

  

Intercambio: Mover un objeto cargado en memoria hacia otro dispositivo de almacenamiento

Paginación: Mover páginas (estructura lógica) cargadas en marcos de página (estructura física de la memoria real)

Reubicación: Mover un objeto cargado en memoria a otra posición de la memoria

  

Tipos de reubicación aplicable, principalmente a modelos para ejecución de procesos (Código, PIla y datos):

Reubicación estática: El objeto fija su dirección en el momento de la carga, no puede moverse durante la duración del proceso

Reubicación dinámica: El objeto puede moverse durante la duración del proceso

  

_Objeto: tipos de estructuras que pueden almacenarse en memoria._

  

  

## Gestión de Archivos

Archivo: conjunto de registros relacionados

  

Un Sistema de Archivos contiene:

- Métodos de acceso: forma de acceder a los archivos
- Administración de archivos: mecanismos para que los archivos sean almacenados, referidos, compartidos y asegurados
- Administración del almacenamiento auxiliar: para la asignación de espacio a los archivos en los dispositivos de almacenamiento secundario
- Integridad del archivo: garantiza la integridad del archivo

  

  

Estructuras de Archivos

Secuencia de bytes

- El archivo es una serie no estructurada de bytes
- Más flexible
- El SO no ayuda pero tampoco estorba

  

Secuencia de registros

- El archivo es una secuencia de registros de longitud fija, cada uno con su propia estructura interna

  

Árbol

- Árbol de registros
- Cada registro tiene un campo key en una posición fija del registro
- El árbol se ordena mediante el campo key para permitir una rápida búsqueda

  

Tipos de Archivos

- Archivos regulares: aquellos que contienen información del usuario
- Directorios: archivos del sistema para el mantenimiento de una estructura del sistema de archivos
- Archivos Especiales de Caracteres: se usan para modelar dispositivos seriales de E/S
- Archivos Especiales de Bloques: modelar dispositivos de bloque

  

Tipos de Acceso

- Acceso Secuencial: el proceso lee en órden, sin poder saltar registros ni leer en otro órden
- Acceso Aleatorio: el proceso lee en cualquier órden según estos dos métodos
    - Cada operación de lectura da la posición en el archivo por el cual iniciar
    - La operación seek establece la poisición en el archivo y luego leyendose secuencialmente

  

Comando “Map”: hace que el SO asocie un archivo a una dirección virtual

Comando “Unmap”: elimina el archivo del espacio de direcciones virtuales

  

Implementación de Archivos

Asignación contigua: Requiere de un índice con información del comienzo del archivo

![[/image 41.png|image 41.png]]

  

Lista Enlazada: Los bloques del archivo contienen el encadenamiento

Lista Enlazada con índice: Tiene una tabla en la memoria con un índice y bloques libres

Nodo índice: Cada archivo posee un bloque con los índices a los data blocks