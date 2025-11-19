---
tags:
  - bases_datos/NoSQL
---
A diferencia das bases de datos relacionales, MongoDB non usa tablas con filas e columnas, senón que utiliza coleccións con documentos que non teñen un esquema fijo, polo que opcionalmente en cada documento dunha mesma colección temos a liberdade de organizar os datos como precisemos.

A pesar de que a organización dos datos cambian dunha a outra, podemos facer a seguinte correspondencia entre os niveles de organización dos datos en MongoDB e un motor de base de datos relacional:

| Base de datos Relacional | MongoDB       |
| ------------------------ | ------------- |
| Base de datos            | Base de datos |
| Tablas                   | Coleccións    |
| Filas                    | Documento     |
| Columa                   | Campos        |
## Bases de datos
Unha base de datos é un contenedor de coleccións, e cada instancia de MongoDB pode ter múltiples bases de datos.

Cando estamos conectados con un cliente a un servicio de MongoDB o igual que pasa con múltiples clientes de bases de datos relacionales, teremos que realizar unha selección da base de datos coa que queremos traballar antes de empezar a lanzar consultas.

Podemos utilizar os seguintes comandos para listar e usar as bases de datos:
- `show dbs`: Lista as bases de datos.
- `use {nombre_bd}`: Seleciona a base de datos coa que se vai traballar.
- `db`: Mostra a base de datos que está seleccionada.

En MongoDB podemos seleccionar unha base de datos ainda que esta non exista porque MongoDB utiliza un mecanismo de creación implícita, polo cal a base de datos se crea cando executemos un comando de creación da primeira colección ou dun documento na primeira colección.
# Coleccións
Unha colección é un grupo de documentos, equivalente a unha tabla nunha base de datos relacional, coa diferencia que as coleccións non requieren unha estructura fija, polo que os documentos dentro de unha colección poden ter diferentes campos.

Ás coleccións tamén aplica o mecanismo de creación implícita e créanse automáticamente cando se inserta o primeiro documento, pero ademáis, podemos facer unha creación explícita co comando `createCollection()`.

```js
db.createCollection("nombre_coleccion")
db.outra_coleccion.insertOne({nombre: "Pancho", Apellido: "Perro"})
```



