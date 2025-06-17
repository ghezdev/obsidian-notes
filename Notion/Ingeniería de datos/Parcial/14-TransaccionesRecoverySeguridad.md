### **1. Transacciones**

Una **transacción** es una secuencia de una o más operaciones lógicas de base de datos que se tratan como una **única unidad atómica de trabajo**. El propósito principal de una transacción es garantizar la **integridad y consistencia de los datos**, especialmente cuando múltiples usuarios o procesos interactúan con la base de datos simultáneamente.

La característica fundamental es su naturaleza de "todo o nada": o todas las operaciones dentro de una transacción se completan con éxito y sus cambios se guardan permanentemente (`COMMIT`), o ninguna de ellas lo hace y todos los cambios se deshacen (`ROLLBACK`), dejando la base de datos en su estado original.

**Comandos Clave:**

- **`BEGIN TRANSACTION` (o `BEGIN TRAN`)**: Marca el inicio de una transacción explícita.
- **`COMMIT TRANSACTION` (o `COMMIT TRAN`)**: Guarda permanentemente los cambios realizados durante la transacción.
- **`ROLLBACK TRANSACTION` (o `ROLLBACK TRAN`)**: Deshace todos los cambios realizados desde el `BEGIN TRANSACTION`.

**Ejemplo: Transferencia de Fondos**

Imagina una tabla `CuentasBancarias (IDCuenta INT, Saldo DECIMAL)`. Si transfieres $100 de la Cuenta A a la Cuenta B, necesitas dos operaciones:

1. Restar $100 de la Cuenta A.
2. Sumar $100 a la Cuenta B.

Si solo se hace el paso 1 y el sistema falla antes del paso 2, el dinero "desaparecería". Una transacción garantiza que esto no ocurra.

```sql
-- Tabla de ejemplo
CREATE TABLE CuentasBancarias (
    IDCuenta INT PRIMARY KEY,
    Saldo DECIMAL(18, 2)
);
INSERT INTO CuentasBancarias VALUES (1, 1000.00), (2, 500.00);

-- Mostrar saldos iniciales
PRINT 'Saldos iniciales:';
SELECT * FROM CuentasBancarias;

BEGIN TRANSACTION; -- Inicia la transacción

BEGIN TRY
    -- 1. Debitar de la Cuenta 1
    UPDATE CuentasBancarias
    SET Saldo = Saldo - 100.00
    WHERE IDCuenta = 1;

    -- Simular un error (ej. saldo insuficiente, o fallo del sistema)
    -- IF (SELECT Saldo FROM CuentasBancarias WHERE IDCuenta = 1) < 0 RAISERROR('Saldo insuficiente', 16, 1);
    -- Este RAIERROR haría que el CATCH se active y se haga un ROLLBACK

    -- 2. Acreditar a la Cuenta 2
    UPDATE CuentasBancarias
    SET Saldo = Saldo + 100.00
    WHERE IDCuenta = 2;

    COMMIT TRANSACTION; -- Si todo fue bien, guarda los cambios
    PRINT 'Transferencia exitosa!';
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION; -- Si algo falló, deshace todos los cambios
    PRINT 'Transferencia fallida. Cambios revertidos.';
    PRINT 'Error: ' + ERROR_MESSAGE();
END CATCH;

-- Mostrar saldos finales
PRINT 'Saldos finales:';
SELECT * FROM CuentasBancarias;

-- Limpiar tabla
DROP TABLE CuentasBancarias;
```

---

### **2. ACID**

ACID es un acrónimo que describe cuatro propiedades clave que todo sistema de base de datos relacional debe garantizar para que las transacciones sean confiables y para mantener la integridad de los datos.

- **A - Atomicidad (Atomicity)**:
    
    - **Concepto**: Una transacción es una unidad indivisible de trabajo. O todas sus operaciones se completan (`COMMIT`) o ninguna de ellas lo hace (`ROLLBACK`). No hay estados intermedios.
    - **Ejemplo**: En la transferencia bancaria, o se debita de A y se acredita a B, o no ocurre ninguna de las dos cosas.
- **C - Consistencia (Consistency)**:
    
    - **Concepto**: Una transacción debe llevar la base de datos de un estado válido a otro estado válido. Esto significa que todas las reglas y restricciones (claves primarias, foráneas, `CHECK`s, reglas de negocio) deben ser respetadas antes y después de la transacción.
    - **Ejemplo**: Si una regla de negocio dice que el stock de un producto nunca puede ser negativo, una transacción que intente llevarlo a un valor negativo fallaría (y se revertiría), manteniendo la consistencia.
- **I - Aislamiento (Isolation)**:
    
    - **Concepto**: Las transacciones concurrentes deben ejecutarse de forma independiente, de modo que la ejecución de una transacción no interfiera con otra. Para un usuario, parecerá que cada transacción se ejecuta sola, incluso si otras se ejecutan simultáneamente.
    - **Ejemplo**: Si dos usuarios intentan actualizar el mismo registro al mismo tiempo, el aislamiento asegura que las operaciones de uno no vean los datos a medio modificar del otro hasta que la primera transacción se complete.
- **D - Durabilidad (Durability)**:
    
    - **Concepto**: Una vez que una transacción ha sido confirmada (`COMMIT`), sus cambios son **permanentes** y persistirán en la base de datos incluso en caso de fallos del sistema (ej. corte de energía, reinicio del servidor).
    - **Ejemplo**: Después de confirmar la transferencia bancaria, el saldo actualizado de las cuentas estará allí incluso si el servidor se apaga abruptamente y se reinicia. Esto se logra mediante el log de transacciones y los mecanismos de recuperación.

---

### **3. Recovery (Recuperación de Base de Datos)**

- **Qué hace**: Es el proceso de restaurar una base de datos a un estado consistente y operable después de un fallo (hardware, software, energía, errores humanos). El objetivo principal es garantizar la **Durabilidad** de las transacciones ACID.
    
- **Mecanismos Clave**:
    
    - **Log de Transacciones**: Es un registro secuencial de todos los cambios realizados en la base de datos. Cada operación (`INSERT`, `UPDATE`, `DELETE`), inicio/fin de transacción, y `COMMIT`/`ROLLBACK` se escribe primero en el log.
    - **Checkpoints**: Puntos periódicos en los que el motor de la base de datos escribe todas las páginas de datos modificadas de la memoria al disco y marca una entrada en el log. Esto reduce el tiempo necesario para la recuperación.
- **Fases de Recuperación (al iniciar el motor después de un fallo):**
    
    1. **Análisis**: Escanea el log desde el último checkpoint para identificar las transacciones activas al momento del fallo.
    2. **Re-ejecución (Redo / Rollforward)**: Aplica al archivo de datos todos los cambios de las transacciones que fueron confirmadas (`COMMIT`) pero que no habían sido escritas al disco antes del fallo. Esto lleva la base de datos a un estado donde todas las transacciones confirmadas están presentes.
    3. **Deshacer (Undo / Rollback)**: Revierte los cambios de las transacciones que estaban en progreso (no confirmadas) al momento del fallo. Esto asegura la atomicidad.

---

### **4. Transacciones - Entradas en el Log**

El log de transacciones registra cada operación de modificación de datos de forma detallada. Para cada cambio, se registra al menos lo siguiente:

- **Tipo de operación**: (Ej. INSERT, DELETE, UPDATE).
- **Identificador de la transacción**: A qué transacción pertenece esta operación.
- **Fecha y hora**: Cuándo ocurrió.
- **Información de cambio**:
    - **`INSERT`**: La fila completa que se insertó.
    - **`DELETE`**: La fila completa que se eliminó (los valores antiguos).
    - **`UPDATE`**: Los valores antiguos y los nuevos valores de las columnas modificadas.
- **LSN (Log Sequence Number)**: Un identificador único y secuencial para cada registro en el log. Los LSNs se usan para ordenar las operaciones y rastrear el progreso de la recuperación.

Este registro detallado es lo que permite el `UNDO` (con los valores antiguos) y el `REDO` (con los nuevos valores) durante la recuperación.

---

### **5. El Archivo de Log**

- **Qué es**: El archivo de log de transacciones es un archivo físico en el disco (`.ldf` en SQL Server) que almacena el log de transacciones. Es un archivo esencial para la durabilidad y recuperación.
- **Estructura Interna**: Aunque es un archivo continuo, internamente se organiza en **Virtual Log Files (VLFs)**. Cuando el log crece, se añaden más VLFs.
- **Funcionamiento**:
    1. Cada operación DML/DDL se escribe primero en el log (Write-Ahead Logging).
    2. Una vez que una transacción se confirma, sus cambios en el log se marcan como duraderos.
    3. Los datos reales (`.mdf`) se actualizan en memoria (buffer pool) y luego se escriben al disco en segundo plano (a menudo durante los checkpoints).
- **Administración**:
    - El log debe ser respaldado regularmente (especialmente en el Modelo de Recuperación Completo) para permitir su truncamiento y reutilización de espacio. Si el log no se trunca, puede crecer indefinidamente y llenar el disco.
    - El tamaño del log es crucial para el rendimiento y la capacidad de recuperación.

---

### **6. Fallas del Medio (Media Failure)**

- **Qué son**: Ocurren cuando hay un daño físico en el medio de almacenamiento (ej. disco duro) donde residen los archivos de datos (`.mdf`) o de log (`.ldf`) de la base de datos. Esto implica una **pérdida de datos persistente**.
- **Causas**: Falla de hardware (cabezales de lectura/escritura, sectores defectuosos), desastres naturales (incendio, inundación).
- **Impacto**: La base de datos se vuelve inaccesible o los datos están corruptos.
- **Estrategia de Recuperación**:
    - Requiere la **restauración de copias de seguridad**.
    - Si se usa el Modelo de Recuperación Completa, se restauran:
        1. La última copia de seguridad completa.
        2. La última copia de seguridad diferencial (si existe).
        3. Todas las copias de seguridad del log de transacciones realizadas desde la última copia de seguridad completa/diferencial hasta el punto del fallo (o hasta el último log disponible).
    - Esto permite recuperar la base de datos al estado exacto justo antes del fallo (o lo más cercano posible).

---

### **7. Fallas del Sistema (System Failure)**

- **Qué son**: Ocurren cuando hay un fallo en el software (ej. el proceso de SQL Server se bloquea, error en el sistema operativo) o un corte de energía inesperado.
- **Causas**: Bug en el software, sobrecarga del sistema, corte de energía, reinicio forzado del servidor.
- **Impacto**: Los datos que estaban solo en la memoria RAM (buffer cache) se pierden, pero los archivos en disco (`.mdf`, `.ldf`) no suelen estar dañados.
- **Estrategia de Recuperación**:
    - El proceso de recuperación es **automático** cuando el motor de SQL Server se reinicia.
    - Utiliza el **log de transacciones** para:
        - Realizar `REDO` (re-aplicar) las transacciones confirmadas que no habían sido escritas al disco.
        - Realizar `UNDO` (deshacer) las transacciones que estaban en curso (no confirmadas) al momento del fallo.
    - Esto asegura que la base de datos vuelva a un estado consistente (todas las transacciones confirmadas están y ninguna no confirmada lo está) muy rápidamente.

---

### **8. Actualización Diferida (Deferred Update)**

- **Concepto (Académico)**: En un modelo de actualización diferida "puro", las modificaciones de la base de datos se escriben **solo en el log de transacciones** inicialmente. Los cambios reales a los archivos de datos en disco se posponen hasta que la transacción se haya confirmado o hasta que se realice un checkpoint.
- **Ventajas**: Reduce las escrituras directas a los archivos de datos durante la transacción, lo que puede acelerar el procesamiento de transacciones.
- **Desventajas**: Durante la recuperación después de un fallo, si los cambios no se habían escrito al disco, se requiere más trabajo de "redo" desde el log.
- **En SQL Server**: SQL Server utiliza un modelo de **escritura anticipada (Write-Ahead Logging - WAL)** combinado con escrituras asíncronas desde el buffer pool al disco. Aunque los cambios se registran en el log de forma inmediata y síncrona (para garantizar la durabilidad del log), la escritura de las páginas de datos modificadas (dirty pages) desde el buffer pool a los archivos `.mdf` puede ser asíncrona y diferida hasta un checkpoint o hasta que la página sea expulsada de la caché.
    - Existe una característica de "durabilidad retrasada" (`DELAYED_DURABILITY`) en SQL Server que puede hacer que el `COMMIT` sea "diferido" al disco del log, pero esto es diferente del concepto académico de "actualización diferida" de datos.

---

### **9. Actualización Inmediata (Immediate Update)**

- **Concepto**: Las modificaciones de la base de datos se escriben en el log de transacciones y, adicionalmente, se escriben (o al menos se "empujan" para ser escritas) las páginas de datos modificadas **inmediatamente al disco** (o a un caché de disco con garantía de persistencia) **antes de que la transacción se confirme**.
- **Ventajas**: Reduce la cantidad de "redo" que debe hacerse durante la recuperación después de un fallo, ya que los cambios ya están en el disco.
- **Desventajas**: Puede ralentizar el tiempo de respuesta de la transacción, ya que requiere escrituras más sincrónicas a disco.
- **En SQL Server**: SQL Server, como la mayoría de los RDBMS modernos, opera bajo el principio de **Write-Ahead Logging (WAL)**, que es una forma de garantizar la durabilidad sin requerir una "actualización inmediata" estricta de las páginas de datos en el momento del `COMMIT`. El log se escribe de forma inmediata y sincrónica. Las páginas de datos se escriben desde la caché al disco de forma asíncrona, pero el log ya tiene toda la información para la recuperación.

---

### **10. Concurrencia - Problemas (Anomalías)**

La **concurrencia** se refiere a múltiples transacciones accediendo y modificando los mismos datos al mismo tiempo. Sin un control adecuado, esto puede llevar a varias anomalías o problemas de concurrencia, violando la propiedad de **Aislamiento** de ACID.

- **Lecturas Sucias (Dirty Reads)**:
    
    - **Qué es**: Una transacción lee datos que fueron modificados por otra transacción que aún no ha sido confirmada (`COMMIT`). Si la segunda transacción hace `ROLLBACK`, los datos leídos por la primera eran incorrectos (sucios).
    - **Ejemplo**: Transacción A actualiza un saldo a 0. Transacción B lo lee (lee 0). Transacción A falla y hace `ROLLBACK` (el saldo vuelve a 100). Transacción B actuó sobre datos que nunca existieron.
- **Lecturas No Repetibles (Non-Repeatable Reads)**:
    
    - **Qué es**: Una transacción lee la misma fila dos veces y obtiene valores diferentes, porque otra transacción ha modificado y confirmado esa fila entre las dos lecturas de la primera transacción.
    - **Ejemplo**: Transacción A lee el saldo de la Cuenta 1 (1000). Transacción B actualiza el saldo de la Cuenta 1 a 900 y hace `COMMIT`. Transacción A lee de nuevo el saldo de la Cuenta 1 (ahora 900).
- **Lecturas Fantasma (Phantom Reads)**:
    
    - **Qué es**: Una transacción ejecuta una consulta de rango dos veces y la segunda vez encuentra nuevas filas que no existían en la primera lectura, porque otra transacción ha insertado y confirmado esas nuevas filas dentro del rango consultado.
    - **Ejemplo**: Transacción A selecciona todos los productos con stock > 100. Transacción B inserta un nuevo producto con stock 150 y hace `COMMIT`. Transacción A repite la misma consulta y ahora ve el nuevo producto (el "fantasma").
- **Actualizaciones Perdidas (Lost Updates)**:
    
    - **Qué es**: Una transacción actualiza una fila basándose en su valor actual, pero otra transacción ya había actualizado la misma fila previamente y su cambio es sobrescrito y "perdido" por la primera transacción.
    - **Ejemplo**: Transacción A lee Stock=10. Transacción B lee Stock=10, luego actualiza a Stock=12 y hace `COMMIT`. Transacción A actualiza a Stock=15 (basado en su lectura original de 10). El cambio de B (12) se pierde.

Los **niveles de aislamiento de transacciones** de SQL Server (`READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`, `SNAPSHOT`) se utilizan para controlar qué anomalías se permiten o se previenen, equilibrando la consistencia con la concurrencia y el rendimiento.

---

### **11. Seguridad**

- **Qué es**: En el contexto de las bases de datos, la seguridad se refiere a las medidas y políticas implementadas para **proteger los datos y los recursos del sistema de base de datos** contra accesos no autorizados, modificación, destrucción o divulgación.
- **Objetivos Clave**:
    - **Confidencialidad**: Asegurar que solo los usuarios autorizados puedan ver los datos.
    - **Integridad**: Garantizar que los datos sean precisos, consistentes y no hayan sido modificados de forma no autorizada.
    - **Disponibilidad**: Asegurar que los datos y el sistema estén accesibles para los usuarios autorizados cuando sea necesario.
- **Capas de Seguridad**:
    - **Seguridad a nivel de red**: Firewalls, cifrado de tráfico.
    - **Seguridad a nivel del sistema operativo**: Permisos de archivos, gestión de usuarios.
    - **Seguridad a nivel de motor de base de datos**: Autenticación, autorización, auditoría.
    - **Seguridad a nivel de aplicación**: Lógica de la aplicación para filtrar datos o imponer reglas.
    - **Seguridad física**: Protección del hardware del servidor.
- **Principio de Mínimo Privilegio**: Un concepto fundamental es otorgar a los usuarios (o aplicaciones) solo los permisos mínimos necesarios para realizar sus tareas.

---

### **12. Seguridad - Control de Accesos**

El **control de accesos** es el mecanismo principal para implementar la seguridad dentro de la base de datos. Se divide en dos componentes principales:

1. **Autenticación**:
    
    - **Qué es**: El proceso de **verificar la identidad** de un usuario o entidad que intenta conectarse a la base de datos. Es el "¿quién eres?".
    - **En SQL Server**:
        - **Logins**: Son las identidades a nivel del servidor. Pueden ser:
            - **Autenticación de Windows**: Se confía en la autenticación del sistema operativo (usuarios/grupos de dominio o locales).
            - **Autenticación de SQL Server**: SQL Server gestiona el nombre de usuario y la contraseña internamente.
2. **Autorización**:
    
    - **Qué es**: El proceso de **determinar qué acciones o recursos** un usuario autenticado puede acceder o realizar. Es el "¿qué puedes hacer?".
    - **En SQL Server**: Se gestiona a través de:
        - **Usuarios de Base de Datos (Database Users)**: Un login se mapea a un usuario dentro de una base de datos específica. Los permisos se otorgan a los usuarios (o roles).
        - **Roles**: Son colecciones de permisos. Pueden ser:
            - **Roles Fijos de Servidor**: Permisos predefinidos a nivel de servidor (ej. `sysadmin`, `securityadmin`).
            - **Roles Fijos de Base de Datos**: Permisos predefinidos a nivel de base de datos (ej. `db_owner`, `db_datareader`, `db_datawriter`).
            - **Roles de Base de Datos Definidos por el Usuario**: Puedes crear tus propios roles para agrupar permisos de forma lógica y asignarlos a usuarios.
        - **Permisos (`GRANT`, `DENY`, `REVOKE`)**:
            - **`GRANT`**: Otorga permisos específicos (ej. `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `EXECUTE`) a un usuario o rol sobre un objeto (tabla, vista, procedimiento, etc.).
            - **`DENY`**: Niega explícitamente un permiso. Un `DENY` siempre tiene prioridad sobre un `GRANT`.
            - **`REVOKE`**: Elimina un permiso que fue `GRANT`ado o `DENY`ado previamente.

**Ejemplo de Control de Acceso (Autorización):**

```sql
-- Suponiendo que el login 'MiLogin' ya existe y está autenticado.

USE MiBaseDeDatos; -- Asegúrate de estar en la base de datos correcta
GO

-- 1. Crear un usuario de base de datos a partir de un login
CREATE USER MiUsuarioDB FOR LOGIN MiLogin;
GO

-- 2. Crear un rol personalizado para "Lectores"
CREATE ROLE db_lectores;
GO

-- 3. Otorgar permisos al rol
GRANT SELECT ON CuentasBancarias TO db_lectores;
GO

-- 4. Asignar el usuario al rol
ALTER ROLE db_lectores ADD MEMBER MiUsuarioDB;
GO

-- Ahora, 'MiUsuarioDB' (y por ende 'MiLogin') solo podrá realizar SELECT en CuentasBancarias,
-- pero no INSERT, UPDATE o DELETE.

-- Si quieres negar explícitamente (tiene prioridad)
-- DENY INSERT ON CuentasBancarias TO MiUsuarioDB;
```