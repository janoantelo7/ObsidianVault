---
tags:
  - big_data
---
Casi todos os sistemas de información necesitan dar persistencia os datos cos que se traballan. Para esto utilizanse sistemas de almacenamento de datos, que poden ser algo tan sencillo como un simple archivo na misma máquina onde se ejecutan ou un gestor de base de datos en un servidor remoto ou incluso un clúster formado por varias máquinas. 

Hai múltiples tipos de sistemas de almacenamiento de datos atendendo aos distintos tipos de clasificacións, pero neste caso aplicado ao _Big Data_ centrar nos seguintes tipos:
- **Según o tipo de procesamento dos datos**: Dependendo do tipo de consultas que fan e das características que precisan cumplir as transaccións as que teñen que dar soporte. Podemos clasificalos en:
	- **Sistemas OLTP (On-Line Transaction Processing)**: Sistemas diseñados para ser capaces de responder a consultas de selección de elevados volumenes de datos e nos que o procesamento de transaccións é máis secundario.
	- **Sistemas OLAP (On-Line Analytical Processing)**: Sistemas diseñados para ser capaces de responder a consultas de selección de elevados volumenes de datos e nos que o procesamento de transaccións é máis secundario.
- **Segundo a forma en que se almacenan os datos**:
	- **Bases de datos relacionales**: O almacenamento "clásico", basase en tablas entre as que podemos definir relacións e nas que os datos almacénanse e organízanse en forma de filas. Estas utilizan a linguaxe SQL para a administración e para a explotación dos datos.
	- **Bases de datos NoSQL**: Que utilizan mecanismos de almacenamiento que non está baseado en tablas e filas do clásico modelo relacional, ademáis de non utilizar a linguaxe SQL como linguaxe principal de consulta. Aínda así algunhas dan compatibilidade para SQL.
- **Segundo a tipología dos datos que son capaces de almacenar**: Con esto referimonos á capacidade de estos datos de encaixar en estructuras fijas de almacenamiento segundo a súa naturaleza.
	- **Datos estructurados**: Son os que utilizan un formato estándar de organización dos datos, que fai que a forma de acceder a eles sexa sempre igual e predecible, o que fai que sexan máis sencillos de manejar. Utilizan estructuras en forma de tabla para almacenar os datos. Son os que utilizan as bases de datos relacionales e ficheros de texto como un CSV.
	- **Datos non estructurados**: Son os que pola súa naturaleza non se poden almacenar en estructuras de almacenamento estándar, o que os convirte nos máis dificilmente manexables. Algúns destos datos non estructurados son: Imágenes, vídeos, sonidos, archivos PDF, datos de redes sociales...
	- **Datos semiestruturados**: Son os que están a medio camiño entre os anteriores, xa que poden adaptar parcialmente a estructuras de almacenamiento estándar pero poden ter parte de esta estructura variable ou incluso estar composos parcialmente de datos non estructurados. Algúns ejemplos destos son: Correos electrónicos, ficheros de linguajes de marcas (JSON, XML, BSON...).
# Sistemas de análisis e operacionales
No ámbito de [[00 - Introducción ao Big Data#^79b429|Big Data]] é fundamental distinguir entre os **sistemas operacionales** e os **sistemas de análisis**, xa que cumplen funcións complementarias dentro do ecosistema de gestión e explotación dos datos.
## Sistemas opreacionales e procesamento OLTP
No análisis de datos chámase sistemas opreacionales os que **dan soporte a operativa diaría dunha organización**. Algúns exemplos son:
- Aplicación de gestión de personal e nóminas dun departamento de Recursos Humanos.
- Aplicación de facturación dun departamento de ventas.
- Tienda online de calquer tipo de negocio.
- Gestión de citas dun sistema público de sanidade.

Algo que caracteriza os sistemas operacionales é a súa **potencial criticidade** dependendo do proceso de negocio o que den soporte, xa que **un fallo que implique que non estea disponible pode sopoñer unha parada na actividade da organización cun posible impacto económico**.

Os sistemas opreracionales na súa maior parte utilizan **sistemas de procesamento de datos tipo OLTP (On-Line Transaction Processing)**, que se caracterizan por:
- Búscase facilitar e administrar transaccións, que poden estar formadas por varios procesos que se ejecutan de forma ordenada.
- Este tipo de sistemas a nivel de base de datos fan **opreacións tanto de lectura e escritura que afectan a volumes de datos reducidos**.
- Utilizan **bases de datos relacionales E/R normalizadas**.
## Sistemas de análise
Un **sistema de análise** é aquel que se utiliza para **examinar e interpretar grandes volumes de datos**, co obxectivo de **obter coñocemento útil e apoiar a toma de decisións**.

A diferencia dos sistemas operacionales, que gestionan as operacións diarias, os sistemas de análise traballan con **datos históricos e agregados**, permitindo realizar **consultas complexas**, **comparacións e visualizacións**.

Pola súa utilidade este tipo de sistemas utilizanse en multitude de organizacións de ámbitos moi distintos. Imos poñer algúns exemplos:
- **No ámbito empresarial**: Estos sistemas pódense utilizar en toma de decisións co fin de mellorar a productividade, incrementar os márgenes de beneficios, ganar en competitividade, obter melloras generales no funcionamento da empresa e as condicións de traballo...
- **No ámbito científico**: Utilizanse entre outras cousas para atopar patróns de datos. Un exemplo é o que se fai en medicina para determinar a posibilidade de desarrollar determinadas enfermedades en base o estudio de determinados comportamentos, hábitos ou por ter uns genes determinados.
- **Na administración pública**: Pode utilizarse para mellorar os servicios e buscar formas de aforrar cartos. Un exemplo é o que fai a axencia tributaria para detectar posibles patróns de fraude e así centrar os esforzos de investigación en casos nos que haxa máis posibilidades de atopar algo.

Aínda que non se aplica en todos os sistemas de análisis, nalgúns destos utilizase un sistema de procesamento de datos OLAP, que se caracteriza por:
- A gestión das transaccións é un aspecto secundario, porque as escrituras fanse de forma programada.
- A nivel de base de datos están diseñados para optimizar as **operacións de lectura de grandes volumes de datos**.
- Dentro destos encaixan os que chamamos **sistemas analíticos**.
- No caso de utilizar bases de datos relacionales estas diseñanse seguindo os principios do modelado dimensional.
- Polo seu uso analítico **almacenan información histórica**.

Nos sistemas de análisis basados en OLAP utilizase o concepto de **[cubo OLAP](https://es.wikipedia.org/wiki/Cubo_OLAP)** para referise a que os datos almacénanse nun vector multidimensional onde cada dimensión representa unha das entidades polas que podemos facer os nosos estudios analíticos. Cada intersección de eixes neste cubo correspóndese cunha combinación de valores de cada unha das dimensión que da lugar ás medidas que se utilizarán para medir o proceso de negocio.

Hai varias implementacións de almacenamento en cubos OLAP que poden clasificarse nos seguintes tres tipos:
- **ROLAP (Relational OLAP)**: Utiliza un **motor de base de datos relaciona** para o almacenamento. Estos sitemas requieren un tipo de modelado particular.
- **MOLAP (Muldimensional OLAP)**: Utilizan un **motor de bases de datos multidimensional** para o almacenamento. Esos sitemas utilizan mecanismos nos que os datos precalcularonse para mellorar o tempo de resposta.
- **HOLAP (Hybrid OLAP)**: Emprega o mesmo tempo un motor relacional e un multidimensional para almacenar os datos.

Aínda que **hai sistemas de análise que non utilizan tecnologías OLAP tradicionales**, en estes, **siguen utilizandose os terminos de dimensións e medidas** como concepto lógico, entre outras cousas pola súa facilidade para integrarse en ferramentas de visualización e BI.
## Big Data en sistemas opreacionales e de análisis
No contexto actual, os **sistemas de almacenamiento e procesamento Big Data** converteronse nun elemento esencial nos sistemas de información pola súa capacidade para **almacenar, procesar e analizar volumes de información**.

Estas características dos sistemas Big Data encaixan mellor coas necesidades analíticas que coas transaccionais. Así no seu uso máis común a súa relación cos sistemas opreacionais e de análisis é a siguiente:
- Os sistemas operacionales **generan e alimentan os datos** que se almacenan na plataforma Big Data
- Os **sistemas de análisis** utilizan as súas capacidades de **almacenamiento e procesamiento** dos sistemas Big Data para **transformar os datos en información útil**.

Aínda así o papel do Big Data nos operacionales non é exclusivo de servir de destino dos seus datos para análisis, e veremos que úsanse en sistemas opreacionales cando é necesario **procesar grandes volumes de datos en tempo real** para **tomar decisións automáticas e inmediatas**. Algúns ejempls son:
- **En comercio electrónico**:
	- Generar recomendacións de compra mentres o usuario navega
	- Adaptar os precios segundo o comportamiento actual
- **Banca**:
	- Monitorización de transaccións en tempo real
	- Detectar patróns sospeitosos de fraude e bloquear operacións de forma automática
- **IoT e sensores industriales**:
	- Monitorización constante dos sensores que generan datos de forma continua
	- Axustar o comportamiento das máquinas e lanzar alertas ante fallos
- **Mobilidade e transporte**:
	- Gestionar en tempo real a posición dos vehículos e solicitudes de usuarios
	- Calcular rutas óptimas e tempos estimados de chegada
# Arquitecturas para sistemas de análisis
Aínda que é posible traballar directamente cos datos no seu origen, os sistemas de análisis constrúense sobre un repositorio de datos.

Inicialmente este repositorio separado para as tarefas de análisis de datos era o denominado **Enterprise Data Warehouse** (EDW). Co paso do tempo e a aparición de necesidaes analíticas de datos máis complejos apareceron outros tipos de repositorios como son o **Data Lake** e o **Data Lakehouse**.

Todos estes caracterízanse por:
- **Integrar datos de diferentes sistemas nun único repositorio**: Dentro da organización existen múltiples sistemas que contan con información con interés analítico e esta integración nun mismo repositorio facilita a combinación de datos de todos eles.
- **Ter toda ou gran parte da información histórica da organización**: Moitos sistemas operacionales requieren o archivo da información histórica por motivos de optimización. Estes repositorios proporcionan a capacidade de almacenar esta información para seguir tendo a posibilidade de seguir explotándoa con fins analíticos.
- **Unha vez feita a carga son repositorios illados dos operacionales**: Esto implica que as tareas de análisis non terán impacto no día a día dos sistemas opreacionales. Hai que ter en conta que os sistemas de análisis basanse en consultas de elevados volumes de datos que de facelos nun operacional poden comporometer o seu correcto funcionamento. É por eso que as cargas nestos repositorios suelen facerse en horas de baixa carga do opreacional para afectar o menos posible ao seu funcionamento.
