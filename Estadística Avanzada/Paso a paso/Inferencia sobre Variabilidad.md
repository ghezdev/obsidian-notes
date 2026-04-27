### Situación 1: Inferencia sobre una Sola Población (Distribución Chi-Cuadrado $\chi^2$)

Esta situación aparece cuando querés controlar la precisión de un solo proceso (ej. el tiempo de respuesta de un servidor o el error en los pesos de paquetes).

#### ¿Cómo identificarla en la consigna?

- Busca frases como: "Estimar la varianza...", "Hallar un intervalo para el desvío...", o "Verificar si la variabilidad supera un máximo de...".
    
- **Dato clave:** Solo hay **un grupo** de datos o una sola muestra.
    

#### Paso a Paso: Intervalo de Confianza (Estimación)

1. **Identificar datos muestrales:** Necesitás el tamaño de la muestra ($n$) y el desvío estándar muestral ($S$) o la varianza ($S^2$).
    
2. **Definir el Nivel de Confianza ($1-\alpha$):** Por ejemplo, 95% ($\alpha=0,05$).
    
3. **Uso de la App "Probability Distributions":**
    
    - Seleccioná la distribución **Chi-square**.
        
    - Ingresá los grados de libertad: $v = n - 1$.
        
    - Buscá los valores críticos $\chi^2_{\alpha/2}$ y $\chi^2_{1-\alpha/2}$ (las "colas" de la distribución).
        
4. **Calcular los límites:**
    
    - Límite Inferior ($A'$): $\sqrt{\frac{(n-1)S^2}{\chi^2_{1-\alpha/2}}}$.
        
    - Límite Superior ($B'$): $\sqrt{\frac{(n-1)S^2}{\chi^2_{\alpha/2}}}$. _(Si te piden varianza, no uses la raíz cuadrada)_.
        

#### Paso a Paso: Ensayo de Hipótesis (Control)

1. **Plantear Hipótesis:** Generalmente es una prueba de control (hipótesis optimista):
    
    - $H_0: \sigma \le \sigma_0$ (El proceso está bajo control).
        
    - $H_1: \sigma > \sigma_0$ (La variabilidad aumentó).
        
2. **Calcular el Estadístico de Prueba (Pivote):** $\chi^2_c = \frac{(n-1)S^2}{\sigma_0^2}$.
    
3. **Decisión:** Compará $\chi^2_c$ con el valor crítico de la App para un riesgo $\alpha$. Si $\chi^2_c > \chi^2_{1-\alpha}$, rechazás $H_0$.
    

---

### Situación 2: Comparación de Dos Poblaciones (Distribución F de Fisher)

Se usa para comparar si un método nuevo es más preciso que uno viejo (ej. comparar dos algoritmos de optimización).

#### ¿Cómo identificarla en la consigna?

- Busca: "Comparar dos máquinas...", "Verificar si el nuevo método reduce el desvío en un X%...", o "¿Son las varianzas iguales?".
    
- **Dato clave:** Tenés **dos muestras independientes** ($n_1, S_1$ y $n_2, S_2$).
    

#### Paso a Paso: Ensayo de Hipótesis

1. **Definir el parámetro de comparación ($\phi$):** Se define como la relación entre desvíos $\phi = \sigma_1 / \sigma_2$.
    
2. **Plantear Hipótesis:**
    
    - Para igualdad: $H_0: \sigma_1 = \sigma_2$ (o $\phi = 1$).
        
    - Para mejora específica (ej. reducir desvío un 20%): $H_0: \phi \ge 0,8$.
        
3. **Calcular el Estadístico de Prueba:** $j^2 = \frac{S_1^2}{S_2^2}$.
    
4. **Uso de la App "Probability Distributions":**
    
    - Seleccioná la distribución **F**.
        
    - Ingresá $v_1 = n_1 - 1$ (numerador) y $v_2 = n_2 - 1$ (denominador).
        
    - Obtené el valor crítico $F_{(1-\alpha; v_1, v_2)}$.
        
5. **Regla de Decisión:** Si $j^2$ cae en la zona de rechazo (típicamente $j^2 > F_{crit}$), se concluye que las variabilidades son distintas.

- - -
### Fundamento Matemático: ¿Por qué estas distribuciones?

- **Chi-Cuadrado ($\chi^2$):** Es básicamente la suma de cuadrados de variables normales estándar. Como la varianza se calcula sumando cuadrados de desviaciones $(x_i - \bar{x})^2$, es natural que su distribución sea una Chi-cuadrado escalada.
    
- **Distribución F:** Es el **cociente** de dos variables Chi-cuadrado independientes (cada una dividida por sus grados de libertad). Por eso la usamos para comparar dos varianzas: es literalmente una relación de dispersiones.

- - -

### Checklist para el Examen:

1. **¿Cuántas poblaciones hay?** (1 $\rightarrow \chi^2$ | 2 $\rightarrow F$).
    
2. **¿Piden desvío o varianza?** (Cuidado con elevar al cuadrado o aplicar raíz).
    
3. **¿La consigna pide "asegurar" algo?** (Planteá eso en la Hipótesis Alternativa $H_1$, y lo opuesto en $H_0$).
    
4. **App:** Siempre verificá los Grados de Libertad ($n-1$) antes de buscar el valor crítico.