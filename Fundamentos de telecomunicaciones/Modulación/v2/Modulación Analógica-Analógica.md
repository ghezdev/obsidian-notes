### Portadora analógica a Moduladora analógica

> _"Se modulan parámetros de una onda portadora senoidal: amplitud, frecuencia o fase."_

![[Pasted image 20250803173026.png]]

#### 🔊 a. Amplitud (AM)
En **AM**, se usa una **portadora senoidal continua** (analógica) cuya **amplitud se modifica** en proporción a los valores instantáneos de una **señal moduladora analógica** (por ejemplo, voz o música).
 
Fórmula típica:
$$s(t) = [A + m(t)] \cdot \cos(2\pi f_c t)$$

Donde:

- $A$: amplitud de la portadora.

- $m(t)$: señal moduladora analógica.

- $f_c$​: frecuencia de la portadora.

- La señal modulada contiene la **frecuencia portadora** y dos **bandas laterales**.

- La **frecuencia y fase** de la portadora permanecen constantes.

- Se varía la **amplitud** de la portadora en proporción a la señal de información.

- Sensible al **ruido**.

- Usada en radiodifusión AM.


#### 🎶 b. Frecuencia (FM)

En **FM**, la **frecuencia de la portadora** varía en función del valor instantáneo de la **señal moduladora analógica**.

Fórmula:
$$s(t) = A \cdot \cos\left(2\pi f_c t + 2\pi k_f \int m(t) dt\right)$$

Donde:

- $k_f$​: sensibilidad de frecuencia.

- $m(t)$: señal moduladora.

- Se varía la **frecuencia** de la portadora.

- Mucho más **robusta al ruido** que AM. No hay ruido

- Usada en radio FM y enlaces de microondas.

- La **amplitud y fase** permanecen constantes.


![[Pasted image 20250803173115.png]]


#### 🔁 c. Fase (PM)

En **PM**, es la **fase de la portadora** la que se modifica proporcionalmente al valor de la señal moduladora.    

Fórmula:
$$s(t) = A \cdot \cos\left(2\pi f_c t + k_p \cdot m(t)\right)$$

Donde:

- $k_p$​: sensibilidad de fase.

- $m(t)$: señal moduladora analógica.

- PM es conceptualmente similar a FM, pero la modulación se aplica **directamente a la fase**.

- Se varía la **fase** de la portadora según la señal.

- Menos común en analógica, pero base de muchas técnicas digitales.

- La **amplitud y frecuencia** permanecen constantes.

![[Pasted image 20250803173325.png]]