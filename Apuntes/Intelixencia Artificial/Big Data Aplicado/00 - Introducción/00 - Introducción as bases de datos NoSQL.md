---
tags:
  - big_data
  - bases_datos/NoSQL
---
# Tipos de bases de datos NoSQL
Dentro das bases de datos NoSQL encontramos distintas variedades na fomra en que almacenan os datos. Entre as cales podemos destacar os seguintes tipos:
- Documentais
- Clave-valor
- Columnares
- Orientadas a grafos
## Documentais
As bases de datos NoSQL documentais almacenan datos como documentos para o que se empregan formatos semiestructurados como JSON, XML ou BSON que non teñen que cumplir un esquema determinado con antelación. 

Non existe o concepto de táboa, pero si o de colección onde agrupamos documentos similares para axudarnos a organizar os documentos.

Un **exemplo** de este tipo son:
- [[Apuntes/Servicios/Bases de datos/Mongodb/01 - Introducción#Qué é?|MongoDB]]
- Apache CouchDB
## Clave-valor
As bases de datos NoSQL de pares clave-valor son a forma máis simple de base de datos NoSQL onde os datos organizanse nun diccionario de pares clave-valor, onde a clave é similar á Primary Key que tiñamos nas táboas dos modelos relacionales e o valor é unha colección de datos.

Un **exemplo** de este tipo son: 
- Aerospike
- HBase
- CouchBase
- Redis
- Berkeley DB
- Voldemort
## Columnares
As bases de datos columnares organizan o almacenamento dos datos en columnas en vez de filas, que é o almacenamento tradicional das bases de datos relacionais.

Estas bases de datos columnares empregan habitualmente a linguaxe de consulta SQL, polo que vemos que NoSQL non implica suprimir o uso de esta linguaxe.

As bases de datos columnares teñen a ventaxa que reducen as lecturas de dosco nas consultas típicas dos sistemas OLAP.

Un **exemplo** de este tipo son:
- MariaDB ColumnStore
- Apache Cassandra
- Vertica
## Orientadas a grafos
As bases de datos de grafos organizan a información nunha estructura de grafo onde os nodos almacenan os datos e as aristas serven para relacionar os nodos. Tanto para os nodos como para as aristas pódense definir atributos adicionais. A flexibilidade de estas bases de datos ven das posibilidades de crear relacións complexas que establecemos coas aristas.

Se o trasladamos ao concepto do modelo relacional os nodos poden ser instancias dunha entidade (filas dunha táboa) e as aristas as relacións entre elas. Esto fai que montar unha base de datos orientada a grafos utilizando un motor de base de datos relacional é posible, pero en este caso non obtemos ningún beneficio de empregalas.

Un **exemplo** de este tipo son:
- AllegroGraph
- Neo4j

# Exemplos de uso de bases de datos NoSQL
As bases de datos NoSQL son ideais para certos tipos de aplicacións e casos de uso onde os datos son grandes, variados e xéranse a alta velocidade. Imos ver algúns casos de uso:
- Datos generados en redes sociales: publicacións, comentarios, interaccións dos usuarios... (HBase e Cassandra)
- Datos con xerarquías e relacións complexas como recomendacións e likes en redes sociales (Neo4j)
- Datos de sensores e IoT (Apache Cassandra)
- Recomendacións de productos en mercado electrónico (Redis e MongoDB)
- Almacenamento de datos de sesións e datos temporais en aplicacións web (Redis)
- Videoxogos en linea, para os que hai que almacenar moitas tipologías de datos dos xogadores concurrentes e ser capaces de escalar cos incrementos dos usuarios.