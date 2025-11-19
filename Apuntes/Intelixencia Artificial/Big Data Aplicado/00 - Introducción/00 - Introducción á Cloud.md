---
tags:
  - big_data
  - cloud
---
Con Cloud referimonos a software que utilizamos a través de Internet, que está aloxado en servidores remotos. Dentro do concepto Cloud diferenciamos dous tipos:
- Cloud para uso personal
- Cloud para infraestructura tecnolóxica
## Segundo o seu tipo
### Cloud para uso personal
Con personal non falamos só das que se utilizan a nivel personal, senon tamén poden ser utilizadas a nivel profesional, pero sempre son ferramentas que empregamos nun ordenador de escritorio, portátil, tablet ou smartphone.

Dentro de estas aplicacións podemos destacar os seguintes exemplos:
- **Almacenamiento**: Ferramentas que nos permiten gardar datos en servidores remotos e compartir archivos entre distintos dispositivos e con outras personas, como son: Google Drive, OneDrive, Dropbox...
- **Suites ofimáticas**: Ferramentas que a maiores de poder ser utilizadas en local, tamén se poden utilizar en un navegador e facilitan a colaboración como: Office 365 e Google Docs.
- **Comunicacións e conferencias**: Coas que poder facer chamadas de voz, videochamadas e conferencias como: Google Meet, Microsoft Teams.
- **Software de productividade**: Aplicacións nas que generar notas, documentación, gestión de tareas. Exemplos: Notion, Evernote...
- **Videoxogos**: Plataformas que nos permiten xogar sen ter que invertir en videoconsolas ou nun PC gaming como son: Geforce Now, Xbox Cloud Gaming.
### Cloud para infraestructura tecnolóxica
En este tipo falamos de solucións cloud con un ámbito de uso a nivel de infraestructura tecnolóxica dunha empresa. En este caso referimonos ao seguinte:
- **Servidores**: Físicos e virtuales onde teremos montados diferentes aplicacións como servicios de directorio, servidores web, servidores de correo, Firewalls...
- **Redes**: Infraestructura como routers, switches...
- **Almacenamento**: Cabinas de discos, dispositivos NAS... que utilizan algún tipo de configuración RAID con redundancia para o almacenamento dos datos.
## Infraestructura Cloud e infraestructura On-premises
### Infraestructura On-premises
É a infraestructura que temos físicamente nas instalacións dunha empresa, o cal implica que son administrados na súa totalidade pola organización. Estos servicios suelen estar alojados en CPDs (Centro de procesamento de datos) ou Data Centers (Centros de datos), que dependendo do volume que precisen pode ser un simple armario Rack ou varios armarios Rack en unha sala independiente.
#### Ventajas
- Total control sobre a infraestructura.
- Os datos da organización non están aloxados en sistemas de terceros.
- Custos en infraestructura máis previsibles.
- Latencia baixa e mellor rendemento xa que os datos están na mesma rede local que os equipos de traballo.
#### Desventajas
- Necesita un espacio dedicado.
- Hai que facer unha gran inversión inicial.
- Requiere definir un plan de continxencia para o caso de fallo do CPD.
- Obsolescencia do hardware e software.
### Infraestructura Cloud
Na infraestructura Cloud os servicios están localizados na nube, no CPD dunha empresa que presta este servicio utilizando sistemas de pago por uso. 

O sistema de pago por uso implica que se pagará máis ou menos en función de:
- **A cantidade de horas que fagamos uso dos recursos**: Canto máis tempo máis se paga, por eso, é habitual implantar mecanismos de liberación de recursos en horarios de baixa carga.
- **O dimensionamento dos recursos contratados**: Pagamos máis cantos máis servicios e/ou recursos de hardware para estes servicios contratemos.

Hai unha gran variedad de servicios de Cloud que podemos contratar, os cales os podemos categorizar nas seguintes categorías:
- **Infraestructura como Servicio (IaaS)**: Ofrece recursos básicos de hardware.
	- _Máquinas virtuais (VMs)_: Instancias configurables con CPU, memoria e rede (EC2 en AWS, [[01 - Máquinas Virtuales#Máquinas virtuales en Azure (IaaS)|Azure VM]] en Azure, Compute Engine en GCP).
	- _Almacenamento en bloque_: Discos persistentes conectados ás VMs (Amazon EBS, Azure Disk Storage).
	- _Redes virtuais_: Configuración de subredes, balanceadores, IPs elásticas, VPNs (AWS VPC, Azure Virtual Network).
	- _Balanceadores de carga_: Distribúen o tráfico entre servidores (AWS ELB, Azure Load Balancer).
- **Plataforma como Servicio (PaaS)**: Ofrece un entorno de execución para aplicacións sen gestionar a infraestructura subyacente.
	- _Servicios de bases de datos gestionadas_: Amazon RDS, Azure SQL Database, Cloud SQL.
	- _Servicios de análise e Big Data_: Amazon EMR, Azure HDInsight, Dataproc.
	- _Servicios de integración e colas de mensaxes_: AWS SQS, Azure Service Bus,  Pub/Sub.
	- _Servicios de aplicacións web_: AWS Elastic Beanstalk, Azure App Service, Google App Engine.
- **Software como Servicio (SaaS)**: Aplicacións completas accesibles dende o navegador, sen gestionar infraestructura.
	- _Correo electrónico e colaboración_: Microsoft 365, Google Workspace.
	- _CRM / ERP en línea_: Salesforce, SAP Cloud.
	- _BI e analítica_: PowerBI, Looker, Tableau Cloud.
- **Outros servicios especializados**
	- _Contenedores e orquestación_: Docker, Kubernetes (EKS, AKS, GKE).
	- _Servicios sen servidor (serverless)_: AWS Lambda, Azure Functions, Cloud Functions.
	- _Inteligencia artificial e machine learning_: AWS SageMaker, Azure ML, Vertex AI.
	- _Servicios de almacenamiento de objetos_: S3, Azure Blob Storage, Cloud Storage.
	- _Servicios de seguridade e monitorización_: CloudWatch, Azure Monitor, Stackdriver.
#### Ventajas
- **Facilidade de escalado**: Se temos un servicio que se nos queda pequeno podemos aumentar a capacidade de computo con facilidade, iso si co seu correspondente incremento no prezo.
- **Gran variedade de servicios**: Podemos contratar máquinas virtuais completas que personalizamos totalmente ata servicios individuais como unha base de datos ou un servidor web.
- **Velocidade de implementación**: Montar un servicio leva moito menos tempo, empregando os asistentes e plantillas de contornas preconfiguradas que ofrecen as plataformas Cloud.
- **Non hai que facer plans de continxencia**, nin de seguridade nin de actualización de software e hardware, porque é algo que xa forma parte do servicio que contratas.
- **Non hai que facer un gasto por adiantado grande**: Pagamos polo que empregamos dende o principio sen ter que facer unha gran inversión para poñer en marcha a infraestrutura
#### Desventajas
- **Gasto continuado e perigro de cargos adicionais**: Inesperados por unha mala gestión.
- **Solucións menos flexibles**: En situacións onde necesitamos un nivel de personalización máis grande dos servicios que queremos contratar.
- **Dependencia do proveedor**: Que pode ser un problema se queremos facer un cambio nun momento dado a outro proveedor ou intrafestructura on-premises.
- **Total dependencia da conexión a Internet**
- **Latencia alta e peor rendemento** ca se os comparamos cunha rede local.
- **Os datos xa non están an empresa**: O cal a parte da potencial preocupación de cedelos a terceiros poden supoñer problemas legales polas leyes europeas.
## Infraestructura en Cloud de almacenamento
| Tipo de datos                          | AWS                                       | Azure                                             | Google Cloud                       |
| -------------------------------------- | ----------------------------------------- | ------------------------------------------------- | ---------------------------------- |
| Base de datos relacionales             | Amazon RDS                                | Azure SQL Database                                | Cloud SQL                          |
| Bases de datos baseadas en obxectos    | Amazon S3                                 | Azure Blob Storage, Azure Data Lake Storage Gen2  | Cloud Storage                      |
| Almacenamiento para máquinas virtuales | Amazon EBS                                | Azure Disk Storage e Azure File Storage           | Pesisten Disk                      |
| Almacenamento de datos a longo plazo   | Amazon Glacier                            | Azure Blob Storage - Archive Tier<br>Azure Backup | Cloud Storage - Archive y Coldline |
| Big Data                               | Amazon EMR                                | Azure HDInsight<br>Azure Data Lake Storage        | Dataproc e BigQuery                |
| NoSQL                                  | Dynamo DB<br>Amazon Keyspaces (cassandra) | Azure Cosmos DB                                   | Firestore<br>Bigtable              |
