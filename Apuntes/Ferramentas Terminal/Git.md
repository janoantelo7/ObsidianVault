---
tags:
  - utilidades
---
# Qué é?
Git é un sistema de control de versións distribuído que permite a múltiples desenvolvedores traballar no mesmo proxecto ao mesmo tempo, facendo seguimento dos cambios no código e facilitando a colaboración. Permite crear ramas, fusionar versións e reverter cambios facilmente.
# Instalación de Git
Nas distribucións de Linux, Git debería estar nos repositorios do sistema. Por ejemplo, en Debian podemos [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes|instalalo]] da seguinte maneira:
```bash
sudo apt install git
```
## Configurar ferramentas
### Globalmente
Podemos establecer un nombre de usuario e correo electrónico para todos os repositorios de maneria global. Estos parámetros só se usan se non están especificados de maneira local no repositorio.

Establecer o nombre de usuario para os commits en todos os repositorios.
```bash
git config --global user.name "[nombre]"
```

Establecer o correo electrónico para os commits en todos os repositorios.
```bash
git config --global user.email "[email]"
```
### Localmente
Podemos establecer os parámetros anteriores **por cada repositorio** da seguinte maneira. Estos comandos deben realizarse dentro do repositorio no que os queiramos aplicar.

Establecer o nombre de usuario para os commits.
```bash
git config user.name "[nombre]"
```

Establecer o correo electrónico para os commits
```bash
git config user.email "[email]"
```
# Repositorios
## Crear un repositorio localmente
Podemos crear un repositorio localmente da seguinte maneira. Primeiro necesitamos crear unha carpeta que será o noso repositorio e movernos a ela. Unha vez estamos na carpeta que acabamos de crear, na terminal executamos o seguinte comando.
```bash
git init
```

A maiores, podemos conectar este repositorio local con un repositorio existente en GitHub ou GitLab da seguinte maneira. Primeiro temos que asegurarnos de que existe o repositorio en GitHub/GitLab.

Unha vez temos a url do repositorio podemos facer os seguintes comandos dende o noso repositorio local:
```bash
git remote add origin https://github.com/username/repo
git push -u origin master
```

De maneira alternativa, tamén podemos conectarnos co repo de github mediante **claves ssh**. En ese caso cambiamos a url do comando de `git remote`.
```bash
git remote add origin git@github.com:username/repo
git push -u origin master
```

Se queremos listar o repositorio remoto que temos configurado podemos velo co seguinte comando.
```bash
git remote -v
```
## Obter un repositorio remoto
Podemos descargarnos un repositorio remoto dende unha url existente en GitHub/GitLab.
```bash
# se o descargamos mediante url
git clone https://github.com/username/repo

# podemos descargalo tamén mediatne ssh
git clone git@github.com/username/repo
```

# Ramas
As ramas son unha característica esencial en Git. Permitennos crear múltiples líneas de desarrollo paralelas dentro de un repositorio.
## Crear unha nova rama
Podemos crear unha nova rama basada no contido actual do repositorio utilizando o seguinte comando.
```bash
git branch <nombre_rama>
```
## Cambiar entre ramas
Para movernos de unha rama a outra, utilizamos o seguinte comando.
```bash
git checkout <nombre_rama>
```

Alternativamente, **desde git 2.23**, podemos utilizar tamén
```bash
git switch <nombre_rama>
```

Estos dous comandos tamén aplican se nos queremos cambiar a unha rama remota. Basta con poñer o nombre da rama remota á que nos queiramos mover e git baixarase os cambios de esa rama.

No caso de que queiramos crear e cambiar a unha nova rama podemos simplemente utilizar o seguinte comando.
```bash
git checkout -b <nombre_rama>
```
## Listar ramas
Para ver unha lista de todas as ramas no noso repositorio local utilizamos.
```bash
git branch
```

Se queremos ver as ramas remotas podemos utilizar.
```bash
git branch -r
```
## Eliminar unha rama
Unha vez non necesitemos unha rama podemos eliminala co seguinte comando.
```bash
git branch -d <nombre_rama>
```

Este comando solo eliminará a rama se xa foi fusionada. Se queremos forzar a eliminación de unha rama que non foi fusionada usamos.
```bash
git branch -D <nombre_rama>
```
# Ciclo básico de traballo
Este apartado fai referencia aos comandos que nos permiten xestionar e sincronizar os cambios realizados no código, tanto de forma local como de forma remota.
## Facer cambios
O primeiro paso é realizar modificacions nos ficheros do repositorio. Unha vez feitos estos cambios podemos preparar os ficheros para ser confirmados e registrados no historial de cambios.
### Añadir ficheros
Este comando añade os ficheros modificados á area de preparación, tamén conocida como staging area. É decir, aquí añadimos que cambios en ficheros queremos incluir no próximo commit. Podemos añadir un único fichero ou todos os ficheros.
```bash
git add <nombre_fichero>
```

Se queremos añadir todos os ficheros modificados utilizamos.
```bash
git add .
```
### Mover ficheros / Renombrar ficheros
No caso de que necesitemos renombrar ou mover de ubicación un fichero dentro do repositorio, utilizamos o comando `git mv`. É preferible utilizar este comando a facelo desde as utilidades que nos ofrezca o sistema operativo, xa que Git registra estos cambios e preparaos para o próximo commit.
```bash
# renombrar fichero
git mv <nombre_fichero> <novo_nombre>

# mover fichero
git mv <ubicacion_fichero> <nova_ubicacion>
```
### Confirmar cambios
Unha vez que enviamos os ficheros á area de preparación, confirmamos os cambios co comando `git commit`. Un commit é un punto de control que garda unha versión específica do proxecto con un mensaxe que describe os cambios realizados. O comando a utilizar sería o seguinte.
```bash
git commit -m "<mensaxe descriptivo>"
```

É importante que os mensaxes sexan descriptivos e claros, podemos axudarnos da seguinte [web]([Commitlint Online - lint commit messages online](https://commitlint.io/)) para seguir un estándar á hora de crear estos mensaxes.
## Sincronizar co repositorio remoto
É recomendable manter o repositorio local sincronizado co repositorio remoto. Para esta tarefa valemonos de dúas ferramentas `git pull` e `git push`.
### Traer cambios cara o repositorio local
Antes de empezar a realizar cambios no repositorio local, é recomendable baixarse os cambios do repositorio remoto para así evitar conflictos. Para esto utilizamos o seguinte comando.
```bash
git pull
```
### Enviar cambios cara o repositorio remoto
Despois de realizar e confirmar os cambios locales, é importante envialos hacia o repositorio remoto. Para esta función valemonos do seguinte comando.
```bash
git push
```

Este comando aseguranos que os cambios que realizamos no noso equipo local tamén estén reflejados no servidor remoto.
# Descartar o último commit
Se fixemos un commit e o lanzamos sin querer ao repositorio remoto podemos executar os seguintes comandos na terminal para descartar o commit que non queríamos enviar ao repositorio remoto. 

Con este comando volvemos ao commit anterior no noso repositorio local.
```bash
git reset --hard HEAD~1
```

Con este outro comando sobreescribimos o repositorio remoto co noso repositorio local.
```bash
git push origin {NOME_RAMA} --force
```

>[!WARNING] Atención
>Estos dous comandos deben utilizarse con coidado e só cando sexa necesario, como por exemplo subimos sin querer unha contraseña a un repositorio remoto.

