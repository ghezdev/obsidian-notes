# Modelo de Gumbel del máximo

- Es una distribución continua de probabilidad.
- Se utiliza para modelar el valor extremo **máximo** (el más alto) dentro de un conjunto de variables aleatorias.
- Es uno de los tres tipos de distribuciones de valores extremos, usado para eventos raros, como catástrofes naturales o máximos de carga.

**Ejemplos**

- Mayor temperatura registrada en un año.
- Nivel máximo de agua en una represa durante una tormenta.
- Mayor carga que soporta una estructura antes de romperse.
- Tiempo de vida **máximo** antes de falla en sistemas paralelos.

---

# **¿Qué mirar en la Consigna?**

- **"Mayor valor observado" o "evento extremo máximo":** Si la consigna hace énfasis en el evento más grande, más fuerte o más tardío.
- **"Condiciones extremas":** Menciones a récords, picos o máximos históricos.
- **"Modelar catástrofes o máximos críticos"** como el máximo caudal, temperatura, presión, etc.
- **"Distribución de valor extremo tipo I (Gumbel)"**: Puede mencionarse así en la consigna en lugar de nombrarla como “del máximo”.

### **En resumen, si la consigna se enfoca en el valor más grande o evento extremo superior, pensá en el modelo Gumbel del máximo.**

---

# **Función de densidad de probabilidad**

## Dominio de la VA: $x \in \mathbb{R}$

## Función de densidad de probabilidad: 

## $\theta = \text{Mo}$ = parámetro de localización

## $\beta = \text{parámetro de escala (unidades de la variables).}$

## $f(x) = \left( \frac{1}{\beta} \right)^{-(\frac{x - \theta}{\beta})} \cdot e^{ -e^{ -\left( \frac{x - \theta}{\beta} \right) } }$
---

## Moda: $M_0 = \theta$

## Mediana: $Me = \theta - \beta \cdot \left[ \ln(\ln 2) \right]$

## Esperanza matemática/Media: $E(x) = \mu = \theta + \beta \cdot C$ con $C = 0{,}5772$

## Varianza: $v = \sigma^2 = \frac{\pi^2}{6} \cdot \beta^2$

## Desviación estándar:

## Fractil/Percentil: $x_{(\alpha)} = \theta - \beta \cdot \ln(-\ln(\alpha))$


---

# **Función de distribución acumulada**

## Izquierda: $P(x <= x_0) = F(x)_{Gmax} = e^{ -e^{ -\left( \frac{x - \theta}{\beta} \right) } }$

## Derecha: $P(x >= x_0) = G(x)_{Gmax} = 1 - F(x)_{Gmax}$

## Rango:

---

# **Expectativas parciales**

---

# **Parámetros**

## $\theta = \text{Mo}$ = parámetro de localización

## $\beta = \text{parámetro de escala (unidades de la variables).}$

- - -
# Gráfico 

![[Pasted image 20250620183448.png]]

