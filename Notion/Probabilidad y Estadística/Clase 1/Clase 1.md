### Estadística

Ciencia con la que se recopilan, organizan, procesan, analizan e interpretan datos para facilitar la toma de decisiones

  

### Estadística inferencial

Estudia la probabilidad de éxito de las diferentes soluciones posibles a un problema

  

### Estadística descriptiva

Resume la información de conjuntos más o menos, numerosos de datos

- Se encarga de recoger, almacenar, ordenar, realizar tablas o gráficos y calcular parámetros básicos sobre el conjunto de datos
- Trata de describir algo, pero no de cualquier forma, sino de manera cuantitativa

  

### Población [N]

Número de observaciones

  

### Muestra [n]

Subconjunto de una población

  

### Tipos de datos

- Cualitativos
    - Nominales
    - Ordinales
- Cuantitativos
    - Discretos
    - Continuos

  

### Métodos tabulares y gráficos según datos

- Cualitativos
    - Métodos tabulares
        - Distribución de frecuencia
        - Distribución de frecuencia relativa
        - Distribución de frecuencia porcentual
        - Tabulación cruzada
    - Métodos gráficos
        - Gráfico de barras
        - Gráfico de torta
- Cuantitativos
    - Métodos tabulares
        - Distribución de frecuencia
        - Distribución de frecuencia relativa
        - Distribución de porcentual
        - Distribución de frecuencia acumulada
        - Distribución de frecuencia relativa acumulada
        - Distribución de frecuencia porcentual acumulada
        - Tabulación cruzada
    - Métodos gráficos
        - Gráficos de puntos
        - Histogramas
        - Ojivas
        - Diagramas de tallo y hojas
        - Diagramas de dispersión

  

### Distribución de frecuencias

Resumen tabular de datos que muestra el número (frecuencia) de elementos en cada una de las diferentes clases disyuntas (que no se sobreponen)

  

### Frecuencia absoluta [fi]

Es el número de veces que aparece un valor

  

### Frecuencia relativa [fr]

Expresa la **proporción** de veces que ocurre un valor en relación con el total de datos

$$fr = \frac{f_i}{n}$$

### Frecuencia porcentual [fr%]

Es la frecuencia relativa expresada en porcentaje

$$fr\% = fr * 100$$

### Frecuencia acumulada [Fi]

Se obtiene sumando las frecuencias absolutas de todos los valores anteriores más el actual. Nos indica cuántos datos tienen un valor menor o igual a un cierto punto.

$$F_i = F_{i-1} + f_i$$

  

> [!important] Clase = Elemento parte del conjunto a analizar

  

### Regla de Sturges

$$k = 1 + 3.3log(N) \ con \ k ∈ ℕ$$

Para el análisis de datos cuantitativos, la regla de sturges te permite aproximarte al mejor numero de clases/elementos a considerar

  

### Amplitud/Ancho

Para agrupar datos, necesitamos ponerle un intervalo, este intervalo va a tener una amplitud o diferencia, el cual es esta

$$A = \frac{valor\ máximo \ de \ la \ muestra\ - valor\ mínimo\ de \ la \ muestra}{k} \ con \ A∈ℕ$$

  

### Tratamiento de datos cualitativos

![[/image 36.png|image 36.png]]

![[/image 1 13.png|image 1 13.png]]

![[/image 2 13.png|image 2 13.png]]

![[/image 3 11.png|image 3 11.png]]

### Tratamiento de datos cuantitativos

![[/image 4 9.png|image 4 9.png]]

![[/image 5 8.png|image 5 8.png]]

$$k = 1 + 3.3 * log(20)\\  
k = 1 + 3.3 * 1.3\\  
k = 5.29 = 5$$

$$A = \frac{33-12}{5.29}\\  
A = 4.038 = 4$$

![[/image 6 7.png|image 6 7.png]]

  

Si empezáramos el intervalo inicial desde el valor mínimo de la muestra, o sea 12, en la última clase el intervalo superaría los valores que tenemos disponibles.  
Ajustamos manualmente el intervalo inicial reduciendo el límite inferior así la última clase no se sobrepasa, pero respetando la amplitud del intervalo  

  

![[/image 7 7.png|image 7 7.png]]

![[/image 8 6.png|image 8 6.png]]

![[/image 9 6.png|image 9 6.png]]

![[/image 10 6.png|image 10 6.png]]

![[/image 11 6.png|image 11 6.png]]

  

  

### Medidas de tendencia central

- Media ⇒ Promedio
- Moda ⇒ Dato de mayor frecuencia
- Mediana ⇒ Dato central

  

## Datos no agrupados

---

### Media poblacional [μ]

$$\mu = \frac{\sum_{i=1}^{N} X_i}{N}$$

### Media muestral [x̅]

$$x̄ = \frac{\sum_{i=1}^{n} X_i}{n}$$

> [!important] No es necesario ordenar los datos

  

### Datos agrupados

---

### Media poblacional [μ]

$$\mu = \frac{\sum_{i=1}^{k} x_i * f_i}{N}$$

### Media muestral [x̅]

$$x̄ = \frac{\sum_{i=1}^{k} x_i * f_i}{n}$$

### Numero de elementos/clases

$$N = n = \sum_{i=1}^{k} f_i$$

> [!important] Cuando los datos están agrupados en **intervalos**, **no conocemos los valores exactos dentro de cada clase**. En lugar de trabajar con cada dato individual, tomamos un **valor representativo** para cada intervalo.
> 
> $$Valor\ representativo= x_i = \frac{L_s + L_i}{2}$$
> 
> También trabajamos con la contribución de cada intervalo en la suma total de los datos.  
> La idea es que, como **no tenemos los valores exactos dentro de cada intervalo**, **asumimos que todos los datos de ese intervalo están concentrados en su punto medio**.  
>   
>   
> 
> $$Contribución\ en \ la \ suma\ total = x_i * f_i$$

  

> [!important]
> 
> ![[/image 12 6.png|image 12 6.png]]

  

### Moda en datos agrupados [Mo]

$$Mo = L_i + a * \frac {(f_i - f_{i-1})}{(f_i - f_{i-1})+(f_i - f_{i+1})}$$

L_i = Límite inferior de la clase modal

L_s = Límite superior de la clase modal

a = amplitud del intervalo

f_i = frecuencia absoluta de la clase modal

  

### Mediana en datos no agrupados [Me]

Cuando n es impar

$$Me = x_{\frac{n+1}{2}}$$

Cuando n es par

$$Me = \frac{x_{\frac{n}{2}} + x_{\frac{n}{2} + 1}}{2}$$

> [!important]
> 
> ![[/image 13 6.png|image 13 6.png]]

> [!important] Es necesario ordenar los datos

  

### Mediana en datos agrupados [Me]

$$Me = L_i + \frac{\frac{n}{2} - F_{i-1}}{f_i} * A_i$$

n/2 = posición de la clase mediana

F_i = frecuencua acumulada de la clase  
A_i = amplitud de la clase  

  

### Percentiles

$$P_k = L_i + \frac{ \frac{kN}{100} - F_{i-1}}{ f_i } * A$$

> [!important]
> 
> ![[/image 14 5.png|image 14 5.png]]

  

### Cuartiles

$$Q_k = L_i + \frac{ \frac{kN}{4} - F_{i-1}}{ f_i } * A$$

> [!important]
> 
> ![[/image 15 5.png|image 15 5.png]]

  

### Decil

$$D_k = L_i + \frac{ \frac{kN}{10} - F_{i-1}}{ f_i } * A$$

> [!important]
> 
> ![[/image 16 4.png|image 16 4.png]]