---
tags:
  - azure
---
# Roles
Os roles en Azure son un conxunto de permisos que se utilizan para controlar o que pode facer un usuario dentro de que recursos.

Polo que podemos definir os roles nos seguintes apartados que tamén nos axudarán á hora de definir roles:
- **Quen:** quen pode executar accions.
- **Que:** que accions pode executar.
- **Donde:** donde se poden realizar estas accións según o rol.

Existen dous tipos de roles:
- **Roles de Azure:** Estos roles controlan os permisos para gestionar recursos de Azure, como máquinas virtuales, bases de datos, etc. Por ejemplo, un usuario co rol de "Colaborador de máquina virtual" pode crear e administrar máquinas virtuales, pero non pode cambiar a configuración dunha rede virtual. Tamén é importante recalcar que estos roles teñen herencia polo que se lle asignamos un rol a un usuario nunha suscripción ese usuario terá permisos sobre os recursos de esa suscripción.
- **Roles de [[06 - Entra ID#Qué é Microsoft Entra ID?|Entra ID]]:**  Estos roles controlan permisos para  gestionar recursos dentro de Entra ID. Por ejemplo, un usuario co rol "Administrador de usuarios" pode crear, modificar e eliminar usuarios.

A definición de un rol ten a seguinte estructura:
```json
"Actions": [
	"*"
],
"NotActions": [
	"Auth/*/Delete"
],
"DataAction": [],
"NotDataActions": [],
"AssignableScopes": [
	"/"
]
```

A continuación explicamos cada sección:
* **Actions:** O apartado `actions` define as accions dentro do plano de control que permite o rol.
* **NotActions:** Este apartado é unha lista de accións que exculimos dos permisos que se definen en `actions`. Este apartado está por encima de `actions`.
* **DataAction:** Define as accións que permite o rol dentro do plano de datos.
* **NotDataActions:**  Este apartado define a lista de exclusións para as accións dentro do plano de datos.
* **AssignableScopes:** Este apartado define en que niveles de ámbito se pode asignar este rol. 
