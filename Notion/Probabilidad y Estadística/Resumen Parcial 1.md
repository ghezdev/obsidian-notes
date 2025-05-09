
# Población \[N\]

Número de observaciones

# Muestra \[n\]

Subconjunto de una población

# Tipos de datos

## Cualitativos

Datos que no son medibles, se utilizan palabras o categorías

- Ordinales: *Tienen un órden o jerarquía*
- Nominales: *No tienen un órden o jerarquía*


## Cuantitativos

Datos que son medibles, se utilizan números o escalas

- Discretos
- Continuos

# Distribución de frecuencias
- - - 

Resumen tabular de datos que muestra el número (frecuencia) de elementos en cada una de las diferentes clases disyuntas (que no se sobreponen)
  
> [!important] Clase = Elemento parte del conjunto a analizar

## Frecuencia absoluta \[fi\]

Es el número de veces que aparece un elemento
  
## Frecuencia relativa \[fr\]

Expresa la **proporción** de veces que aparece un elemento en relación con el total de elementos

$$fr = \frac{f_i}{n}$$

## Frecuencia porcentual \[fr%\]

Es la frecuencia relativa expresada en porcentaje. La representación porcentual de un elemento en relación con el total de elementos

$$fr\% = fr * 100$$

## Frecuencia acumulada \[Fi\]

Se obtiene sumando las frecuencias absolutas de todos los valores anteriores más el actual. Nos indica cuántos datos tienen un valor menor o igual a un cierto punto.

$$F_i = F_{i-1} + f_i$$
  
### Regla de Sturges

$$k = 1 + 3.3log(N) \ con \ k ∈ ℕ$$

Para el análisis de datos cuantitativos, la regla de sturges te permite aproximarte al mejor numero de clases/elementos a considerar

  

### Amplitud/Ancho

Para agrupar datos, necesitamos ponerle un intervalo, este intervalo va a tener una amplitud o diferencia, el cual es esta

$$A = \frac{valor\ máximo \ de \ la \ muestra\ - valor\ mínimo\ de \ la \ muestra}{k} \ con \ A∈ℕ$$

# Datos agrupados
---

### Media poblacional \[μ\]
$$\mu = \frac{\sum_{i=1}^{k} x_i * f_i}{N}$$

### Media muestral \[x̅\]
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

  

## Moda \[Mo\]
$$Mo = L_i + a * \frac {(f_i - f_{i-1})}{(f_i - f_{i-1})+(f_i - f_{i+1})}$$
$$
L_i = Límite\ inferior\ de\ la\ clase\ modal
$$
$$ 
L_s = Límite\ superior\ de\ la\ clase\ modal
$$$$
a = amplitud\ del\ intervalo
$$$$
f_i = frecuencia\ absoluta\ de\ la\ clase\ modal
$$


## Mediana en datos agrupados \[Me\]
$$
Me = L_i + \frac{\frac{n}{2} - F_{i-1}}{f_i} * A_i
$$
$$
n/2 = posición de la clase mediana
$$
$$
F_i = frecuencua acumulada de la clase
$$
$$
A_i = amplitud de la clase
$$


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


