---
tags:
  - linux
  - utilidades/openldap
---
En este documento vamos a ver os comandos básicos que podemos utilizar á hora de administrar un servidor [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Qué é?|OpenLDAP]].
# Agregar entradas
Á hora de agregar entradas en OpenLDAP debemos crear un fichero [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Ficheros LDIF|LDIF]] que contendrá os datos que queremos añadir. O comando é o seguinte:
```bash
ldapadd -x -D "cn=Manager,dc=jano,dc=local" -W -f fichero.ldif
```

A sintaxis de este comando é a seguinte:
- `-x`: Modo simple sin autenticación SASL.
- `-D`: Especifica o DN (Distinguished Name) do usuario administador.
- `-W`: Solicita a contraseña do usuario administrador.
- `-f` Indica o fichero LDIF que contén a entrada LDAP.

Alternativamente, tamén podemos utilizar o seguinte comando:
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f archivo.ldif
```

A sintaxis de este comando é a seguinte:
- `-Y EXTERNAL`: Indica que se vai utilizar autenticación externa a través do usuario do sistema.
- `-H ldapi:///`: Especifica que se vai utilizar o protocolo LDAPI para a conexión.
- `-f`: Indica o fichero LDIF que contén a entrada LDAP.

Este comando debemos utilizalo nun dos seguintes casos:
- Cando esteemos no mesmo servidor onde se executa OpenLDAP.
- Cando o servidor LDAP está configurado para permitir a autenticación externa.
# Modificar unha entrada
Se queremos modificar unha entrada debemos crear un fichero que contendrá os cambios que queiramos facer. Por exemplo se queremos modificar un usuario que teñamos creado no sistema creamos o seguinte fichero LDIF:
```ldif
dn: uid=panchoperro,ou=Perros,dc=jano,dc=local
changetype: modify
replace: uidNumber
uidNumber: 2001
```

Este fichero o que fai é na entrada do usuario `uid=panchoperro,ou=Perros,dc=jano,dc=local` modifica o número de uid. Para aplicar este cambio utilizamos o seguinte comando:
```bash
ldapmodify -x -D "cn=Manager,dc=jano,dc=local" -W -f archivo.ldif
```

Tamén podemos añadirlle máis valores a unha entrada existente creamos o seguinte fichero:
```ldif
dn: uid=panchoperro,ou=Perros,dc=jano,dc=local
changetype: modify
add: mail
mail: pancho@perro.com
```

Este fichero o que fai é añadir a entrada mail na entrada da base de datos `uid=panchoperro,ou=Perros,dc=jano,dc=local` e unha vez que añade ese campo ponlle o valor de `pancho@perro.com`.
# Eliminar unha entrada
Se queremos eliminar unha entrada en OpenLDAP utilizamos o comando `ldapdelete`. A sintaxis de este comando é a seguinte:
```bash
ldapdelete -x -D "cn=Manager,dc=jano,dc=local" -W "uid=panchoperro,ou=Perros,dc=jano,dc=local"
```

A sintaxis de este comando é similar a todas as anteriores:
- `-x`: Modo simple sin autenticación SASL.
- `-D`: Especifica o DN (Distinguished Name) do usuario administador.
- `-W`: Solicita a contraseña do usuario administrador.
- `"uid=panchoperro,ou=Perros,dc=jano,dc=local"`: O DN da entrada que queremos eliminar.
