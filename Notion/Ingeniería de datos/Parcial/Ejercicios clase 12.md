1. **Crear un procedimiento totalCompraPr al cual se le envíe como parámetro un número de cliente “desde” y un número de cliente “hasta”. El procedimiento deberá calcular y guardar en la tabla ComprasHist el número de cliente  y el monto total comprado de cada cliente. Si el cliente ya existe, registrar en una tabla de errores el número de cliente y el mensaje de error “Cliente ya existente” y continuar con el procesamiento de los demás clientes. Devolver por pantalla un total de control que indique la cantidad de clientes leídos, la cantidad de clientes grabados y la cantidad de erróneos.**

```sql
DROP table ComprasHist;
Create table ComprasHist (
     cliente_num  int,
    total     decimal(12,2)
    );

DROP table ComprasError
Create table ComprasError (
     cliente_num  int,
    mensaje      varchar(20)
    );

ALTER procedure totalCompraPr (@clienteDde int, @clienteHta int) As
begin
--
     declare compras_c cursor local for
              select c.cliente_num, sum(precio_unit * cantidad) total
                  from clientes c join facturas f on c.cliente_num = f.cliente_num
                                  join facturas_det d on d.factura_num = f.factura_num
                    where @clienteDde <= c.cliente_num and c.cliente_num <= @clienteHta
                    group by c.cliente_num;
    --
       declare @cliente_num int, @total int
       declare @clientesTot int, @clientesOk int, @clientesError int
       --
       Set @clientesTot=0
       set @clientesOk=0
       set @clientesError= 0
       --
       OPEN compras_c
       fetch compras_c into @cliente_num, @total
       --
       while @@FETCH_STATUS = 0
       begin
         begin tran
         begin try
           set @clientesTot += 1
             if exists (select 1 from comprasHist where cliente_num = @cliente_num)
                  THROW 50001, 'Cliente repetido', 1
        insert into comprasHist (cliente_num, total)
                 values (@cliente_num, @total);
             set @clientesOk += 1
      end try
      begin catch
             if ERROR_NUMBER() != 50001
               begin
                   rollback;
                   THROW
               end
             insert into ComprasError (cliente_num, mensaje)
                    values (@cliente_num, ERROR_MESSAGE());
             set @clientesError += 1
         end catch        
         commit
      fetch compras_c into @cliente_num, @total
    end
       CLOSE compras_c
       DEALLOCATE compras_c
       print 'Total Clientes:' + cast(@clientesTot as varchar)
       print 'Cliente Ok:' + cast(@clientesOk as varchar)
       print 'Clientes error:' + cast(@clientesError as varchar)
--
end
```

- - -

2.       **Seleccionar número de cliente, nombre, monto total comprado, y número, nombre y monto total comprado de un cliente 2, y comparándolos y mostrándolos de a pares. El monto del primer cliente deberá ser mayor al del segundo. Mostrar la consulta ordenada por número de cliente y monto del segundo cliente.**

```sql
select c1.cliente_num, c1.nombre, c1.apellido, sum(d1.precio_unit * d1.cantidad) total1,
       c2.cliente_num, c2.nombre, c2.apellido, c2.total2
  from clientes c1 join facturas f1 on c1.cliente_num = f1.cliente_num
                join facturas_det d1 on d1.factura_num = f1.factura_num
             , (select c2.cliente_num, c2.nombre, c2.apellido, sum(d2.precio_unit * d2.cantidad) total2
                 from clientes c2 join facturas f2 on c2.cliente_num = f2.cliente_num
                                join facturas_det d2 on d2.factura_num = f2.factura_num
                 group by c2.cliente_num, c2.nombre, c2.apellido ) c2
 where c1.cliente_num != c2.cliente_num
 group by c1.cliente_num, c1.nombre, c1.apellido,
          c2.cliente_num, c2.nombre, c2.apellido, c2.total2
  having sum(d1.precio_unit * d1.cantidad) > c2.total2
  order by 1, total2 desc
```

- - -

3.        **Se requiere listar para la provincia de Buenos Aires el par de clientes que sean los que suman el mayor monto facturado, con el formato de salida:**

**'Nombre Provincia',  'Apellido, Nombre', 'Apellido, Nombre', 'Total Solicitado' (*0)**

 **(*0) El total solicitado contendrá la suma de los dos clientes.**

```sql
SELECT TOP 1 provincia_desc, c1.nombre+', '+c1.apellido, c2.nombre+', '+c2.apellido
             , totcli1 + totcli2 'Total'
  FROM provincias p JOIN clientes c1 ON (p.provincia_cod = c1.provincia_cod)
                    JOIN clientes c2 ON (p.provincia_cod = c2.provincia_cod)
                    JOIN (SELECT f1.cliente_num, SUM(precio_unit*cantidad) totcli1
                            FROM facturas f1 JOIN facturas_det d1
                                              ON (f1.factura_num = d1.factura_num)
                           GROUP BY f1.cliente_num) totc1 
                             ON (c1.cliente_num = totc1.cliente_num)
                    JOIN (SELECT f2.cliente_num, SUM(precio_unit*cantidad) totcli2
                            FROM facturas f2 JOIN facturas_det d2
                                              ON (f2.factura_num = d2.factura_num)
                           GROUP BY f2.cliente_num) totc2 
                             ON (c2.cliente_num = totc2.cliente_num)
WHERE c1.cliente_num > c2.cliente_num AND p.provincia_desc = 'Buenos Aires'
ORDER BY 4 DESC
```

- - -

4.

**Seleccionar los clientes de mayor monto comprador por cada provincia.**

```sql
SELECT provincia_cod, c.cliente_num, sum(precio_unit*cantidad) total
from clientes c join facturas o on c.cliente_num = o.cliente_num
                join facturas_det i on o.factura_num = i.factura_num
WHERE c.cliente_num = (SELECT top 1 c2.cliente_num
                     from clientes c2 join facturas o2 on c2.cliente_num = o2.cliente_num
                              join facturas_det i2 on o2.factura_num = i2.factura_num
                     WHERE c2.provincia_cod = c.provincia_cod
                     group by c2.cliente_num
                     order by sum(i2.precio_unit*i2.cantidad) DESC)
GROUP BY provincia_cod, c.clientE_num
ORDER by 1, 3 desc, 2
```

- - -

5.

**Crear un trigger que ante cambios (inserts, borrados, modificaciones) en las filas factura_detalle de una factura en particular, mantenga un atributo montoTOTAL con el monto correcto (p x q) en dicha factura.**

```sql
ALTER trigger mantieneTotal on facturas_det
AFTER INSERT, DELETE, UPDATE AS
begin
--
    update facturas
          set montoTotal = (select sum(d.precio_unit * d.cantidad)
                              from facturas_det d
                             where d.factura_num = f.factura_num)
         from facturas f
         where f.factura_num  in (select distinct(coalesce(i.factura_num, d.factura_num))
                                 from inserted i FULL OUTER join deleted d
                                               on i.factura_num = d.factura_num and
                                                     i.renglon = d.renglon)
--
end
```

- - -

6.

**Crear un trigger que ante compras efectuadas por los clientes, valide lo siguiente:**

**Que los fabricantes de CABA o Buenos Aires puedan vender a clientes de todo el país excepto a los de Tierra del Fuego.**

**Que los demás fabricantes de otras provincias solo puedan vender mercaderías a clientes de las mismas provincias.**

**Asuma que las operaciones son de una misma factura que puede tener varios renglones.**

```sql
ALTER  trigger controlaProvinciaVta on facturas_det
AFTER INSERT AS
begin
--
    Declare @nro_factura int, @cliente_num int, @provincia_cli char(2)
       Declare @provincia_fab char(2)
    Select distinct @provincia_cli = c.provincia_cod
      from INSERTED I JOIN facturas f ON i.factura_num = f.factura_num
                      JOIN clientes c ON c.cliente_num = f.cliente_num;
    Declare detalle_cur CURSOR LOCAL FOR
              Select f.provincia_cod
                from INSERTED I JOIN productos p ON i.producto_cod = p.producto_cod
                                JOIN fabricantes f ON f.fabricante_cod = p.fabricante_cod
    OPEN detalle_cur
       FETCH detalle_cur INTO @provincia_fab
       While @@FETCH_STATUS=0
       begin
           if @provincia_fab NOT IN ('CF', 'BA')
             begin
                 if @provincia_fab != @provincia_cli
                        THROW 50001, 'Venta invalida', 1
             end
             else
                 if @provincia_cli = 'TF'
                        THROW 50001, 'Venta invalida', 1
        --  
           FETCH detalle_cur INTO @provincia_fab
       end
       CLOSE Detalle_cur
       DEALLOCATE detalle_cur
end
```