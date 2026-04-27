
### ¿Cómo identificar un problema de Bernoulli?

Buscá estas señales en la consigna:

- La variable es discreta: "cantidad de artículos defectuosos", "número de inscriptos", "televidentes que ven un programa".
    
- Solo hay dos resultados posibles (Éxito o Fracaso).
    
- La población es infinita o el muestreo es con reposición (probabilidad $p$ constante).
    

---

### Situación 1: Estimación de la Proporción (Intervalos de Confianza)

Aparece cuando tenés una muestra y querés proyectar el porcentaje real de la población.

#### Paso a Paso:

1. **Recolectar datos:** Necesitás el tamaño de la muestra ($n$) y la cantidad de éxitos observados ($r$). Calculá la proporción muestral: $\hat{p} = r/n$.
    
2. **Elegir el método (¿Exacto o Aproximado?):**
    
    - **Exacto (Binomial):** Siempre es preferible si $n$ es chico.
        
    - **Aproximación Normal:** Usala solo si $n \cdot \hat{p} > 10$ y $n \cdot (1-\hat{p}) > 10$.
        
3. **Uso de la App "Probability Distributions":**
    
    - **Para el límite inferior ($A$):** Seleccioná **Binomial**, poné $n$ y buscá el valor de $p$ tal que la probabilidad acumulada sea $\alpha/2$.
        
    - **Para el límite superior ($B$):** Buscá el valor de $p$ tal que la probabilidad acumulada sea $1 - \alpha/2$.
        
    
    > **Tip de Pro:** En la App también podés usar la distribución **F** para hallar estos límites de forma exacta si preferís fórmulas directas.
    

---

### Situación 2: Ensayos de Hipótesis (Toma de Decisiones)

Se usa cuando querés "asegurar" si un cambio funcionó o si se cumple una especificación.

#### Paso a Paso:

1. **Plantear las Hipótesis ($H_0$ y $H_1$):**
    
    - **Criterio Pesimista:** Si hay riesgo económico, asumís que el porcentaje **no** mejoró ($H_0: p \ge p_0$).
        
    - **Criterio Optimista:** Para controles de rutina ($H_0: p \le p_0$).
        
2. **Definir el Error Tipo I ($\alpha$):** Es el riesgo de rechazar la verdad (falso positivo).
    
3. **Calcular el valor crítico ($r_c$):**
    
    - En la App (Binomial), ingresás $n$ y el $p_0$ de la hipótesis. Buscá el valor de $r$ que deje un área igual a $\alpha$ en la cola correspondiente.
        
4. **Regla de decisión:**
    
    - Si tu $r$ observado es más extremo que el $r_c$, **rechazás $H_0$**.
        

---

### Situación 3: Cálculo del Tamaño de Muestra ($n$)

¿Cuántos datos necesito para que mi estimación sea precisa?.

#### Paso a Paso:

1. **Identificar el error admitido ($e$):** Por ejemplo, $\pm 2\%$ ($e = 0,02$).
    
2. **Usar la fórmula de la Normal (Aproximación):**
    
    $$n = \left[ \frac{Z_{(1-\alpha/2)}}{e} \right]^2 \cdot \hat{p} \cdot (1-\hat{p}) + 1$$
    
    .
    
    - Si no tenés un $\hat{p}$ previo, usá $0,5$ (es el caso de máxima varianza, el "peor escenario").


- - -

### El toque del Ingeniero: ¿Por qué aproximar?

Como programador, sabés que calcular factoriales grandes (necesarios para la Binomial: $\binom{n}{r}$) es computacionalmente costoso y puede dar _overflow_. Por eso, cuando el dataset es grande ($n$ grande), los estadísticos "optimizan" usando la **Distribución Normal**. Es como pasar de un algoritmo $O(2^n)$ a uno $O(1)$.

- **Aproximación Poisson:** Se usa cuando el evento es muy raro ($p$ muy chico, menor a 0,10). En la guía se menciona el **Criterio de Mermoz** para decidir cuándo es válida.