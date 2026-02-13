# Integral de linea

1 - Es un campo vectorial?
1.1 - Es conservativo?
1.1.1 - Es cerrada la curva?
1.1.1.1 - Resultado = 0
1.1.1.2 - Obtener la ecuación potencial, restar punto final con punto inicial en ecuación potencial, ese resultado es el resultado de la integral de línea
1.1.2 - Parametrizar la curva y resolver la integral directamente 

| Tipo de campo            | Tipo de integral | Fórmula                                        | ¿Qué representa?                            |
| ------------------------ | ---------------- | ---------------------------------------------- | ------------------------------------------- |
| **Escalar** $(f)$        | Integral escalar | $\displaystyle \int_C f, dS$                   | Acumulación del escalar sobre la curva      |
| **Vectorial** $(\vec F)$ | **Circulación**  | $\displaystyle \int_C \vec F \cdot d\vec r$    | Trabajo del campo “a lo largo” de la curva  |
| **Vectorial** $(\vec F)$ | **Flujo**        | $\displaystyle \int_C \vec F \cdot \vec n, dS$ | Fluido atravesando perpendicular a la curva |


Perfecto, vamos a armar **tres “recetas”** claras, una para cada caso:

  

1. Campo **escalar**

2. Campo **vectorial – circulación**

3. Campo **vectorial – flujo**

  

---

  

## 🟦 1) Integral de línea de un **campo escalar**

  

Forma general:

$$

\int_C f, dS

$$

  

### Paso a paso

  

1. **Identificá el campo escalar y la curva**

  

* Campo: (f(x,y)) (o (f(x,y,z)))

* Curva (C): recta, circunferencia, parábola, etc.

  

2. **Parametrizá la curva**

  

* En 2D: $( \vec r(t) = (x(t), y(t))), (a \le t \le b)$

* En 3D: $( \vec r(t) = (x(t), y(t), z(t))), (a \le t \le b)$

  

3. **Calculá la velocidad y su norma**

  

* $(\vec r'(t) = (x'(t), y'(t)))$

* $(|\vec r'(t)| = \sqrt{x'(t)^2 + y'(t)^2}) (en 3D agregás (z'(t)^2))$

  

4. **Reemplazá en la integral**

$$

\int_C f, dS

= \int_a^b f(x(t),y(t)),|\vec r'(t)|,dt

$$

  

5. **(Si te lo piden) calculás la integral**

Pero el procedimiento termina en el planteo.

  

---

  

## 🟩 2) Integral de línea de un **campo vectorial – CIRCULACIÓN**

  

Forma general:

$$

\int_C \vec F \cdot d\vec r

$$

  

En 2D: $(\vec F(x,y) = (P(x,y), Q(x,y)))$

  

### Paso a paso

  

1. **Identificá el campo vectorial y la curva**

  

* Campo: $(\vec F = (P,Q))$

* Curva (C) (segmentos, triángulo, circunferencia, etc.)

  

2. **Parametrizá la curva**

  

* $( \vec r(t) = (x(t), y(t))), (a \le t \le b)$

  

3. **Calculá la derivada de la curva**

  

* $(\vec r'(t) = (x'(t), y'(t)))$

  

4. **Armá el producto punto $( \vec F(\vec r(t)) \cdot \vec r'(t))$**

$$

\vec F(\vec r(t)) = \big(P(x(t),y(t)),\ Q(x(t),y(t))\big)

$$

$$

\vec F(\vec r(t)) \cdot \vec r'(t)

= P(x(t),y(t)),x'(t) + Q(x(t),y(t)),y'(t)

$$

  

5. **Escribí la integral**

$$

\int_C \vec F\cdot d\vec r

= \int_a^b \big(P(x(t),y(t)),x'(t) + Q(x(t),y(t)),y'(t)\big),dt

$$

  

6. **(Opcional) Atajo si el campo es conservativo**

  

* Si $(\dfrac{\partial P}{\partial y} = \dfrac{\partial Q}{\partial x})$, buscás potencial (f) y hacés:

$$

\int_C \vec F\cdot d\vec r = f(B) - f(A)

$$

  

---

  

## 🟥 3) Integral de línea de un **campo vectorial – FLUJO**

  

Forma general:

$$

\int_C \vec F \cdot \vec n, dS

$$

  

En 2D: $(\vec F(x,y) = (P,Q))$ y $(\vec n)$ es la normal unitaria a la curva.

  

### Paso a paso (versión con parametrización)

  

1. **Identificá el campo y la curva**

  

* Campo: $(\vec F = (P,Q))$

* Curva (C) en el plano (normalmente cerrada, tipo borde de una región)

  

2. **Parametrizá la curva**

  

* $( \vec r(t) = (x(t), y(t))), (a \le t \le b)$

(Sentido antihorario si te lo piden.)

  

3. **Calculá la derivada y la longitud**

  

* $(\vec r'(t) = (x'(t), y'(t)))$

* $(|\vec r'(t)| = \sqrt{x'(t)^2 + y'(t)^2})$

  

4. **Encontrá una normal unitaria**

Una normal perpendicular a la tangente $((x'(t),y'(t)))$ es:

$$

\vec n(t) = \frac{(y'(t), -x'(t))}{|\vec r'(t)|}

$$

(esta es una de las dos posibles normales; el signo se ajusta según el sentido que te pidan)

  

5. **Armá el producto punto $(\vec F(\vec r(t))\cdot \vec n(t))$**

$$

\vec F(\vec r(t)) = (P(x(t),y(t)), Q(x(t),y(t)))

$$

$$

\vec F(\vec r(t))\cdot \vec n(t)

= \frac{P(x(t),y(t)),y'(t) - Q(x(t),y(t)),x'(t)}{|\vec r'(t)|}

$$

  

6. **Multiplicá por $(dS = |\vec r'(t)|,dt)$**

$$

\vec F(\vec r(t))\cdot \vec n(t), dS

= \big(P(x(t),y(t)),y'(t) - Q(x(t),y(t)),x'(t)\big),dt

$$

  

7. **Escribí la integral de flujo**

$$

\int_C \vec F \cdot \vec n, dS

= \int_a^b \big(P(x(t),y(t)),y'(t) - Q(x(t),y(t)),x'(t)\big),dt

$$

  

---

  

## 🧠 Mini-resumen para que no se mezclen

  

* **Campo escalar** (f):

$$

\int_C f,dS = \int f(x(t),y(t)),|\vec r'(t)|,dt

$$

  

* **Campo vectorial – circulación** $(\vec F)$:

$$

\int_C \vec F\cdot d\vec r

= \int \big(P,x' + Q,y'\big),dt

$$

  

* **Campo vectorial – flujo** $(\vec F)$:

$$

\int_C \vec F\cdot \vec n, dS

= \int \big(P,y' - Q,x'\big),dt

$$

  

Si querés, después vemos **un mismo ejemplo** y te muestro cómo se ven las **tres integrales distintas** sobre la misma curva.


# ✔️ ¿Por qué te sirve saber si el campo es conservativo?

Porque si **el campo es conservativo**, la integral de línea **no depende del camino**, solo de los puntos inicial y final:

$$
\int_C \vec F\cdot d\vec r = f(B) - f(A)  
$$

donde (f) es la función potencial.

---

# ✔️ ¿Qué pasa si la curva es cerrada?

Si la curva vuelve al punto inicial, entonces:

- (A = B)
    
- Entonces:
    
$$
f(B) - f(A) = f(A) - f(A) = 0  
$$

Por eso:
$$
\oint_C \vec F \cdot d\vec r = 0  
$$

---

### ❌ Si el campo **no** es conservativo

No podés usar la función potencial →  
**tenés que calcular la integral a mano (parametrizando cada lado del triángulo o usando Green en 2D).**




# PASO A PASO PARA OBTENER FUNCIÓN POTENCIAL 

Buenísimo, vamos paso a paso **solo para sacar la función potencial** (f(x,y)) de tu campo.

El campo es:  
$$

\vec F(x,y) = (P(x,y), Q(x,y)) =

\left(-\frac{2}{x}y - 4 + y^2,; -2\ln(x) + 2y + 2xy\right)

$$

---

## 0️⃣ (Opcional pero importante) Verificar que es conservativo

En 2D:
$$

\vec F \text{ es conservativo } \Longleftrightarrow P_y = Q_x

$$


* $(P(x,y) = -\dfrac{2}{x}y - 4 + y^2)$  

$$

P_y = \frac{\partial}{\partial y}\left(-\frac{2}{x}y - 4 + y^2\right)

= -\frac{2}{x} + 2y

$$

  

* $(Q(x,y) = -2\ln(x) + 2y + 2xy)$

  

$$

Q_x = \frac{\partial}{\partial x}\left(-2\ln(x) + 2y + 2xy\right)

= -\frac{2}{x} + 2y

$$

  

Entonces:

  

$$

P_y = Q_x \quad \Rightarrow \quad \vec F \text{ es conservativo (en } x>0\text{)}

$$

  

Así que **sí existe** función potencial (f(x,y)).

  

---

  

## 1️⃣ Planteo para la función potencial

  

Buscamos (f(x,y)) tal que:

  

$$

\nabla f = \vec F \quad\Longleftrightarrow\quad

\begin{cases}

f_x = P(x,y) \

f_y = Q(x,y)

\end{cases}

$$

  

Es decir:

  

$$

f_x(x,y) = -\frac{2}{x}y - 4 + y^2

$$

  

---

  

## 2️⃣ Integrar (f_x) respecto de (x)

  

Integramos **P** respecto de (x), considerando (y) como constante:

  

$$

f(x,y) = \int \left(-\frac{2}{x}y - 4 + y^2\right),dx + g(y)

$$

  

Hacemos término a término:

  

* $(\displaystyle \int -\frac{2}{x}y,dx = -2y\int \frac{1}{x},dx = -2y\ln x)$

* $(\displaystyle \int -4,dx = -4x)$

* $(\displaystyle \int y^2,dx = x y^2) (porque (y^2) es constante frente a (x))$

  

Entonces:

  

$$

f(x,y) = -2y\ln x -4x + x y^2 + g(y)

$$

  

donde (g(y)) es una “constante” que puede depender de (y).

  

---

  

## 3️⃣ Derivar (f) respecto de (y) y compararla con (Q)

  

Ahora calculamos $(f_y)$ a partir de esta expresión:

  

$$

f(x,y) = -2y\ln x -4x + x y^2 + g(y)

$$

  

Derivamos con respecto a (y):

  

* $(\dfrac{\partial}{\partial y}(-2y\ln x) = -2\ln x)$

* $(\dfrac{\partial}{\partial y}(-4x) = 0)$

* $(\dfrac{\partial}{\partial y}(x y^2) = 2xy)$

* $(\dfrac{\partial}{\partial y}(g(y)) = g'(y))$

  

Entonces:

  

$$

f_y(x,y) = -2\ln x + 2xy + g'(y)

$$

  

Pero sabemos que **debe coincidir con** (Q(x,y)):

  

$$

Q(x,y) = -2\ln(x) + 2y + 2xy

$$

  

Igualamos:

  

$$

-2\ln x + 2xy + g'(y) = -2\ln x + 2y + 2xy

$$

  

Simplificamos los términos iguales en ambos lados:

  

* El $(-2\ln x)$ se cancela.

* El $(2xy)$ se cancela.

  

Queda:

  

$$

g'(y) = 2y

$$

  

---

  

## 4️⃣ Integrar (g'(y)) para obtener (g(y))

  

$$

g'(y) = 2y \quad\Rightarrow\quad g(y) = \int 2y,dy = y^2 + C

$$

  

La constante (C) es global y no importa para la integral de línea, así que la podemos ignorar.

  

---

  

## 5️⃣ Escribir la función potencial final

  

Reemplazamos (g(y)) en (f(x,y)):

  

$$

f(x,y) = -2y\ln x -4x + x y^2 + y^2 + C

$$

  

Normalmente se toma (C=0):

  

$$

\boxed{f(x,y) = -2y\ln x -4x + x y^2 + y^2}

$$

  

Esa es la **función potencial** de tu campo $(\vec F)$.

  

Con esta (f), para el ítem (b) después podrías hacer:

  

$$

\int_C \vec F\cdot d\vec r = f(B) - f(A)

$$

  

sin parametrizar la curva, usando los puntos inicial y final de la curva $(y = \ln x)$ con $(1 \le x \le e^2)$.







Perfecto, Guillermo.  
Te explico **exactamente** cómo verificar si un campo es conservativo, y por qué aparecen esas derivadas.

---

# 🟩 CASO 1: CAMPO VECTORIAL **EN 2D**

[  
\vec F(x,y) = (P(x,y),\ Q(x,y))  
]

### ✔️ Criterio para saber si es conservativo:

[  
\boxed{\frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}}  
]

### ✔️ ¿Por qué?

Porque en 2D, el rotor es un vector que apunta en la dirección (k):

[  
\nabla \times \vec F =  
\left(0,\ 0,\ \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y} \right)  
]

Entonces:

[  
\vec F \text{ conservativo}  
\Longleftrightarrow  
\nabla \times \vec F = 0  
\Longleftrightarrow  
\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} = 0  
]

---

# 🟥 CASO 2: CAMPO VECTORIAL **EN 3D**

[  
\vec F(x,y,z) = (P,Q,R)  
]

### ✔️ Criterio para saber si es conservativo:

[  
\boxed{\nabla \times \vec F = \vec 0}  
]

Es decir, que las tres componentes del rotor sean 0:

[  
\nabla \times \vec F =  
\left(  
R_y - Q_z,;  
P_z - R_x,;  
Q_x - P_y  
\right)  
]

Para que sea conservativo:

[  
\begin{cases}  
R_y - Q_z = 0 \  
P_z - R_x = 0 \  
Q_x - P_y = 0  
\end{cases}  
]

---

# 🧠 **¿Qué hago con esas derivadas? (Respuesta concreta)**

👉 **Calculás el rotor (curl).**  
👉 Si te da **(0,0,0)** → el campo es **conservativo**.  
👉 Si **no da cero** → **no es conservativo**.

---

# 🟦 PERO: ojo con el dominio

Además de que el rotor dé 0, el dominio del campo debe ser **simplemente conexo** (sin agujeros).

Ejemplo clásico:  
[  
\vec F = \left(-\frac{y}{x^2+y^2},\ \frac{x}{x^2+y^2}\right)  
]  
Tiene rotor = 0, **pero NO es conservativo** porque el origen está excluido → dominio con hueco.

---

# 🟣 RESUMEN FINAL

## ✔️ En 2D:

[  
\boxed{\vec F \text{ conservativo} \iff \frac{\partial P}{\partial y}=\frac{\partial Q}{\partial x}}  
]

## ✔️ En 3D:

[  
\boxed{\vec F \text{ conservativo} \iff \nabla\times \vec F = \vec 0}  
]

## ✔️ Y si es conservativo:

Existe una función potencial (f) tal que:  
[  
\vec F = \nabla f  
]

y la integral de línea se vuelve:

[  
\int_C \vec F\cdot d\vec r = f(B)-f(A)  
]

---

Si querés, te hago una **plantilla paso a paso** para verificar conservatividad en cualquier ejercicio del parcial.









Buenísima pregunta, esto entra DIRECTO en el parcial.

La idea clave es:

> **La masa de un alambre = integral de la densidad a lo largo de la curva (por longitud).**

Vamos paso a paso.

---

## 1️⃣ Datos que tenés

- La **forma del alambre** viene dada por una **parametrización**:
    
    - En 2D: (\vec r(t) = (x(t), y(t))), (a \le t \le b)
        
    - En 3D: (\vec r(t) = (x(t), y(t), z(t))), (a \le t \le b)
        
- La **densidad lineal** (masa por unidad de longitud) es una función:  
    [  
    \delta(x,y) \quad \text{o} \quad \delta(x,y,z)  
    ]
    

---

## 2️⃣ Fórmula teórica

La **masa** del alambre es:

[  
m = \int_C \delta, dS  
]

Es una **integral de línea escalar**: integral de la densidad sobre la longitud de la curva.

---

## 3️⃣ Pasar a la parametrización

Usás la receta de integral de línea escalar:

1. **Reemplazás la densidad en la curva**:  
    [  
    \delta(\vec r(t)) = \delta(x(t), y(t)) \quad \text{o} \quad \delta(x(t), y(t), z(t))  
    ]
    
2. **Calculás la velocidad de la parametrización**:
    
    - En 2D:  
        [  
        \vec r'(t) = (x'(t), y'(t)), \quad  
        |\vec r'(t)| = \sqrt{x'(t)^2 + y'(t)^2}  
        ]
        
    - En 3D:  
        [  
        \vec r'(t) = (x'(t), y'(t), z'(t)), \quad  
        |\vec r'(t)| = \sqrt{x'(t)^2 + y'(t)^2 + z'(t)^2}  
        ]
        
3. **Armás la integral en términos de (t)**:  
    [  
    \boxed{  
    m = \int_a^b \delta(\vec r(t)) , |\vec r'(t)| , dt  
    }  
    ]
    

Eso es TODO el procedimiento.

---

## 4️⃣ Intuición física (para que no se te olvide)

- (dS) es un **pedacito de longitud** del alambre.
    
- (\delta) es **cuánta masa hay por unidad de longitud**.
    
- Entonces (\delta , dS) = **masa de un pedacito**.
    
- La integral **suma todas esas masas** a lo largo del alambre.
    

---

## 5️⃣ Mini-resumen tipo machete

> **Masa de un alambre con forma parametrizada (\vec r(t)) y densidad (\delta):**
> 
> [  
> m = \int_C \delta, dS  
> = \int_a^b \delta(\vec r(t)),|\vec r'(t)|,dt  
> ]

Si querés, en el próximo mensaje me das un ejemplo concreto (tipo: (r(t) = (t^2, 2t)), (\delta(x,y)=x+y)) y te lo planteo sin resolver.




Claro Guillermo, te explico **exacto y claramente** cómo funciona el **Teorema de Green**, cuándo se usa, y por qué lo usé en tu ejercicio de flujo.  
Te prometo que cuando terminemos, vas a saber **exactamente cuándo aplicarlo en un parcial** sin dudar.

---

# 🟢 1) ¿Qué dice el Teorema de Green?

Conecta **una integral de línea** en una curva cerrada, con **una integral doble** sobre la región encerrada.

### Tiene **dos versiones**:

---

## ✅ **Versión de CIRCULACIÓN**

Si ( \vec F = (P, Q) ) y (C) es una curva cerrada antihoraria:

$$
\oint_C (P,dx + Q,dy)= \iint_D \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right), dA  
$$

---

## 🟥 **Versión de FLUJO** ← esta es la que usamos

$$
\oint_C \vec F\cdot \vec n, dS= \iint_D (\nabla\cdot \vec F), dA= 

\iint_D (P_x + Q_y), dA  
$$

**Atención: flujo → divergencia.**

---

# 🟦 2) ¿Cuándo puedo usar Green?

Siempre que se cumpla:

1. **La curva es cerrada**  
    ✔ triángulo  
    ✔ cuadrado  
    ✔ circunferencia  
    ✔ poligonal cerrada  
    ❌ NO sirve en curvas abiertas
    
2. **La curva está en el plano**  
    (solo para 2D)
    
3. **La orientación es antihoraria**  
    (si es horaria, sale negativo)
    
4. El campo (F=(P,Q)) es “suave” (continuo, derivable).
    

---

# 🟩 3) ¿Por qué se usa Green? (VENTAJA)

Porque Green transforma una **integral horrible de línea** en una **integral doble facilísima**.

En tu ejercicio:

### Te pedían un **flujo** a través de una circunferencia:

[  
\oint_C \vec F\cdot \vec n, dS  
]

Parametrizar eso es feo porque implica:

- derivar (r(t))
    
- obtener el normal unitario
    
- multiplicar por (F(r(t)))
    
- integrar desde (0) a (2\pi)
    

_**MUCHO TRABAJO.**_

---

### Pero con Green:

# [  
\oint_C \vec F\cdot \vec n, dS

\iint_D (P_x + Q_y), dA  
]

y la región D era un **disco de radio 1**, donde la integral doble era trivial:

[  
\iint_D 1+2y, dA  
]

El término (2y) se va por simetría, y queda solo el área del disco → (\pi).

Fue **infinitamente más fácil**.

---

# 🔵 4) Entonces… ¿por qué lo apliqué en tu ejercicio?

### ✔ La curva era **cerrada**

→ circunferencia de radio 1

### ✔ Estaba en el **plano**

→ lo que pide Green

### ✔ Te pedían un **flujo**

→ usa la versión de divergencia (P_x+Q_y)

### ✔ Era más rápido ver simetría del disco

→ integral doble inmediata

### ✔ Parametrizar era más engorroso

→ Green lo hace trivial

Por eso **SIEMPRE** que tengas:

- **flujo** o **circulación**
    
- **curva cerrada**
    
- **en 2D**
    

la pregunta automática es:

> **¿Puedo usar Green?**

Y la respuesta suele ser: **Sí, y me ahorro un montón de trabajo.**

---

# 🎯 5) Resumen estilo “machete para el parcial”

### ✔ **Usar Green cuando:**

- curva cerrada
    
- campo vectorial 2D
    
- pedís flujo → usar divergencia
    
- pedís circulación → usar rotor 2D
    
- región encerrada es fácil (círculo, rectángulo, triángulo)
    

### ❌ **NO usar Green cuando:**

- curva NO es cerrada
    
- campo en 3D
    
- integral de línea escalar
    
- la región encerrada no es simple de describir
    

---

# Si querés, te muestro 3 ejercicios rápidos:

- uno donde conviene usar Green
    
- uno donde NO conviene
    
- uno donde es opcional
    

Así te queda clarísimo cuándo aplicarlo.



| Qué estás calculando | Dimensión | Integral        | Por qué aparece el “1”      |
| -------------------- | --------- | --------------- | --------------------------- |
| Área                 | 2D        | $\iint_D 1,dA$  | Sumas pedacitos de área     |
| Volumen              | 3D        | $\iiint_E 1,dV$ | Sumas pedacitos de volumen  |
| Longitud             | 1D        | $\int_C 1,ds$   | Sumas pedacitos de longitud |


  

## 1. Datos del ejercicio

  

$$

\vec F(x,y) = (P(x,y),Q(x,y))=

\big(6xe^y+\sin x,; 3x^2e^y+2y+(y-x)^2\big)

$$

  

C es **la semicircunferencia de radio 3** centrada en el origen, sobre el lado izquierdo

$(x^2+y^2=9,\ x\le 0)$, recorrida como en el dibujo: de ((0,3)) hacia ((0,-3)) por el arco.

  

Queremos $\displaystyle \int_C \vec F\cdot d\vec r$.

  

---

  

## 2. Truco para usar Green

  

El Teorema de Green vale para **curvas cerradas**.

La semicircunferencia no es cerrada, así que hacemos:

  

* Cerramos la curva agregando el segmento del eje (y) entre ((0,-3)) y ((0,3)).

  

Llamo:

  

* $C_{\text{arco}}$: la semicircunferencia (lo que pide el ejercicio).

* $C_{\text{seg}}$: el segmento vertical (x=0) de ((0,-3)) a ((0,3)).

* $C_{\text{cerrada}} = C_{\text{arco}} \cup C_{\text{seg}}$.

  

La orientación de $C_{\text{cerrada}}$ es positiva (antihoraria) tal como está dibujado:

bajás por el arco y subís por el eje (y).

  

Entonces:

  

$$

\oint_{C_{\text{cerrada}}} \vec F\cdot d\vec r = \int_{C_{\text{arco}}} \vec F\cdot d\vec r + \int_{C_{\text{seg}}} \vec F\cdot d\vec r

$$

  

Y Green nos da:

  

$$

\oint_{C_{\text{cerrada}}} \vec F\cdot d\vec r

=

  

\iint_D\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)dA

$$

  

donde (D) es el semidisco $x^2+y^2\le 9,\ x\le 0$.

  

Al final vamos a despejar la integral del arco:

  

$$

\int_{C_{\text{arco}}} \vec F\cdot d\vec r

=

  

\iint_D(\cdots)dA - \int_{C_{\text{seg}}} \vec F\cdot d\vec r

$$

  

---

  

## 3. Calculamos el “rotor escalar”

  

$$

P=6xe^y+\sin x,\qquad Q=3x^2e^y+2y+(y-x)^2

$$

  

$$

\frac{\partial Q}{\partial x}=6xe^y+2x-2y,\qquad

\frac{\partial P}{\partial y}=6xe^y

$$

  

$$

\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}

= (6xe^y+2x-2y)-6xe^y

= 2x-2y

$$

  

Así que:

  

$$

\iint_D\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)dA

=

  

\iint_D (2x-2y),dA

$$

  

---

  

## 4. Integral sobre el semidisco en polares

  

Región (D): semidisco de radio 3, lado izquierdo.

  

En polares en el plano (xy):

  

$$

x = r\cos\theta,\quad y = r\sin\theta,\quad dA = r,dr,d\theta

$$

  

Para el semidisco izquierdo:

  

* radio: $0 \le r \le 3$

* ángulo: $\dfrac{\pi}{2} \le \theta \le \dfrac{3\pi}{2})  (donde (\cos\theta \le 0)$

  

El integrando:

  

$$

2x-2y = 2r\cos\theta - 2r\sin\theta

$$

  

Entonces:

  

$$

\iint_D (2x-2y),dA

=

  

\int_{\theta=\pi/2}^{3\pi/2}

\int_{r=0}^{3}

(2r\cos\theta - 2r\sin\theta), r,dr,d\theta

$$

  

$$

  

\int_{\pi/2}^{3\pi/2}

\int_0^3 2r^2(\cos\theta - \sin\theta),dr,d\theta

$$

  

Integrando en (r):

  

$$

\int_0^3 2r^2,dr = 2\cdot\frac{3^3}{3} = 18

$$

  

$$

\Rightarrow \iint_D (2x-2y),dA

=

  

\int_{\pi/2}^{3\pi/2} 18(\cos\theta - \sin\theta),d\theta

$$

  

$$

= 18\left[\sin\theta + \cos\theta\right]_{\pi/2}^{3\pi/2}

= 18\big[(-1+0) - (1+0)\big] = 18(-2) = -36

$$

  

Así que:

  

$$

\oint_{C_{\text{cerrada}}} \vec F\cdot d\vec r = -36

$$

  

---

  

## 5. Integral sobre el segmento del eje (y)

  

Parámetro para (C_{\text{seg}}):

$$

\vec r(t) = (0,t),\quad -3\le t\le 3

$$

$$

\vec r'(t) = (0,1)

$$

  

En ese segmento, (x=0), (y=t):

  

$$

P(0,t) = 0,\quad

Q(0,t) = 3\cdot 0^2 e^{t} + 2t + (t-0)^2 = 2t + t^2

$$

  

$$

\vec F\cdot d\vec r = P,dx + Q,dy = Q,dt = (2t+t^2),dt

$$

  

Entonces:

  

$$

\int_{C_{\text{seg}}} \vec F\cdot d\vec r

= \int_{-3}^{3} (2t+t^2),dt

= \left[t^2 + \frac{t^3}{3}\right]_{-3}^{3}

= (9+9) - (9-9) = 18

$$

  

---

  

## 6. Despejamos la integral sobre el arco

  

$$

\oint_{C_{\text{cerrada}}} \vec F\cdot d\vec r

  

\int_{C_{\text{arco}}} \vec F\cdot d\vec r

+

\int_{C_{\text{seg}}} \vec F\cdot d\vec r

$$

  

$$

-36 = \int_{C_{\text{arco}}} \vec F\cdot d\vec r + 18

$$

  

$$

\boxed{\displaystyle \int_{C_{\text{arco}}} \vec F\cdot d\vec r = -36 - 18 = -54}

$$

  

---

  

**Respuesta:**

$$

\int_C \vec F\cdot d\vec r = -54

$$

donde (C) es la semicircunferencia mostrada en el gráfico.