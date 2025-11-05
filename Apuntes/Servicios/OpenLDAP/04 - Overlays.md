---
tags:
  - linux
  - openldap
---
# Qué é?
Un **overlay** en OpenLDAP é un módulo que extende a funcionalidade do servidor LDAP. Actúa como unha capa adicional que pode modificar o comportamento predeterminado do servidor sen cambiar o código base do mismo. Os overlays utilizanse para agregar novas características, mellorar a seguridade, optimizar o rendemento ou aplicar políticas de control específicas.

Os overlays a menudo están documentados en unha páxina do manual de Linux, coa seguinte convención de nombres `slapo-<nombre_overlay>`.
# Tipos comúns de overlays
- **accesslog**: Garda un rexistro detallado das operacións realizadas na base de datos LDAP.
- **auditlog**: Similar ao accesslog, pero garda as entradas de modificación nun archivo de texto plano.
- **memberof**: Mantén automáticamente os atributos de pertenencia dun usuario nun grupo. Específicamente, actualiza o atributo `memberof` cando un usuario é añadido ou eliminado de un grupo.
- **syncprov**: Implementa a funcionalidade de sincronización de bases de datos entre servidores LDAP. É crucial para a replicación.
- **ppolicy**: Implementa políticas de contraseñas, como a lonxitude mínima, a expiración de contraseñas, o bloqueo de contas, etc.
- **unique**: Asegura que un atributo teña valores únicos en  toda a base de datos, como un identificador de empregado ou correo electrónico.
- **rwm (rewrite/remap)**: Permite reescribir e remapear os DN nas operacións LDAP.
# Creación overlays
Os overlays definense en formato `.ldif`. Un exemplo de configuración de un overlay `ppolicy` sería o seguinte:

Fichero `ppolicy_overlay.ldif`:
```ldif
dn: olcOverlay={0}ppolicy,olcDatabase={2}mdb,cn=config
changetype: add
objectClass: olcOverlayConfig
objectClass: olcPPolicyConfig
olcOverlay: {0}ppolicy
olcPPolicyDefault: cn=default,ou=Policies,dc=jano,dc=local
olcPPolicyHashCleartext: TRUE
olcPPolicyUseLockout: TRUE
```

Este overlay aplicamolo co seguinte comando:
```bash
ldapadd -Y EXTERNAL -H ldapi:/// -f ppolicy_overlay.ldif
```
## Estructura
En este apartado vamos a desgranar o fichero que utilizamos arriba de ejemplo para entender como se forman os overlays.

```ldif
dn: olcOverlay={0}ppolicy,olcDatabase={2}mdb,cn=config
```
Este é o apartado do Distinguished Name (DN) que identifica a configuración do overlay no servidor LDAP en este caso da `ppolicy`.
- **olcOverlay={0}ppolicy**:
	- **`olcOverlay`**: Indica que estamos definindo un overlay.
	- **`{0}`**: Este é o identificador numérico que indica que é o primeiro overlay configurado en esta base de datos. O número `{0}` utilizase para establecer o orden no que os overlays son procesados. Se houbese outros overlays aplicados a esta base de datos, tendrían números incrementales `{1}`, `{2}`, etc. Este número non é obligatorio pero sí que é unha boa práctica. 
	- **`ppolicy`**: É o nombre do overlay específico, neste caso, a política de contraseñas (Password Policy).
- **olcDatabase={2}mdb**:
	- **`olcDatabase`**: Esto especifica que o overlay aplicase a unha base de datos en particular.
	- **`{2}`**: Indica que este overlay está asociado coa terceira base de datos configurada no servidor, xa que a numeración de bases de datos empeza en **`{0}`**.
	- **`mdb`**: É o tipo de backend utilizado para esta base de datos. `mdb` é un dos backends comúns en OpenLDAP.
- **cn=config**:
	- Este é o contexto de configuración global de OpenLDAP, o que indica que esta configuración é parte da estructura de configuración dinámica de OpenLDAP.

No seguinte apartado, explico o contido do LDIF que se encarga de definir o overlay.
- **changetype: add**:
	- Indica que a operación LDIF está añadindo unha nova entrada ao servidor LDAP. En este caso, estase añadindo un overlay.
- **objectClass: olcOverlayConfig**: 
	- Este atributo define que a entrada é un overlay. `olcOverlayConfig` é a clase de obxeto utilizada para configurar overlays en OpenLDAP.
- **objectClass: olcPPolicyConfig**:
	- Define que este overlay en particular é unha política de contraseñas. Específicamente, `objectClass: olcPPolicyConfig` é a clase de obxeto que configura cómo se aplican as políticas de contraseñas nesta base de datos.
- **olcOverlay: {0}ppolicy**:
	- este atributo especifica o tipo de overlay (`ppolicy`) e confirma que é o primeiro (`{0}`) na secuencia de overlays asociados á base de datos `{2}mdb`.
- **olcPPolicyDefault: cn=default,ou=Policies,dc=jano,dc=local**:
	- Este atributo define a política de contraseñas predeterminada que se vai aplicar aos usuarios en esta base de datos.
	- **cn=default,ou=Policies,dc=jano,dc=local** é o DN da entrada LDAP que contén os detalles da política de contraseñas predeterminada.
- **olcPPolicyHashCleartext: TRUE**:
	- Este atributo indica que as contraseñas en texto claro serán convertidas a hashes automáticamente ao almacenalas. Esto é importante para a seguridade, asegurando que as contraseñas non se almacenan en texto plano.
- **olcPPolicyUseLockout: TRUE**: 
	- Este atributo habilita a función do bloqueo de contas. Se se configuran os parámetros correspondentes na política de contraseñas, este overlay pode bloquear contas de usuario despois de un número definido de intentos de autenticación fallidos.
