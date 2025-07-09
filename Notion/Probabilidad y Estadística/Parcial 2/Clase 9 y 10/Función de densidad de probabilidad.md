# Función de Densidad de Probabilidad (FDP)

## Concepto

La **Función de Densidad de Probabilidad (FDP)**, usualmente denotada como f(x), es una función matemática que describe la **probabilidad relativa** de que una **variable aleatoria continua** tome un valor dado. A diferencia de las variables discretas, donde la probabilidad se asigna directamente a cada valor, para las variables continuas la probabilidad de que tomen un valor _exacto_ es cero. Por eso, la FDP nos indica dónde es más probable encontrar la variable dentro de un rango de valores.

Imaginá que estás lanzando un dardo a un blanco continuo. La FDP te diría qué tan probable es que el dardo caiga en una región específica del blanco, no en un punto exacto. Cuanto más alto sea el valor de f(x) en un punto x, más probable es que la variable aleatoria se encuentre cerca de ese valor.

Formalmente, para que una función sea una FDP, debe cumplir dos condiciones:

1. **No negatividad:** f(x)≥0
2. 
3. para todo x Las probabilidades no pueden ser negativas.
    
2. **Área bajo la curva igual a 1:** La integral de la FDP en todo su rango debe ser igual a 1. Esto representa que la suma de todas las probabilidades posibles debe ser 1 (o el 100%). ∫−∞∞​f(x)dx=1
    

## Para qué sirve

Saber sobre la Función de Densidad de Probabilidad es fundamental porque nos permite:

- **Calcular probabilidades para rangos de valores:** La principal utilidad de la FDP es que, al **integrar** la función entre dos puntos a y b, podemos obtener la probabilidad de que la variable aleatoria caiga dentro de ese intervalo. P(a≤X≤b)=∫ab​f(x)dx
- **Comprender la forma de la distribución:** La FDP nos da una imagen visual de cómo se distribuyen los datos. Por ejemplo, una FDP "alta y delgada" indica que los datos están concentrados alrededor de la media, mientras que una FDP "ancha y plana" sugiere que los datos están más dispersos.
- **Determinar la moda:** El punto (o puntos) donde la FDP alcanza su valor máximo es la **moda** de la distribución, es decir, el valor más probable.
- **Derivar otras propiedades de la distribución:** A partir de la FDP, se pueden calcular otras características importantes de la distribución, como la media (valor esperado), la varianza y los percentiles.
- **Comparar distribuciones:** Al visualizar las FDP de diferentes variables aleatorias, podés comparar fácilmente cómo se comportan sus distribuciones.

## Ejemplo de uso

Consideremos una variable aleatoria continua X que representa el tiempo (en minutos) que un cliente espera en la fila de un banco. Supongamos que la Función de Densidad de Probabilidad para X es:

f(x)={0.5e−0.5x0​para x≥0para x<0​

Esta es la FDP de una **distribución exponencial**, a menudo usada para modelar tiempos entre eventos.

**Pregunta:** ¿Cuál es la probabilidad de que un cliente espere entre 2 y 4 minutos?

Para calcular esta probabilidad, integramos la FDP en el intervalo [2,4]:

P(2≤X≤4)=∫24​0.5e−0.5xdx

Resolviendo la integral:

∫0.5e−0.5xdx=0.5(−0.5e−0.5x​)=−e−0.5x

Ahora evaluamos en los límites:

P(2≤X≤4)=[−e−0.5(4)]−[−e−0.5(2)]P(2≤X≤4)=[−e−2]−[−e−1]P(2≤X≤4)=−0.1353+0.3679 P(2≤X≤4)=0.2326

Así, la probabilidad de que un cliente espere entre 2 y 4 minutos es de aproximadamente **0.2326 o 23.26%**.

---

## Datos extra

### Moda

La **moda** de una distribución continua es el valor de x donde la FDP f(x) alcanza su valor máximo. Para encontrarla, podés calcular la primera derivada de f(x), igualarla a cero y resolver para x. Luego, verificá la segunda derivada para asegurar que es un máximo. Si la FDP tiene un pico, ese es el valor modal. Algunas distribuciones (como la uniforme) no tienen una moda única o pueden tener múltiples modas.

### Mediana

La **mediana** (M) es el valor de X que divide la distribución en dos partes iguales, de modo que la probabilidad de que la variable aleatoria sea menor o igual a M es 0.5, y la probabilidad de que sea mayor o igual a M también es 0.5. Se calcula resolviendo la siguiente ecuación:

∫−∞M​f(x)dx=0.5

### Esperanza matemática

La **Esperanza Matemática** o valor esperado (E[X] o μ) de una variable aleatoria continua es el promedio ponderado de todos los valores posibles que la variable puede tomar, donde los "pesos" son dados por la FDP. Representa el "centro de masa" de la distribución. Se calcula como:

E[X]=μ=∫−∞∞​x⋅f(x)dx

Si tenés una función de una variable aleatoria, g(X), la esperanza de g(X) es:

E[g(X)]=∫−∞∞​g(x)⋅f(x)dx

### Varianza

La **Varianza** (Var(X) o σ2) mide la dispersión o variabilidad de los datos alrededor de la media. Un valor alto indica que los datos están muy dispersos, mientras que un valor bajo indica que están más concentrados. Se calcula como:

Var(X)=E[(X−μ)2]=∫−∞∞​(x−μ)2f(x)dx

Una fórmula más práctica para el cálculo es:

Var(X)=E[X2]−(E[X])2=∫−∞∞​x2f(x)dx−μ2

### Desviación estándar

La **Desviación Estándar** (σ) es la raíz cuadrada de la varianza. Es la medida de dispersión más utilizada porque está en las mismas unidades que la variable aleatoria original, lo que facilita su interpretación.

σ=Var(X)![](data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="400em" height="1.28em" viewBox="0 0 400000 1296" preserveAspectRatio="xMinYMin slice"><path d="M263,681c0.7,0,18,39.7,52,119
c34,79.3,68.167,158.7,102.5,238c34.3,79.3,51.8,119.3,52.5,120
c340,-704.7,510.7,-1060.3,512,-1067
l0 -0
c4.7,-7.3,11,-11,19,-11
H40000v40H1012.3
s-271.3,567,-271.3,567c-38.7,80.7,-84,175,-136,283c-52,108,-89.167,185.3,-111.5,232
c-22.3,46.7,-33.8,70.3,-34.5,71c-4.7,4.7,-12.3,7,-23,7s-12,-1,-12,-1
s-109,-253,-109,-253c-72.7,-168,-109.3,-252,-110,-252c-10.7,8,-22,16.7,-34,26
c-22,17.3,-33.3,26,-34,26s-26,-26,-26,-26s76,-59,76,-59s76,-60,76,-60z
M1001 80h400000v40h-400000z"></path></svg>)​

### Expectativas parciales izquierda, derecha y en un rango

Las expectativas parciales se refieren al valor esperado de la variable aleatoria cuando esta se restringe a un cierto intervalo.

- **Esperanza parcial izquierda:** Es el valor esperado de X dado que X es menor o igual a un valor c. E[X∣X≤c]=P(X≤c)∫−∞c​x⋅f(x)dx​
    
- **Esperanza parcial derecha:** Es el valor esperado de X dado que X es mayor o igual a un valor c. E[X∣X≥c]=P(X≥c)∫c∞​x⋅f(x)dx​
    
- **Esperanza parcial en un rango:** Es el valor esperado de X dado que X está en un intervalo [a,b]. E[X∣a≤X≤b]=P(a≤X≤b)∫ab​x⋅f(x)dx​
    

---

## Cómo darme cuenta si tengo que aplicar esto en un ejercicio

1. **La variable es continua:** El indicio más importante es que la variable aleatoria en el problema puede tomar cualquier valor dentro de un rango (por ejemplo, tiempo, peso, altura, temperatura, resistencia, etc.), no solo valores discretos.
2. **Se pide la probabilidad de un intervalo:** Si la pregunta te pide la probabilidad de que la variable caiga entre dos valores (ej. "entre 20 y 25 tn", "más de 1.5 tn", "menos de 100 horas"), o si te dan la FDP explícitamente y te piden calcular una probabilidad o alguna de las "Datos extra", es una señal clara.
3. **Te dan una función f(x) con ciertas características:** Si el problema te proporciona una función f(x) que es no negativa y cuya integral total es 1, y te dice que describe el comportamiento de una variable, esa es tu FDP.
4. **El problema menciona una distribución continua específica:** Si te dicen que la variable sigue una "Distribución Normal", "Weibull", "Gamma", "Exponencial", "Gumbel", o "Pareto", automáticamente sabés que estás trabajando con una FDP, ya que estas son distribuciones de probabilidad para variables continuas.
5. **Se te pide calcular la media, varianza, moda o mediana de una variable continua:** Todos estos conceptos se derivan directamente de la FDP.