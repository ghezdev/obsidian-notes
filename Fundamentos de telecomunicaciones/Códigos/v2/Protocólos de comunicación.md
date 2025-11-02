## 📌 1. **Protocolos orientados a carácter**

- También llamados **orientados a byte**.
    
- Usan **caracteres especiales** del código de control (ASCII u otro) para **marcar el inicio y el fin de una trama**.
    
- Ejemplos de caracteres de control:
    
    - **STX** (_Start of Text_) → inicio
        
    - **ETX** (_End of Text_) → fin
        
- La trama puede incluir otros bytes de control para direccionamiento, verificación de errores, etc.
    
- **Problema:** si el carácter especial aparece dentro de los datos, el receptor podría interpretarlo como fin de trama por error.
    
- **Solución:** usar _caracteres de escape_ para “enmascarar” los bytes especiales en los datos.
    
- **Ejemplo de protocolo:** BISYNC (Binary Synchronous Communication).

- Lo usa el teclado o la pc.

---

## 📌 2. **Protocolos orientados a bit**

- No usan caracteres especiales, sino **secuencias de bits únicas** para marcar el inicio y fin de la trama.
    
- Una secuencia típica: **01111110** (del protocolo HDLC).
    
- **Ventaja:** independencia del código de caracteres (sirve para cualquier tipo de datos binarios).
    
- **Problema:** la misma secuencia de inicio/fin podría aparecer dentro de los datos.
    
- **Solución:** _bit stuffing_ (inserción de bits de relleno).

- Lo usa internet.

- Es el protocolo que más ancho de banda aprovecha por la independencia del alfabeto, menor redundancia y detección de errores sofisticadas.

---

## 📌 3. **Inicio y fin de trama y Bits de relleno (Bit Stuffing)**

• Los datos tienen un número arbitrario de bits y admite códigos de caracteres con un número arbitrario de bits por carácter.

No es muy eficiente.

• Si el receptor pierde la pista de donde está debe explorar la entrada en busca de banderas pues estas están presentes en los límites de las tramas no en los datos.