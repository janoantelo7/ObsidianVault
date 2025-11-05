---
tags:
  - openldap
  - linux
---
# Qué son?
Os **módulos** en [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Qué é?|OpenLDAP]] son extensions que permiten ampliar a funcionalidade do servidor. Estos módulos ofrecen soporte adicional, como novos [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Backends|backends]], [[Apuntes/Servicios/OpenLDAP/01 - Introducción#Overlays|overlays]] e outras características. Os exemplos de módulos comúns son:
- `back_bdb`: Backend basado en BerkleyDB.
- `back_hdb`: Backend xerárquico (tamén basado en BerkleyDB).
- `back_mdb`: Backend basado en LMDB.
- `ppolicy`: Módulo para políticas de contraseñas.
# Carga de módulos
Os módulos carganse dinámicamente mediante o uso de ficheros LDIF. En este fichero definimos o módulo que vamos a cargar da seguinte maneira. 

Exemplo para cargar o módulo de `ppolicy`:
```ldif
dn: cn=module{0},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: ppolicy.la
```

Unha vez definido  este fichero, cargamos o modulo co seguinte comando:
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f ppolicymodule.ldif
```

Podemos ver todos os módulos que temos cargados co seguinte comando:
```bash
ldapsearch -Y EXTERNAL -H ldapi:/// -b "cn=module{0},cn=config"
```


