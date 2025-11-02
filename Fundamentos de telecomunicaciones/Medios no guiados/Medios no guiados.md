Los conocemos comúnmente como antenas.

Una antena sirve para mandar ondas radioeléctricas formadas por señales electromagnéticas. Las señales electromagnéticas tienen una parte eléctrica y magnética. A la eléctrica la puedo modificar. Gracias a la parte magnética la señal se propaga.

Uno es perpendicular al otro SIEMPRE.

![[Pasted image 20250809173603.png]]

_Polarización:_ En qué sentido está mi campo eléctrico (el único que puedo controlar). Puede ser polarización lineal (vertical, horizontal), circular, elíptico.

Es necesario controlar quién usa cada frecuencia en la que se transmite.

Espectro radioeléctrico: todo el juego de frecuencias desde 3KHz hasta 300GHz controlado a nivel internacional. Si pago soy dueño de cierta frecuencia de manera temporal. Hay ciertas frecuencias liberadas como 2.4GHz.

¿Quién regula esto? La UIT, organismo de la ONU con sede en Ginebra.

El espectro se divide dependiendo de si estamos en frecuencias muy bajas, bajas, medianas, etc. Son 8 en total.

Si aumento la frecuencia, la longitud de onda disminuye.

La propagación cambia de acuerdo a las frecuencias que transmito

![[Pasted image 20250809173755.png]]

## Propagación según la frecuencia

- ***Onda terrestre***: La señal se propaga siguiendo la curvatura de la tierra. Uso en frecuencias medias y bajas. Solo depende de la potencia que emite, porque solo le afecta la atenuación del aire.

- ***Onda espacial***: Se usa en frecuencias altas. La ionosfera me permite usarla de espejo para llegar más lejos. Durante el día, la ionosfera permite que ciertas frecuencias del sol no entren, cargándose de energía y ensanchándose, permitiendo el rebote.

- ***Onda directa***: propagación en línea recta. No se puede reflejar. Se usa en frecuencias muy altas.

![[Pasted image 20250809174121.png]]

## Propagación de las ondas electromagnéticas

![[Pasted image 20250809174416.png]]

![[Pasted image 20250809174421.png]]

![[Pasted image 20250809174426.png]]

![[Pasted image 20250809174429.png]]

![[Pasted image 20250809174435.png]]

## Horizonte Radioeléctrico

$$𝑫 = 4,14 \sqrt{𝐻1}$$
$D$ se mide en kilómetros

## Zona de fresnel

Es el volumen de espacio que la onda ocupará entre el emisor de una onda y un receptor. Calcular esto nos ayudará a garantizar la recepción de dicha señal.

![[Pasted image 20250809174613.png]]

Hay que garantizar que entre las antenas no haya obstáculos


## Antena

La señal eléctrica va por un cable hasta una antena, y esa antena la convierte en una señal electromagnética que se propaga en el aire.

Para calcular una antena, lo primero que tengo que saber es a **qué frecuencia voy a transmitir, y, por tanto, la longitud de onda**.

La parte eléctrica de una onda está en la **amplitud**. Tengo que aprovechar el **diferencial de energía**, porque ahí está transmitida la información que quiero. Entonces, el tamaño de la antena va a ser (idealmente): $Longitud\ de\ onda / 2$

Podría hacer también la antena de $Longitud\ de\ onda / 4$, pero perdería energía, o sea, mayor atenuación, por eso para compensar tengo que aumentar la potencia.

Puedo seguir dividiendo por potencias de dos

![[Pasted image 20250809174805.png]]

Antena AM 125m

![[Pasted image 20250809174812.png]]

Antena bluetooth 6cm

## Tipos de antena 

Yagi: orientadas para la polarización horizontal y vertical

![[Pasted image 20250809174831.png]]

Disco parabólica:

![[Pasted image 20250809174836.png]]

## Características básicas

• Diagrama de Radiación: distribución espacial de la energía radiada

• Polarización: orientación del campo eléctrico, vertical, horizontal y circular

• Ganancia: relación entre la intensidad de radiación y la que produciría otra antena de referencia, en la misma dirección

• Impedancia: la que presenta a la línea de alimentación de la energía.

• Ancho de Banda: rango útil de frecuencias

• Ganancia: relación entre la intensidad de radiación y la que produciría otra antena de referencia, en la misma dirección

• Se expresa en decibeles y sus unidades derivadas

• Decibel es una expresión logarítmica que se usa para indicar una relación de potencias o tensiones eléctricas

• Representa un valor con respecto a otro de referencia

## Potencia Isotrópica Radiada Equivalente – PIRE

Cantidad de potencia que emitiría una antena isotrópica teórica

PIRE = Pt – Lc + Ga

PIRE y PT (potencia del transmisor) son dBm, Lc (las pérdidas del cable) en dB, y Ga (la ganancia de la antena) en dBi (respecto de la Pi)

Es la potencia que debería tener el transmisor, usando una antena isotrópica (ideal), para que el receptor esté en las mismas condiciones que el transmisor.

## Criterios para evaluar un medio de transmisión

• Coste, de los materiales y la instalación.

• Velocidad, máximo nº de bps que se pueden transmitir.

• Atenuación, tiene que ver con la resistencia del cable.

• Interferencia electromagnética (EMI), sensibilidad del medio a la energía electromagnética externa que interfiere con la señal.

• Seguridad, entendida como protección contra intrusos.