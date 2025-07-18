# **Creación de base de datos con tablas y relaciones - Daniel Alejando Duran Franco**



```sql
-- Tabla pago --

CREATE TABLE pago (
    id_pago SMALLINT UNSIGNED,
    id_cliente SMALLINT UNSIGNED,
    id_empleado TINYINT UNSIGNED,
    id_alquiler INT,
    total DECIMAL(5,2),
    fecha_pago DATETIME,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_pago),
    FOREIGN KEY (id_cliente) REFERENCES cliente (id_cliente),
    FOREIGN KEY (id_empleado) REFERENCES empleado (id_empleado),
    FOREIGN KEY (id_alquiler) REFERENCES alquiler (id_alquiler)
);

-- Tabla alquiler --

CREATE TABLE alquiler (
    id_alquiler INT,
    fecha_alquiler DATETIME,
    id_inventario MEDIUMINT UNSIGNED,
    id_cliente SMALLINT UNSIGNED,
    fecha_devolucion DATETIME,
    id_empleado TINYINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_alquiler),
    FOREIGN KEY (id_inventario) REFERENCES inventario (id_inventario),
    FOREIGN KEY (id_cliente) REFERENCES cliente (id_cliente),
    FOREIGN KEY (id_empleado) REFERENCES empleado (id_empleado)
);

-- Tabla cliente --

CREATE TABLE cliente (
    id_cliente SMALLINT UNSIGNED,
    id_almacen TINYINT UNSIGNED,
    nombre VARCHAR(45),
    apellidos VARCHAR(45),
    email VARCHAR(50),
    id_direccion SMALLINT UNSIGNED,
    activo TINYINT(1),
    fecha_creacion DATETIME,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_cliente),
    FOREIGN KEY (id_almacen) REFERENCES almacen (id_almacen),
    FOREIGN KEY (id_direccion) REFERENCES direccion (id_direccion)
);

-- Tabla almacen --

CREATE TABLE almacen (
    id_almacen TINYINT UNSIGNED,
    id_empleado_jefe TINYINT UNSIGNED,
    id_direccion SMALLINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_almacen),
    FOREIGN KEY (id_direccion) REFERENCES direccion (id_direccion)
);

-- Tabla empleado --

CREATE TABLE empleado (
    id_empleado TINYINT UNSIGNED,
    nombre VARCHAR(45),
    apellidos VARCHAR(45),
    id_direccion SMALLINT UNSIGNED,
    imagen BLOB,
    email VARCHAR(50),
    id_almacen TINYINT UNSIGNED,
    activo TINYINT(1),
    username VARCHAR(16),
    password VARCHAR(40),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_empleado),
    FOREIGN KEY (id_direccion) REFERENCES direccion (id_direccion),
    FOREIGN KEY (id_almacen) REFERENCES almacen (id_almacen)
);

-- Tabla direccion --

CREATE TABLE direccion (
    id_direccion SMALLINT UNSIGNED,
    direccion VARCHAR(50),
    direccion2 VARCHAR(20),
    distrito VARCHAR(50),
    id_ciudad SMALLINT UNSIGNED,
    codigo_postal VARCHAR(10),
    telefono VARCHAR(20),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_direccion),
    FOREIGN KEY (id_ciudad) REFERENCES ciudad (id_ciudad)
);

-- Tabla idioma --

CREATE TABLE idioma (
    id_idioma TINYINT UNSIGNED,
    nombre VARCHAR(20),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_idioma)
);

-- Tabla ciudad --

CREATE TABLE ciudad (
    id_ciudad SMALLINT UNSIGNED,
    nombre VARCHAR(50),
    id_pais SMALLINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_ciudad),
    FOREIGN KEY (id_pais) REFERENCES pais (id_pais)
);

-- Tabla pelicula --

CREATE TABLE pelicula (
    id_pelicula SMALLINT UNSIGNED,
    titulo VARCHAR(255),
    descripcion TEXT,
    año_lanzamiento YEAR,
    id_idioma TINYINT UNSIGNED,
    id_idioma_original TINYINT UNSIGNED,
    duracion_alquiler TINYINT UNSIGNED,
    rental_rate DECIMAL(4,2),
    duracion SMALLINT UNSIGNED,
    replacement_cost DECIMAL(5,2),
    clasificacion ENUM('G','PG','PG-13','R','NC-17'),
    caracteristicas_especiales SET('Trailers','Commentaries','Deleted Scenes','Behind the Scenes'),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_pelicula),
    FOREIGN KEY (id_idioma) REFERENCES idioma (id_idioma)
);

-- Tabla film_text --

CREATE TABLE film_text (
    film_id SMALLINT UNSIGNED,
    title VARCHAR(255),
    description TEXT,
    PRIMARY KEY (film_id)
);

-- Tabla pelicula_categoria --

CREATE TABLE pelicula_categoria (
    id_pelicula SMALLINT UNSIGNED,
    id_categoria TINYINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_pelicula, id_categoria)
);

-- Tabla categoria --

CREATE TABLE categoria (
    id_categoria TINYINT UNSIGNED,
    nombre VARCHAR(25),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_categoria)
);

-- Tabla pelicula_actor --

CREATE TABLE pelicula_actor (
    id_actor SMALLINT UNSIGNED,
    id_pelicula SMALLINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_actor, id_pelicula)
);

-- Tabla actor --

CREATE TABLE actor (
    id_actor SMALLINT UNSIGNED,
    nombre VARCHAR(45),
    apellidos VARCHAR(45),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_actor)
);

-- Tabla pais --

CREATE TABLE pais (
    id_pais SMALLINT UNSIGNED,
    nombre VARCHAR(50),
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_pais)
);

-- Tabla inventario --

CREATE TABLE inventario (
    id_inventario MEDIUMINT UNSIGNED,
    id_pelicula SMALLINT UNSIGNED,
    id_almacen TINYINT UNSIGNED,
    ultima_actualizacion TIMESTAMP,
    PRIMARY KEY (id_inventario),
    FOREIGN KEY (id_pelicula) REFERENCES pelicula (id_pelicula),
    FOREIGN KEY (id_almacen) REFERENCES almacen (id_almacen)
);
```

