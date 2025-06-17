
- **GETDATE()**:
    - **Explicación**: Devuelve la fecha y hora actuales del sistema operativo del servidor en formato `DATETIME` (hora local).
    - **Ejemplo**:
        ```sql
        SELECT GETDATE() AS FechaHoraActual;
        -- Resultado: 2025-06-16 16:45:30.123 (hora de tu servidor)
        ```
        
- **SYSDATETIME()**:
    - **Explicación**: Devuelve la fecha y hora actuales del sistema operativo del servidor en formato `DATETIME2` con mayor precisión.
    - **Ejemplo**:
        ```sql
        SELECT SYSDATETIME() AS FechaHoraActualPrecisa;
        -- Resultado: 2025-06-16 16:45:30.1234567 (hora de tu servidor)
        ```
        
- **GETUTCDATE()**:
    - **Explicación**: Devuelve la fecha y hora actuales del sistema operativo del servidor en formato `DATETIME` (hora universal coordinada - UTC).
    - **Ejemplo**:
        ```sql
        SELECT GETUTCDATE() AS FechaHoraUTC;
        -- Resultado: 2025-06-16 19:45:30.123 (UTC, si tu servidor es -03:00)
        ```
        
- **SYSUTCDATETIME()**:
    - **Explicación**: Devuelve la fecha y hora actuales del sistema operativo del servidor en formato `DATETIME2` (UTC, con mayor precisión).
    - **Ejemplo**:
        ```sql
        SELECT SYSUTCDATETIME() AS FechaHoraPrecisaUTC;
        -- Resultado: 2025-06-16 19:45:30.1234567 (UTC, si tu servidor es -03:00)
        ```
        
- **DATEPART(intervalo, fecha)**:
    - **Explicación**: Extrae una parte específica de una fecha como un número entero.
    - **Intervalos comunes**: `year`, `month`, `day`, `hour`, `minute`, `second`, `millisecond`, `week`, `weekday`, `quarter`, `dayofyear`.
    - **Ejemplo**:
        ```sql
        SELECT DATEPART(year, '2024-12-25') AS Anio,
               DATEPART(month, '2024-12-25') AS Mes,
               DATEPART(day, '2024-12-25') AS Dia;
        -- Resultado: Anio=2024, Mes=12, Dia=25
        ```
        
- **YEAR(fecha)` / `MONTH(fecha)` / `DAY(fecha)**:
    - **Explicación**: Funciones abreviadas para extraer el año, mes o día de una fecha. Son equivalentes a `DATEPART(year, fecha)`, `DATEPART(month, fecha)` y `DATEPART(day, fecha)`.
    - **Ejemplo**:
        ```sql
        SELECT YEAR(GETDATE()) AS AnioActual,
               MONTH(GETDATE()) AS MesActual,
               DAY(GETDATE()) AS DiaActual;
        -- Resultado: 2025, 6, 16
        ```
        
- **DATEADD(intervalo, numero, fecha)**:    
    - **Explicación**: Suma (o resta si `numero` es negativo) un número especificado de unidades a una fecha.
    - **Ejemplo**:
        ```sql
        SELECT DATEADD(day, 7, GETDATE()) AS SemanaDespues;
        -- Resultado: La fecha actual más 7 días
        
        SELECT DATEADD(month, -1, '2025-03-15') AS MesAnterior;
        -- Resultado: 2025-02-15 00:00:00.000
        ```
        
- **DATEDIFF(intervalo, fecha_inicio, fecha_fin)**:
    - **Explicación**: Calcula la diferencia entre dos fechas en el `intervalo` especificado. Solo cuenta los "cruces" de límites del intervalo.
    - **Ejemplo**:
        ```sql
        SELECT DATEDIFF(day, '2025-06-01', '2025-06-16') AS DiasEntreFechas;
        -- Resultado: 15
        
        SELECT DATEDIFF(year, '1990-12-31', '1991-01-01') AS DiferenciaAnios;
        -- Resultado: 1 (aunque solo hay 1 día de diferencia real)
        ```
        
- **DATENAME(intervalo, fecha)**:
    - **Explicación**: Devuelve el nombre de la parte de fecha especificada (ej. nombre del mes, nombre del día de la semana) como una cadena de caracteres. La cultura del servidor puede afectar el resultado.
    - **Ejemplo**:
        ```sql
        SELECT DATENAME(month, GETDATE()) AS NombreMes;
        -- Resultado: 'June' (o 'Junio', según configuración de idioma)
        
        SELECT DATENAME(weekday, '2025-06-16') AS NombreDiaSemana;
        -- Resultado: 'Monday' (o 'Lunes')
        ```
        
- **EOMONTH(fecha `[, meses_a_sumar]`)**:
    - **Explicación**: Devuelve el último día del mes de la fecha especificada. Un segundo parámetro opcional permite calcular el fin de mes para un mes futuro o pasado.
    - **Ejemplo**:
        ```sql
        SELECT EOMONTH(GETDATE()) AS FinDeMesActual;
        -- Resultado: 2025-06-30
        
        SELECT EOMONTH('2025-01-15', 1) AS FinDeFebrero;
        -- Resultado: 2025-02-28 (o 29 si es bisiesto)
        ```
        
- **DATEFROMPARTS(año, mes, día)**:
    - **Explicación**: Construye un valor `DATE` a partir de valores numéricos de año, mes y día. Si los valores son inválidos (ej. mes 13, día 32), devuelve un error.
    - **Ejemplo**:
        ```sql
        SELECT DATEFROMPARTS(2025, 12, 25) AS Navidad2025;
        -- Resultado: 2025-12-25
        ```
        
- **DATETIMEFROMPARTS(año, mes, día, hora, minuto, segundo, milisegundo)**:
    - **Explicación**: Construye un valor `DATETIME` a partir de sus componentes numéricos. (Existen funciones similares para `DATETIME2FROMPARTS`, `TIMEFROMPARTS`, etc.).
    - **Ejemplo**:
        ```sql
        SELECT DATETIMEFROMPARTS(2025, 1, 1, 9, 0, 0, 0) AS DiaDeAnioNuevo;
        -- Resultado: 2025-01-01 09:00:00.000
        ```
        
- **ISDATE(expresion)**:
    - **Explicación**: Devuelve 1 si la expresión puede ser convertida a un tipo de fecha/hora (`DATE`, `DATETIME`, `SMALLDATETIME`); de lo contrario, devuelve 0. No es tan robusto como `TRY_CONVERT`.
    - **Ejemplo**:
        ```sql
        SELECT ISDATE('2025-12-31') AS EsFecha, ISDATE('FechaInvalida') AS NoEsFecha;
        -- Resultado: 1, 0
        ```
        
- **CAST(expresion AS TipoDatoFecha)**:
    - **Explicación**: Convierte una expresión (ej. una cadena de caracteres o un número) a un tipo de dato de fecha/hora.
    - **Ejemplo**:
        ```sql
        SELECT CAST('2025-06-16 10:00:00' AS DATETIME2) AS StringADatetime2;
        -- Resultado: 2025-06-16 10:00:00.0000000
        ```
        
- **CONVERT(TipoDatoFecha, expresion, `[estilo]`)**:
    - **Explicación**: Convierte una expresión a un tipo de dato de fecha/hora. Ofrece un parámetro `estilo` opcional que es crucial para interpretar cadenas de fecha en formatos específicos.
    - **Estilos comunes (para strings a fecha/hora)**:
        - `101`: `mm/dd/yyyy`
        - `103`: `dd/mm/yyyy`
        - `120`: `yyyy-mm-dd hh:mi:ss` (ODBC canonical)
        - `121`: `yyyy-mm-dd hh:mi:ss.mmm` (ODBC canonical con milisegundos)
    - **Ejemplo**:                                  
        ```sql
        SELECT CONVERT(DATE, '16/06/2025', 103) AS FechaDesdeStringDDMMYYYY;
        -- Resultado: 2025-06-16
        
        SELECT CONVERT(VARCHAR(20), GETDATE(), 120) AS FechaHoraAStringFormatoSQL;
        -- Resultado: '2025-06-16 16:45:30' (aproximadamente)
        ```
        
- **TRY_CAST(expresion AS TipoDatoFecha) / TRY_CONVERT(TipoDatoFecha, expresion, `[estilo]`)**:
    - **Explicación**: Intentan una conversión de forma segura. Si la conversión falla (ej. cadena inválida para una fecha), devuelven `NULL` en lugar de un error. **Extremadamente útil para la limpieza de datos y la robustez del código.**
    - **Ejemplo**:
        ```sql
        SELECT TRY_CONVERT(DATE, '30/02/2025', 103) AS FechaImposible;
        -- Resultado: NULL (2025 no tiene 30 de febrero, no lanza error)
        
        SELECT TRY_CAST('texto' AS DATE) AS StringInvalido;
        -- Resultado: NULL
        ```