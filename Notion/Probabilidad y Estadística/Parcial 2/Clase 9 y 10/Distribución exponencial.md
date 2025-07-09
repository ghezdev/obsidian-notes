- Es una distribución continua de probabilidad.
- Se utiliza para describir el tiempo/distancia/longitud que transcurre en realizar una actividad/evento.

**Ejemplos**

- Tiempo de espera para ser atendido en un banco.
- Tiempo necesario para cargar un camión.
- Distancia entre los principales defectos de una carretera.
- Tiempo de vida de un componente.

- - -
# **¿Qué mirar en la Consigna?**

- **"Tiempo/Distancia/Longitud entre eventos":** ¿La variable de interés es el _lapso_ o la _cantidad de espacio_ entre un suceso y el siguiente? Esto es crucial. No importa si son segundos, metros o kilómetros; si mide el intervalo _hasta_ que algo pasa, es exponencial.
    - **Ejemplo:** "Tiempo entre llamadas", "Distancia entre fallas", "Vida útil de un componente".
      
- **"Ocurrencia aleatoria/continua a una tasa constante":** La consigna suele describir eventos que pasan de forma impredecible pero con una tasa promedio estable en un flujo continuo (de tiempo, de espacio, etc.). Esto se relaciona con los **procesos de Poisson**.
    
- **"Sin Memoria":** Si el problema implica que el pasado no afecta el futuro (por ejemplo, que un cable que ya funcionó 100m sin fallas tiene la misma probabilidad de fallar en los próximos 10m que un cable nuevo), estás ante una distribución exponencial.
    
- **Parámetro: "Media del tiempo/distancia hasta el evento":** Si te dan directamente el promedio de ese "tiempo", "distancia" o "longitud" que pasa entre eventos, como la "longitud media entre fallas", es un fuerte indicio del modelo exponencial.

### **En resumen, si la consigna te pide analizar cuánto dura o cuánto espacio hay entre sucesos que ocurren de manera aleatoria y constante, pensá en el modelo exponencial.**

- - -
# **Función de densidad de probabilidad**

## Dominio de la VA: $X >= 0$

## Con: $λ=\frac{1}{μ}​$

## Entonces: $f(x)=λe^{-λx}$

- - -
## Moda $M_o = 0$

## Mediana $M_e = \frac{ln2}{x}$

## Esperanza matemática/Media  $μ = \frac{1}{λ}$

## Varianza $v=σ^{2} = \frac{1}{λ^{2}}$

## Desviación estándar $σ = \frac{1}{λ}$

## Fractil/Percentil $x_{a}=-\frac{ln(1-a)}{λ}$ con $a = posición fractil$

- - -
# **Función de distribución acumulada**

## Izquierda $P(x <= x_0) = F_{exp}(x/λ) = 1-λe^{-λx}$

## Derecha $P(x >= x_0) = G_{exp}(x/λ) = λe^{-λx}$

## Rango $P(x_0 <= x <= x_1) = P(x <= x_1) - P(x_0 <= x)$

- - -
# **Expectativas parciales**

## Izquierda $H_{exp}(x/λ) = \frac{1}{λ}*F_{gamma}(x/2; λ)$

## Derecha 

- - -
# **Parámetros**: 

# $λ$ = numero medio de fallas por unidad de continuo

- - -
# **Gráfico**

![[Pasted image 20250620155437.png]]

- - -
# **Geogebra**

![[Imagen de WhatsApp 2025-06-20 a las 15.53.49_49af3e48.jpg]]