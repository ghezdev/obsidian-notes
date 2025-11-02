

# Unidad 7

#### 🔹 1. Curvas

- Definición general de una **curva** en el plano o en el espacio.
    
- Tipos de curvas:
    
    - **Curva suave** → su derivada es continua (sin quiebres bruscos).
        
    - **Curva suave a trozos** → compuesta de segmentos suaves.
        
    - **Curva cerrada** → el punto inicial y final coinciden.
        
    - **Curva simple** → no se cruza a sí misma.
        
    - **Curva cerrada simple** → cerrada y sin cruces.



#### 🔹 2. Longitud de arco de una curva

- Se deduce integrando el módulo de la derivada de la parametrización de la curva
    
- El concepto fundamental:    $$L = \int_a^b |\mathbf{r}'(t)| \, dt$$
    
    donde $\mathbf{r}(t)$ es la parametrización de la curva.

derivada = vector tangente da la dirección y velocidad instantánea del recorrido
modulo = magnitud = qué tanto avanza sobre la curva por unidad de t. 

Al integrarla, se suman pequeños desplazamientos para obtener la longitud total del camino recorrido


#### 🔹 4. Integrales de Línea de Escalares

- Generalización de la integral de una variable a funciones de varias variables sobre una curva.
    
- Fórmula general: $$\int_C f(x,y)\, ds = \int_a^b f(x(t),y(t))|\mathbf{r}'(t)|\, dt$$
    donde $f$ es un **campo escalar** y $C$ la curva.

$f(x(t),y(t)$ = altura 

$|\mathbf{r}'(t)|$ = base 

$\int_a^b f(x(t),y(t))|\mathbf{r}'(t)|\, dt$ = base x altura de a trozos dentro de un rango = area de la desde la curva hasta la función

Area de una porción de la superficie cilíndrica que se forma sobre una determinada curva

> [!note]
> Si la curva es suave a trozos
> ![[Pasted image 20251023234455.png]]



#### 5. Integrales de Línea Vectoriales

- Se integran **campos vectoriales** a lo largo de una curva:    $$\int_C \mathbf{F}\cdot d\mathbf{r} = \int_a^b \mathbf{F}(\mathbf{r}(t))\cdot\mathbf{r}'(t)\,dt$$
- Representan el **trabajo** realizado por un campo de fuerzas a lo largo de un recorrido.
    
- Ejemplos para campos en R2\mathbb{R}^2R2 y R3\mathbb{R}^3R3.



## 1) Longitud de curva (solo “largo”)

**Analogía:** un hilo curvo.  
**Qué hacés:** lo estirás y medís con una regla.  
**Qué suma:** solo **metros de hilo**.  
**Resultado:** el **largo** del camino.  
**Mini-ejemplo:** bordes de una pista → te da cuántos metros tiene.

> Fórmula idea: sumar “pasitos” de largo: (L=\int ds).

---

## 2) Integral curvilínea **escalar** (\int_C f,ds) (largo **ponderado**)

**Analogía:** un **rodillo de pintura** que gasta “(f)” litros por metro.  
**Qué hacés:** das la vuelta pintando el borde.  
**Qué suma:** **(pintura por metro) × (metros)**.  
**Resultado:** **pintura total** usada (o masa total si (f) es densidad, etc.).  
**Mini-ejemplo:** si (f\equiv 1) → gastás 1 por metro → sale **el mismo largo** que en (1).  
Si (f=x+y) → gastás más donde (x+y) es grande → te da una **suma ponderada** del camino.

> Fórmula idea: (\int_C f,ds=\int f(r(t)),|r'(t)|,dt).

---

## 3) Integral curvilínea **vectorial** (\int_C \mathbf F\cdot d\mathbf r) (empuje **a favor del camino**)

**Analogía:** caminás y hay **viento** (\mathbf F).  
**Qué hacés:** medís cuánto te **empuja en la dirección en la que caminás**.  
**Qué suma:** **(empuje tangencial) × (pasito)** = trabajo/circulación.  
**Resultado:** **trabajo total** que hizo el viento sobre tu recorrido.  
**Mini-ejemplo:** si el viento te empuja siempre a favor, el número es grande; si te frena, puede salir chico o incluso negativo.

> Fórmula idea (2D): (\int_C \mathbf F\cdot d\mathbf r=\int_C P,dx+Q,dy).

---

### En una línea cada uno

- **Longitud:** “cuento metros de hilo”.
    
- **Escalar:** “cuento metros de hilo **pesados** con (f)” (pintura/masa por metro).
    
- **Vectorial:** “cuento cuánto me **empuja** el viento a lo largo del camino” (trabajo).