  

CLUBES (codClub, fecFund, nombre, domicilio, descripción)

JUGADORAS ( codJugador, nombre, apellido, fechaNac, DNI, domicilio, codClub)

PARTIDOS (fecha, codClub1, codClub2, campeonato, goles1, goles2)

TABLA POSICIONES (codCampeonato, codClub, puntos)

CAMPEONATO (codCampeonato, fechaCampeonato)

  

### Cardinalidad

- Campeonatos puede tener 0-N posiciones
- Jugadoras puede tener 0-1 clubes

  

### Columnas constantes

![[/image 16.png|image 16.png]]

![[/image 1 7.png|image 1 7.png]]

  

### Columnas calculadas

![[/image 2 7.png|image 2 7.png]]

![[/image 3 7.png|image 3 7.png]]

  

### Limitar cantidades de filas

![[/image 4 6.png|image 4 6.png]]

![[/image 5 5.png|image 5 5.png]]

  

> [!important] el offset y fetch forman parte del order by

  

### Cláusula Distinct

![[/image 6 5.png|image 6 5.png]]

  

### Where - Operadores

![[/image 7 5.png|image 7 5.png]]

  

  

![[/image 8 4.png|image 8 4.png]]

![[/image 9 4.png|image 9 4.png]]

  

  

![[/image 10 4.png|image 10 4.png]]

  

% = comodines

%A = que empiecen con A

%LAN% = que contengan LAN

%TO = que terminen con TO

  

![[/image 11 4.png|image 11 4.png]]

  

[JM]% = que empiecen con J o que empiecen con M

[B-M]% = que empiecen con letras que estén comprendidos entre la B y la M (C, D, E, F…)

_A% = que empiecen con la segunda letra en A

__A% = que empiecen con la tercera letra en A

  

![[/image 12 4.png|image 12 4.png]]

![[/image 13 4.png|image 13 4.png]]

![[/image 14 3.png|image 14 3.png]]

  

![[/image 15 3.png|image 15 3.png]]

![[/image 16 2.png|image 16 2.png]]

  

![[image 17.png]]

![[image 18.png]]

  

![[image 19.png]]

  

![[image 20.png]]

  

> [!important] Usar CAST

  

![[image 21.png]]

  

![[image 22.png]]