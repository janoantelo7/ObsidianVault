---
tags:
  - linux
  - openldap
---
# Qué é?
OpenLDAP é unha implementación de código aberto do protocolo LDAP (Lightweight Directory Access Protocol), que se utiliza para acceder e xestionar servizos de directorios. OpenLDAP permite a creación, modificación e consulta de entradas nun directorio, facilitando a administración centralizada de usuarios, contrasinais, permisos e outros recursos nunha rede. É amplamente utilizado en empresas e organizacións para autenticar e autorizar usuarios, así como para xestionar información de configuración e recursos compartidos.
# Glosario e Arquitectura
## Servidor LDAP (slapd)
**slapd** é o proceso principal do servidor OpenLDAP. É o responsable de manexar as solicitudes dos clientes, xestionar as operacións de búsqueda, modificación, adición e eliminación de entradas no directorio. Hai dúas maneiras de configuralo:
- **slapd.conf**: Esta maneira está camiño de ser deprecada.
- **slapd-config**: Esta é a maneira actual de configurar o servidor e está basada en un sistema de configuración que se aplica dinámicamente en tempo de ejecución.
## Backends
Os **backends** son módulos que definen cómo e donde se almacenan físicamente os datos do directorio. OpenLDAP soporta varios tipos de backends. Os tipos comuns de backends son:
- **hdb y bdb**: Utilizan a base de datos de Berkely DB. Son adecuados para grandes volúmenes de datos e ofrecen bo rendimiento de lectura e escritura. Actualmente están deprecated.
- **mdb**: É o backend predeterminado en versións máis recientes. Ofrece alto rendimiento e eficiencia no uso de memoria.
- **ldap**: Permitenos que o servidor actúe como proxy cara outro servidor LDAP.
- **passwd**: Accede aos ficheros de contraseñas do sistema.
## Esquemas (schemas)
Os **[[02 - Schemas#Qué é?|schemas]]** definen a estructura dos datos almacenados no directorio. Especifican os atributos e clases de objetos permitidos, asegurando que a información se almacene de maneira consistente e estructurada. Os componentes dos esquemas son os seguintes:
- **Clases de objetos**: Definen tipos de entradas, por exemplo; usuario, grupo, dispositivo.
- **Atributo**: Especifican propiedades asociadas ás clases de objetos, por exemplo; nombre, correo electrónico, número de teléfono.
- **Sintaxis e reglas de correspondencia**: Determinan o formato e cómo se comparan os atributos.
## Overlays
Os **[[04 - Overlays#Qué é?|overlays]]** son módulos que extenden a funcionalidad do servidor. Permiten añadir características adicionales e personalizar o comportamento do servidor. Alguns exemplos de overlays son:
- **accesslog**: Rexistra os cambios realizados no directorio para auditoría.
- **syncprov**: Proporciona sincronización entre múltiples servidores LDAP.
- **ppolicy**: Implementa políticas de contraseñas avanzadas.
- **memberof**: Mantén automáticamente atributos de pertenencia a grupos.
## Módulos
Os [[03 - Módulos#Qué son?|módulos]] en un servidor OpenLDAP son extensions que permiten ampliar a funcionalidade do servidor. Permiten que o servidor LDAP cargue compoñentes extras que non están integrados de forma predeterminada.
## Ficheros LDIF
Os ficheros LDIF (LDAP Data Interchange Format) son uns ficheros en texto plano que son utilizados para insertar, modificar ou eliminar entradas do directorio LDAP. 
## Módulos vs Overlays vs Schemas
| Característica    | Módulos                                                                                 | Schemas                                                        | Overlays                                            |
| ----------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------- |
| **Próposito**     | Extenden o servidor LDAP con novas funcionalidades dinámicas (backends, overlays, etc.) | Definen a estructura dos obxectos e atributos da base de datos | Modifican o comportamento do backend                |
| **Configuración** | Carganse dinámicamente e teñen o seu propio apartado                                    | Carganse sobre a configuración do sistema                      | Configuranse encima de unha base de datos existente |
| **Impacto**       | Añaden funcionalidades ao servidor                                                      | Definen como se organizan os datos                             | Modifican o comportamento da base de datos          |
# Instalación
No seguinte apartado vamos a explicar como instalar OpenLDAP en un servidor [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes|Centos]] ou RHEL. O primeiro paso que temos que facer é habilitar o paquete EPEL co seguinte comando.
```bash
dnf install epel-release epel-next-release
```

Unha vez temos EPEL habilitado, debemos instalar os seguintes paquetes para o seu funcionamento.
```bash
dnf install openldap-servers openldap-clients
```
- **openldap-servers**: Conten o daemon slapd e as ferramentas relacionadas.
- **openldap-clients**: Inclúe ferramentas para interactuar co servidor LDAP.

Ao acabar de instalar esos paquetes, o seguinte que facemos é habilitar o servicio no sistema de OpenLDAP.
```bash
systemctl enable --now slapd
```

Primeiro, temos que generar o hash da contraseña co seguinte comando.
```bash
slappasswd
```

Unha vez que temos o string da contraseña creamos o seguinte fichero (`vim chrootpw.ldif`) para aplicar a contraseña. Esta contraseña é a que está relacionada co usuario _root_ do directorio de configuración de OpenLDAP. É unha contraseña esencial para que os administradores poidan realizar cambios na configuración do servidor, utilizando ferramentas como `ldapmodify` ou `ldapadd`. 
```ldif
dn: olcDatabase={0}config,cn=config
changetype: modify
add: olcRootPW
olcRootPW: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxx
```

Aplicamos a configuración definida no fichero co seguinte comando.
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f chrootpw.ldif
```

Unha vez feito eso importamos os seguintes esquemas básicos.
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/cosine.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/nis.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/inetorgperson.ldif
```

Esos esquemas sirven para o seguinte:
- **cosine**: Este esquema proporciona unha serie de atributos e clases xenéricos, como usuarios, grupos e organizacións. Sirve como unha base sólida para construir directorios máis complexos.
- **nis**: Este esquema está diseñado para integrar OpenLDAP co servicio de información NIS. Permite almacenar información de NIS como usuarios, grupos e hosts.
- **inetorgperson**: Este esquema define atributos específicos para representar personas, como o nombre completo, dirección de correo electrónico, número de teléfono, etc. É moi utilizado para almacenar a información sobre os usuarios.

Ahora, creamos un fichero chamado `chdomain.ldif` que utilizaremos para definir o nombre de dominio, os accesos á base de datos, establecemos a contraseña e o nombre do usuario _root_  de ese dominio.
```ldif
dn: olcDatabase={1}monitor,cn=config
changetype: modify
replace: olcAccess
olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth"
  read by dn.base="cn=Manager,dc=jano,dc=local" read by * none

dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcSuffix
olcSuffix: dc=jano,dc=local

dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcRootDN
olcRootDN: cn=Manager,dc=jano,dc=local

dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcRootPW
olcRootPW: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxx

dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcAccess
olcAccess: {0}to attrs=userPassword,shadowLastChange by
  dn="cn=Manager,dc=jano,dc=local" write by anonymous auth by self write by * none
olcAccess: {1}to dn.base="" by * read
olcAccess: {2}to * by dn="cn=Manager,dc=jano,dc=local" write by * read
```

Aquí abaixo desgranamos o fichero e explicamos como funciona e que fai cada apartado de el:

```ldif
dn: olcDatabase={1}monitor,cn=config
changetype: modify
replace: olcAccess
olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth"
  read by dn.base="cn=Manager,dc=jano,dc=local" read by * none
```
Aquí modificamos o acceso á base de datos de monitoreo. Na línea olcAccess definimos quen pode leer os datos de monitoreo. Neste caso:
- **`gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth`**: Establecemos que os procesos do sistema root poden leer.
- **`cn=Manager,dc=jano,dc=local`**: O usuario administrador do dominio pode leer.
- **`* none`**: todos os demais usuarios non teñen acceso.

```ldif
dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcSuffix
olcSuffix: dc=jano,dc=local
```
En este apartado, establecemos o sufijo (o dominio) da base de datos principal. Ahora, a base de datos LDAP manexará as entradas baixo o dominio `dc=jano,dc=local`.

```ldif
dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcRootDN
olcRootDN: cn=Manager,dc=jano,dc=local

dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcRootPW
olcRootPW: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxx
```
Na primeira parte establecemos o Distinguished Name (DN) do administrador da base de datos, que neste caso será `cn=Manager,dc=jano,dc=local`. Na segunda parte, añadimos a contraseña de este usuario (`cn=Manager,dc=jano,dc=local`) en formato cifrado SSHA (aquí podemos aprobeitar o que generamos ao principio, ou generar outra co mismo comando de `slappasswd`).

```ldif
dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcAccess
olcAccess: {0}to attrs=userPassword,shadowLastChange by
  dn="cn=Manager,dc=jano,dc=local" write by anonymous auth by self write by * none
olcAccess: {1}to dn.base="" by * read
olcAccess: {2}to * by dn="cn=Manager,dc=jano,dc=local" write by * read
```
En esta parte do fichero, establecemos os accesos á base de datos. As reglas son as seguintes:
- A primeira regla establece o acceso ao atributo `userPassword` e `shadowLastChange`. Nela definimos que o usuario administador (`cn=Manager`) ten permisos de lectura. Os usuarios autenticados poden modificar a súa propia contraseña (`self write`). Os usuarios anónimos solo poden autenticarse e nadie máis ten acceso (`* none`).
- A segunda regla establece que calquer usuario pode leer a raíz do DN.
- A terceira regla establece que o administrador (`cn=Manager`) pode escribir en toda a base de datos, mentres que todos os demais poden leer.

Aplicamos a configuración definida en ese fichero co seguinte comando.
```bash
ldapmodify -Y EXTERNAL -H ldapi:/// -f chdomain.ldif
```

Como paso final, creamos un fichero chamado `basedomain.ldif` que utilizamos para definir e estructurar a base de datos LDAP inicial para o novo dominio, neste caso `dc=jano,dc=local`. 
```ldif
dn: dc=jano,dc=local
objectClass: top
objectClass: dcObject
objectclass: organization
o: Jano local
dc: jano

dn: cn=Manager,dc=jano,dc=local
objectClass: organizationalRole
cn: Manager
description: Directory Manager

dn: ou=People,dc=jano,dc=local
objectClass: organizationalUnit
ou: People

dn: ou=Group,dc=jano,dc=local
objectClass: organizationalUnit
ou: Group
```

A continuación desgranamos o fichero para explicar o que fai concretamente.

```ldif
dn: dc=jano,dc=local
objectClass: top
objectClass: dcObject
objectclass: organization
o: jano local
dc: jano
```
Este apartado, crea a entrada raíz do dominio. Nel definimos o seguinte:
- **dn: dc=jano,dc=local**: Este é o Distinguished Name (DN) da entrada raíz do dominio que se está creando.
- **objectClass: top**: É un `objectClass` obligatorio que debe estar presente en todas as entradas.
- **objectClass: dcObject**: Define que esta entrada é un dominio (`dc`).
- **objectClass: organization**: Indica que esta entrada tamén é unha organización.
- **o: jano local**: Espeficica o nombre da organización, en este caso, "jano local".
- **dc: jano**: Define a parte `dc=jano` do DN, indicando o nombre do dominio.

```ldif
dn: cn=Manager,dc=jano,dc=local
objectClass: organizationalRole
cn: Manager
description: Directory Manager
```
En este apartado, creamos a entrada para o administrador do dominio. 
- **dn: cn=Manager,dc=jano,dc=local**: Define o DN para o administrador do directorio.
- **objectClass: organizationalRole**: Este `objectClass` define a entrada como un rol dentro da organización, neste caso, "Manager".
- **cn: Manager**: O nome común (Common Name) deste rol é "Manager".
- **description: Directory Manager**: Unha descrición adicional indicando que esta entrada é para o "Director do Directorio".

```ldif
dn: ou=People,dc=jano,dc=local
objectClass: organizationalUnit
ou: People
```
Ahora creamos a unidad organizativa "People", que é onde típicamente se almacenan as entradas dos usuarios.
- **dn: ou=People,dc=jano,dc=local**: Define a unidad organizativa dentro do dominio.
- **objectClass: organizationalUnit**: Indica que esta entrada é unha unidad organizativa (OU).
- **ou: People**: Especifica o nombre de esta unidad organizativa.

```ldif
dn: ou=Group,dc=jano,dc=local
objectClass: organizationalUnit
ou: Group
```
En este apartado definimos a unidad organizativa "Group", onde típicamente se almacenarán os grupos.
- **dn: ou=Group,dc=jano,dc=local**: Define outra unidad organizativa llamada "Group".
- **objectClass: organizationalUnit**: Indica que esta entrada é unha unidad organizativa (OU).
- **ou: Group**: Especifica o nombre de esta unidad organizativa.

Aplicamos a configuración definida arriba co seguinte comando.
```bash
ldapadd -x -D cn=Manager,dc=jano,dc=local -W -f basedomain.ldif
```
