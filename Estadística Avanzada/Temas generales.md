Para aprobar con éxito el **Primer Parcial** (programado para la **Clase 9**, el 28 de abril ), necesitás dominar los cimientos de la Inferencia Estadística. Pensalo como el entrenamiento de un modelo de clasificación: tenés que saber qué tan "seguro" estás de tus predicciones y cuánta muestra necesitás para que el error no arruine el resultado.

Aquí tenés el "stack" tecnológico de conceptos que entran, organizados por la lógica de la materia:

### 1. Inferencia sobre Medias Poblacionales ($\mu$)

Es el núcleo del parcial. Se trata de estimar el promedio de una población total a partir de una muestra.

- **Varianza Poblacional Conocida (Uso de $Z$):** Cuando tenés los logs históricos del desvío ($\sigma$).
    
- **Varianza Poblacional Desconocida (Uso de $t$ de Student):** Cuando solo tenés el desvío de la muestra ($S$). Aquí la distribución es más "pesada" en las colas para compensar la incertidumbre.
    
- **Poblaciones Infinitas vs. Finitas:** Si la población es pequeña (finita), debés aplicar el **Factor de Corrección por Finitud** ($\sqrt{\frac{N-n}{N-1}}$).
    
- **Tamaño de Muestra ($n$):** Calcular cuántos datos necesitás para no superar un error de estimación ($e$) prefijado.
    

### 2. Inferencia sobre Variabilidad ($\sigma$ o $\sigma^2$)

En ingeniería, a veces no importa tanto el promedio, sino la estabilidad del proceso (que no haya _jitter_ o variaciones locas).

- **Distribución Chi-Cuadrado ($\chi^2$):** La herramienta para crear intervalos de confianza sobre la varianza.
    
- **Relación entre límites:** Aprender a calcular $n$ para que el intervalo de dispersión sea lo más angosto posible.
    

### 3. Procesos de Bernoulli (Proporciones $p$)

Esto es fundamental para **Machine Learning** (ej. tasa de clics o precisión de un clasificador binario).

- **Muestreo a la Binomial:** Estimar la probabilidad de éxito ($p$) en eventos de "pasa/no pasa".
    
- **Aproximaciones:** Saber cuándo usar la **Normal** (si $n \cdot p > 10$) o **Poisson** (si $p$ es muy chico) para simplificar cálculos.
    
- **Teoría del Control:** Definir límites para saber si un proceso sigue "bajo control" o si el porcentaje de errores se disparó.
    

### 4. Ensayos de Hipótesis (La lógica de decisión)

Es el `if-else` de la estadística.

- **Hipótesis Nula ($H_0$) y Alternativa ($H_1$):** El planteo inicial.
    
- **Errores de Decisión:**
    
    - **Error Tipo I ($\alpha$):** Riesgo del productor (rechazar algo bueno).
        
    - **Error Tipo II ($\beta$):** Riesgo del consumidor (aceptar algo malo).
        
- **Potencia del Ensayo ($1 - \beta$):** La capacidad del test para detectar un cambio real cuando existe.
    
- **Curva Característica Operativa (OC) y de Potencia:** Gráficos que muestran cómo varía el riesgo según el valor real del parámetro.
    

**Dato clave para tu App:** Recordá que para **Medias (desvío desconocido)** usás la función `t`, para **Varianzas** usás `Chi-Square` y para **Proporciones** podés usar `Binomial` o `Normal` según el caso.
