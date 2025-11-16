---
~
---
### Práctica de la clase 3

![[Pasted image 20250829183544.png]]

**Necesidades**
- Informe de ventas 
- Control de stock 
- Registro de ventas confiables 
- Control de productos para abastecerse  y planificar compras 
- Contar con un inventario 

**Requisitos funcionales** 
- Automatizar el proceso de pedidos y gestión de stock 
- Registrar ventas 
- Controlar inventario 
- Obtener reportes confiables para la toma de decisiones 

```
- El sistema debe permitir registrar ventas de productos 
- El sistema debe actualizar el stock antes de una venta
- El sistema debe generar 1 factura por cada venta 
- El sistema debe registrar pedidos digitales 
- El sistema debe realizar reportes semanales de ventas por periodos configurables 
- El sistema debe realizar reportes semanales de pedidos por periodos configurables
```

**Requisitos no funcionales** *técnicos*
- CRUD de ventas 
- Logs de Inventario 
- Querys predefinidas para los reportes 

```
- El sistema debe tener un tiempo de respuesta de 3 segundos 
- El sistema debe tener interfaz amigable al usuario
- El sistema debe ser accesible en androind e ios  
- El sistema debe permitir acceso a usuarios autorizados 
- El sistema debe autorizar el ingreso de usuario y clave 
```

**Requisitos de dominio** _relacionado al tipo de negocio_
- Articulos 
- Ventas 
- Clientes 

```
- El sistema debe registrar el iva en la factura 
- 
```

**Requisitos de negocio**
- Aumentar las ventas
- Disminuir las pérdidas de clientes 

```
- El sistema debe mejorar las ganancias 
- El sistema debe mejorar las ventas
- El sistema debe mejorar el tiempo de respuesta hacia los clientes 
 
```

**Requisitos de diseño e implementación** _la implementacion es un técnico pero relacionado con el negocio, el diseño es literalmente diseño, colores, marcas, etc_
- Motor de base de datos 
- Base de datos 
- Integración whatsapp con la base de datos 

```
- El sistema debe integrarse con la AFIP para la facturación 
- 
```

**Requisitos de transición**
- ETL de ventas

```
- El sistema debe ser capaz de migrar los datos de un lugar a otro
```


> [!note] 
> El parcial va a ser preguntas relacionadas a las prácticas de la clase 

![[Pasted image 20250829184733.png]]

1. Incorrecto, ambiguo, el sistema debe responder en menos de 1 segundo, funcional.


- - -

# Elicitación 

**Es un proceso interactivo para comprender, descubrir, documentar y validar las necesidades reales del usuario stakeholder para un sistema de software**

entrada → proceso → salida 
necesidades de stakeholders → conjunto de actividades → requisitos del producto de software

Por donde empezar 

- **¿Para quien es el beneficio/resultado de la solución?** Todo el que reciba un impacto directo o indirecto con la existencia del producto 

- **¿Que se quiere resolver y por qué hoy no se ha solucionado?** Las soluciones de software existen para hacer realidad un estado deseado. Para eso hay que conocer el estado actual 

- **¿Por qué es importante resolverlo?** Objetivos del producto con respecto a los clientes. Los requisitos se alinearan en la dirección predefinida de los objetivos de la empresa 

## Desafíos comunes 

- Los stakeholders a veces no saben lo que quieren 
- No saben expresarlo bien 
- Pueden ser contradictorios 
- Lenguaje técnico y negocio puede diferir

### No debe comenzar con - Mejor decir 

- **¿Que es lo que quiere que haga?** - *¿Que situaciones quiere resolver, cuales son tus necesidades?*

### **Stakeholders**

- Patrocinadores
- Usuarios directos:  usan el software, 
- Usuarios indirectos: reciben un beneficio indirecto del software
- Definidores de reglas: individuos que establecen reglas de negocio 

### **DINO**

**D**eseables: requerimientos esteticos, nice to have, se hacen si se tiene el tiempo para hacerse 
**I**mportantes: requerimientos de gran valor pero que pueden esperar, se negocian por otros mas prioritarios 
**N**o implementables: requerimientos poco valor con costo alto 
**O**


**Elicitar los requisitos debe incluir y empezar con la empatía**

Puntos clave para lograr empatía 
1. **Contexto del usuario y del software.** *Comprender el entorno geografico, cultura, hardware, software*
2. **Dominio de la información.** *Entender el vocabulario, conceptos y significados que usan los usuarios* 
3. **Interacciones y actividades.** *Analizar cómo las personas se relacionan, comparten información y colaboran* 
4. **Comportamiento esperado.** *Definir cómo debe reaccionar el sistema en eventos y estímulos*


> [!note] 
> **FINAL ES ORAL**

