---
tags:
  - linux
  - openldap
---
# Qué é?
Un schema en [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Qué é?|OpenLDAP]] define a estructura e as reglas dos datos que se poden almacenar en un directorio LDAP. É similar a un esquema en unha base de datos relacional, onde se especifican os tipos de datos, relacions e restriccions das tablas. En LDAP, un schema define o seguinte:
- **Atributos**: Os diferentes tipos de datos que poden ser almacenados no directorio.
- **Objetos de clase (object classes)**: Agrupacións de atributos que definen o tipo de entradas (obxectos) que poden existir no directorio.
- **Sintaxis**: Especifica o formato e a naturaleza dos valores dos atributos.
- **Reglas de correspondencia (matching rules)**: Define cómo comparar valores de atributos durante as búsquedas e operacions en LDAP.
# Archivos de schemas en OpenLDAP
Os schemas están definidos en ficheros coa extensión `.schema` que é a extensión vella e a nova maneira de definilos é mediante ficheros `.ldif` e podense encontrar en un dos siguientes directorios:
- **/etc/ldap/schema**: En distribucións **Debian**.
- **/etc/openldap/schema**: En distribucións **RHEL**.

Un exemplo de un de estos ficheros sería o seguinte:
```schema
attributetype ( 2.5.4.3 NAME 'cn'
    DESC 'Common Name'
    EQUALITY caseIgnoreMatch
    SUBSTR caseIgnoreSubstringsMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.15{64} )

objectclass ( 2.5.6.6 NAME 'person'
    DESC 'RFC2256: a person'
    SUP top STRUCTURAL
    MUST ( sn $ cn )
    MAY ( userPassword $ telephoneNumber $ seeAlso $ description ) )
```
## Componentes principais
1. **Atributos (atributes)**:
	- Son as unidades básicas de información en LDAP. Cada atributo ten un nombre e un tipo de dato asociado.
	- Exemplo: "cn" (common name), "main" (correo electrónico).
1. **Clases de objeto (Object Classes)**:
	- Son definicións que agrupan un conxunto de atributos baixo un nombre común, describindo o  tipo de obxeto que pode ser almacenado no directorio LDAP.
	- Exemplo: A clase do obxeto "inetOrgPerson" inclúe atributos como "cn", "sn", "mail", etc.
2. **Sintaxis (syntaxes)**:
	- Define o tipo de datos que pode almacenar un atributo, como cade ade caracteres, número, fecha, etc.
	- Exemplo: "Directory string", "Integer".
3. **Reglas de correspondencia (matching rules)**:
	- Especifican cómo se comparan os valores dos atributos durante as operacions de búsqueda.
	- Exemplo: "caseIgnoreMatch" para comparar cadenas ignorando maiúsculas e minúsculas.
## Carga e Xestión dos Schemas
Os schemas poden cargarse no servidor durante a configuración inicial ou agregarse dinámicamente. Por exemplo se queremos cargar un dos schemas básicos utilizamos o seguinte comando:
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/cosine.ldif
```

Podemos listar os schemas que temos cargados co seguinte comando:
```bash
ldapsearch -Y EXTERNAL -H ldapi:/// -b cn=schema,cn=config dn
```

No caso que queiramos eliminar un schema (esto é unha tarefa delicada). Utilizamos os seguintes comandos.

Identificamos o DN correspondiente ao schema que desexamos eliminar. Algo parecido a `cn=schemaName,cn=schema,cn=config`.
```bash
ldapsearch -Y EXTERNAL -H ldapi:/// -b cn=schema,cn=config -LLL
```

Unha vez temos o DN podemos eliminar o schema utilizando `ldapdelete`.
```bash
ldapdelete -Y EXTERNAL -H ldapi:/// "cn=schemaName,cn=schema,cn=config"
```

Os schemas comúns en OpenLDAP son:
- **core.schema**: Contén definicións básicas e esenciales, como "person", "organizationalUnit".
- **inetorgperson.schema**: Añade atributos e clases de obxeto para manexar información de personas nun entorno de internet, comúnmente utilizado para información de contacto.
- **cosine.schema**: Define atributos e clases de obxeto adicionales relacionados con aplicacións de rede.
- **nis.schema**: Este schema sirve para garantizar a interoperabilidade co sistema NIS.
