---
tags:
  - mysql
---
# Bases de datos
## Crear base de datos
Podemos crear unha [[01 - Introducción a SQL#Base de datos|base de datos]] en MySQL co siguiente comando:
```mysql
CREATE DATABASE <db_name> CHARACTER SET utf8mb4;
```
## Seleccionar a base de datos
Á hora de traballar con unha base de datos, primeiro é necesario seleccionala. Podemos seleccionala co seguinte comando.
```mysql
USE <db_name>;
```
# Tablas
## Crear tablas
Unha vez temos creada a base de datos, podemos emprezar a crear [[01 - Introducción a SQL#Tabla|tablas]] dentro da propia base de datos para almacenar datos en elas. No seguinte exemplo vamos a crear unha tabla chamada "fabricante".
```mysql
CREATE TABLE fabricante (  
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,  
  nombre VARCHAR(100) NOT NULL  
);
```
En este exemplo, a tabla que creamos ten dúas propiedades (columnas). Unha delas chamase "id" que é a primary key (clave primaria), esto quere decir que será o identificador principal dos datos de esa tabla, almacenará datos de tipo **INT** (números enteiros) e esta irá aumentando o número según se vaian añadindo datos.

A outra propiedade chamase "nombre" e almacenará datos de tipo **VARCHAR** (todo tipo de carácteres), o **not null** indica que non pode estar vacía.
## Relacionar tablas
Para este exemplo creamos outra tabla, que se relacionará coa tabla fabricante que creamos antes.
```mysql
CREATE TABLE producto (  
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,  
  nombre VARCHAR(100) NOT NULL,  
  precio FLOAT NOT NULL,  
  id_fabricante INT UNSIGNED NOT NULL,  
  FOREIGN KEY (id_fabricante) REFERENCES fabricante(id)  
);
```

En esta tabla só cambia a última orden **FOREING KEY**, que indica que a propiedad de esta tabla chamada "id_fabricante" fai referencia (**REFERENCES fabricante(id)**) á propiedade "id" da tabla fabricante. Dito de outra maneira, os datos que se introduzcan en "id_fabricante" deben coincidir cos que hai en "id" da tábla fabricante.
## Insertar datos en tablas
Unha vez sabemos crear tablas, tamén é importante saber insertar datos en tablas. Para esto utilizamos o seguinte comando `insert into`. A sentencia básica para esto é:
```mysql
insert into <tabla> values();
```
Dentro do paréntesis de `values()` metemos os datos que queremos introducir dentro da tabla separados por coma(`,`).

Por exemplo, vamos insertar varios datos na tabla que creamos antes chamada `fabricante`. 
```mysql
INSERT INTO fabricante VALUES(1, 'Asus');
INSERT INTO fabricante VALUES(2, 'Lenovo');
INSERT INTO fabricante VALUES(3, 'Hewlett-Packard');
INSERT INTO fabricante VALUES(4, 'Samsung');
INSERT INTO fabricante VALUES(5, 'Seagate');
```
# Mostrando datos
Outra función básica de calquer xestor de bases de datos, é o de poder seleccionar datos das tablas que pertenecen á base de datos. Dentro de este apartado vamos a ver como podemos mostrar xusto o que nos interesa mostrar. Neste apartado vamos a traballar coas tablas que creamos arriba.
## Mostrar todos os datos de unha tabla
Para mostrar todos os datos de unha tabla en MySQL basta con utilizar a seguinte sentencia.
```mysql
select * from <tabla>;
```

Aquí o asterísco(`*`) significa todos os atributos que ten a tabla.
## Mostrar só un atributo da tabla
Para mostrar só un [[01 - Introducción a SQL#Columna (atributo)|atributo]] da tabla, bastanos con escribir unha sentencia similar á anterior pero cambiando o asterísco(`*`) polo nombre da propiedade a seleccionar.
```mysql
select <nombre_atriburo> from <tabla>;
```
## Mostrar os datos filtrados por unha condición
Ahora ben, se queremos facer consultas máis complexas, como por exemplo, mostrar todos os datos que temos pero en base a unha condición. Por exemplo, mostramos todos os productos que vende Samsung en Amazon, pois para esto debemos utilizar o parámetro `where` así as nosas queries poden cumplir coa condición desexada..
```mysql
select * from <tabla> where <nombre_atributo>=<valor_atributo>;
```

Continuando co exemplo anterior podemos facer:
```mysql
select * from fabricante where nombre="Samsung";
```
### Operadores
Non só podemos utilizar o operador de igualdade (`=`), senon que o linguaxe de MySQL acepta moitos outros que son: 

| Operador | Descripción                                                                 |
| -------- | --------------------------------------------------------------------------- |
| =        | Igual                                                                       |
| !=       | Non igual                                                                   |
| >        | Maior que                                                                   |
| <        | Menor que                                                                   |
| >=       | Maior ou igual                                                              |
| <=       | Menor ou igual                                                              |
| like     | similar ao igual, pero busca patróns, é decir, podemos buscar coincidendias |
## Mostrando os datos con varias condicions
Cando queremos mostrar datos onde haxa varias condicions where debemos utilizar dous operadores clave que son and e or.
### AND
Este operador quere decir que o que seleccionas cumple as dúas condicions, por exemplo, seleccionamos todo dos productos que costen máis de 100 pero que o id sexa inferior a 5.
```mysql
select * from <tabla> where <condicion1> and <condicion2>;
```

A query do exemplo sería a seguinte:
```mysql
select * from producto where precio>100 and id<5;
```
### OR
Este operador quere decir que o que seleccionas unhas das dúas condicións. 
```mysql
select * from <tabla> where <condicion1> or <condicion2>;
```
Na siguiente sentencia seleccionamos os productos onde o nombre conteña a palabra memoria e o id sexa igual ou inferior a 2.
```mysql
select * from producto where nombre like 'memoria%' or id<=2;
```
## Mostrando datos que cumplen certos patróns
Para mostrar resultados que cumplen certos patróns utilizamos o opeador `LIKE`.

Podemos empregalo de diversas manerias á hora de buscar elementos dentro da base de datos. As máis comúns son as seguintes:
### Empeza con
Para buscar elementos que cumplan o patrón de empeza con utilizamos a seguinte expresión no operador `like`.
```mysql
select * from <tabla> where <nombre_atributo> like "<letra>/<patron>%";
```

Esto quere decir, buscamos na tabla o atributo que empece coa letra/patron que nos queiramos. Esto vese mellor no seguinte exemplo no que buscamos todos os fabricantes que empecen por "S".
```mysql
select * from fabricante where nombre like "s%"
```
### Acaba con
Para buscar patróns de texto que cumplan coa siguiente condición utilizamos a seguinte expresión.
```mysql
select * from <tabla> where <nombre_atributo> like "%<letra>/patron>";
```

No seguinte exemplo no que buscamos todos os fabricantes que rematen con patron "te" vemos como aplicar a seguinte query.
```mysql
select * from fabricante where nombre like "%te";
```
### Contén
Para buscar expresións que indiquen texto que contén uns caracteres no medio pero que empeza e acaba con calquer cousa utilizamos a seguinte expresión.
```mysql
select * from <tabla> where <nombre_atributo> like "%<letra>/<patron>%";
```

A continuación podemos ver un exemplo que aplica a query para buscar todos os fabricantes que conteñen a letra "e".
```mysql
select * from fabricante f where nombre like "%e%";
```
## Mostrando os datos de maneira ordenada
Para mostrar os datos de tabla ordenados en función do valor de un atriburo utilizamos a orden `ORDER BY`.
```mysql
select * from <tabla> order by <nombre_atributo>;
```

Por defecto, o `order by` ordena os datos de menor a maior (ou de A-Z, en caso de ser texto). Se queremos invertir o orden e mostrar de maior a menor debemos utilizar `desc` xunto con `order by`.
```mysql
select * from <tabla> order by <nombre_atributo> desc;
```
## Mostrando o maior de unha columna
Para escoller o maior de unha columna debemos utilizar no select o operador **max**.
```MySQL
select max(<columna>) from <tabla>;
```
## Mostrando o menor de unha columna
Para escoller o menor de unha columna debemos utilizar no select o operador **min**.
```mysql
select min(<columna>) from <tabla>;
```
## Mostrando o número total de datos
Se queremos mostrar o número total de datos de unha columna utilizamos o método **count**.
```mysql
select count(*) from <tabla>;
```
Se queremos filtrar para quitar os valores NULL, debemos escoller unha columna en concreto en lugar de utilizar o asterísco.
## Mostrando a suma dos datos de unha columna
Para mostrar a suma numérica dos datos de unha columna (esa columna ten que conter números) debemos utilizar o operador **sum** no select.
```mysql
select sum(<columna_numerica>) from <tabla>;
```
## Mostrando a media dos datos de unha columna
Se queremos mostrar a media numérica dos datos de unha columna (esa columna ten que conter números) debemos utilizar o operador **avg** no select.
```mysql
select avg(<columna_numerica>) from <tabla>;
```
## Mostrando resultados onde buscamos certos valores
Se queremos buscar certos valores dentro de unha columna podemos utilizar o operador **in**.
```mysql
select * from <tabla> where <columa> in (<valores>)
```
se queremos indicar varios valores temos que separalos por comas.
## Mostrando os valores que non sexan os que especificamos
Se queremos sacar todos os elementos de unha lista menos uns cantos valores podemos utilizar o operador **not in**.
```mysql
select * from <tabla> where <columna> not in (<valores>)
```
Esto o que fai é devolvernos todos os valores que non sexan os que nos especificamos.
## Mostrar resultados onde a concidión esté entre dous valores
Podemos filtrar os resultados por unha condición que esté entre dous valores utilizando o operador **between**.
```mysql
select * from <tabla> where <columna> between <valor1> and <valor2>
```
## Creando alias para as columnas
En MySQL podemos crear un alias para as columnas e así sexa máis sencillo traballar con elas.
```mysql
select max(<columna>) as <alias> from <tabla>;
```
## Unindo diferentes tablas
Para unir diferentes tablas utilizamos o operador `join`. Hai varios tipos de operadores joins dependendo do tipo de unión que queiramos facer.
* **inner join**: devolve todos os resultados que coinciden nas dúas tablas.
* **left join**: devolve **_todos_** os resultados da tabla da **_esquerda_** e todos os que **_coincidan_** da tabla da _**dereita**_.
* **right join**: devolve todos os resultados que **_coincidan_** da tabla da **_esquerda_** e **_todos_** os resultados da tabla da **_dereita_**.

Cando falamos de tabla da dereita ou esquerda estamonos a referir a que lugar ocupan con respecto ao operador `join`. Podemos ver un exemplo abaixo onde a tabla **_producto_** ocupa o lugar de tabla da esquerda e a tabla **_fabricante_** ocupa o lugar de tabla da dereita.
```MySQL
select * from producto p inner join fabricante f on p.fabricante_id =f.id;
```
### inner join
o operador `inner join` utilizase para combinar dúas tablas mostrando os resultados que coincidan entre as dúas tablas. Abaixo mostramos un exemplo de como utilizar a seguinte query.
```MySQL
select * from producto p inner join fabricante f on p.fabricante_id =f.id;
```

O resultado de esta query é a seguinte:

| id  | nombre             | precio  | fabricante_id | id  | nombre  |
| --- | ------------------ | ------- | ------------- | --- | ------- |
| 1   | iPhone 14          | 999.99  | 1             | 1   | Apple   |
| 2   | MacBook Air        | 1299.99 | 1             | 1   | Apple   |
| 8   | AirPods Pro        | 249.99  | 1             | 1   | Apple   |
| 3   | Galaxy S22         | 799.99  | 2             | 2   | Samsung |
| 9   | Smart Monitor M8   | 699.99  | 2             | 2   | Samsung |
| 4   | PlayStation 5      | 499.99  | 3             | 3   | Sony    |
| 5   | XPS 13             | 999.99  | 4             | 4   | Dell    |
| 7   | Monitor UltraSharp | 299.99  | 4             | 4   | Dell    |
| 6   | Envy Laptop        | 849.99  | 5             | 5   | HP      |
| 10  | Impresora DeskJet  | 149.99  | 5             | 5   | HP      |
En esta tabla vemos todos os productos que teñen un fabricante e todos os fabricantes que teñen un producto.
### left join
O `left join` empregase para seleccionar todos os campos da tabla da esquerda e solo os que coincidan da tabla da dereita.
```MySQL
select * from producto p left join fabricante f on p.fabricante_id =f.id;
```

| id  | nombre             | precio   | fabricante_id | id  | nombre  |
| --- | ------------------ | -------- | ------------- | --- | ------- |
| 1   | iPhone 14          | 999.99   | 1             | 1   | Apple   |
| 2   | MacBook Air        | 1,299.99 | 1             | 1   | Apple   |
| 3   | Galaxy S22         | 799.99   | 2             | 2   | Samsung |
| 4   | PlayStation 5      | 499.99   | 3             | 3   | Sony    |
| 5   | XPS 13             | 999.99   | 4             | 4   | Dell    |
| 6   | Envy Laptop        | 849.99   | 5             | 5   | HP      |
| 7   | Monitor UltraSharp | 299.99   | 4             | 4   | Dell    |
| 8   | AirPods Pro        | 249.99   | 1             | 1   | Apple   |
| 9   | Smart Monitor M8   | 699.99   | 2             | 2   | Samsung |
| 10  | Impresora DeskJet  | 149.99   | 5             | 5   | HP      |
| 11  | Walkman            | 79.99    |               |     |         |
Como podemos ver na taboa de arriba vemos todos os productos incluidos aqueles que non teñen fabricante.
### right join
O `right join` é cando collemos todos os datos da tabla da dereita e solo os datos que coincidan da tabla da esquerda.
```MySQL
select * from producto p right join fabricante f on p.fabricante_id =f.id;
```

|id|nombre|precio|fabricante_id|id|nombre|
|---|---|---|---|---|---|
|1|iPhone 14|999.99|1|1|Apple|
|2|MacBook Air|1,299.99|1|1|Apple|
|8|AirPods Pro|249.99|1|1|Apple|
|3|Galaxy S22|799.99|2|2|Samsung|
|9|Smart Monitor M8|699.99|2|2|Samsung|
|4|PlayStation 5|499.99|3|3|Sony|
|5|XPS 13|999.99|4|4|Dell|
|7|Monitor UltraSharp|299.99|4|4|Dell|
|6|Envy Laptop|849.99|5|5|HP|
|10|Impresora DeskJet|149.99|5|5|HP|
|||||6|Asus|
En esta tabla vemos como se mostran todos os fabricantes ainda que non teñan ningún producto.
## Mostrando os resultados agrupados
En SQL podemos mostrar os resultados agrupados por un parámetro. Para eso utilizamos o operador `GROUP BY`. 
```MySQL
select sum(precio), fabricante_id from producto p group by fabricante_id;
```

| sum(precio) | fabricante_id |
| ----------- | ------------- |
| 79.99       |               |
| 2,549.97    | 1             |
| 1,499.98    | 2             |
| 499.99      | 3             |
| 1,299.98    | 4             |
| 999.98      | 5             |
En esta tabla vemos a suma dos precios dos productos que vende cada un dos fabricantes.
## Unindo varias sentencias select
Para unir varias sentencias select utilizamos o operador `UNION`, hai que ter en conta o seguinte á hora de utilizalo.
* Cada select co union ten que ter as mismas columnas.
* As columnas en cada select teñen que estar no mismo orden.
* As columnas teñen que ter o mismo tipo de dato.
```MySQL
SELECT nombre AS nombre_elemento, 'Producto' AS tipo
FROM producto
UNION
SELECT nombre AS nombre_elemento, 'Cliente' AS tipo
FROM cliente;
```

Esta query devolvenos os nombres dos clientes e dos productos sen estar repetidos en unha sola tabla:

| nombre_elemento    | tipo     |
| ------------------ | -------- |
| iPhone 14          | Producto |
| MacBook Air        | Producto |
| Galaxy S22         | Producto |
| PlayStation 5      | Producto |
| XPS 13             | Producto |
| Envy Laptop        | Producto |
| Monitor UltraSharp | Producto |
| AirPods Pro        | Producto |
| Smart Monitor M8   | Producto |
| Impresora DeskJet  | Producto |
| Walkman            | Producto |
| Juan Perez         | Cliente  |
| Maria Lopez        | Cliente  |
| Carlos Sanchez     | Cliente  |
| Ana Gomez          | Cliente  |
| Luis Fernandez     | Cliente  |
## Mostrando grupos de datos filtrados por unha condición
Para mostrar grupos de datos filtrados por unha condición utilizamos o operador `having`.
O operador `having` utilizase despois de aplicar a cláusula `group by`.
```MySQL
SELECT f.nombre AS fabricante, COUNT(p.id) AS total_productos
FROM fabricante f
LEFT JOIN producto p ON f.id = p.fabricante_id
GROUP BY f.id
HAVING COUNT(p.id) > 1;
```

Esa query devolvenos os fabricantes que teñen máis de un producto asociado. A tabla resultante de esa query sería:

| fabricante | total_productos |
| ---------- | --------------- |
| Apple      | 3               |
| Samsung    | 2               |
| Dell       | 2               |
| HP         | 2               |
Cando utilizamos todos os operadores e máis un `having` a orde de cada un sería:
```MySQL
SELECT nombre_columna
FROM nombre_tabla
WHERE condicion
GROUP BY nombre_columna
HAVING condicion
ORDER BY nombre_columna;
```
## Mostrando resultados que conteñen valores null
Os valores `null` é que quere decir que ese campo non contén información, para saber se un campo é `null` ou non utilizamos no `where` a condición `is null`.
```MySQL
select * from producto where fabricante_id is null;
```

Esta query devolvenos todos os productos que non teñen un fabricante asociado:

| id  | nombre  | precio | fabricante_id |
| --- | ------- | ------ | ------------- |
| 11  | Walkman | 79.99  |               |
## Mostrando valores que non son null
Esto é basicamente o contrario do elemento anterior, consiste en eliminar os valores que non teñen datos en un campo.

Esta query devolvenos todos os productos que teñen un fabricante asociado:

| id  | nombre             | precio  | fabricante_id |
| --- | ------------------ | ------- | ------------- |
| 1   | iPhone 14          | 999.99  | 1             |
| 2   | MacBook Air        | 1299.99 | 1             |
| 3   | Galaxy S22         | 799.99  | 2             |
| 4   | PlayStation 5      | 499.99  | 3             |
| 5   | XPS 13             | 999.99  | 4             |
| 6   | Envy Laptop        | 849.99  | 5             |
| 7   | Monitor UltraSharp | 299.99  | 4             |
| 8   | AirPods Pro        | 249.99  | 1             |
| 9   | Smart Monitor M8   | 699.99  | 2             |
| 10  | Impresora DeskJet  | 149.99  | 5             |
