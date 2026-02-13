Modulación digital-digital - Codificación de línea

Sirve para neutralizar el ruido (codificación Manchester). Lo usan los teclados de computadoras para evitar mandarle ruido a la pc.

## 🔌 **Codificación en línea**

> _La codificación en línea consiste en representar los bits digitales mediante formas específicas de señal digital (1s y 0s), adaptadas al medio físico de transmisión._

### 🧾 Justificación técnica:

- Se utiliza cuando la **portadora es digital** (por ejemplo, una línea de transmisión de impulsos eléctricos).
    
- Su función no es modular en amplitud/frecuencia/fase, sino **codificar directamente** los bits en formas de onda eléctricas.
    
- Elige una **convención temporal** para representar los bits, y puede incorporar:
    
    - Control de **nivel DC** (evitar corriente continua acumulada)
        
    - Facilitación de la **sincronización**
        
    - **Detección de errores** (en algunos casos)
        

---

## 🧩 Tipos principales de codificación en línea

### 1. **NRZ – Non Return to Zero**

- El bit **1** se representa con un nivel alto; el **0**, con un nivel bajo (o viceversa).
    
- 🧾 Problema: largas secuencias iguales dificultan la sincronización.
    
- Variante **NRZ-I**: cambia de nivel solo cuando hay un '1'.
    

---

### 2. **RZ – Return to Zero**

- Cada bit vuelve a 0 en la mitad del intervalo.
    
- Mejora la sincronización.
    
- Requiere mayor ancho de banda.
    

---

### 3. **Manchester**

- Bit '1': transición de alto a bajo.
    
- Bit '0': transición de bajo a alto.
    
- 🧠 Ventaja: siempre hay transición → fácil sincronización.
    
- Utilizado en **Ethernet clásico (10Base-T)**.
    

---

### 4. **Differential Manchester**

- Cada bit tiene al menos una transición.
    
- La presencia o ausencia de transición al inicio del bit determina su valor.
    
- Más robusto ante inversión de polaridad del cable.
    

---

### 5. **AMI – Alternate Mark Inversion**

- '0' → nivel 0 (sin señal); '1' → alterna entre nivel positivo y negativo.
    
- Controla componente DC y facilita detección de errores.