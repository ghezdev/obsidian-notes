- **`+` (Operador de Concatenación)**:
    
    - **Explicación**: Une dos o más cadenas de caracteres. Si alguna parte de la expresión es `NULL`, el resultado completo es `NULL`.
    - **Ejemplo**:
        ```sql
        SELECT 'Hola' + ' ' + 'Mundo';
        -- Resultado: 'Hola Mundo'
        
        SELECT 'Parte1' + NULL + 'Parte2';
        -- Resultado: NULL
        ```
        
- **CONCAT(cadena1, cadena2, ..., cadenan)**:
    
    - **Explicación**: Une dos o más cadenas de caracteres. A diferencia del operador `+`, `CONCAT` trata los valores `NULL` como cadenas vacías (`''`), lo que a menudo es más conveniente.
    - **Ejemplo**:        
        ```sql
        SELECT CONCAT('Nombre:', ' ', 'Juan', ' ', 'Perez');
        -- Resultado: 'Nombre: Juan Perez'
        
        SELECT CONCAT('Valor: ', NULL, ' unidades');
        -- Resultado: 'Valor:  unidades'
        ```
        
- **LEN(expresion_cadena)**:
    - **Explicación**: Devuelve el número de caracteres de la expresión de cadena especificada, excluyendo los espacios en blanco finales.
    - **Ejemplo**:
        ```sql
        SELECT LEN('  SQL Server   ');
        -- Resultado: 10 (contando 'SQL Server')
        
        SELECT LEN('Palabra');
        -- Resultado: 7
        ```
        
- **SUBSTRING(expresion, inicio, longitud)**:
    - **Explicación**: Extrae una parte de una cadena de caracteres, comenzando en una posición específica y con una longitud determinada. La posición de inicio es 1-basada.
    - **Ejemplo**:
        ```sql
        SELECT SUBSTRING('Desarrollo SQL', 5, 6);
        -- Resultado: 'rrollo' (empieza en la 5ta posición 'r', toma 6 caracteres)
        ```
        
- **LEFT(expresion_cadena, longitud)**:
    - **Explicación**: Devuelve la parte izquierda de una cadena con el número de caracteres especificado.
    - **Ejemplo**:
        ```sql
        SELECT LEFT('Código Postal', 5);
        -- Resultado: 'Código'
        ```
        
- **RIGHT(expresion_cadena, longitud)**:
    - **Explicación**: Devuelve la parte derecha de una cadena con el número de caracteres especificado.
    - **Ejemplo**:
        ```sql
        SELECT RIGHT('Nombre Completo', 8);
        -- Resultado: 'Completo'
        ```
        
- **CHARINDEX(subcadena, expresion_cadena `[, inicio]`)**:
    - **Explicación**: Devuelve la posición inicial de la primera aparición de una subcadena dentro de una cadena. La búsqueda puede comenzar desde una posición opcional.
    - **Ejemplo**:
        ```sql
        SELECT CHARINDEX('mundo', 'Hola mundo, lindo mundo');
        -- Resultado: 6 (la 'm' de la primera ocurrencia de 'mundo')
        
        SELECT CHARINDEX('mundo', 'Hola mundo, lindo mundo', 7);
        -- Resultado: 19 (la 'm' de la segunda ocurrencia de 'mundo', buscando desde pos 7)
        ```
        
- **PATINDEX('%patron%', expresion_cadena)**:
    - **Explicación**: Devuelve la posición inicial de la primera aparición de un patrón en una expresión de cadena. Permite el uso de comodines (`%`, `_`, `[]`, `[^]`) como en `LIKE`.
    - **Ejemplo**:
        ```sql
        SELECT PATINDEX('%[0-9]%', 'ABC123XYZ');
        -- Resultado: 4 (la posición del primer dígito)
        
        SELECT PATINDEX('%[^a-zA-Z]%', 'TextoSinNumeros');
        -- Resultado: 0 (no encontró ningún carácter que no sea letra)
        ```
        
- **REPLACE(expresion_cadena, cadena_a_buscar, cadena_reemplazo)**:
    - **Explicación**: Reemplaza todas las apariciones de una subcadena específica dentro de una cadena con otra cadena de reemplazo.
    - **Ejemplo**:
        ```sql
        SELECT REPLACE('www.ejemplo.com', '.com', '.org');
        -- Resultado: 'www.ejemplo.org'
        
        SELECT REPLACE('Uno, Dos, Tres, Dos', 'Dos', 'Cuatro');
        -- Resultado: 'Uno, Cuatro, Tres, Cuatro'
        ```
        
- **LTRIM(expresion_cadena)**:
    - **Explicación**: Elimina los espacios en blanco iniciales (a la izquierda) de una cadena.
    - **Ejemplo**:
        ```sql
        SELECT '(' + LTRIM('   Mi Texto') + ')';
        -- Resultado: '(Mi Texto)'
        ```
        
- **RTRIM(expresion_cadena)**:
    - **Explicación**: Elimina los espacios en blanco finales (a la derecha) de una cadena.
    - **Ejemplo**:
        ```sql
        SELECT '(' + RTRIM('Mi Texto   ') + ')';
        -- Resultado: '(Mi Texto)'
        ```
        
- **TRIM(`[caracteres_a_recortar FROM]` expresion_cadena)**:
    - **Explicación**: Elimina el carácter especificado (o espacios por defecto) de ambos extremos de una cadena. Si no se especifican `caracteres_a_recortar`, recorta espacios.
    - **Ejemplo**:
        ```sql
        SELECT TRIM('  Texto con espacios  ');
        -- Resultado: 'Texto con espacios'
        
        SELECT TRIM('._' FROM '._.Mi.Texto._.');
        -- Resultado: 'Mi.Texto'
        ```
        
- **UPPER(expresion_cadena)**:
    - **Explicación**: Convierte todos los caracteres alfabéticos de una cadena a mayúsculas.
    - **Ejemplo**:
        ```sql
        SELECT UPPER('mi nombre');
        -- Resultado: 'MI NOMBRE'
        ```
        
- **LOWER(expresion_cadena)**:
    - **Explicación**: Convierte todos los caracteres alfabéticos de una cadena a minúsculas.
    - **Ejemplo**:
        ```sql
        SELECT LOWER('Mi Nombre');
        -- Resultado: 'mi nombre'
        ```
        
- **REPLICATE(expresion_cadena, numero_de_veces)**:
    - **Explicación**: Repite una expresión de cadena un número especificado de veces.
    - **Ejemplo**:
        ```sql
        SELECT REPLICATE('X', 5);
        -- Resultado: 'XXXXX'
        
        SELECT REPLICATE('0', 3) + '123';
        -- Resultado: '000123' (útil para rellenar a la izquierda)
        ```
        
- **FORMAT(valor, formato_string, `[cultura]`)**:
    - **Explicación**: Formatea un valor de tipo numérico, fecha/hora o string con el formato y la cultura especificados. Muy flexible para la presentación.
    - **Ejemplo**:
        ```sql
        SELECT FORMAT(GETDATE(), 'yyyy-MM-dd HH:mm:ss');
        -- Resultado: '2025-06-16 16:00:00' (aproximadamente, dependiendo de la hora actual)
        
        SELECT FORMAT(12345.67, 'C', 'es-ES');
        -- Resultado: '12.345,67 €' (símbolo de moneda y separadores según la cultura)
        ```
        
- **CAST(expresion AS tipo_dato)**:
    - **Explicación**: Convierte una expresión de un tipo de dato a otro. Es una conversión genérica.
    - **Ejemplo**:
        ```sql
        SELECT CAST(12345 AS VARCHAR(10));
        -- Resultado: '12345' (string)
        
        SELECT CAST(GETDATE() AS VARCHAR(20));
        -- Resultado: 'Jun 16 2025  4:00PM' (o similar, depende del formato por defecto)
        ```
        
- **CONVERT(tipo_dato, expresion, `[estilo]`)**:
    - **Explicación**: Convierte una expresión de un tipo de dato a otro, similar a `CAST`, pero ofrece un parámetro `estilo` adicional para conversiones de fecha/hora y algunos tipos de datos especiales.
    - **Ejemplo**:
        ```sql
        SELECT CONVERT(VARCHAR(10), GETDATE(), 103);
        -- Resultado: '16/06/2025' (formato dd/mm/yyyy)
        
        SELECT CONVERT(INT, '123');
        -- Resultado: 123 (entero)
        ```

- **LIKE (Operador)**:
    - **Explicación**: Se utiliza en la cláusula `WHERE` para buscar patrones específicos en una columna de tipo cadena. Es sensible a la intercalación (collation) de la columna.
    - **Comodines (Wildcards)**:
        - `%`: Representa cero, uno o varios caracteres.
        - `_` (guion bajo): Representa un único carácter.
        - `[]`: Representa un conjunto de caracteres (ej. `[aeiou]` para cualquier vocal).
        - `[^]`: Representa cualquier carácter _que no esté_ en el conjunto.
    - **Ejemplo**:
        ```sql
        -- Buscar nombres que empiezan con 'A'
        SELECT Nombre FROM Clientes WHERE Nombre LIKE 'A%';
        
        -- Buscar nombres que tienen 'an' en cualquier posición
        SELECT Nombre FROM Clientes WHERE Nombre LIKE '%an%';
        
        -- Buscar códigos de producto que tienen 'X' como segundo carácter
        SELECT CodigoProducto FROM Productos WHERE CodigoProducto LIKE '_X%';
        
        -- Buscar palabras que empiezan con una vocal
        SELECT Palabra FROM Diccionario WHERE Palabra LIKE '[AEIOU]%';
        ```