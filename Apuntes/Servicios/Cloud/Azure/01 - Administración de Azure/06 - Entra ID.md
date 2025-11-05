---
tags:
  - azure
---
# Qué é Microsoft Entra ID?
_Microsoft Entra ID_ é un servicio de administración de identidades e acceso basado na nube. Cando falamos de identidades estamos a falar de: usuarios, aplicacións, etc.
# Tenants
Un **tenant** é a representación dixital da túa organización dentro dos servicios en nube de Microsoft. 

É un contenedor lógico e aislado que alberga todos os objetos da organización, como:
- **Usuarios e grupos**: As contas dos empleados e as agrupacións para gestionar permisos.
- **Aplicacións**: As túas aplicacións registradas (tanto de Microsoft como de terceiros).
- **Dispositivos**: Os PCs, portátiles e móviles que se registraron.
- **Licenzas e políticas**: A configuración de seguridad e acceso que define como interactúan os usuarios e os recursos.
# Usuarios e grupos
## Usuarios
Dentro de un [[#Tenants|tenant]] de Entra ID, cada usuario é un objeto de identidad que representa a unha persona e define seu acceso aos recursos da organización. As propiedades de cada usuario (como o nombre ou departamento) podense gestionar, e a nivel de API, manipulanse como objetos estructurados (similares a JSON).

Existen principalmente dous orígenes para os usuarios:
-   **Miembros:** Son usuarios nativos do tenant, que normalmente pertenecen á propia organización.
-   **Invitados:** Son usuarios externos que se invitan ao tenant para colaborar en recursos específicos, o que se conoce como colaboración B2B (Business-to-Business).

Para gestionar os permisos, tanto a miembros como a invitados podenselle asignar **[[#Roles|roles]]**. Un usuario con un rol administrativo asignado é o que comúnmente conocese como un **administrador**. Estos roles son os que conceden os permisos para realizar operaciones específicas dentro de Azure e Microsoft 365. 
## Grupos
Os **grupos de Entra ID** son coleccións de usuarios que facilitan a xestión de accesos e permisos en Microsoft Entra ID.

En lugar de asignar permisos individualmente a cada usuario, podense engadir a un grupo e despois asignar permisos a ese grupo. Deste xeito, calquera membro do grupo herdará os permisos asignados, o que simplifica enormemente a administración e a seguridade.

Hai dous tipos de grupos:
- **Grupos de seguridade:** son usados para administrar o acceso a recursos.
- **Grupos de Microsoft 365:** son usados para dar acceso a correo electrónico, calendario, ficheros, etc.

Podemos asignar usuarios aos grupos de distintas maneiras:
- **Asignados:** asignamos de maneira manual un usuario a un grupo.
- **Dinámicos:** o grupo ten unha regla de pertenencia que evalúa se un usuario de Entra ID a cumple para asignalo ao grupo. Esta regla pode ser, por exemplo, que se un usuario pertenece a un departamento o asigna a ese grupo.
