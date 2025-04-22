![[/image 15.png|image 15.png]]

  

1. Las claves candidatas serían  
    - **Terminal**: codTerminal  
    - **Factura**: nroFact  
    - **Clientes**: codCliente  
    - **Autos**: marcaAuto y modeloAuto
2. k

![[/image 1 6.png|image 1 6.png]]

d.

![[/image 2 6.png|image 2 6.png]]

  

  

### Estructura

![[/image 3 6.png|image 3 6.png]]

  

### Esquemas

- Agrupación lógica de objetos
- Su implementación depende del motor
- Un nombre de objeto de BD debe ser único en cada esquema
- En SQL Server el esquema default es **dbo**
- En Oracle no existe el esquema como tal

  

### Tablas

- Objeto que funciona como contenedor de información
- Compuesta por filas y columnas

  

![[/image 4 5.png|image 4 5.png]]

  

Los tipos de datos dependen del motor utilizado, algunos de sql server son

![[/image 5 4.png|image 5 4.png]]

  

### Tablas - Constraints

- Tipos de datos
- Obligatoriedad
- Checks
- Default
- PKs, UKs
- Claves foráneas

  

### Constraint - Tipos de datos y obligatoriedad

![[/image 6 4.png|image 6 4.png]]

  

### Constraint - Check

![[/image 7 4.png|image 7 4.png]]

  

### Constraint - Default

![[/image 8 3.png|image 8 3.png]]

  

### Constraint - Primary key

- Corresponde a la clave primaria
- Identifica unívocamente cada fila
- Puede ser simple o compuesta
- Sólo puede haber una en cada tabla
- No pueden contener valores nulos

  

### Constraint - Unique

- Corresponde a las claves alternativas o secundarias
- Identifica unívocamente cada fila
- Puede ser simple o compuesta
- Puede haber más de una en cada tabla
- Puede contener valores nulos

  

![[/image 9 3.png|image 9 3.png]]

  

  

### Constraint - Foreign key

- Atributos que hacen referencia a una clave de otra tabla
- Puede ser simple o compuesta
- Pueden haber varias en cada tabla
- Representan relaciones entre tablas

  

![[/image 10 3.png|image 10 3.png]]

  

  

### Operador ALTER

- Se utiliza para modificar objetos
- En el caso de las tablas se puede utilizar para agregar, modificar o borrar columnas y/o constraints

  

![[/image 11 3.png|image 11 3.png]]

  

### Operador DROP

- Se utiliza para borrar objetos de la BD
- Una vez borrados no se pueden recuperar

  

![[/image 12 3.png|image 12 3.png]]

  

  

![[/image 13 3.png|image 13 3.png]]

  

![[/image 14 2.png|image 14 2.png]]

![[/image 15 2.png|image 15 2.png]]

  

```SQL
CREATE TABLE CLUBES (
    codClub INT PRIMARY KEY,
    nombreClub VARCHAR(100) NOT NULL,
    fecFundacion DATE,
    Domicilio VARCHAR(200),
    nombreJugadora VARCHAR(100)[], 
    codJugadora INT[]
);

CREATE TABLE JUGADORAS (
    codJugadora INT PRIMARY KEY,
    Nombre VARCHAR(100) NOT NULL,
    Apellido VARCHAR(100) NOT NULL,
    FechaNac DATE,
    Domicilio VARCHAR(200),
    DNI VARCHAR(20) UNIQUE NOT NULL,
    codClub INT,
    FOREIGN KEY (codClub) REFERENCES CLUBES(codClub)
);

CREATE TABLE PARTIDOS (
    codCamp INT,
    codClub INT,
    puntosObtenidos INT,
    descClub VARCHAR(200),
    fechaComienzo DATE,
    codClub1 INT,
    codClub2 INT,
    fechaPartido DATE,
    golesClub1 INT,
    golesClub2 INT,
    PRIMARY KEY (codCamp, codClub, codClub1, codClub2, fechaPartido),
    FOREIGN KEY (codClub1) REFERENCES CLUBES(codClub),
    FOREIGN KEY (codClub2) REFERENCES CLUBES(codClub)
);
```

```SQL
-- Tabla de Clubes (normalizada)
CREATE TABLE CLUBES (
    codClub INT PRIMARY KEY,
    nombreClub VARCHAR(100) NOT NULL,
    fecFundacion DATE,
    Domicilio VARCHAR(200)
);

-- Tabla de Jugadoras (normalizada)
CREATE TABLE JUGADORAS (
    codJugadora INT PRIMARY KEY,
    Nombre VARCHAR(100) NOT NULL,
    Apellido VARCHAR(100) NOT NULL,
    FechaNac DATE,
    Domicilio VARCHAR(200),
    DNI VARCHAR(20) UNIQUE NOT NULL
    -- codClub INT --
    -- FOREIGN KEY (codClub) REFERENCES CLUBES(codClub) --
);

-- REVISAR SI ESTA TABLA ES NECESARIA O ES PORQUE CUMPLE ALGUNA REGLA DE NORMALIZACIÓN --
-- Tabla de relación Club-Jugadora (resuelve la relación M:N)
CREATE TABLE CLUB_JUGADORA (
    codClub INT,
    codJugadora INT,
    fechaInicio DATE NOT NULL,
    PRIMARY KEY (codClub, codJugadora),
    FOREIGN KEY (codClub) REFERENCES CLUBES(codClub),
    FOREIGN KEY (codJugadora) REFERENCES JUGADORAS(codJugadora)
);

-- Tabla de Campeonatos
CREATE TABLE CAMPEONATOS (
    codCamp INT PRIMARY KEY,
    fechaComienzo DATE,
    descripcion VARCHAR(200)
);

-- Tabla de Partidos (normalizada)
CREATE TABLE PARTIDOS (
    codPartido INT PRIMARY KEY,
    codCamp INT,
    codClubLocal INT,
    codClubVisitante INT,
    fechaPartido DATE,
    golesLocal INT,
    golesVisitante INT,
    -- PRIMARY KEY (codClubLocal, fechaPartido), --
    FOREIGN KEY (codCamp) REFERENCES CAMPEONATOS(codCamp),
    FOREIGN KEY (codClubLocal) REFERENCES CLUBES(codClub),
    FOREIGN KEY (codClubVisitante) REFERENCES CLUBES(codClub),
    UNIQUE (codCamp, codClubLocal, codClubVisitante, fechaPartido)
);

-- Tabla de Puntos por Campeonato
CREATE TABLE PUNTOS_CAMPEONATO (
    codCamp INT,
    codClub INT,
    puntosObtenidos INT,
    PRIMARY KEY (codCamp, codClub),
    FOREIGN KEY (codCamp) REFERENCES CAMPEONATOS(codCamp),
    FOREIGN KEY (codClub) REFERENCES CLUBES(codClub)
);
```

> [!important] En el examen se puede tener apuntes. No se puede traer la notebook. Puedo llevar las notas en un pendrive

  

CLUBES (codClub, fecFund, nombre, domicilio, descripción)

JUGADORAS ( codJugador, nombre, apellido, fechaNac, DNI, domicilio, codClub)

PARTIDOS (fecha, codClub1, codClub2, campeonato, goles1, goles2)

TABLA POSICIONES (codCampeonato, codClub, puntos)

CAMPEONATO (codCampeonato, fechaCampeonato)