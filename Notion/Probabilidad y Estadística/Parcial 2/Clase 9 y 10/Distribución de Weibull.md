- Es una distribución continua de probabilidad.
- Se utiliza para modelar el **tiempo de vida útil** de un componente o sistema.
- Generaliza a la distribución exponencial: permite representar tasas de fallo **crecientes, constantes o decrecientes**.
- Muy utilizada en análisis de confiabilidad, mantenimiento y riesgo.

**Ejemplos**

- Tiempo hasta la falla de un motor, componente eléctrico o electrónico.
- Duración de vida de productos en garantía.
- Análisis de fatiga de materiales bajo estrés.

---
# **¿Qué mirar en la Consigna?**

- **"Tiempo hasta que un componente falle":** Si la variable aleatoria representa un tiempo de vida útil o duración bajo cierto uso, es buena candidata a Weibull.
    
- **"Fallas mecánicas bajo condiciones de uso exigentes":** Si hay contexto industrial o de ingeniería, es frecuente el uso de Weibull.
    
- **"Me dan parámetros β (forma) y ω (escala)":** Son los dos parámetros clásicos de Weibull.
    
- **"El riesgo de falla cambia con el tiempo":** Weibull permite modelar tasas de fallo que **aumentan** o **disminuyen** (a diferencia de la exponencial que es constante).
    

### **En resumen, si la consigna menciona duración bajo estrés, falla por desgaste o riesgo de falla no constante, pensá en la Weibull.**

---
# **Función de densidad de probabilidad**

## Dominio de la VA: $X \geq 0$

## Función de densidad de probabilidad: 

## ω: parámetro de **forma**.
## β: parámetro de **escala** (cambia la dispersión).

## $f(x) = \omega \left( \frac{1}{\beta} \right)^{\omega} \cdot x^{\omega - 1} \cdot e^{- \left( \frac{x}{\beta} \right)^{\omega}}$

---
## Moda:  

## $M_0 = 0 \quad \text{(si } \omega \leq 0)$ 
## $M_0 = \beta \cdot \left(1 - \frac{1}{\omega}\right)^{\frac{1}{\omega}} \quad \text{(si } \omega \geq 1)$

## Mediana: $Me = \beta \cdot (\ln 2)^{1/\omega}$

## Esperanza matemática/Media: $E(x) = \mu = \beta \cdot \left[\Gamma\left(1 + \frac{1}{\omega}\right)\right]$

## Varianza: $v = \sigma^2 = \beta^2 \left[ \Gamma\left(1 + \frac{2}{\omega} \right) - \Gamma^2\left(1 + \frac{1}{\omega} \right) \right]$

## Desviación estándar: $\sigma = \sqrt{ \beta^2 \left[ \Gamma\left(1 + \frac{2}{\omega} \right) - \Gamma^2\left(1 + \frac{1}{\omega} \right) \right] }$

## Fractil/Percentil: $x_{(\alpha)} = \beta \cdot \left( -\ln(1 - \alpha) \right)^{1/\omega}$

---
# **Función de distribución acumulada**

## Izquierda: $P(x \leq x_0) = F_w\left(\frac{x}{\beta}; \omega\right) = 1-e^{-\left(\frac{x}{\beta}\right)^{\omega}}$

## Derecha: $P(x \geq x_0) = G_w\left(\frac{x}{\beta}; \omega\right) = e^{-\left(\frac{x}{\beta}\right)^{\omega}}$

## Rango:

---
# **Expectativas parciales**

USAR PROGRAMA DE DOS
## Izquierda:

## Derecha:

---

# **Parámetros**

## ω: parámetro de **forma**.

## β: parámetro de **escala** (cambia la dispersión).

- - -
# **Gráfico**

![[Pasted image 20250620165704.png]]

- - -
# Geogebra 

![[Imagen de WhatsApp 2025-06-20 a las 17.41.57_94104519.jpg]]

- - -
### 🔍 ¿Cómo saber cuál usar en un ejercicio?

#### 1. **¿Mencionan que la tasa de fallas es constante?**

- ✅ **Sí** → usa **Exponencial**
- ❌ **No**, o **dicen que la tasa de fallas cambia** con el tiempo → usa **Weibull**

#### 2. **¿Hay información sobre “vida útil”, “desgaste”, “envejecimiento”?**

- ✅ **Sí** (por ejemplo, “la probabilidad de que falle aumenta con el tiempo”) → **Weibull con α>1**

#### 3. **¿Es un tiempo entre eventos aleatorios e independientes?**

- ✅ **Sí** (ej: espera entre buses, llamadas, clientes) → **Exponencial**

#### 4. **¿El enunciado te da valores para α y β?**

- ✅ Entonces claramente es **Weibull**
- Si solo te dan λ, lo más probable es que sea **exponencial**


| Característica                        | Modelo Exponencial                                                                                      | Modelo Weibull                                                       |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Tipo de distribución**              | Distribución de probabilidad continua                                                                   | Distribución de probabilidad continua                                |
| **Parámetros**                        | Un parámetro: λ>0 (tasa)                                                                                | Dos parámetros: α>0 (forma), β>0 (escala)                            |
| **Función de tasa de falla (hazard)** | Constante: λ                                                                                            | Variable: depende de α:                                              |
|                                       |                                                                                                         | - α < 1: tasa decreciente                                            |
|                                       |                                                                                                         | - α = 1: constante (→ se reduce a exponencial)                       |
|                                       |                                                                                                         | - α > 1: tasa creciente                                              |
| **Memoria**                           | **Sin memoria** (la probabilidad de falla no depende del tiempo pasado)                                 | **Con memoria** (la probabilidad sí depende del tiempo transcurrido) |
| **Casos típicos de uso**              | - Vida útil de componentes sin desgaste- Tiempo entre eventos independientes (ej: llamadas telefónicas) | - Vida útil de componentes con desgaste o envejecimiento             |
| **Relación entre ambas**              | Es un caso especial de Weibull con α = 1                                                                | Generaliza la exponencial                                            |
