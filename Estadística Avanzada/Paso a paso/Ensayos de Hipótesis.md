### 1. El Planteo: $H_0$ vs $H_1$

En estadística, somos conservadores. Siempre asumimos que no pasó nada nuevo a menos que tengamos pruebas abrumadoras.

- **Hipótesis Nula ($H_0$):** Es el "Status Quo". Representa la igualdad o que no hay cambios.
    
- **Hipótesis Alternativa ($H_1$):** Es lo que querés demostrar, la "novedad".
    
- **La Lógica del Criterio:** Según tu guía, hay dos enfoques según el riesgo:
    
    - **Criterio Pesimista:** Se usa cuando hay un riesgo económico o de seguridad. Ponés como $H_0$ lo que **no** querés que pase (ej. "el nuevo producto es malo") para que la prueba sea más exigente.
        
    - **Criterio Optimista:** Se usa en controles de rutina. Ponés como $H_0$ que todo está bien.
        

---

### 2. El Nivel de Riesgo (Error Tipo I - $\alpha$)

Antes de mirar los datos, definís tu **tolerancia al error**.

- $\alpha$ es la probabilidad de rechazar $H_0$ cuando en realidad era verdadera.
    
- En términos de IA, es un **Falso Positivo**: decir que un modelo es mejor cuando no lo es.
    

---

### 3. La Zona de Decisión (El Valor Crítico)

Aquí es donde usás la lógica de "si-entonces". Calculás un **Límite o Valor Crítico ($X_c$)** que separa el territorio de "aceptación" del de "rechazo".

#### Paso a Paso con la App:

1. Elegí la distribución según el problema ($Z$ si conocés $\sigma$ , $t$ si no ).
    
2. Ingresá los parámetros (como los grados de libertad $v = n-1$ para $t$ ).
    
3. Poné el valor de $\alpha$ en la cola correspondiente (izquierda, derecha o ambas si es bilateral ).
    
4. La App te devolverá el valor crítico (el cuantil).
    

---

### 4. La Regla de Decisión y el Veredicto

Es un condicional simple:

> **IF** el valor observado de la muestra ($x$) cae en la Zona de Rechazo **THEN** rechazo $H_0$.

- **Si rechazás $H_0$:** Decís que los resultados son **estadísticamente significativos**. Hay evidencia suficiente para el cambio.
    
- **Si no rechazás $H_0$:** No decís que $H_0$ es "cierta", sino que **no hay pruebas suficientes** para descartarla. Es como un juicio: el acusado es "no culpable" por falta de pruebas, no necesariamente "inocente".
    

---

### El "Power" del Test (Potencia $1-\beta$)

Esto te va a encantar porque se relaciona con el **Recall** en ML.

- **Error Tipo II ($\beta$):** Es el **Falso Negativo**. No detectar un cambio que sí ocurrió.
    
- **Potencia ($1-\beta$):** Es la capacidad del test para detectar el cambio. Un test con poca potencia es como un antivirus desactualizado: no detecta nada aunque esté infectado.
    

### Resumen para el examen

Para resolver cualquier ejercicio de la guía (como el 24 de la página 9), seguí siempre este orden:

1. **Paso 1:** Planteo de $H_0$ y $H_1$ según el criterio.
    
2. **Paso 2:** Definir $\alpha$.
    
3. **Paso 3:** Calcular el tamaño de muestra $n$ o usar el dado.
    
4. **Paso 4:** Establecer la **Condición de Rechazo** y el valor crítico con la App.
    
5. **Paso 5:** Comparar con el dato de la muestra y dar la **Regla de Decisión** (conclusión en palabras).