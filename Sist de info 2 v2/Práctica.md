# 📑 **Caso de Estudio – Gimnasio “Vitalidad”** (similar al modelo de parcial)

El gimnasio **Vitalidad** quiere un sistema de gestión para modernizar sus operaciones. Actualmente, los registros de clientes, pagos y reservas de clases se hacen en papel, lo que genera confusiones y quejas de los socios.

**Objetivos del sistema:**

- Permitir a los clientes registrarse online, reservar clases y consultar disponibilidad.
    
- Permitir a los clientes pagar cuotas (efectivo, tarjeta o transferencia).
    
- Permitir a los instructores consultar la lista de alumnos inscriptos en sus clases.
    
- Permitir a los administradores generar reportes de asistencia, pagos y facturación.
    
- Integrarse con un sistema externo de pagos.
    
- Cumplir con las normativas fiscales vigentes en facturación.


Caso de uso

ID: 777
Nombre: Reservar clases 
Creado por: Guillermo Hernández 
Última actualización por: Guillermo Hernández 
Fecha Creación: 19/09/2025
Fecha Actualización: 19/09/2025
Actor: Cliente 
Descripción: El sistema debe permitir al cliente poder reservar una clase.
Precondiciones:
1 - Consultar clases disponibles a reservar 
Postcondiciones: 
1 - Reservar la clase 
2 - No mostrar más en la consulta de clases la clase reservada. 
Prioridad: Alta
Frecuencia de uso: Alta 
Flujo normal:
1 - Consultar la disponibilidad de clases 
2 - Seleccionar la clase de preferencia 
3 - Enviar al checkout de pago
4 - Pago de la cuota 
5 - Reservar la clase seleccionada y pagada
Flujo alternativo: 
1.1 - No hay clases disponibles 

4.1 - Falla en el pago de la cuota 
4.2 - Informar que lo intente en otro momento 

5.1 - Fallo en la reserva 
5.2 - Informar que lo intente en otro momento 
Excepciones: N/A
Includes: Consultar disponibilidad 
Excludes: N/A
Requerimientos funcionales: 
RF07 El sistema debe permitir reservar una clase a un cliente
Requerimientos no funcionales: RNF08 El sistema debe cambiar el estado reserva de una clase a resevado cuando se reserva la clase
Notas: