# Modelo de Gumbel del mínimo

- Es una distribución continua de probabilidad.
- Se utiliza para modelar el valor extremo **mínimo** (el más pequeño) en un conjunto de variables aleatorias.
- Comúnmente usada para representar **fallas tempranas**, es decir, aquellas que ocurren debido a los puntos más débiles o vulnerables de un sistema.

**Ejemplos**

- Tiempo hasta la **primera falla** en un conjunto de componentes.
- **Temperatura mínima** registrada en un periodo.
- **Presión mínima** que provoca rotura en un sistema.
- **Vida útil más corta** entre varios productos probados simultáneamente.

---

# **¿Qué mirar en la Consigna?**

- **"Primera falla" o "fallos tempranos":** Si la consigna hace énfasis en lo primero que falla o en la parte más débil del sistema.
- **"Valor más bajo" entre varios elementos aleatorios:** Casos donde el mínimo entre observaciones es la variable de interés.
- **"Distribución extrema del mínimo":** Si explícitamente se menciona que la distribución del mínimo sigue Gumbel (a veces lo hacen).
- **"Fallas iniciales en componentes críticos":** Contextos de ingeniería o análisis de riesgos donde se busca estudiar el primer punto de quiebre.

### **En resumen, si la consigna se enfoca en eventos extremos bajos, especialmente el primer fallo o el más débil, pensá en el modelo Gumbel del mínimo.**

---

# **Función de densidad de probabilidad**

## Dominio de la VA: $x \in \mathbb{R}$

## Función de densidad de probabilidad: 

## $\theta = \text{Mo}$ = parámetro de localización

## $\beta = \text{parámetro de escala (unidades de la variables).}$

## $f(x) = \left( \frac{1}{\beta} \right)^\frac{x - \theta}{\beta} \cdot e^{ -e^{ \left( \frac{x - \theta}{\beta} \right) } }$

---
## Moda: $M_0 = \theta$

## Mediana: $Me = \theta + \beta \cdot \left[ \ln(\ln 2) \right]$

## Esperanza matemática/Media: $E(x) = \mu = \theta - \beta \cdot C$ con $C = 0{,}5772$

## Varianza: $v = \sigma^2 = \frac{\pi^2}{6} \cdot \beta^2$

## Desviación estándar:

## Fractil/Percentil: $x_{(\alpha)} = \theta + \beta \cdot \ln(-\ln(1 - \alpha))$

---

# **Función de distribución acumulada**

## Izquierda:

## Derecha: $P(x >= x_0) = G(x)_{Gmin} = e^{-e^{\left(\frac{x - \theta}{\beta}\right)}}$

## Rango: $P(x <= x_0) = F(x)_{Gmin} = 1 - G(x)_{Gmin}$


---

# **Expectativas parciales**


---

# **Parámetros**

## $\theta = \text{Mo}$ = parámetro de localización

## $\beta = \text{parámetro de escala (unidades de la variables).}$

- - -
# Gráfico 

![[Pasted image 20250620183433.png]]

