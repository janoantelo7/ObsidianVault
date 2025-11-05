---
tags:
  - utilidades/openldap
---
Á hora de traballar con usuarios e grupos en [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Qué é?|OpenLDAP]] utilizaremos os ficheros [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Ficheros LDIF|ldif]] para crear os nosos obxectos. Definiremos un elemento por fichero, pero podemos definir cantos queiramos. Por exemplo, no fichero das unidades organizativas podríamos definir vairas.
# Unidades Organizativas
Para crear as unidades organizativas creamos un fichero ldif chamado `ou.ldif`, por exemplo. Que será onde definiremos as nosas unidades organizativas. O contido de este fichero será o seguinte:
```ldif
dn: ou=Perros,dc=jano,dc=local
objectClass: top
objectClass: organizationalUnit
ou: Perros
```

Cargamos os datos de este fichero no noso servidor LDAP co comando `ldapadd`:
```bash
ldapadd -x -D 'cn=Manager,dc=jano,dc=local' -W -f ou.ldif
```

Se queremos borrar a unidad organizativa que acabamos de crear podemos simplemente utilizar o seguinte comando:
```bash
ldapdelete -x -D 'cn=Manager,dc=jano,dc=local' -W 'ou=Perros,dc=jano,dc=local'
```

Podemos buscar as unidades organizativas cos seguintes comandos:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(objectClass=organizationalUnit)"
```

Se queremos buscar unha unidad organizativa en concreto utilizamos:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(ou=Perros)" +
```
# Grupos
A continuación, vamos ver como podemos crear un grupo dentro de unha unidad organizativa. Para esto creamos un fichero chamado `grupo.ldif`:
```ldif
dn: cn=Jefes,ou=Perros,dc=jano,dc=local
objectClass: top
objectClass: posixGroup
gidNumber: 2000
cn: Jefes
```

Unha vez definido os grupos que queremos crear podemos aplicalos co seguinte comando:
```bash
ldapadd -x -D 'cn=Manager,dc=jano,dc=local' -W -f grupo.ldif
```

Á hora de borrar o grupo empregamos o seguinte comando:
```bash
ldapdelete -x -D 'cn=Manager,dc=jano,dc=local' -W 'cn=Jefes,ou=Perros,dc=jano,dc=local'
```

Para buscar todos os grupos utilizamos o seguinte comando:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(objectClass=posixGroup)"
```

Se queremos buscar un grupo en concreto utilizamos:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(cn=Jefes)" +
```
# Usuarios
Igual que creamos unidades organizativas e grupos, para crear usuarios creamos un fichero ldif cos datos dos usuarios que queremos crear no sistema. A contraseña do usuario podemos generala co comando de `slappasswd`:
```ldif
dn: uid=Pancho,ou=Perros,dc=jano,dc=local
objectClass: top
objectClass: posixAccount
objectClass: inetOrgPerson
objectClass: person
cn: pancho
uid: panchoperro
uidNumber: 2000
gidNumber: 2000
homeDirectory: /home/pancho
loginShell: /bin/bash
userPassword: {SSHA}434fdasfe43Ff45r4--4!VRG23
sn: Perro
mail: pancho@panchoperro.com
givenName: Pancho
```

Se queremos crear estos usuarios no servidor utilizamos igual que para o resto de elementos o seguinte comando:
```bash
ldapadd -x -D 'cn=Manager,dc=jano,dc=local' -W -f usuarios.ldif
```

Para eliminar un usuario podemos aplicar o siguiente comando:
```bash
ldapdelete -x -D "cn=Manager,dc=jano,dc=local" -W "uid=pancho,ou=Perros,dc=jano,dc=local"
```

Podemos listar todos os usuarios co seguinte comando:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(objectClass=posixAccount)"
```

Se polo contrario queremos mostrar só un usuario podemos utilizar o seguinte comando:
```bash
ldapsearch -x -LLL -b "dc=jano,dc=local" "(uid=panchoperro)"
```

