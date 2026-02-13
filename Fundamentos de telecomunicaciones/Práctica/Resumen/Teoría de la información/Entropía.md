La **entropía $H$** es una medida del **contenido promedio de información** por símbolo emitido por una fuente. Fue introducida por Claude Shannon, y se calcula así para una fuente discreta:

$$
H = - \sum^{n}_{i=1} p_i * log_2(p_i)
$$
donde:
- $p_i$​ es la probabilidad de ocurrencia del símbolo $i$ y $0≤p_i​≤1$ para todo $i$
  
- El logaritmo es en base 2 porque la unidad es el **bit**
  
- Se asume que $0*log(0)=0$ por convención matemática
  

### Ejemplo 

Una **fuente binaria** emite dos símbolos posibles (por ejemplo: 0 y 1). Entonces su entropía se expresa:

$$
H(p) = −p* log_2(p) −(1−p)* log_2(1−p)
$$

donde $p$ es la probabilidad de un símbolo (el otro tiene probabilidad $1−p$ ).

- - -
## 📉 ¿Cuándo es mínima la entropía?

La entropía **se minimiza cuando la fuente es completamente predecible**, es decir:

- Cuando $p=1$ y $1−p=0$, o
- Cuando $p=0$ y $1−p=1$

Entonces:

$$H=−1⋅log_2(1)−0⋅log_2(0)=0$$

👉 **No hay incertidumbre**, porque siempre se emite el mismo símbolo.

---

## 📈 ¿Cuándo es máxima la entropía?

La entropía binaria es máxima cuando p=0.5p = 0.5p=0.5. En ese caso:

$$H=−0.5 * log_2(0.5)−0.5*log_2(0.5)=1 bit/símbolo$$

Porque hay **máxima incertidumbre**: ambos símbolos son igual de probables.

---

## 🧠 Entonces, ¿qué necesitás recordar?

1. La **entropía mide la incertidumbre promedio**.
   
2. Si uno de los mensajes tiene **probabilidad 0**, entonces **no aporta información**.
   
3. La entropía es **mínima (cero)** cuando un símbolo tiene probabilidad 1 y el otro 0.

- - -
### 🧠 Idea clave:

- **Entropía mínima:** distribución totalmente sesgada → un símbolo con probabilidad 1, los demás 0.
  
- **Entropía máxima:** distribución totalmente uniforme → todos los símbolos tienen igual probabilidad.