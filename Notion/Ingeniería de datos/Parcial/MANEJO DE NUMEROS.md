- **ABS(numero)**:
    - **Explicación**: Devuelve el valor absoluto (número sin signo) de una expresión numérica.
    - **Ejemplo**:
        ```sql
        SELECT ABS(-15.75) AS ValorAbsoluto;
        -- Resultado: 15.75
        ```
        
- **ROUND(numero, decimales `[, operacion]`)**:
    - **Explicación**: Redondea una expresión numérica al número de decimales especificado. El tercer parámetro opcional (`0` para truncar, `1` para redondear) es poco usado; el valor por defecto es redondear.
    - **Ejemplo**:
        ```sql
        SELECT ROUND(123.456, 2) AS Redondeo;    -- Redondea a 2 decimales
        -- Resultado: 123.46
        
        SELECT ROUND(123.456, 0) AS RedondeoSinDecimales; -- Redondea al entero más cercano
        -- Resultado: 123.00
        
        SELECT ROUND(123.456, -1) AS RedondeoDecena; -- Redondea a la decena más cercana
        -- Resultado: 120.00
        ```
        
- **CEILING(numero)**:
    - **Explicación**: Devuelve el entero más pequeño que es mayor o igual que el número dado (redondea hacia arriba).
    - **Ejemplo**:
        ```sql
        SELECT CEILING(123.45) AS EnteroArriba;
        -- Resultado: 124
        
        SELECT CEILING(-123.45) AS EnteroArribaNegativo;
        -- Resultado: -123
        ```
        
- **FLOOR(numero)**:
    - **Explicación**: Devuelve el entero más grande que es menor o igual que el número dado (redondea hacia abajo).
    - **Ejemplo**:
        ```sql
        SELECT FLOOR(123.99) AS EnteroAbajo;
        -- Resultado: 123
        
        SELECT FLOOR(-123.01) AS EnteroAbajoNegativo;
        -- Resultado: -124
        ```
        
- **POWER(base, exponente)**:
    - **Explicación**: Devuelve el valor de una expresión elevado a la potencia de otra expresión.
    - **Ejemplo**:
        ```sql
        SELECT POWER(2, 3) AS DosAlCubo;
        -- Resultado: 8.0
        ```
        
- **SQRT(numero)**:
    - **Explicación**: Devuelve la raíz cuadrada de una expresión numérica. El número debe ser no negativo.
    - **Ejemplo**:
        ```sql
        SELECT SQRT(25) AS RaizCuadrada;
        -- Resultado: 5.0
        ```
        
- **SIGN(numero)**:
    - **Explicación**: Devuelve el signo de un número: `+1` si es positivo, `-1` si es negativo, `0` si es cero.
    - **Ejemplo**:
        ```sql
        SELECT SIGN(100) AS SignoPositivo, SIGN(-50) AS SignoNegativo, SIGN(0) AS SignoCero;
        -- Resultado: 1, -1, 0
        ```
        
- **RAND( `[semilla]`)**:
    - **Explicación**: Devuelve un valor `FLOAT` pseudoaleatorio de 0 a 1 (exclusivo). Una semilla opcional permite generar una secuencia repetible.
    - **Ejemplo**:
        ```sql
        SELECT RAND() AS NumeroAleatorio;       -- Cada ejecución dará un valor diferente
        -- Resultado: 0.123456789 (ejemplo)
        
        SELECT RAND(123) AS NumeroAleatorioFijo; -- Siempre dará el mismo valor para la misma semilla
        -- Resultado: 0.702758253723326
        ```
        
- **LOG(numero `[, base]`)**:
    - **Explicación**: Devuelve el logaritmo natural de un número (base e) o el logaritmo de un número en una base especificada.
    - **Ejemplo**:
        ```sql
        SELECT LOG(10) AS LogaritmoNatural;
        -- Resultado: 2.302585092994046
        
        SELECT LOG(100, 10) AS LogaritmoBase10;
        -- Resultado: 2.0
        ```
        
- **LOG10(numero)**:
    - **Explicación**: Devuelve el logaritmo en base 10 de una expresión `FLOAT`.
    - **Ejemplo**:
        ```sql
        SELECT LOG10(1000) AS Logaritmo1000;
        -- Resultado: 3.0
        ```
        
- **SUM(expresion) (Función de Agregación)**:
    - **Explicación**: Calcula la suma de todos los valores de una expresión numérica dentro de un grupo (o de todas las filas si no hay `GROUP BY`).
    - **Ejemplo**:    
        ```sql
        -- Suponiendo una tabla Ventas con columna Monto
        SELECT SUM(Monto) AS TotalVentas FROM Ventas;
        -- Resultado: Suma de todos los montos
        ```
        
- **AVG(expresion) (Función de Agregación)**:
    - **Explicación**: Calcula el promedio de todos los valores de una expresión numérica.
    - **Ejemplo**:
        ```sql
        SELECT AVG(Calificacion) AS PromedioCalificaciones FROM Evaluaciones;
        -- Resultado: Promedio de las calificaciones
        ```
        
- **MIN(expresion) / MAX(expresion) (Funciones de Agregación)**:
    - **Explicación**: Devuelven el valor mínimo/máximo de una expresión en un grupo.
    - **Ejemplo**:
        ```sql
        SELECT MIN(Precio) AS PrecioMasBajo, MAX(Precio) AS PrecioMasAlto FROM Productos;
        -- Resultado: El precio más bajo y el más alto
        ```
        
- **ISNUMERIC(expresion)**:
    - **Explicación**: Devuelve 1 si la expresión es un tipo numérico válido; de lo contrario, devuelve 0. **Advertencia**: Puede devolver 1 para algunos formatos de moneda o símbolos que no son numéricos puros (ej. `'$100'`, `'-'`). Para validación estricta, `TRY_CAST` o `TRY_CONVERT` son mejores.
    - **Ejemplo**:
        ```sql
        SELECT ISNUMERIC('123'), ISNUMERIC('abc'), ISNUMERIC('$10.50');
        -- Resultado: 1, 0, 1 (cuidado con '$10.50')
        ```