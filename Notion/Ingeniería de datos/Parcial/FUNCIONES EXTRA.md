- **COALESCE(expresion1, expresion2, ..., expresionN)**:
    - **Explicación**: Evalúa las expresiones en orden y devuelve la primera que no sea `NULL`. Es útil para proporcionar valores predeterminados o de respaldo cuando un valor es `NULL`.
    - **Ejemplo**:
        ```sql
        -- Si Descripcion es NULL, usa 'Sin Descripción'; si no, usa Descripcion.
        SELECT COALESCE(Descripcion, 'Sin Descripción') AS DescripcionFinal
        FROM Productos;
        
        -- Busca el primer número de teléfono disponible (casa, trabajo, móvil)
        SELECT COALESCE(TelefonoCasa, TelefonoTrabajo, TelefonoMovil, 'No Contacto') AS ContactoPrincipal
        FROM Clientes;
        ```
        
- **ISNULL(expresion, valor_reemplazo)**:
    - **Explicación**: Reemplaza un valor `NULL` con el `valor_reemplazo` especificado. Es similar a `COALESCE` pero solo toma dos argumentos y el tipo de dato de retorno se determina por el tipo de `expresion` (puede haber conversión implícita).
    - **Ejemplo**:
        ```sql
        -- Si Precio es NULL, usa 0.00; si no, usa Precio.
        SELECT ISNULL(Precio, 0.00) AS PrecioConCero
        FROM Productos;
        
        -- Conteo de elementos, donde NULLs no cuentan
        SELECT COUNT(ISNULL(Cantidad, 0)) FROM Ordenes; -- Cuenta filas donde Cantidad NO es NULL
        ```