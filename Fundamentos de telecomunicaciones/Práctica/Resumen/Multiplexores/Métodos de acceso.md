## 📌 ¿Qué es un método de acceso?

Un **método de acceso** (o _multiple access method_) es la **forma en la que varios usuarios o dispositivos comparten un mismo medio de transmisión** (cable, fibra, enlace de radio, etc.) **de manera ordenada**, evitando interferirse entre sí.

Es decir:

- Tenemos **un recurso limitado** (el canal de comunicación).
    
- Hay **muchos que quieren usarlo** al mismo tiempo.
    
- El método de acceso define **cómo se reparte ese recurso** entre todos para que la comunicación sea posible y eficiente.
    

---

## 🎯 Objetivos de un método de acceso

- **Evitar colisiones** (que dos usuarios transmitan a la vez en la misma porción del canal).
    
- **Optimizar el uso del ancho de banda** disponible.
    
- **Garantizar calidad de servicio** (QoS) según el tipo de tráfico: voz, datos, video, etc.
    
- **Permitir escalabilidad** (soportar más usuarios sin degradar excesivamente el servicio).
    

---

## 📍 Clasificación general

Los métodos de acceso más comunes se basan en **dividir el canal compartido** de distintas formas:

1. **En el tiempo** → TDMA (_Time Division Multiple Access_).
    
2. **En códigos** → CDMA (_Code Division Multiple Access_).
    
3. **En subportadoras ortogonales** → OFDMA (_Orthogonal Frequency Division Multiple Access_).

---

💡 Diferencia clave con **multiplexación**:

- **Multiplexación** → Combina señales para enviarlas por un canal. Puede ser entre señales de un mismo usuario o de varios, no importa si hay control de acceso o no.
    
- **Método de acceso** → Reglas y técnicas **para que varios usuarios accedan** a un mismo medio compartido de forma coordinada, evitando interferencias.