## 📘 **Clase 1: Funciones y Campos**

- **Qué es una función**: Relación que a cada entrada le asigna una salida.  
    👉 Ejemplo: una máquina de jugo 🍊: metés una fruta (entrada) y te da jugo (salida).
    
- **Función escalar**: A cada punto le da un número.  
    👉 Ejemplo: un **mapa de temperaturas**: cada lugar tiene un valor de °C.
    
- **Campo escalar**: Representa una magnitud en el espacio (como temperatura, presión, densidad).  
    👉 Analógico: un “mapa de calor” en Google Maps.
    
- **Campo vectorial**: A cada punto se le asigna un vector (dirección + magnitud).  
    👉 Ejemplo: los **vientos en un mapa meteorológico** 🌬️.
    
- **Curvas de nivel**: Lugares donde la función tiene el mismo valor.  
    👉 Ejemplo: las **líneas en un mapa topográfico** indican igual altura.
    

✅ **Cuándo usarlo**: para modelar magnitudes que dependen de varias variables (temperatura, presión, fuerzas).  
✅ **Qué obtenés**: visualización clara del fenómeno en espacio 2D o 3D.

---

## 📘 **Clase 2: Funciones vectoriales y Curvas parametrizadas**

- **Función vectorial**: La salida es un vector, no un número.  
    👉 Ejemplo: la posición de un dron en vuelo 🛸 (x, y, z según el tiempo).
    
- **Curvas paramétricas**: En vez de dar y=f(x), se expresan con un parámetro t.  
    👉 Ejemplo: el recorrido de un auto 🚗:  
    x(t) = velocidad_x·t, y(t) = velocidad_y·t.
    
- **Campos vectoriales**: Modelan fuerzas o velocidades en cada punto del espacio.  
    👉 Ejemplo: campo gravitacional 🌍, campo eléctrico ⚡, flujo de aire.
    

✅ **Cuándo usarlo**: cuando el movimiento o fenómeno no se describe bien con ecuaciones simples.  
✅ **Qué obtenés**: una forma flexible de describir trayectorias y fuerzas.

---

## 📘 **Clase 3: Límites y derivadas parciales**

- **Límite en varias variables**: cómo se comporta una función al acercarse a un punto desde diferentes direcciones.  
    👉 Ejemplo: caminar hacia una esquina desde la calle de arriba o desde la de al lado 🏙️.
    
- **Continuidad**: no hay saltos ni “agujeros”.  
    👉 Ejemplo: un puente bien construido vs. uno con huecos.
    
- **Derivadas parciales**: muestran cómo cambia la función si variás **solo una variable** y las otras quedan fijas.  
    👉 Ejemplo: una receta 🍕: si cambias solo la cantidad de harina (x), ¿cómo cambia el sabor, dejando todo lo demás igual?
    

✅ **Cuándo usarlo**: para estudiar cómo influyen variables individuales en un sistema.  
✅ **Qué obtenés**: información direccional sobre los cambios.

---

## 📘 **Clase 4: Derivadas direccionales y gradiente**

- **Derivada direccional**: mide el cambio en cualquier dirección, no solo en ejes.  
    👉 Ejemplo: subir una montaña ⛰️: podés subir derecho (x), lateral (y) o en diagonal.
    
- **Gradiente**: vector que apunta hacia donde la función crece más rápido.  
    👉 Ejemplo: si tirás agua en una montaña, siempre baja en dirección opuesta al gradiente.

Dirección de máximo crecimiento 
cos( teta ) = 1
teta = 0

Dirección de minimo crecimiento 
cos ( teta ) = -1
teta = pi

Dirección de nulo crecimiento 
cos(teta) = 0
teta = pi/2 y teta = (3/2)\*pi

![[Pasted image 20250916204719.png]]

![[Pasted image 20250916204732.png]]

✅ **Cuándo usarlo**: para saber hacia dónde optimizar (máximo crecimiento) o prever dirección de mayor variación.  
✅ **Qué obtenés**: dirección de máximo cambio y pendiente asociada.

---

## 📘 **Clase 5: Extremos, planos tangentes y regla de la cadena**

- **Curvas de nivel + gradiente**: el gradiente es perpendicular a las curvas de nivel.  
    👉 Ejemplo: en un mapa de altura, el gradiente te indica “la subida más empinada”.
    
- **Planos tangentes**: aproximan una superficie en un punto.  
    👉 Ejemplo: poner una mesa sobre una colina: la mesa es el plano tangente.
    
- **Máximos y mínimos locales**: encontrar picos y valles de la función.  
    👉 Ejemplo: hallar la cima más alta o el valle más profundo en un terreno.
    
- **Hessiana y segunda derivada**: permiten distinguir entre máximo, mínimo o punto de silla.  
    👉 Ejemplo: como ver si estás en la cima de una montaña, en un valle, o en una “silla de caballo” 🐎.
    
- **Regla de la cadena y Jacobiana**: cómo cambian las funciones compuestas con varias variables.  
    👉 Ejemplo: si cambiás el precio de la uva 🍇 y eso afecta el vino 🍷 y luego el precio del vino afecta la ganancia 💵, la regla de la cadena te conecta todo.
    

✅ **Cuándo usarlo**: para optimización, aproximaciones y análisis de sistemas complejos.  
✅ **Qué obtenés**: herramientas para tomar decisiones (máximos, mínimos, dirección de cambio).

---

📌 En pocas palabras:

- **Clase 1** → Qué son funciones y campos.
    
- **Clase 2** → Cómo representamos trayectorias y fuerzas.
    
- **Clase 3** → Cómo varían funciones de varias variables (derivadas parciales).
    
- **Clase 4** → Hacia dónde cambian más rápido (gradiente, direccionales).
    
- **Clase 5** → Optimización y aplicaciones (máximos, planos tangentes, regla de la cadena).