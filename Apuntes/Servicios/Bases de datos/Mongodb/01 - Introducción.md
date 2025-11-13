---
tags:
  - bases_datos/NoSQL
---
# Qué é?
MongoDB é unha base de datos NoSQL orientada a documentos, o que significa que almacena datos en un documentos similares a JSON. É altamente utilizada pola súa capacidade de manexar grandes volúmenes de datos e a súa flexibilidade na estructura de datos.
# Conceptos
## Base de datos
A base de datos é un contenedor das coleccións. Unha instancia de MongoDB pode ter varias bases de datos.
## Colección
É un grupo de documentos. É o equivalente a unha [[01 - Introducción a SQL#Tabla|tabla]] en bases de datos relacionales, pero sin esquemas definidos.
## Documento
É o registro básico en MongoDB, é similar a unha fila nunha tabla SQL. Un documento almacenase en formato BSON (extensión binaria de JSON). 

Ejemplo de documento:
```json
{
  "nombre": "Juan",
  "edad": 28,
  "ciudad": "Madrid"
}
```
## Campo
É un par clave-valor en un documento. É similar a unha columna nunha tabla SQL.
