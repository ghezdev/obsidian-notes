# Algebra relacional

## Operaciones básicas

### Unión [**∪]**

Sean 2 relaciones **compatibles** A y B, la UNION entre ámbas es una relación del mismo tipo cuyo cuerpo está formado por las tuplas de A, de B o de ámbas

![[/image 7.png|image 7.png]]

  

### Intersección [∩]

Sean 2 relaciones compatibles A y B, la **intersección** entre ámbas es una relación del mismo tipo cuyo cuerpo está formada por las tuplas pertenecientes a **ámbas** relaciones

![[/image 1 4.png|image 1 4.png]]

  

### Diferencia [-]

Sean 2 relaciones **compatibles** A y B, la DIFERENCIA entre ámbas es una relación R cuyo cuerpo está formada por las tuplas pertenecientes de A pero no a B

![[/image 2 4.png|image 2 4.png]]

  

### Producto [X]

Sean 2 relaciones A y B, el **PRODUCTO** entre ámbas es una relación cuya cabecera es la combinación de las cabeceras de ámbas y cuyo cuerpo está formado por las tuplas t tales que t es la **combinación** de una tupla de A y una de B

![[/image 3 4.png|image 3 4.png]]

  

  

## Operaciones adicionales

### Restricción (Select) [σ]

Retorna una relación que contiene las tuplas de una relación que satisface una condición específica

![[/image 4 3.png|image 4 3.png]]

  

### Proyección (Project) [**π**]

Retorna una relación que contiene las tuplas que quedan en la relación después de tomar los atributos especificados

![[/image 5 2.png|image 5 2.png]]

  

### Junta (Join) [**⋈**]

- Normalmente retorna una relación con la combinación de ámbas cabeceras para aquellas tuplas cuyos atributos en común tengan valores iguales
- Normalmente la “Junta” es un **equijoin** aunque también pueden compararse con una condición diferente a la igualdad
- Subconjunto del Producto Cartesiano

![[/image 6 2.png|image 6 2.png]]

  

### Division [%]

- Sea una relación A de grado **m + n** donde A puede definirse como un conjunto de pares de valores <x,y>. Sea una relación B de grado **n**, donde B puede definirse como un conjunto de valores <y>
- Al aplicar el operador división A % B el resultado será una relación C de grado m donde C puede definirse como el conjunto de valores x tales que el par aparece en A para todos los valores “y” que aparecen en B
- Los atributos de la **relación resultado**, tienen los mismos nombres que los primeros m atributos de A

![[/image 7 2.png|image 7 2.png]]

  

  

### Propiedades del Álgebra relacional

- Se pueden anidar operaciones
- Se producen resultados intermedios
- Las operaciones se realizan sobre las relaciones
- Se cumple la propiedad de cierre o clausura

  

### Combinación de operaciones

Seleccionar los nombres de proveedores de CABA y nombre de partes aprovisionados en mas de 20 unidades

![[image 8.png]]

Otra solución

![[image 9.png]]

  

### Operadores de totales

- **SUM**: calcula totales
- **COUNT / COUNTD**: cantidades
- **MIN**: mínimos
- **MAX**: máximos
- **AVG**: promedios

  

### Uso de operadores

_Relación Operador_ (_atributo_) AS _atributo_

- **AS**: agrupa atributos

  

Seleccionar la cantidad total aprovisionada de cada parte (cantidades agrupadas por partes)

![[image 10.png]]

  

  

> [!important] Página para practicar álgebra relacional
> 
> [https://dbis-uibk.github.io/relax/calc/local/uibk/local/0](https://dbis-uibk.github.io/relax/calc/local/uibk/local/0)

  

### Ejercicios

![[image 11.png]]

![[image 12.png]]

  

- Tablas para la pagina
    
    Proveedores = {  
    vid,proveedor,status,ciudad  
    V1,Smith,20,Londres  
    V2,Jones,10,Paris  
    V3,Blake,30,Paris  
    V4,Clark,20,Londres  
    V5,Adams,30,Atenas  
    }  
    
    Proyectos = {  
    yid,proyecto,ciudad  
    Y1,Clasificador,Paris  
    Y2,Monitor,Roma  
    Y3,OCR,Atenas  
    Y4,Consola,Atenas  
    Y5,RAID,Londres  
    Y6,EDS,Oslo  
    Y7,Cinta,Londres  
    }  
    
    Partes = {  
    pid,partes,color,peso,ciudad  
    P1,Tuerca,Rojo,12.0,Londres  
    P2,Perno,Verde,17.0,Paris  
    P3,Tornillo,Azul,17.0,Roma  
    P4,Tornillo,Rojo,14.0,Londres  
    P5,Leva,Azul,12.0,Paris  
    P6,Engrane,Rojo,19.0,Londres  
    }  
    
    Vpy = {  
    vid,pid,yid,cant  
    V1,P1,Y1,200  
    V1,P1,Y4,700  
    V2,P3,Y1,400  
    V2,P3,Y3,200  
    V2,P3,Y3,200  
    V2,P3,Y4,500  
    V2,P3,Y5,600  
    V2,P3,Y6,400  
    V2,P3,Y7,800  
    V2,P5,Y1,100  
    V3,P3,Y1,200  
    V3,P4,Y2,500  
    V4,P6,Y3,300  
    V4,P6,Y7,300  
    V5,P2,Y2,200  
    V5,P2,Y4,100  
    V5,P5,Y5,500  
    V5,P5,Y7,100  
    V5,P6,Y2,200  
    V5,P1,Y4,100  
    V5,P3,Y4,200  
    V5,P4,Y4,800  
    V5,P5,Y4,400  
    V5,P6,Y4,500  
    }  
    

  

1. Proyectos
2. σciudad='Londres'(Proyectos)
3. πvid(σyid='Y1'(Vpy))
4. πvid(σpid='P3'(σyid='Y1'(Vpy)))
5. πcolor,ciudad(Partes)
6. πcolor(Partes⨝(σyid='Y2'(Vpy)))
7. πvid((σcolor='Rojo'(Partes)⨝Vpy)⨝(ρA(σciudad='Londres'(Proyectos))∪(σciudad='Paris'(Proyectos))))
8. Obtener las partes de cada proyecto que no esten en cada proyecto πpid(πpid(Partes)⨯πyid(Proyectos)-πpid,yid(Vpy))
9. vpy{p#, y#} % y{y#}
10. ==p countd(p#) as total==
11. ==select p _color=Azul AVG(Peso) as Promedio==
12. ==select _y#=Y2 vpy SUM(cant) as Total==
13. ==Select _y#=Y4 vpy countd(p#) as Cantidad==
14. vpy [p#] SUM(cant) as Total