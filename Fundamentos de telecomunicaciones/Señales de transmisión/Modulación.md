## 🔁 ¿Qué es la Modulación?

La **modulación** consiste en **modificar una señal portadora** (una onda periódica, generalmente senoidal) para que **transporte la información** que se desea transmitir.
$$\text{Señal modulada } = \text{Portadora + Información}$$

La **portadora** tiene estas características:

- Amplitud $A$
  
- Frecuencia $f$
  
- Fase $\phi$
  

La señal **informativa** modifica uno o más de estos parámetros.

---

## 🎯 ¿Por qué necesitamos modular?

1. Para **adecuar la señal al canal** (ej: onda de radio, fibra óptica, etc.).
   
2. Para **transmitir señales de baja frecuencia** por medios que requieren frecuencias altas.
   
3. Para permitir **multiplexación** (varios mensajes en el mismo canal).
   
4. Para **reducir interferencias** y aprovechar mejor el espectro.

---

## 🎛️ Tipos de Modulación

---

### 🔊 A. **Modulación Analógica** (usada para señales continuas como voz o música)

#### 1. **AM – Amplitude Modulation**

- Se **modifica la amplitud** de la portadora según la señal informativa.
  
- Frecuencia y fase se mantienen constantes.  $$s(t) = [1 + m(t)] \cdot \cos(2\pi f_c t)$$
- Sencilla pero **sensible al ruido**.


#### 2. **FM – Frequency Modulation**

- Se **modifica la frecuencia** de la portadora.
  
- Amplitud y fase constantes.$$f(t) = f_c + k \cdot m(t)$$
- **Más robusta al ruido** (por eso se usa en radio FM).
   

#### 3. **PM – Phase Modulation**

- Se **modifica la fase** de la portadora según la señal.
$$s(t) = A \cdot \cos(2\pi f_c t + k \cdot m(t))$$

---

### 💾 B. **Modulación Digital** (la señal informativa es digital, ej. bits 0 y 1)

#### 4. **ASK – Amplitude Shift Keying**

- Se transmiten bits cambiando la **amplitud** de la portadora.
    - Ej: 0 → sin señal, 1 → portadora con amplitud A.

Fácil de implementar, pero muy **sensible al ruido**.

#### 5. **FSK – Frequency Shift Keying**

- Se transmiten bits cambiando la **frecuencia**.
    - Ej: 0 → 1200 Hz, 1 → 2200 Hz.

Más robusta que ASK.

#### 6. **PSK – Phase Shift Keying**

- Se transmiten bits modificando la **fase** de la portadora.
    - Ej: 0 → fase 0°, 1 → fase 180° (BPSK).
      
    - Se puede usar más fases: QPSK (4), 8PSK, etc.

**Muy eficiente**, especialmente en condiciones ruidosas.

#### 7. **QAM – Quadrature Amplitude Modulation**

- Combina **amplitud y fase** para codificar varios bits por símbolo.

Ejemplo:
- 16-QAM: 4 bits por símbolo
  
- 64-QAM: 6 bits por símbolo
  

Usado en WiFi, DVB, 4G/5G, etc. **Alta eficiencia espectral**, pero más **sensible a ruido** si el orden es alto.

---

## 🧠 ¿Cómo elegir qué técnica usar?

Depende de:
- Nivel de **ruido** en el canal.
  
- **Ancho de banda** disponible.
  
- Velocidad de datos requerida.
  
- Potencia de transmisión disponible.