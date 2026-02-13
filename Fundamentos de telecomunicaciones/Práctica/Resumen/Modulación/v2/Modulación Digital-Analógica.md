## 💾 **Modulación con Portadora Digital**

Aquí, la **portadora** ya no es una onda senoidal continua como en AM/FM/PM, sino una **señal digital** (por ejemplo, una secuencia de pulsos). Lo que se hace es **modular sus características** (amplitud, duración, posición, etc.) para representar una señal analógica original.

Este tipo de modulación se usa comúnmente en sistemas de **digitalización de señales analógicas**, como en telefonía, audio, sensores, etc.

- - -
### Ventajas y Desventajas

Debo tener sistemas sincrónicos, por eso deben tener una señal de reloj con tren de pulsos cuadrados o triangulares.

La frecuencia nos va a decir cuándo tomar la muestra, y debe cumplir el teorema del muestreo (Nyquist)

Ventajas

• Inmune al ruido

• Circuitos digitales sencillos

• Facilidad en reconocer un estado definido

• Señalización simple

• Control del canal junto con datos

• Encriptable, QoS (etiquetar datos para que otro sistema se dé cuenta de las prioridades), Monitoreo.

Desventajas

• Mayor BW - Nyquist

• Necesidad conversión A/D y D/A

• Sincronización

---

### 🔢 Tipos de Modulación con Portadora Digital

### 1. **PAM – Pulse Amplitude Modulation**

> Modulación por amplitud de pulsos.

- La **amplitud de cada pulso digital** representa el valor instantáneo de la señal analógica.

- Es una técnica **analógica a digital** (aunque el resultado aún es una señal analógica en forma de pulsos).

- La señal analógica se **muestrea** periódicamente.

- Cada muestra se convierte en un pulso de **amplitud proporcional** a su valor.

Fórmula:
$$s(t) = \sum_{n=-\infty}^{\infty} m(nT_s) \cdot \delta(t - nT_s)$$

Donde:

- $m(nT_s)$: valor de la señal analógica en el instante de muestreo.

- $T_s$​: período de muestreo.


### 📦 Uso típico:

- Primer paso en sistemas PCM.

- Transmisión de audio o video en sistemas antiguos.

- Se envían **pulsos a intervalos regulares**, cuya **amplitud representa** el valor instantáneo de la señal analógica.

- Es una **etapa previa** en sistemas como PCM.

- Muy sensible al **ruido en amplitud**.


---

### 2. **PDM – Pulse Duration Modulation**

> Modulación por duración de pulsos.

- También se llama **PWM – Pulse Width Modulation**.

- Todos los pulsos tienen la **misma amplitud**, pero su **duración (ancho)** varía proporcionalmente a la señal analógica.

- Cada valor de la señal moduladora se representa mediante un pulso de duración proporcional.

- Ideal para sistemas con componentes que responden a tiempo de activación (motores, fuentes de alimentación).


### 📦 Uso típico:

- Control de motores eléctricos.

- Electrónica de potencia.

- Audio digital (PWM en amplificadores clase D).

---

### 3. **PPM – Pulse Position Modulation**

> Modulación por posición de pulsos.

- Pulsos de igual amplitud y duración, pero su **posición en el tiempo** cambia según la señal analógica.

- Cada valor de la señal se representa desplazando el pulso dentro de su ventana temporal.


### 📦 Uso típico:

- Comunicaciones ópticas.

- Infrarrojos (ej. controles remotos).

- Es más **resistente al ruido en amplitud**.


---

### 4. **PCM – Pulse Code Modulation**

> Modulación por código de pulsos.

- Transforma una señal analógica en una **secuencia de palabras binarias** (digital puramente).

- La señal analógica es:
    1. **Muestreada** (según Nyquist),
        
    2. **Cuantificada** (discretización de valores),
        
    3. **Codificada** (en binario).
    

Fórmula para el número de bits por muestra:
$$\text{Bits por muestra} = \log_2(N)$$

Donde $N$ es el número de niveles de cuantificación.

### 📦 Uso típico:

- Telefonía digital (Ej: G.711)

- CD de audio

- Transmisión digital en redes


---

### 5. **Delta Modulation**

> Variante simplificada de PCM.

Variante de PCM más simple: en lugar de codificar el valor completo de cada muestra, codifica si **sube o baja** respecto a la anterior.

- Genera una secuencia de bits (1 = sube, 0 = baja).
    
- Más eficiente en términos de ancho de banda.
    
- Puede sufrir **sobrecarga** si la señal varía rápido.
    

### 📦 Uso típico:

- Voz digital en sistemas de bajo ancho de banda.
    
- Codificadores de audio con baja complejidad.

- En lugar de enviar el valor completo de cada muestra, se envía **si sube o baja respecto a la anterior**.
    
- Requiere menos bits.
    
- Más eficiente, pero **sensible a variaciones rápidas**.

- - -

|Técnica|Parámetro modulado|Señal moduladora|Tipo de codificación|
|---|---|---|---|
|**PAM**|Amplitud del pulso|Analógica|Pulsos analógicos|
|**PDM**|Duración del pulso|Analógica|Pulsos analógicos|
|**PPM**|Posición del pulso|Analógica|Pulsos analógicos|
|**PCM**|Código binario completo|Analógica|Digital puro|
|**Delta**|Diferencia entre muestras|Analógica|Digital binario (1/0)|
