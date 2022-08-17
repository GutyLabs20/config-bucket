# config-bucket

## comando para lombock
### java -jar lombock....(la versión que tengas)
### para agregar el Openfeign, se agrega una nueva dependencia maven OpenFeign.
### agregar una nueva interfaz con el nombre openfeign.

USE db_pizzeria;

create table cliente(
 	id_cliente int NOT NULL,
 	nombre VARCHAR(200) NOT NULL,
 	apellido VARCHAR(200) NOT NULL,
 	celular VARCHAR(200) NOT NULL,
 	direccion VARCHAR(200) NOT NULL,
  	PRIMARY KEY(id_cliente)
);

create TABLE pizza(
 	id_pizza int NOT NULL,
 	nombrepizza VARCHAR(200) NOT NULL,
 	descripcion VARCHAR(200) NOT NULL,
  	PRIMARY KEY(id_pizza)
);


create TABLE pizzeria(
 	id_pizzeria int NOT NULL,
 	direccion VARCHAR(200) NOT NULL,
 	sede VARCHAR(200) NOT NULL,
  	PRIMARY KEY(id_pizzeria)
);

create table cliente_pizza(
 	id_cliente int NOT NULL,
 	id_pizza int NOT NULL,
  	FOREIGN KEY(id_cliente ) REFERENCES cliente (id_cliente )  on delete cascade on update cascade,
 	FOREIGN KEY(id_pizza ) REFERENCES pizza( id_pizza )  on delete cascade on update cascade
);

create table pizzeria_pizza(
 	id_pizzeria int NOT NULL,
 	id_pizza int NOT NULL,
  	FOREIGN KEY(id_pizza ) REFERENCES pizza (id_pizza )  on delete cascade on update cascade,
 	FOREIGN KEY(id_pizzeria ) REFERENCES pizzeria( id_pizzeria )  on delete cascade on update cascade
);