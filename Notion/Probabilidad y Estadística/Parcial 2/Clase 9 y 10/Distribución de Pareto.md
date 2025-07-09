# Distribución de Pareto

- Es una distribución continua de probabilidad.
- Modela fenómenos donde **pocas observaciones representan una gran parte del total**, y la mayoría representan una parte muy pequeña.
- Se utiliza cuando se quiere modelar **valores con colas pesadas**: grandes valores poco frecuentes pero posibles.
    

**Ejemplos**

- Distribución de la riqueza (el 20% de las personas tiene el 80% del dinero).
- Tamaño de ciudades (pocas ciudades grandes, muchas pequeñas).
- Tiempos de espera muy largos en ciertos sistemas.
- Saldos bancarios o ingresos de una población.
    

---

# **¿Qué mirar en la Consigna?**

- **"Valores extremos grandes posibles":** Si pueden aparecer pocos valores muy altos (columna derecha larga o pesada), Pareto es buena candidata.
- **"Distribución de tipo 80/20":** Si una parte pequeña de las observaciones tiene una gran participación (ley de Pareto).
- **"Valores mayores que un umbral mínimo θ\thetaθ":** Toda la variable se define para valores mayores que ese umbral, por ejemplo, x≥160x \geq 160x≥160 U$s.
- **"Distribución con media mayor que la mediana" o "asimétrica a la derecha":** Un indicio de que podría ser Pareto.

### **En resumen, si se modelan fenómenos de concentración desigual y posibilidad de valores muy grandes, pensá en Pareto.**

---

# **Función de densidad de probabilidad**

## Dominio de la VA: $x \geq \theta$ donde θ>0

## Función de densidad de probabilidad: 

## θ: mínimo valor posible (parámetro de escala).

## b: parámetro de forma (determina la "cola").

## $b=\frac{\mu}{\mu-\theta}$

## $f(x) = \frac{b}{x} \left( \frac{\theta}{x} \right)^b \quad x \geq \theta$

---

## Moda:

## Mediana: $Me = \theta \cdot 2^{1/b}$

## Esperanza matemática/Media: $E(x)=\mu=\frac{\theta b}{b-1}$

## Varianza: $v = \sigma^2 = \frac{b \cdot \theta^2}{(b-1)^4(b-2)}$

## Desviación estándar:

## Fractil/Percentil: $x(\alpha) = \frac{\theta}{(1-\alpha)^{1/b}}$

---

# **Función de distribución acumulada**

## Izquierda: $F(x) = 1 - \left( \frac{\theta}{x} \right)^b \quad x \geq \theta$

## Derecha:

## Rango:

---

# **Expectativas parciales**

_(Generalmente se calculan numéricamente. Se pueden derivar, pero no tienen formas cerradas simples.)_

---

# **Parámetros**

## θ: mínimo valor posible (parámetro de escala).

## b: parámetro de forma (determina la "cola").

- - -
# Gráfico 

![[Pasted image 20250620211159.png]]
