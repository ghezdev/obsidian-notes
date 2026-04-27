
Exacto — **la fórmula del intervalo de confianza (IC) cambia según dos cosas**:

1. si conocés **σ (desvío poblacional)**
    
2. si la población es **finita o (aprox.) infinita**
    

Te lo dejo ordenado como para parcial 👇

---

# 🧠 🔥 IDEA CLAVE

$$IC = \bar{x} \pm \text{ERROR MUESTRAL}$$

👉 Lo único que cambia entre fórmulas es el **error muestral**

---

# 📊 🔹 CASOS QUE TENÉS QUE SABER

## ✅ 1. σ conocido + población infinita

$$
IC = \bar{x} \pm Z \cdot \frac{\sigma}{\sqrt{n}}  
$$

### ✔ Error muestral:

$$
E = Z \cdot \frac{\sigma}{\sqrt{n}}  
$$

---

## ✅ 2. σ conocido + población finita

$$
IC = \bar{x} \pm Z \cdot \frac{\sigma}{\sqrt{n}} \cdot \sqrt{\frac{N - n}{N}}  
$$

### ✔ Error muestral:

$$
E = Z \cdot \frac{\sigma}{\sqrt{n}} \cdot \sqrt{\frac{N - n}{N}}  
$$

---


$$
t = \frac{\bar{x} - \mu}{s / \sqrt{n}}  
$$


## ✅ 3. σ desconocido + población infinita

$$
IC = \bar{x} \pm t \cdot \frac{s}{\sqrt{n}}  
$$

### ✔ Error muestral:

$$
E = t \cdot \frac{s}{\sqrt{n}}  
$$

---

## ✅ 4. σ desconocido + población finita

$$
IC = \bar{x} \pm t \cdot \frac{s}{\sqrt{n}} \cdot \sqrt{\frac{N - n}{N}}  
$$

### ✔ Error muestral:

$$
E = t \cdot \frac{s}{\sqrt{n}} \cdot \sqrt{\frac{N - n}{N}}  
$$

---

# 🎯 🔥 RESUMEN VISUAL (esto memorizalo)

| Caso             | Distribución | Error muestral                    |
| ---------------- | ------------ | --------------------------------- |
| σ conocido       | Z            | $Z \cdot \frac{\sigma}{\sqrt{n}}$ |
| σ desconocido    | t            | $t \cdot \frac{s}{\sqrt{n}}$      |
| población finita | + corrección | $\times \sqrt{\frac{N-n}{N}}$     |

---

# 🧠 🔹 REGLA DE DECISIÓN (clave examen)

1. ¿σ es conocido?
    
    - Sí → Z
        
    - No → t
        
2. ¿n/N > 5%?
    
    - Sí → agrego corrección finita
        
    - No → la ignoro
        

---

# 🔍 🔹 INTUICIÓN

👉 Todo es el mismo concepto:

$$
\text{Error} = \text{(valor crítico)} \times \text{(incertidumbre)}  
$$

Donde:

- Valor crítico → Z o t
    
- Incertidumbre → (\sigma/\sqrt{n}) o (s/\sqrt{n})
    
- Ajuste → corrección finita
    

---

# 🚨 ERRORES TÍPICOS

❌ Usar Z cuando σ es desconocido  
❌ Olvidarse de la corrección finita  
❌ Usar t con σ conocido

---

# 🧠 1. ¿CAMBIA LA FÓRMULA DE TAMAÑO DE MUESTRA?

👉 **Sí, cambia según qué estés estimando y qué información tengas.**

## 🔹 CASO 1: MEDIA con σ conocido (el más común)

$$ n = \left(\frac{Z \cdot \sigma}{E}\right)^2 $$

👉 Este es el que ya usaste.

## 🔹 CASO 2: MEDIA con σ desconocido

👉 **En teoría debería usar t**, pero:

⚠️ Problema:

- No sabés σ
- No sabés n (¡lo estás calculando!)

👉 Entonces:

✅ Se usa **Z igual**, con una estimación de σ






- - -
- - -
- - -

Entiendo perfectamente. El mundo de las fórmulas de estadística puede parecer un "choose your own adventure" (elige tu propia aventura), pero tiene una lógica de programación muy clara. Si esto fuera un código, serían puros bloques `if/else`.

Vamos a organizar el "mapa de fórmulas" según lo que te pide el profesor, separando por la cantidad de información que tenés.

---

## Caso 1: Dos Riesgos ($\alpha$ y $\beta$)

Este es el caso de tu ejercicio (Gerente de Compras vs. Gerente de Producción). Aquí no solo buscás el **valor crítico**, sino que a veces necesitás calcular el **tamaño de la muestra ($n$)** para cumplir con ambos.

### Con Desviación Poblacional conocida ($\sigma$)

Es el caso "amigable" para hacer a mano.

- **Fórmula para $n$:**
    
    $$n = \left[ \frac{(Z_\alpha + Z_\beta) \cdot \sigma}{\mu_0 - \mu_1} \right]^2$$
    
- **Fórmula para el Valor Crítico ($\bar{x}_c$):**
    
    $$\bar{x}_c = \mu_0 \pm Z_\alpha \cdot \frac{\sigma}{\sqrt{n}}$$
    

### Con Desviación Poblacional DESCONOCIDA ($s$)

Como dijo tu profesor, **aquí no profundizamos**. ¿Por qué? Porque para sacar el valor de la tabla (T de Student) necesitás los grados de libertad ($n-1$), ¡pero no conocés $n$! Esto requiere un proceso iterativo (probar un $n$, ver si da, ajustar) que se hace con software como Excel, SPSS o Python.

---

## Caso 2: Un solo Riesgo ($\alpha$)

Es el más común. Tenés un tamaño de muestra fijo ($n$) y solo un nivel de significación (ej. "calculá con un 5% de error").

### Subcaso A: $\sigma$ Conocida (Usamos Z - Normal)

Se usa cuando el enunciado te da la varianza de la "población" o de "históricos".

- **Valor Crítico:**
    
    $$\bar{x}_c = \mu_0 \pm Z_\alpha \cdot \frac{\sigma}{\sqrt{n}}$$
    

### Subcaso B: $\sigma$ Desconocida (Usamos T de Student)

Es lo que harás en el punto **b** de tu ejercicio, porque tenés 10 datos pero no la desviación real de la fábrica.

- **Valor Crítico:**
    
    $$\bar{x}_c = \mu_0 \pm t_{(\alpha, n-1)} \cdot \frac{s}{\sqrt{n}}$$
    
    _(Donde $s$ es la desviación que calculás vos de la muestra)._
    

---

## Caso 3: Proporciones (Porcentajes)

A veces el ejercicio no es de "espesor en $\mu$", sino de "porcentaje de piezas falladas".

- **Valor Crítico de la Proporción ($p_c$):**
    
    $$p_c = P_0 \pm Z_\alpha \cdot \sqrt{\frac{P_0 \cdot (1 - P_0)}{n}}$$
    

---

## ¿Qué pasa con los Grados de Libertad ($df$)?

Me preguntaste: _"¿Cómo los obtengo si no me dan $n$?"_.

1. **Si estás en el Caso 1 (calculando $n$):** No usás grados de libertad inicialmente. Usás la tabla **Z** (Normal) como una aproximación. Una vez que obtenés un $n$, podés "refinar" usando T, pero para exámenes de grado, si calculás $n$, usás Z.
    
2. **Si el $n$ es muy grande ($n > 30$):** Los grados de libertad son tantos que la tabla T se vuelve igual a la tabla Z. Muchos profesores te dejan usar Z directamente para ahorrar tiempo.
    
3. **La regla de oro:** Siempre que uses la desviación de la muestra ($s$) y tengas el $n$, tus grados de libertad son:
    
    $$\text{gl (o df)} = n - 1$$
    

---

## Resumen de "Sentido de la flecha" ($\pm$)

¿Cuándo sumás y cuándo restás? Mirá tu $H_1$:

- Si $H_1: \mu < \text{algo}$ (Cola izquierda): **Restás**. El valor crítico es menor a la media.
    
- Si $H_1: \mu > \text{algo}$ (Cola derecha): **Sumás**. El valor crítico es mayor a la media.
    
- Si $H_1: \mu \neq \text{algo}$ (Dos colas): Tenés **dos valores críticos**, uno sumando y otro restando, usando $\alpha/2$.
    

### Aplicado a tu ejercicio (Ítem b):

Como tenés $n=10$ y no conocés $\sigma$, estás en el **Caso 2, Subcaso B**.

1. Calculás el desvío $s$ de tus 10 datos.
    
2. Buscás en la tabla T el valor para 9 grados de libertad ($10-1$).
    
3. **Restás** de $58$, porque tu miedo es que el espesor sea menor.
    

¿Te animás a intentar calcular el desvío estándar ($s$) de esos números o preferís que te pase un tip para hacerlo rápido?



- - -
- - -
- - -

Perfecto. Tu hoja tiene fórmulas de **estimación**, **intervalos de confianza**, **tests de hipótesis**, **errores tipo I/II**, **potencia**, **tamaño de muestra**, **varianza**, **desvío estándar** y **proporciones**. La idea no es memorizar todo, sino saber responder: **¿qué parámetro estoy estudiando?, ¿conozco σ?, ¿la muestra es grande?, ¿es intervalo o test?, ¿es unilateral o bilateral?**

Voy a explicártelas por bloques para que las puedas usar en examen.

---

# 1. Población vs muestra

En tu hoja aparece esta tabla:

|Concepto|Población|Muestra|
|---|--:|--:|
|Promedio|`μ`|`x̄`|
|Varianza|`σ²`|`S²`|
|Desvío estándar|`σ`|`S`|
|Proporción|`p` o `P`|`p̂`|

Esto es clave.

La **población** es el conjunto total que querés estudiar. Sus valores reales suelen ser desconocidos.

La **muestra** es una parte de esa población. Con la muestra calculás estimadores.

Por ejemplo:

- `μ`: promedio real de todos los clientes.
    
- `x̄`: promedio observado en una muestra de clientes.
    
- `σ²`: varianza real poblacional.
    
- `S²`: varianza calculada con la muestra.
    
- `p`: proporción real poblacional.
    
- `p̂`: proporción observada en la muestra.
    

La lógica general de casi todo el parcial es:

> Uso datos de la muestra para estimar o testear algo de la población.

---

# 2. Intervalo de confianza para `μ` con `σ` conocido

Fórmula general:

[  
P\left(\bar{x} - z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}} \leq \mu \leq \bar{x} + z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}\right)=1-\alpha  
]

La usás cuando querés estimar el **promedio poblacional `μ`** y te dicen que la **desviación estándar poblacional `σ` es conocida**.

Ejemplo típico:

> Una máquina produce piezas. Se sabe que σ = 4 mm. Se toma una muestra de n = 40 piezas con promedio 102 mm. Construir un intervalo del 95% para μ.

Ahí usás normal `Z`.

La estructura es:

[  
IC = \bar{x} \pm z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}  
]

Donde:

- `x̄` es el promedio muestral.
    
- `σ` es el desvío poblacional conocido.
    
- `n` es el tamaño de muestra.
    
- `z` sale de la tabla normal.
    
- `1 - α` es el nivel de confianza.
    

Por ejemplo, si el nivel de confianza es 95%:

[  
1-\alpha = 0.95  
]

Entonces:

[  
\alpha = 0.05  
]

Como el intervalo es bilateral, repartís el error en dos colas:

[  
\alpha/2 = 0.025  
]

Entonces buscás:

[  
z_{1-\alpha/2} = z_{0.975}  
]

Que suele ser:

[  
z_{0.975} = 1.96  
]

---

# 3. Error de muestreo para `μ` con `σ` conocido

El error de muestreo, también llamado margen de error, es:

[  
E = z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}  
]

Tu hoja también tiene despejado el tamaño muestral:

[  
n = \left(\frac{z_{1-\alpha/2}\sigma}{E}\right)^2  
]

La usás cuando el ejercicio dice algo como:

> ¿Qué tamaño de muestra se necesita para estimar μ con un error máximo de 2 unidades y confianza del 95%?

Ahí no estás calculando un intervalo. Estás calculando **cuántos datos necesitás tomar**.

La lógica es:

[  
E = z \frac{\sigma}{\sqrt{n}}  
]

Despejando:

[  
n = \left(\frac{z\sigma}{E}\right)^2  
]

Importante: si te da decimal, normalmente redondeás **hacia arriba**, porque no podés tomar 38.2 observaciones. Serían 39.

---

# 4. Intervalo de confianza para `μ` con `σ` desconocido

Fórmula:

[  
P\left(\bar{x} - t_{\nu;1-\alpha/2}\frac{S}{\sqrt{n}} \leq \mu \leq \bar{x} + t_{\nu;1-\alpha/2}\frac{S}{\sqrt{n}}\right)=1-\alpha  
]

La usás cuando querés estimar `μ`, pero **no conocés `σ` poblacional**. Entonces usás `S`, el desvío estándar muestral.

La estructura es:

[  
IC = \bar{x} \pm t_{\nu;1-\alpha/2}\frac{S}{\sqrt{n}}  
]

Donde:

[  
\nu = n - 1  
]

`\nu` son los grados de libertad.

Acá usás distribución **t de Student**, no normal Z.

La diferencia práctica es:

- Si conozco `σ`, uso `Z`.
    
- Si no conozco `σ`, uso `t`.
    
- Para `t`, necesito grados de libertad:
    

[  
\nu = n - 1  
]

Ejemplo:

> Se toma una muestra de 12 alumnos. El promedio fue 74 y el desvío muestral fue 8. Construir un intervalo del 95% para μ.

Como no conozco `σ`, uso `t`.

---

# 5. Error de muestreo para `μ` con `σ` desconocido

La idea es parecida al caso anterior, pero con `t` y `S`:

[  
E = t_{\nu;1-\alpha/2}\frac{S}{\sqrt{n}}  
]

El problema es que `t` depende de `n`, porque:

[  
\nu = n - 1  
]

Entonces, cuando querés calcular tamaño muestral con `σ` desconocido, puede volverse iterativo o aproximado. En muchos ejercicios se usa una muestra piloto para obtener `S`.

---

# 6. Errores en test de hipótesis

En tu hoja aparece:

[  
\alpha = P(RH_0 / H_0 \text{ verdadera})  
]

[  
\beta = P(No \ RH_0 / H_0 \text{ falsa})  
]

Traducido:

## Error tipo I: `α`

Es rechazar `H₀` cuando `H₀` era verdadera.

Ejemplo:

`H₀`: el medicamento no tiene efecto.  
Rechazo `H₀` y digo que sí tiene efecto, pero en realidad no tenía.

Eso es un falso positivo.

## Error tipo II: `β`

Es no rechazar `H₀` cuando `H₀` era falsa.

Ejemplo:

`H₀`: el medicamento no tiene efecto.  
No rechazo `H₀`, pero en realidad sí tenía efecto.

Eso es un falso negativo.

## Potencia

La potencia del test es:

[  
1-\beta  
]

Es la probabilidad de rechazar `H₀` cuando realmente hay que rechazarla.

En palabras simples:

> La potencia mide qué tan bueno es el test para detectar una diferencia real.

---

# 7. Test de hipótesis para `μ` con `σ` conocido

Lo usás cuando querés testear una afirmación sobre el promedio poblacional `μ`, y conocés `σ`.

Hay tres casos.

---

## 7.1 Test unilateral derecho

Hipótesis:

[  
H_0: \mu \leq \mu_0  
]

[  
H_1: \mu > \mu_0  
]

Lo usás cuando querés probar que el promedio es **mayor** que cierto valor.

Ejemplo:

> La empresa quiere demostrar que el rendimiento promedio supera los 32 km/l.

Entonces:

[  
H_0: \mu \leq 32  
]

[  
H_1: \mu > 32  
]

El valor crítico para el promedio muestral es:

[  
\bar{x}_c = \mu_0 + z_{1-\alpha}\frac{\sigma}{\sqrt{n}}  
]

Regla de rechazo:

[  
\text{Si } \bar{x} > \bar{x}_c, \text{ rechazo } H_0  
]

Es decir: rechazo si el promedio muestral cae demasiado a la derecha.

---

## 7.2 Test unilateral izquierdo

Hipótesis:

[  
H_0: \mu \geq \mu_0  
]

[  
H_1: \mu < \mu_0  
]

Lo usás cuando querés probar que el promedio es **menor** que cierto valor.

Ejemplo:

> Se quiere probar que el tiempo promedio de espera es menor a 10 minutos.

Entonces:

[  
H_0: \mu \geq 10  
]

[  
H_1: \mu < 10  
]

Valor crítico:

[  
\bar{x}_c = \mu_0 - z_{1-\alpha}\frac{\sigma}{\sqrt{n}}  
]

Regla de rechazo:

[  
\text{Si } \bar{x} < \bar{x}_c, \text{ rechazo } H_0  
]

Rechazás si el promedio muestral cae demasiado a la izquierda.

---

## 7.3 Test bilateral

Hipótesis:

[  
H_0: \mu = \mu_0  
]

[  
H_1: \mu \neq \mu_0  
]

Lo usás cuando querés probar si el promedio es **distinto**, sin importar si es mayor o menor.

Ejemplo:

> Se quiere verificar si una máquina está calibrada para producir piezas de 50 gramos.

Entonces:

[  
H_0: \mu = 50  
]

[  
H_1: \mu \neq 50  
]

Valores críticos:

[  
\bar{x}_{c1,c2} = \mu_0 \pm z_{1-\alpha/2}\frac{\sigma}{\sqrt{n}}  
]

Regla de rechazo:

[  
\text{Si } \bar{x} < \bar{x}_{c1} \text{ o } \bar{x} > \bar{x}_{c2}, \text{ rechazo } H_0  
]

Como es bilateral, hay dos zonas de rechazo: una a la izquierda y otra a la derecha.

---

# 8. Test de hipótesis para `μ` con `σ` desconocido

Es igual conceptualmente al anterior, pero cambiás `Z` por `t` y `σ` por `S`.

La usás cuando:

- Querés testear `μ`.
    
- No conocés `σ`.
    
- Tenés `S` calculado desde la muestra.
    

---

## 8.1 Unilateral derecho

[  
H_0: \mu \leq \mu_0  
]

[  
H_1: \mu > \mu_0  
]

Valor crítico:

[  
\bar{x}_c = \mu_0 + t_{\nu;1-\alpha}\frac{S}{\sqrt{n}}  
]

Regla:

[  
\text{Si } \bar{x} > \bar{x}_c, \text{ rechazo } H_0  
]

---

## 8.2 Unilateral izquierdo

[  
H_0: \mu \geq \mu_0  
]

[  
H_1: \mu < \mu_0  
]

Valor crítico:

[  
\bar{x}_c = \mu_0 - t_{\nu;1-\alpha}\frac{S}{\sqrt{n}}  
]

Regla:

[  
\text{Si } \bar{x} < \bar{x}_c, \text{ rechazo } H_0  
]

---

## 8.3 Bilateral

[  
H_0: \mu = \mu_0  
]

[  
H_1: \mu \neq \mu_0  
]

Valores críticos:

[  
\bar{x}_{c1,c2} = \mu_0 \pm t_{\nu;1-\alpha/2}\frac{S}{\sqrt{n}}  
]

Regla:

[  
\text{Si } \bar{x} < \bar{x}_{c1} \text{ o } \bar{x} > \bar{x}_{c2}, \text{ rechazo } H_0  
]

---

# 9. Versión con estadístico de prueba

Tu hoja trabaja mucho con valores críticos directamente sobre `x̄`, pero también podés encontrarlo como estadístico.

Si `σ` es conocido:

[  
Z_{calc} = \frac{\bar{x} - \mu_0}{\sigma/\sqrt{n}}  
]

Si `σ` es desconocido:

[  
T_{calc} = \frac{\bar{x} - \mu_0}{S/\sqrt{n}}  
]

La decisión es equivalente.

Para unilateral derecho:

[  
Z_{calc} > z_{1-\alpha}  
]

Para unilateral izquierdo:

[  
Z_{calc} < -z_{1-\alpha}  
]

Para bilateral:

[  
|Z_{calc}| > z_{1-\alpha/2}  
]

Con `T` es igual, pero usando tabla t con:

[  
\nu = n - 1  
]

---

# 10. Tamaño de muestra para test de hipótesis de `μ`

En tu hoja aparece la fórmula para calcular `n` en tests de hipótesis.

Para test unilateral:

[  
n = \left(\frac{(z_{1-\alpha}+z_{1-\beta})\sigma}{\mu_1-\mu_0}\right)^2  
]

Para test bilateral:

[  
n = \left(\frac{(z_{1-\alpha/2}+z_{1-\beta})\sigma}{\mu_1-\mu_0}\right)^2  
]

La usás cuando el ejercicio te dice:

> Queremos diseñar un test con nivel de significación α y potencia 1 - β para detectar una diferencia entre μ₀ y μ₁.

Acá aparecen dos valores:

- `μ₀`: valor bajo la hipótesis nula.
    
- `μ₁`: valor alternativo que querés poder detectar.
    
- `α`: probabilidad de error tipo I.
    
- `β`: probabilidad de error tipo II.
    
- `1 - β`: potencia.
    

La diferencia importante es:

[  
|\mu_1-\mu_0|  
]

Cuanto más chica sea la diferencia que querés detectar, más grande tiene que ser la muestra.

---

# 11. Curva característica operativa y curva de potencia

En tu hoja aparecen dos gráficos:

- Curva característica operativa: muestra `β`.
    
- Curva de potencia: muestra `1 - β`.
    

La **curva característica operativa** te dice:

[  
\beta(\mu_1)  
]

Es decir, para distintos valores reales de `μ`, cuál es la probabilidad de **no rechazar H₀**.

La **curva de potencia** te dice:

[  
1-\beta(\mu_1)  
]

Es decir, para distintos valores reales de `μ`, cuál es la probabilidad de **rechazar H₀**.

Relación clave:

[  
\text{Potencia} = 1 - \beta  
]

Si `β` baja, la potencia sube.

---

# 12. Intervalo de confianza para la varianza poblacional `σ²`

Fórmula conceptual:

[  
P\left(\frac{(n-1)S^2}{\chi^2_{\nu;1-\alpha/2}} \leq \sigma^2 \leq \frac{(n-1)S^2}{\chi^2_{\nu;\alpha/2}}\right)=1-\alpha  
]

La usás cuando querés estimar la **varianza poblacional**.

Ejemplo:

> Se quiere estimar la variabilidad real del peso de cierto producto.

Acá no se usa normal ni t. Se usa distribución **chi-cuadrado**.

Los grados de libertad son:

[  
\nu = n - 1  
]

Ojo: la fórmula parece invertida porque la distribución chi-cuadrado no es simétrica.

El límite inferior usa el chi-cuadrado grande y el límite superior usa el chi-cuadrado chico.

---

# 13. Intervalo de confianza para el desvío estándar `σ`

Es igual al anterior, pero al final aplicás raíz cuadrada:

[  
IC_{\sigma} =  
\left[  
\sqrt{\frac{(n-1)S^2}{\chi^2_{\nu;1-\alpha/2}}},  
\sqrt{\frac{(n-1)S^2}{\chi^2_{\nu;\alpha/2}}}  
\right]  
]

Lo usás cuando te piden el intervalo para el **desvío estándar poblacional**, no para la varianza.

Recordá:

[  
\sigma = \sqrt{\sigma^2}  
]

Entonces:

- Si te piden intervalo para `σ²`, dejás los límites como varianzas.
    
- Si te piden intervalo para `σ`, sacás raíz cuadrada a ambos límites.
    

---

# 14. Test de hipótesis para la varianza poblacional `σ²`

Lo usás cuando querés probar una afirmación sobre la varianza real.

El estadístico de prueba es:

[  
\chi^2_{calc} = \frac{(n-1)S^2}{\sigma_0^2}  
]

Donde:

- `S²` es la varianza muestral.
    
- `σ₀²` es la varianza propuesta en `H₀`.
    
- `n - 1` son los grados de libertad.
    

---

## 14.1 Test unilateral derecho para varianza

Hipótesis:

[  
H_0: \sigma^2 \leq \sigma_0^2  
]

[  
H_1: \sigma^2 > \sigma_0^2  
]

Lo usás cuando querés probar que la varianza es **mayor**.

Regla:

[  
\text{Si } \chi^2_{calc} \geq \chi^2_{\nu;1-\alpha}, \text{ rechazo } H_0  
]

---

## 14.2 Test unilateral izquierdo para varianza

Hipótesis:

[  
H_0: \sigma^2 \geq \sigma_0^2  
]

[  
H_1: \sigma^2 < \sigma_0^2  
]

Lo usás cuando querés probar que la varianza es **menor**.

Regla:

[  
\text{Si } \chi^2_{calc} \leq \chi^2_{\nu;\alpha}, \text{ rechazo } H_0  
]

---

## 14.3 Test bilateral para varianza

Hipótesis:

[  
H_0: \sigma^2 = \sigma_0^2  
]

[  
H_1: \sigma^2 \neq \sigma_0^2  
]

Regla:

[  
\text{Si } \chi^2_{calc} \leq \chi^2_{\nu;\alpha/2}  
]

o

[  
\chi^2_{calc} \geq \chi^2_{\nu;1-\alpha/2}  
]

rechazo `H₀`.

---

# 15. Intervalo de confianza para proporción `p`

La proporción aparece cuando estudiás porcentajes, tasas o probabilidades.

Ejemplos:

- proporción de clientes satisfechos;
    
- proporción de piezas defectuosas;
    
- proporción de votantes que prefieren una opción;
    
- proporción de usuarios que compran.
    

La estimación muestral es:

[  
\hat{p} = \frac{x}{n}  
]

Donde:

- `x` es la cantidad de casos favorables.
    
- `n` es el tamaño de la muestra.
    

Por ejemplo, si 80 de 200 clientes compraron:

[  
\hat{p} = \frac{80}{200} = 0.4  
]

---

## 15.1 Intervalo aproximado normal para `p`

Tu hoja dice que podés usar normal si se cumplen:

[  
n\hat{p} > 10  
]

y

[  
n(1-\hat{p}) > 10  
]

Si ambas condiciones se cumplen:

[  
IC = \hat{p} \pm z_{1-\alpha/2}  
\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}  
]

La usás cuando la muestra es suficientemente grande.

---

## 15.2 Intervalo exacto para `p`

Tu hoja también incluye una fórmula usando distribución F de Fisher-Snedecor.

Ese intervalo se usa cuando la aproximación normal no es confiable, especialmente si:

- `n` es chico;
    
- `p̂` está muy cerca de 0;
    
- `p̂` está muy cerca de 1;
    
- no se cumplen las condiciones `n p̂ > 10` y `n(1-p̂) > 10`.
    

En examen, si te dan esa fórmula, probablemente quieran que la uses cuando el caso no permite normal.

---

# 16. Tamaño de muestra para estimar una proporción

Fórmula aproximada:

[  
n = \frac{z_{1-\alpha/2}^2 \hat{p}(1-\hat{p})}{E^2}  
]

La usás cuando el ejercicio dice:

> ¿Qué tamaño de muestra se necesita para estimar una proporción con error máximo E y confianza del 95%?

Donde:

- `E` es el error máximo tolerado.
    
- `p̂` puede venir de una muestra piloto.
    
- Si no tenés `p̂`, a veces se usa:
    

[  
\hat{p}=0.5  
]

Porque maximiza:

[  
\hat{p}(1-\hat{p})  
]

y da el tamaño muestral más conservador.

---

# 17. Test de hipótesis para proporción `p`

Lo usás cuando querés probar una afirmación sobre una proporción poblacional.

---

## 17.1 Test unilateral derecho para proporción

Hipótesis:

[  
H_0: p \leq p_0  
]

[  
H_1: p > p_0  
]

Valor crítico:

[  
\hat{p}_c = p_0 + z_{1-\alpha}  
\sqrt{\frac{p_0(1-p_0)}{n}}  
]

Regla:

[  
\text{Si } \hat{p} > \hat{p}_c, \text{ rechazo } H_0  
]

---

## 17.2 Test unilateral izquierdo para proporción

Hipótesis:

[  
H_0: p \geq p_0  
]

[  
H_1: p < p_0  
]

Valor crítico:

[  
\hat{p}_c = p_0 - z_{1-\alpha}  
\sqrt{\frac{p_0(1-p_0)}{n}}  
]

Regla:

[  
\text{Si } \hat{p} < \hat{p}_c, \text{ rechazo } H_0  
]

---

## 17.3 Test bilateral para proporción

Hipótesis:

[  
H_0: p = p_0  
]

[  
H_1: p \neq p_0  
]

Valores críticos:

[  
\hat{p}_{c1,c2} = p_0 \pm z_{1-\alpha/2}  
\sqrt{\frac{p_0(1-p_0)}{n}}  
]

Regla:

[  
\text{Si } \hat{p} < \hat{p}_{c1} \text{ o } \hat{p} > \hat{p}_{c2}, \text{ rechazo } H_0  
]

---

# 18. Tamaño de muestra para test de proporción

Tu hoja incluye fórmulas para calcular `n` cuando querés diseñar un test de proporciones con determinado `α` y `β`.

La idea conceptual es parecida al caso de la media.

Para test unilateral:

[  
n =  
\left(  
\frac{  
z_{1-\alpha}\sqrt{p_0(1-p_0)}  
+  
z_{1-\beta}\sqrt{p_1(1-p_1)}  
}{  
p_1-p_0  
}  
\right)^2  
]

Para test bilateral:

[  
n =  
\left(  
\frac{  
z_{1-\alpha/2}\sqrt{p_0(1-p_0)}  
+  
z_{1-\beta}\sqrt{p_1(1-p_1)}  
}{  
p_1-p_0  
}  
\right)^2  
]

Donde:

- `p₀` es la proporción bajo `H₀`.
    
- `p₁` es la proporción alternativa que querés detectar.
    
- `α` es el error tipo I.
    
- `β` es el error tipo II.
    
- `1 - β` es la potencia.
    

---

# 19. Amplitud del intervalo

Tu hoja dice:

[  
Amplitud = 2E_M  
]

y también:

[  
LS - LI = 2E_M  
]

Esto significa:

[  
E_M = \frac{LS - LI}{2}  
]

Donde:

- `LS` es el límite superior.
    
- `LI` es el límite inferior.
    
- `E_M` es el margen de error.
    

Ejemplo:

Si un intervalo es:

[  
[40, 50]  
]

Entonces:

[  
LS - LI = 50 - 40 = 10  
]

Y el margen de error es:

[  
E_M = 5  
]

Porque el intervalo está centrado en:

[  
45 \pm 5  
]

---

# 20. Cómo decidir qué fórmula usar

Esta es probablemente la parte más importante para el examen.

## Paso 1: identificar el parámetro

Preguntate:

¿Qué quiero estudiar?

|Si el problema habla de...|Parámetro|
|---|---|
|Promedio, media, rendimiento medio, tiempo medio|`μ`|
|Variabilidad, dispersión, varianza|`σ²`|
|Desvío estándar|`σ`|
|Porcentaje, proporción, tasa|`p`|

---

## Paso 2: identificar si es intervalo o test

Si dice:

> Construir un intervalo de confianza...

Usás fórmulas de intervalo.

Si dice:

> Probar, verificar, demostrar, contrastar, testear...

Usás test de hipótesis.

---

## Paso 3: si es media, mirar si `σ` es conocida

Para `μ`:

|Caso|Distribución|
|---|---|
|`σ` conocida|Normal Z|
|`σ` desconocida|t de Student|
|proporción `p`|Normal Z o exacta|
|varianza `σ²`|Chi-cuadrado|

---

## Paso 4: si es test, mirar la dirección

|Lo que quiere probar el problema|Hipótesis alternativa|
|---|---|
|“mayor que”, “superior a”, “más de”|`H₁: parámetro > valor`|
|“menor que”, “inferior a”, “menos de”|`H₁: parámetro < valor`|
|“distinto de”, “cambió”, “difiere”|`H₁: parámetro ≠ valor`|

La hipótesis alternativa `H₁` te define el tipo de test:

|Alternativa|Test|
|---|---|
|`>`|unilateral derecho|
|`<`|unilateral izquierdo|
|`≠`|bilateral|

---

# 21. Mapa rápido de uso

|Situación|Fórmula/distribución|
|---|---|
|Intervalo para media con `σ` conocida|Z|
|Intervalo para media con `σ` desconocida|t|
|Test para media con `σ` conocida|Z|
|Test para media con `σ` desconocida|t|
|Intervalo para varianza|Chi-cuadrado|
|Test para varianza|Chi-cuadrado|
|Intervalo para desvío estándar|Raíz del intervalo de varianza|
|Intervalo para proporción, muestra grande|Normal Z|
|Intervalo para proporción, muestra chica|Exacto con F|
|Test para proporción|Normal Z|
|Tamaño de muestra para estimación|margen de error|
|Tamaño de muestra para test|usa `α`, `β` y diferencia detectable|

---

# 22. Regla mental para no equivocarte

Para cada ejercicio, antes de tocar fórmulas, escribí esto:

```text
Parámetro: μ / σ² / σ / p
Objetivo: intervalo / test
Datos: n, x̄, S, σ, p̂, α, β
Distribución: Z / t / χ² / F
Tipo de test: derecho / izquierdo / bilateral
Regla de decisión:
Conclusión en palabras:
```

Eso te ordena todo el ejercicio. En estadística avanzada, muchas veces el error no está en calcular, sino en elegir mal la fórmula.