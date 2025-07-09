¡Genial! Vamos con la **Distribución Exponencial**, muy útil y bastante común en problemas de tiempo de espera, confiabilidad, y procesos de Poisson.

---

# 1. Concepto y características clave

- **¿Qué es?**  
    Es una distribución **continua** que modela el tiempo entre eventos que ocurren con una tasa constante y de forma aleatoria (sin memoria).
    
- **¿Cuándo se usa?**  
    Para modelar tiempos de espera hasta que ocurre un evento (por ejemplo, el tiempo entre llamadas en un call center, la vida útil de un dispositivo sin fallas, tiempo hasta la llegada del próximo cliente).
    
- **Variable que modela:**  
    Variable aleatoria continua, que representa un tiempo o una duración, siempre mayor o igual a 0.
    
- **Memoria sin memoria:**  
    La distribución es “sin memoria”, lo que significa que la probabilidad de que el evento ocurra en el futuro no depende de cuánto tiempo ya haya pasado.
    

---

# 2. Fórmulas básicas y parámetros

- Parámetro:  
    λ>0\lambda > 0 — tasa de eventos por unidad de tiempo (también llamada **parámetro de tasa**).
    
- Función de densidad de probabilidad (pdf):
    
    f(x)=λe−λx,x≥0f(x) = \lambda e^{-\lambda x}, \quad x \geq 0
- Función de distribución acumulada (CDF):
    
    F(x)=P(X≤x)=1−e−λx,x≥0F(x) = P(X \leq x) = 1 - e^{-\lambda x}, \quad x \geq 0
- Esperanza (media):
    
    E[X]=1λE[X] = \frac{1}{\lambda}
- Varianza:
    
    Var(X)=1λ2Var(X) = \frac{1}{\lambda^2}

---

# 3. Tipos de ejercicios comunes

- **Ejercicio tipo 1: Calcular la probabilidad de que el evento ocurra antes de un tiempo tt.**  
    Usar la CDF:
    
    P(X≤t)=1−e−λtP(X \leq t) = 1 - e^{-\lambda t}
- **Ejercicio tipo 2: Calcular la probabilidad de que el evento tarde más que un tiempo tt.**  
    Complemento de la CDF:
    
    P(X>t)=e−λtP(X > t) = e^{-\lambda t}
- **Ejercicio tipo 3: Calcular probabilidades entre dos tiempos aa y bb (con 0≤a<b0 \leq a < b)**
    
    P(a<X≤b)=F(b)−F(a)=e−λa−e−λbP(a < X \leq b) = F(b) - F(a) = e^{-\lambda a} - e^{-\lambda b}
- **Ejercicio tipo 4: Encontrar el tiempo tt asociado a una probabilidad dada pp (cuantiles).**  
    Despejamos de la CDF:
    
    p=1−e−λt  ⟹  t=−ln⁡(1−p)λp = 1 - e^{-\lambda t} \implies t = -\frac{\ln(1-p)}{\lambda}
- **Ejercicio tipo 5: Encontrar la media, varianza o parámetro λ\lambda a partir de datos.**
    

---

# 4. Tips para identificar la distribución en un ejercicio

- Palabras claves:
    
    > “tiempo entre eventos”, “tiempo hasta que pasa algo”, “duración”, “sin memoria”, “evento que sucede a una tasa constante”, “proceso de Poisson”, “espera”, “vida útil”.
    
- Condiciones típicas:
    
    - Variable continua, no negativa.
        
    - Probabilidad de ocurrencia independiente del tiempo pasado.
        
    - Proceso con tasa constante λ\lambda.
        

---

# Ejemplo práctico

> En promedio, una máquina falla cada 5 horas. ¿Cuál es la probabilidad de que funcione más de 3 horas sin fallar?

**Solución:**

- λ=15=0.2\lambda = \frac{1}{5} = 0.2 (eventos por hora)
    
- Queremos P(X>3)P(X > 3)
    

P(X>3)=e−0.2×3=e−0.6≈0.549P(X > 3) = e^{-0.2 \times 3} = e^{-0.6} \approx 0.549

---

¿Querés que te pase ejercicios para que practiques? O que te explique otra distribución?