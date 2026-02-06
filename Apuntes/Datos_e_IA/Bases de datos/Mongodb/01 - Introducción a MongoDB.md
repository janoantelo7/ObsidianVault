---
tags:
  - bases_datos/NoSQL
---
# Qué é?
**MongoDB** é unha base de datos **NoSQL** orientada a documentos, diseñada para gestionar grandes volumes de datos non estructurados ou semiestructurados dun xeito flexible e escalable. A diferencia coas bases de datos tradicionales (SQL), que almacenan datos en tablas con filas e columnas, MongoDB utiliza un **formato de documento** similar a JSON (chamado **BSON**, Binary JSON) para almacenar os datos, o que permite gardar información cunha estructura dinámica e máis complexa. ^1a87a0
## Principais caraccterísticas de MongoDB
- **Documentos**: Os datos almacénanse en documentos BSON, que poden conter estructuras anidadas, como listas e obxetos, o que facilita a representación de datos complexos.
- **Non require un esquema fixo**: A diferenza das bases de datos relacionais, MongoDB non precisa dun esquema predeterminado para os datos, polo que os documentos dentro dunha mesma colección poden ter estruturas diferentes.
- **Escalabilidade horizontal**: MongoDB está diseñado para ser escalable mediante a distribución dos datos en varios servidores ou nodos a través dun proceso chamado sharding, o que permite manejar grandes volumes de datos e tráfico.
- **Alto rendimiento**: MongoDB é adecuado para aplicacións que requieren baixa latencia, xa que ofrece altos niveles de rendimento tanto en lecturas como en escritura.
- **Consultas flexibles**: Aínda que é NoSQL, MongoDB permite realizar consultas avanzadas, indexación e agregación, características típicas das bases de datos relacionais.
- **Casos de uso comúns**: Aplicacións web e móviles, Big Data e análise de datos, Xestión de contenido, Sistemas de recomendación.
## Ventajas
- Flexibilidade na estructura de datos.
- Escalabilidade, adecuada para xestionar grandes cantidades de información.
- Bo rendemento en aplicacións en tempo real que necesitan manexar datos de maneira rápida.
## Desventajas
- Non é tan eficiente en operacións altamente relacionais (como unións complejas entre tablas) en comparación coas bases de datos SQL.
