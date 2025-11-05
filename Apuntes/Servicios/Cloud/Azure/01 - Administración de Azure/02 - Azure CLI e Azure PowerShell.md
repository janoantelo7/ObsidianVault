---
tags:
  - azure
  - powershell
  - linux
---
Podemos manexar Azure dende a linea de comandos con unha das seguintes ferramentas: 
- `azure cli`: É unha ferramenta de terminal que está pensada para ser utilizada dende terminales que están basadas en bash. Son comandos máis similares aos que estamos acostumbrados en linux. ^75a6fc
- `Azure PowerShell`: Esta ferramenta está pensada para ser utilizada con comandos do estilo de Powershell.

Ambas ferramentas se poden utilizar dende a cloud shell ou instalandoas dende a nosa máquina local. A ventajas ventajas que nos proporcionan este tipo de ferramentas son:
- Non ter que loggearnos e navegar pola interfaz de Azure Portal, o que as convirte en unha maneira robusta de administrar Azure.
- Automatizar tarefas mediante scripts.
# Ejemplo de comandos en `azure cli`
## Crear unha máquina virtual en un resource group
Para crear unha máquina virtual mediante `azure cli` facemos os seguintes comandos:
```bash
# obtemos o nombre do resource group e gardamolo en unha variable `rsgrp`
rsgrp=$(az group list --query "[].name" --output tsv)
```

Creamos a máquina virtual dentro de ese [[Apuntes/Servicios/Cloud/Azure/01 - Administración de Azure/01 - Introducción#Qué son os resource groups?|resource group]], co nombre do usuario que lanzou o comando e para **conectarnos** mediante **claves ssh**.
```bash
az vm create -g $rsgrp --name [NOMBRE_VM] --image [IMAGEN_VM] --generate-ssh-keys
```

Podemos generar unha VM para conectarnos por **usuario** e **contraseña** co seguinte comando
```bash
az vm create -g $rsgrp --name [NOMBRE_VM] --image [IMAGEN_VM] --admin-username [USUARIO] --admin-password [CONTRASEÑA]
```
