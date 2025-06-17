# Stores Procedures 

- Son bloques de código almacenado en la BD
- Existen 2 tipos de procedimientos almacenados:
	- Procedures
	- Functions 
- Se almacenan en el catálogo 
	- sys.objects
	- sys.procedures
	- sys.parameters 
	- sys.sql_modules 


# Procedures 

![[Pasted image 20250520185202.png]]

![[Pasted image 20250520185213.png]]

> [!warning] Cuidado
> No se pueden usar desde de un SELECT y puede usar INSERT, UPDATE, DELETE

# Functions

![[Pasted image 20250520185334.png]]

![[Pasted image 20250520185230.png]]


> [!NOTE] Nota
> Se pueden ejecutar funciones desde un SELECT. No puede incluir INSERT, UPDATE, DELETE


La diferencia entre ámbas es dónde se puede usar y qué puede ejecutar.

# TSql - Variables

![[Pasted image 20250520185647.png]]


# TSql - Operadores 

![[Pasted image 20250520185751.png]]


# TSql - Sentencias de control 

![[Pasted image 20250520185819.png]]

![[Pasted image 20250520190324.png]]

![[Pasted image 20250520190448.png]]

![[Pasted image 20250520190525.png]]

![[Pasted image 20250520190537.png]]

![[Pasted image 20250520190620.png]]


# TSql - Asignación de columnas 

![[Pasted image 20250520191223.png]]


# TSql - Cursores 

- Lee un conjunto de filas y las recorre en forma secuencial
- Se utilizan para realizar procesos sobre las filas leídas
- Debe ser declarado como tipo

![[Pasted image 20250520191327.png]]

> [!NOTE] Nota
> Solo vamos a usar las cláusulas que están en azul


![[Pasted image 20250520191435.png]]

![[Pasted image 20250520191615.png]]



# TSql - Transacciones

![[Pasted image 20250520192214.png]]



# TSql - Excepciones

![[Pasted image 20250520192246.png]]



# TSql - Errores

![[Pasted image 20250520192303.png]]

![[Pasted image 20250520192914.png]]

![[Pasted image 20250520192925.png]]


# Triggers 

Es un objeto de BD compuesto por código que se ejecuta automática ante ciertos eventos

- Forman parte de la misma transacción que disparó el trigger 
- Los triggers de DMLs están asociados a tablas o vistas
- Se almacenan en las tablas del catálogo

![[Pasted image 20250520194128.png]]

Eventos:
- ==DML: Insert, Delete, Update== 
- DDL: Create, Alter, Drop, Grant, Revoke 
- Sistema: Logon, Logoff, Startup, Shutdown

Además del evento y el objeto, se define el momento de ejecución del trigger 

Momentos:
- Before (en SQL Server no existe)
- Instead of *En vez de ejecutar x, ejecutá y*
- After

![[Pasted image 20250520194429.png]]

![[Pasted image 20250520194525.png]]

![[Pasted image 20250520194535.png]]


==**ESTUDIAR VISTAS Y SUS RESTRICCIONES**==


Cuando una vista está formada por joins, no le podemos hacer un insert, update, delete.
Lo mismo si la vista tiene group by o funciones agrupadas.
Pero con los triggers, podemos hacerlo. Podemos hacer un trigger para vistas.


# Trigger - Pseudotablas 

- Pertenecen a Sql Server 
- Son tablas que se generan automáticamente cuando usamos triggers 
- Nos permiten identificar las filas que están involucradas en las opreaciones
- TIenen el mismo formato de la tabla / VIew base 
- Se generan según las operaciones 

![[Pasted image 20250520200327.png]]


![[Pasted image 20250520200337.png]]

![[Pasted image 20250520200348.png]]

