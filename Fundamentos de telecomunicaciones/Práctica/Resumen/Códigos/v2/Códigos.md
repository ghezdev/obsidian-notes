## 🔠 ¿Qué es un código?

Tu resumen define:

> _"Conjunto de reglas para representar símbolos o mensajes por medio de otros símbolos."_

En telecomunicaciones, un **código** es un sistema para representar información (como letras, números, señales) en un **formato binario** o digital que sea **transmisible** y/o **procesable**.

Ejemplos cotidianos:

- ASCII (letras a bits)
    
- Morse (letras a puntos y rayas)
    
- Binario (números o símbolos a 0s y 1s)
    

---

## 🎯 ¿Por qué usamos códigos?

Tu resumen destaca dos funciones principales:

1. **Representación**: transformar datos a símbolos binarios.
    
2. **Protección**: detectar y/o corregir errores que ocurren durante la transmisión.
    

---

## 🧠 Propiedades deseables de un código

En el diseño y análisis de códigos, buscamos ciertas **propiedades clave** que garanticen eficiencia y confiabilidad:

- **No ambiguo**: Cada secuencia codificada debe representar **únicamente** un símbolo.
    
- **Único**: No debe haber dos símbolos distintos con el mismo código.
    
- **Eficiente**: Que use la menor cantidad posible de bits promedio.
    
- **Fácil de decodificar**: Que permita identificar rápidamente los límites de cada código.
    

---

## 🗂️ Clasificación de los códigos (según tu resumen)

Tu resumen incluye una **clasificación muy clara** en dos grandes ramas:

### 🔹 **1. Códigos sin detección de errores**

> Usados solo para **representar información**.

Ejemplos:

- **Binario natural**: representación directa de números.
    
- **BCD (Decimal codificado en binario)**: cada dígito decimal se representa con 4 bits.
    
- **Gray**: entre dos números consecutivos solo cambia **1 bit** → útil en electrónica digital.
    
- **ASCII**: para letras, números y símbolos del teclado.
    

---

### 🔸 **2. Códigos con detección y corrección de errores**

> Además de representar, están diseñados para **detectar o corregir errores** de transmisión.

Se dividen en:

- **Códigos de detección**:
    
    - **Paridad**: bit extra para asegurar que el número total de 1s sea par/impar.
        
    - **VRC (Vertical Redundancy Check)**, **LRC (Longitudinal Redundancy Check)**.
        
    - **Checksum**.
        
- **Códigos de corrección**:
    
    - **Hamming**: permite detectar y corregir **1 bit** de error.
        
    - **Códigos CRC (Cyclic Redundancy Check)**: muy usados en redes (Ethernet, USB).
        

---

### 📌 Tabla resumen de clasificación (según tu documento)

| Tipo de Código            | Función principal           | Ejemplos                  |
| ------------------------- | --------------------------- | ------------------------- |
| Sin detección de errores  | Representación pura         | Binario, BCD, ASCII, Gray |
| Con detección de errores  | Detectar errores            | Paridad, VRC, LRC         |
| Con corrección de errores | Detectar y corregir errores | Hamming, CRC              |
