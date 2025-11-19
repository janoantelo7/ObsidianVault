---
tags:
  - big_data
---
_Big Data_ refírese a aqueles conxuntos de datos que, polo seu **gran volume, complexidade e variabilidade**, resultan difíciles de almacenar, procesar e analizar empleando os xestores de bases de datos ou ferramentas tradicionais. Estos datos típicamente cumplen cunha serie de características que comezan todas por V:
- **Volume**: Facendo referencia á elevada cantidade dos mesmos.
- **Velocidade**: Pola rapidez coa que se producen e deben ser procesados os datos, xa que poden perder valor ou quedar obsoletos nun curto espazo de tempo.
- **Variedade**: Pola diversidade de formatos e fontes dos datos, que poden ser estructurados (táboas, rexistros), semiestructurados (JSON, XML) ou non estructurados (texto libre, imaxes, vídeos, sensores, etc.).

Estas son as principais tres V's que se asocian ao Big Data dende o principio, pero a medida que as tecnoloxías foron madurando incorporaronse novas, entre as que destacan:
- **Veracidade**: Referíndose a que os datos deben ser de calidade e precisos
- **Valor**: No sentido de que teñen que ser de utilidade á hora de analizalos na toma de decisións para o negocio.
- **Visualización**: Indicando que para axudar a interpretación dos datos hai que presentalos de forma comprensible e atractiva, para o cal o uso de elementos de visualización é clave.
- **Variabilidade**: Con esta faise referencia a distintos elementos de variación dos datos:
	- Inconsistencias na interpretación dos datos segundo o contexto.
	- Cambios nos formatos e tipos de datos.
	- Cambios na velocidade de xeración de datos.

As tres **primeiras V's** fan referencia á **cantidade** e a **estructura** dos datos, mentres que as **últimas V's** céntranse máis en aspectos de **calidade** e **utilidade** dos datos.
# Escalabilidade horizontal
O volume de datos lonxe de manterse constante, tende a crecer cada vez máis rápido e aínda que o tamaño e o prezo do almacenamento evoluciona e se pode asumir en certa medida o investimento nel, seguimos tendo o  problema de procesar este volume de datos. Polo que se nos presentan dous problemas que hai que solucionar:
- **Ampliar a nosa capacidade de procesamento**: Tradicionalmente, os novos problemas de procesamento solucionáronse aplicando **escalado vertical**, que consiste aumentando os recursos hardware dun servidor, e incluso cando non é suficiente cambiandoo por un servidor máis potente, pero esto está sujeto ás limitacións de amplicación e requiere unha inversión continúa en hardware.
- **Buscar técnicas para acelerar as lecturas e procesamento dos datos**: Procesar grandes volumes de información non é facilmente solucionable a través de hardware máis potente polo seguinte motivo: **Sempre estaremos limitados pola velocidade no acceso á disco**. Isto débese a que aínda que sexamos capaces de procesar a información cada vez máis rápido, a velocidade de acceso ao disco non mellora na mesma proporción.

A solución a esto pasa por un **procesamento distribuído** a través de arquitecturas en clúster en lugar de arquitecturas monolíticas. Estas arquitecturas de clúster serán máis capaces de adaptarse ao crecemento do volume de información canto mellor sexan capaces de executar os seguintes puntos:
- **Escalado horizontal**: Facilidade de expandir o clúster con novos nodos para satisfacer as crecentes necesidades de almacenamento e procesamento.
- **Implantación do equilibrio de carga**: Que o sistema faga unha distribución óptima da carga entre os nodos do clúster. Este punto é clave para garantir o máximo aproveitamento das capacidades conxuntas dos nodos.
- **Comunicación de rede rápidas**: Neste tipo de arquitecturas, a comunicación en rede é moi importante á hora de sincronizar o traballo entre os nodos do clúster. Como compoñente crítico, ten que funcionar o mellor posible, adaptándose ao crecemento, para evitar que a rede se converta nun factor limitante, como antes era o acceso ao disco.

A maiores, estas arquitecturas de clúster para o procesamento distribuído supoñen unha maior complexidade que implica ter que enfrontarse a outro tipo de problemas e retos a resolver: 
- Disponibilidade
- Coherencia dos datos
- Sincronización
- Ancho de banda
- Tratamento de erros
# Big Data e NoSQL
As [[00 - Introducción as bases de datos NoSQL|bases de datos NoSQL]] e o Big Data están moi relacionados, xa que NoSQL grazas á flexibilidade que ofrece para almacenar distintas tipoloxías de datos o non empregar un esquema fijo da solución a moitos dos problemas cando tratamos con datos catalogados como Big Data:
- **Volume**: As bases de datos NoSQL foron deseñadas para o escalado horizontal, para o cal é de gran axuda que non empreguen esquemas fijos, xa que é mais fácil distribuír datos entre servidores sen ter o condicionante dun esquema fixo central.
- **Variedade**: Pola flexibilidade de NoSQL de almacenar diferentes tipoloxías e formatos de datos.
- **Velocidade**: De novo pola flexibilidade do seu esquema, que permite unha carga de datos moi fluída sen ter que estar facendo axustes derivados de algún cambio de estructura nos datos.

As bases de datos NoSQL gardan os datos nunha estructura de datos como pode ser un documento JSON sen precisar un esquema. Esto supón que este tipo de bases de datos son **máis fácilmente escalabes horizontalmente** a través de **arquitecturas distribuídas**. Esto implica que a información estará almacenada en varios servidores e ademais pódese distribuír a carga de procesamento entre eles.

Esta flexibilidade da estructura dos datos e a capacidade de escalado horizontal fan dos sistemas NoSQL unha opción idónea para a explotación de datos con consideración de Big Data.
# Hadoop
Hadoop é unha plataforma opensource con licencia de código aberto de Apache pensada para:
- O almacenamento e procesamento de elevados volumes de datos.
- Ser capaz de traballar con datos sen importar a súa tipoloxía, sexan estes estruturados ou non estruturados.
- Ser despregada en entornos distribuídos de fácil escalado e tolerante a fallos.

Ademáis Hadoop presentase como unha solución que pode ser despregada en hardware "commodity", esto é, hardware genérico que non ten porque ser especializado. Esto non quere decir que o costo sexa baixo en moitos casos.

Podemos ver que Hadoop comparte algunhas das características que xa vimos coas solucións NoSQL de escalabilidade horizontal e capacidade de procesamento de datos desestructurados, pero Hadoop é unha solución moito máis flexible.

Esto é porque **Hadoop é unha plataforma**. Esto quere decir que é unha base sobre a que se desarrollan aplicacións adicionales que fan que sobre Hadoop existan unha gran cantidade de ferramentas capaces de atender a múltiples necesidades e propósitos. Estas ferramentas son as que conforman o denominado **Ecosistema Hadoop**.

Esta flexibilidade de Hadoop é a que se diferencia das solucións NoSQL anteriores, que están diseñadas para satisfacer un único propósito. 

Para esto Hadoop compleméntase con outros compoñentes que conforman o denominado Ecosistema Hadoop, que sirven a múltiples propósitos. Se nos centramos exclusivamente en sistema de almacenamento Hadoop pode ser empregado como base para distintos tipos e motores:
- Bases de datos Clave-Valor con Apache HBase
- Bases de datos columnares con Apache Casandra
- Bases de datos SQL para OLAP con Apache Hive e OLTP con Apache Phoenix
- Bases de datos multidimensionales con Apache Kylin