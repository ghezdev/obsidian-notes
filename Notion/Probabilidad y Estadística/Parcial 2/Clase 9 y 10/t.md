| Distribución                   | Tipo     | Dominio de xx                             | Parámetros principales                         | Variable que modela                              | Ejemplo típico                                                  |
| ------------------------------ | -------- | ----------------------------------------- | ---------------------------------------------- | ------------------------------------------------ | --------------------------------------------------------------- |
| **Exponencial**                | Continua | $x≥0$                                     | $\lambda > 0 (tasa)$                           | Tiempo/distancia entre eventos independientes    | Tiempo entre fallas o llegadas                                  |
| **Weibull**                    | Continua | $x≥0$                                     | $\alpha (forma)$ $\beta (escala)$              | Vida útil con tasa de fallo variable             | Duración de productos con desgaste                              |
| **Gumbel (máximo)**            | Continua | $x \in \mathbb{R}$                        | $\mu (ubicación)$ $\beta (escala)$             | Valor extremo superior                           | Temperatura máxima anual                                        |
| **Gumbel (mínimo)**            | Continua | $x \in \mathbb{R}$                        | $\mu$, $\beta$                                 | Valor extremo inferior                           | Resistencia mínima de materiales                                |
| **Pareto**                     | Continua | $x \geq x_m > 0$                          | $\alpha (forma)$, $x_m (mínimo)$               | Cola pesada, eventos raros                       | Distribución de riqueza, tamaño de ciudades                     |
| **Normal**                     | Continua | $x \in \mathbb{R}$                        | $\mu$, <br>$\sigma > 0$                        | Variable continua simétrica                      | Errores de medición, inteligencia, alturas                      |
| **Lognormal**                  | Continua | $x > 0$                                   | $\mu$, <br>$\sigma > 0$                        | Variable positiva con crecimiento multiplicativo | Ingresos, tiempos de procesos, precios                          |
| **Gamma**                      | Continua | $x \geq 0$                                | $\alpha > 0 (forma)$<br>$\beta > 0 (escala)$   | Tiempo hasta α eventos independientes            | Tiempo total hasta que ocurran varios eventos                   |
| **Poisson**                    | Discreta | $x = 0, 1, 2, \dots$                      | $\lambda > 0 (media)$                          | Conteo de eventos por unidad de tiempo/espacio   | Nro de llamadas por hora, accidentes por día                    |
| **Binomial**                   | Discreta | $x = 0, 1, ..., n$                        | $n: ensayos$, $p: prob. de\ exito$             | Nº de éxitos en n ensayos independientes         | Cuántos productos defectuosos en un lote de 20                  |
| **Pascal (Binomial Negativa)** | Discreta | $x = r, r+1, \dots$                       | $r: éxitos\ deseados$<br>$p: prob.\ de\ exito$ | Ensayos hasta obtener r éxitos                   | Nº de intentos hasta lograr 3 aciertos                          |
| **Hipergeométrica**            | Discreta | $x = \max(0, n + K - N), ..., \min(K, n)$ | $N: total$ <br>$K: éxitos$<br>$n: muestras$    | Éxitos en una muestra sin reemplazo              | Sacar 3 bolas rojas en 5 extracciones de una urna sin reemplazo |


| Categoría                                      | Distribuciones clave                                           | Variable que modelan                                  | Cómo identificar en un enunciado                                    | Ejemplos típicos                                             |
| ---------------------------------------------- | -------------------------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Tiempos o distancias entre eventos**         | Exponencial, Weibull, Gamma                                    | Tiempo o distancia hasta un evento (o k eventos)      | Palabras clave: “tiempo hasta”, “espera”, “vida útil”, “fallo”      | Tiempo entre llamadas, duración de vida, desgaste            |
| **Valores extremos**                           | Gumbel (máximo y mínimo)                                       | Valores máximos o mínimos en muestras                 | “Máximo anual”, “resistencia mínima”, “valor extremo”               | Temperaturas máximas, resistencia mínima, crecidas           |
| **Conteo de eventos**                          | Poisson, Binomial, Pascal (binomial negativa), Hipergeométrica | Número de eventos o éxitos en un conjunto o intervalo | “Número de...”, “cuántos”, “conteo”, “ensayos hasta”                | Llamadas por hora, defectos en lote, intentos hasta r éxitos |
| **Variables continuas simétricas**             | Normal                                                         | Variables continuas simétricas                        | “Distribución simétrica”, “errores”, “promedios”                    | Estatura, errores de medición, IQ                            |
| **Variables continuas asimétricas, positivas** | Lognormal, Pareto                                              | Variables positivas con cola larga                    | “Distribución sesgada”, “crecimiento multiplicativo”, “cola pesada” | Ingresos, precios, tamaños de ciudades, riqueza              |


## 🧩 Tips rápidos para elegir en un examen

- Si es **tiempo hasta un evento** → piensa en **Exponencial**, **Weibull** (más general), o **Gamma** (varios eventos).
    
- Si es **conteo de eventos en intervalo fijo** → casi siempre es **Poisson** o **Binomial** si es número fijo de ensayos.
    
- Si es **número de ensayos hasta lograr éxito(s)** → busca **Geométrica** o **Pascal**.
    
- Si el problema menciona **valores extremos** (máximos o mínimos) → Gumbel.
    
- Si la variable es **simétrica y continúa** → Normal.
    
- Si la variable es **positiva y asimétrica** → Lognormal o Pareto, según si la cola es moderada o pesada.


x ~ Normal ( $\mu$ , $\sigma^2$ )