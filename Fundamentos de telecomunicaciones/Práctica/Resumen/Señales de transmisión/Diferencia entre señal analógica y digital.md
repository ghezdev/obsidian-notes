## 🔊 ¿Qué es una señal?

Una **señal** es una función matemática que **transporta información** en función del tiempo (aunque puede depender de otras variables, como el espacio).

Formalmente:
$$s(t): \mathbb{R} \rightarrow \mathbb{R} \text{ o } \mathbb{C}$$

En telecomunicaciones, las señales representan **datos**, como audio, video, texto, etc.

---

## 🧮 Clasificación: Analógicas vs Digitales

### 1. 📈 Señales Analógicas

- **Valores posibles**: **Infinitos** dentro de un rango.
  
- **Dominio temporal**: **Continuo**.
  
- **Ejemplo**: una onda de audio (voz humana, música).
  
- **Representación**: curva suave y continua.
  

🔁 Varía de forma **suave** y puede tomar **infinitos valores intermedios** entre dos puntos.

#### Ejemplo visual:

Una sinusoide:
$$s(t) = A \cdot \sin(2\pi f t + \phi)$$
![[Pasted image 20250730202044.png]]

---

### 2. 🧲 Señales Digitales

- **Valores posibles**: **Discretos** (normalmente dos: 0 y 1).
  
- **Dominio temporal**: Puede ser **discreto o continuo**.
  
- **Ejemplo**: datos binarios transmitidos por una red.
  
- **Representación**: escalonada, como una secuencia de pulsos.
  

🔁 Toman **un número finito de valores**, usualmente codificados como bits.

---

## ⚖️ Comparación clave

|Característica|Señal Analógica|Señal Digital|
|---|---|---|
|Valores posibles|Infinitos|Finito (ej. 0 y 1)|
|Precisión|Alta (teóricamente infinita)|Limitada (por cuantificación)|
|Ruido|Muy sensible|Más resistente|
|Ejemplo físico|Voz, temperatura, luz|Computadora, red, microcontrolador|
|Transmisión|Modulación AM/FM|Codificación digital (PCM, ASK, etc.)|
|Procesamiento|Circuitos analógicos|Lógica binaria, microchips|

---

## 🧠 ¿Por qué preferimos señales digitales hoy en día?

Aunque las señales analógicas son **naturales** (nuestra voz, imágenes, etc.), las señales digitales:

- Son **más resistentes al ruido**.
  
- Son **más fáciles de procesar y almacenar**.
  
- Permiten **compresión y encriptación**.
  
- Se transmiten mejor por **canales digitales** (como fibra óptica o redes IP).
  

👉 Por eso, **muchas señales analógicas se digitalizan** antes de transmitirlas (por ejemplo: telefonía, música, video en streaming).