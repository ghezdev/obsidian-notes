# Sentencias Dml 

Estas sentencias se utilizan para modificar (insertar, actualizar, borrar, consultar) filas de las tablas (no objetos de la BD)

## Insert 

![[Pasted image 20250513193657.png]]

## Update 

![[Pasted image 20250513193714.png]]

![[Pasted image 20250513193725.png]]


## Delete 

![[Pasted image 20250513193743.png]]


## Insert - Subqueries

![[Pasted image 20250513193844.png]]


## Update - Subqueries

![[Pasted image 20250513193859.png]]

## Delete - Subqueries

![[Pasted image 20250513193923.png]]


## Truncate 

![[Pasted image 20250513194032.png]]

- Borra **todos** los registros 
- Es más rápido que el **DELETE**
- Dependiendo del motor de BD se puede **deshacer**
- **Bloquea** toda la tabla
- No graba una entrada por cada registro borrado en los logs
- Libera espacio 
- Borra los datos pero **no la estructura**


## Create 

- Crea diferentes tipos de objetos en la BD
- Objetos: Tabla, índices, vistas, sinónimos, triggers, store, procedures, etc 

![[Pasted image 20250513194640.png]]

![[Pasted image 20250513194654.png]]

![[Pasted image 20250513194713.png]]


### Otras formas de crear una tabla (copia)

![[Pasted image 20250513194742.png]]


## Alter 

- Se utiliza para modificar objetos
- En el caso de las tablas se puede utilizar para agregar, modificar o borrar columnas y/o constraints 

![[Pasted image 20250513194837.png]]



## Drop 

- Se utiliza para borrar objetos de la BD
- Una vez borrados no se pueden recuperar

![[Pasted image 20250513194909.png]]


## Merge 

Se utiliza esencialmente para realizar procesamiento barch (migraciones, carga de datos, apareos, etc.) de tablas 

![[Pasted image 20250513195024.png]]

Pasemos a un ejemplo para entender mejor su funcionamiento y supongamos tener los siguientes requerimientos:

Dada una tabla **Fuente** y una tabla **Destino** cuyas claves primarias en ámbas es el atributo **código**:
- Si el **código** de la tabla **fuente** existe en la tabla **Destino** y las **direcciones** son diferentes entonces actualizar la dirección de la tabla **Destino**
- Si el **código** de la tabla **fuente** NO existe en la tabla **Destino** entonces insertar en la tabla **destino** el registro de la tabla **Fuente**
- Si el **código** de la tabla **Destino** NO existe en la tabla **Fuente** entonces borrar el registro de la tabla **Destino**

![[Pasted image 20250513195545.png]]

![[Pasted image 20250513195556.png]]

![[Pasted image 20250513195611.png]]

![[Pasted image 20250513195624.png]]


del 10 para atrás con subqueries


> [!NOTE] Queries correlacionadas
> Queries que se relacionan una con la otra a través de subqueries y funcionan como un loop (WHERE EXISTS para queries correlacionadas) (WHERE a IN … para subqueries)



EJ 10)

```SQL
SELECT vfd.cliente_num, vfd.nombre, vfd.apellido

FROM (

SELECT DISTINCT p.producto_cod, c.cliente_num, c.nombre, c.apellido

FROM productos p

JOIN facturas_det fd ON p.producto_cod = fd.producto_cod

JOIN facturas f ON fd.factura_num = f.factura_num

JOIN clientes c ON f.cliente_num = c.cliente_num

WHERE p.fabricante_cod = 'DOTO'

) vfd

GROUP BY vfd.cliente_num, vfd.nombre, vfd.apellido

HAVING COUNT(vfd.producto_cod) = 3
```


ej 12)

![[Pasted image 20250513215047.png]]
![[Pasted image 20250513215348.png]]

esta query no es del todo correcta ya que debería filtrarse también en la tabla de clientes join facturas join facturas det para la fecha dispuesta. 
se obtiene las facturas emitidas mayor a la fecha dada, pero no las facturas de los clientes con la fecha de emision mayor a la fecha dada