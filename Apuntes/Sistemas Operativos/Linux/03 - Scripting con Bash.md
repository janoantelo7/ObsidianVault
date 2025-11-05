---
tags:
  - scripting/bash
---
# Introducción
Para facer scripts en bash é importante ter en conta as siguientes cousas:
- Podemos facer scripts con calquer editor de texto, tanto sexan en terminal como nano ou [[Vim#^a6f529|Vim]], como un máis completo como Visual Studio Code. 
- Todos os scripts empezan con unha **shebang**. Unha shebang non é máis que a maneira de decirlle ao sistema que intérprete ten que utilizar para executar o script. Definimos as shebangs con `#!/`. A máis común é `#!/bin/bash` que se encarga de chamar ao intérprete de bash. 
- Para facer ejecutable o noso script temos que darlle [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Permisos de ficheros/carpetas|permisos]] de execución ao fichero. Podemos facelo de maneira rápida con `chmod +x <nombre_script>`.
- Ejecutamos o script da seguinte maneira: `./<nombre_script>`.
# Variables
Á hora de crear scripts en bash podemos definir variables. As variables son elementos fundamentales en calquer linguaxe de programación. Permiten almacenar a información e manipulala ao largo do programa. 

Se queremos definir unha variable en bash facemolo da seguinte forma. Podemos darlle o nombre que queiramos, neste exemplo definimos unha variable chamada "nombre" que contén o meu nombre. Tanto o nombre como o valor da variable siempre teñen que estar pegados ao simbolo de `=`.
```bash
#!/bin/bash

nombre="jano"
```

Para acceder ao valor da variable que acabamos de crear só temos que escribir o nombre da variable co símbolo de dolar diante `$`.
```bash
#!/bin/bash

nombre="jano"
echo "Ola $nombre" # este programa mostra por terminal "Ola jano"
```

Podemos acceder á variable de tres formas distintas:
- `$nombre`: accede ao contenido da variable.
- `${nombre}`: accede ao contenido da variable pero ideal para concatenar.
- `${nombre:inicio:fin}`: extraer unha subcadea do contenido da variable.

En bash existen un tipo de **variables especiales** as cales son:
- `$0`: nombre do script.
- `$1, $2, $3 ... $n`: parámetros pasados ao script. Número = posición.
- `$#`: número de parámetros pasados ao script.
- `$*` ou `$@`: lista de todos os parámetros pasados ao script.
- `$?`: resultado da execución do último comando. Se foi exitoso devolve 0.
- `${@:-1}`: obter o último argumento pasado ao script.
- `${@:1:$#-1}`: obter todos os argumentos pasados ao script menos o último.
# Estructuras de control

## Comparadores
Segundo o tipo de dato que esteamos a comprar existen diversos tipos de comparadores que podemos utilizar.

Se a comparación é con números enteiros:
- `[ ARG1 -eq ARG2 ]`: verdadeiro se ARG1 é igual que ARG2.
- `[ ARG1 -ne ARG2 ]`: verdadeiro se ARG1 é distinto de ARG2.
- `[ ARG1 -lt ARG2 ]`: verdadeiro se ARG1 é menor que ARG2.
- `[ ARG1 -le ARG2 ]`: verdadeiro se ARG1 é menor ou igual que ARG2.
- `[ ARG1 -gt ARG2 ]`: verdadeiro se ARG1 é maior que ARG2.
- `[ ARG1 -ge ARG2 ]`: verdadeiro se ARG1 é maior ou igual que ARG2.

Se a comparación é con cadenas de texto:
- `[ -z string ]`: verdadeiro se a lonxitude de cadea é 0.
- `[ -n string ]` ou `[ string ]`: verdadeiro se a lonxitude de cadea non é 0.
- `[ string1 == string2 ]`: verdadeiro se as cadenas son iguais.
- `[ string1 != string2 ]`: verdadeiro se as cadenas non son iguais.
- `[ string1 < string2 ]`: veradeiro se string1 vai lexicamente antes que string2.
- `[ string1 > string2 ]`: verdadeiro se string1 vai lexicamente despois que string2.

Tamén podemos facer comparacións acerca de ficheros:
- `[ -a FILE ]`: verdadeiro se existe o fichero.
- `[ -b FILE ]`: verdadeiro se existe o fichero e é un fichero especial de bloques.
- `[ -c FILE ]`: verdadeiro se existe o fichero e é un fichero especial de carácter.
- `[ -d FILE ]`: verdadeiro se existe o fichero e é un directorio.
- `[ -e FILE ]`: verdadeiro se existe o fichero.
- `[ -f FILE ]`: verdadeiro se o fichero existe e é un fichero regular.
- `[ -g FILE ]`: verdadeiro se existe o fichero e ten habilitado o bit SGID.
- `[ -h FILE ]`: verdadeiro se existe o fichero e é un link simbólico.
- `[ -k FILE ]`: verdadeiro se existe o fichero e ten habilitado o sticky bit.
- `[ -p FILE ]`: verdadeiro se existe o fichero e é un tubo con nome (FIFO).
- `[ -r FILE ]`: verdadeiro se existe o fichero e se pode ler.
- `[ -s FILE ]`: verdadeiro se existe o fichero e o seu tamaño é maior que 0.
- `[ -t FD ]`: verdadeiro se o decriptor de fichero FD está aberto e refiere a un terminal.
- `[ -u FILE ]`: verdadeiro se existe o fichero e ten habilitado o bit SUID (set user ID).
- `[ -w FILE ]`: verdadeiro se existe o fichero e se pode escribir.
- `[ -x FILE ]`: verdadeiro se existe o fichero e é executable.
- `[ -O FILE ]`: verdadeiro se existe o fichero e o propietario é o ID de usuario efectivo.
- `[ -G FILE ]`: verdadeiro se existe o fichero e o propietario é o ID de grupo efectivo.
- `[ -L FILE ]`: verdadeiro se existe o fichero e é un enlace simbólico.
- `[ -N FILE ]`: verdadeiro se existe o fichero e foi modificado desde a última lectura.
- `[ -S FILE ]`: verdadeiro se existe o fichero e é un socket.
- `[ FILE1 -nt FILE2 ]`: verdadeiro se o fichero1 foi modificado máis recientemente que o fichero2. Ou se fichero1 existe e fichero2 non.
- `[ FILE1 -ot FILE2 ]`: verdadeiro se o fichero1 é máis vello que fichero2, ou se fichero2 existe e fichero1 non.
- `[ FILE1 -ef FILE2 ]`: verdadeiro se fichero1 e fichero2 refieren ao mismo dispositivo e número de inodo.

Á hora de comparar podemos sustituir os corchetes simples (`[]`) polos corchetes dobles (`[[]]`). Os corchetes dobles ofrecen as seguintes ventaxas con respecto aos simples:
1. Mellor comparación á hora de utilizar patróns globais sen necesitar escapar carácteres especiales como `*` ou `?`.
2. Uso de operadores lóxicos como son `&&` para o and e `||` para o or. Esto posibilitanos comprobar dúas condicions no mesmo bloque.
```bash
if [[ $idade -ge 18 && $idade -le 65 ]]; then
    echo "Tes idade para traballar."
fi
```
3. Xestiona mellor os espazos en blanco á hora de comparar cadenas de texto.
## Condicionales
Os condicionales en bash teñen unha estructura similar á que teñen en outros lenguajes. O máis común de eles é utilizar o `if-else`.
### if-else
A estructura do `if-else` en bash é a seguinte. Este condicional é moi empregado á hora de evaluar unha condición. 
```bash
#!/bin/bash

if [ condición ]
then
    # Comandos si la condición é verdadera
else
    # Comandos si ninguna condición é verdadera
fi
```

Tamén podemos utilizar outra estructura que é a `if-elif-else`. Esto sirvenos para evaluar máis de unha condición. A estructura é a seguinte:
```bash
#!/bin/bash

if [ condición ]
then
    # Comandos si la condición é verdadera
elif [ otra_condición ]
then
    # Comandos si otra_condición é verdadera
else
    # Comandos si ninguna condición é verdadera
fi
```

Podemos utilizar tantos `elif` como queiramos, pero o `else` siempre ten que ser o último da estructura.

Un exemplo práctico de esta estructura sería o seguinte:
```bash
#!/bin/bash

# aqui comprobamos que nos envian dous parámetros
if [ $# -eq 2 ]
then
    # se os parámetros son igual a 2 saludamos
    echo "hola $1, tes $2 anos"
else
    # se os parámetros non son igual a 2 damos un error
    echo "sólo podes enviarme dous argumentos"
fi
```

En este exemplo, se non enviamos dous parámetros á hora de chamar ao script devolveranos a mensaxe de "sólo podes enviarme dous argumentos".
### case
O comando `case` en bash é útil cando tes múltiples condicións que queres comprobar. Funciona de forma similar ao `switch` noutras linguaxes de programación e é unha alternativa máis clara e concisa ao uso de múltiples bloques `if-elif-else` cando tes que tratar con diferentes valores dun parámetro.

A sintaxis básica de `case` é a seguinte:
```bash
case EXPRESIÓN in
    PATRÓN1)
        comandos_a_executar
        ;;
    PATRÓN2)
        comandos_a_executar
        ;;
    PATRÓN3|PATRÓN4)
        comandos_a_executar
        ;;
    *)
        comandos_para_calquera_outro_caso
        ;;
esac
```
Neste exemplo `EXPRESIÓN` é a condición a evaluar polos patrons. No terceriro caso tanto o `PATRÓN3` como o `PATRÓN4` executarían o mismo bloque de código. `*` sería así como a opción por defeto cando non cumple ningunha das outras. 

Un exemplo aplicado de esto sería, un no que solicitamos introducir un número do 1 ao 3 e mostramos por pantalla unha mensaxe.
```bash
#!/bin/bash

echo "Introduce unha opción (1, 2, 3 ou outro valor):"
read opcion

case $opcion in
    1)
        echo "Escolleches a opción 1."
        ;;
    2)
        echo "Escolleches a opción 2."
        ;;
    3)
        echo "Escolleches a opción 3."
        ;;
    *)
        echo "Escolleches unha opción non válida."
        ;;
esac
```

Tamén podes empregar patróns máis complexos, como comodíns para definir rangos de valores ou tipos de entradas:
```bash
#!/bin/bash

echo "Introduce un número entre 1 e 3:"
read numero

case $numero in
    1|2)
        echo "Escolleches 1 ou 2."
        ;;
    3)
        echo "Escolleches 3."
        ;;
    *)
        echo "Escolleches outro valor."
        ;;
esac
```
- `[aeiou]`: este patrón identifica a calquera vocal.
- `[0-9]`: este patrón identifica a calquera díxitio númerico.
- `[A-Z]`: este patrón identifica calquera letra maiúscula.
- `*`: o caso por defecto manexa calquea outro carácter que non coincida cos patróns anteriores.
## Bucles
### while
O bucle `while` realiza un bloque de codigo mentres se cumpla certa condición. Nos bucles whiles é moi importante asegurarse de que en algun momento acaba a condición, xa que se non estaríamos creando un bucle infinito. A estructura do bucle while en bash é a siguiente.
```bash
#!/bin/bash

while [ condicion ]
do
    # bloque de codigo
done
```

Un ejemplo práctico de utilizar un bucle while no que mostramos por pantalla os números do 0 ao 2 sería:
```bash
#!/bin/bash

# iniciamos a variable num en 0
num=0

# mentres o num sexa menor ca 3 facemos o de dentro do while
while [ $num -lt 3 ]
do
    # mostramos o valor da variable num
    echo $num
   
    # incrementamos a variable num para romper o bucle
    # se non incrementamos esta variable facemos un bucle infinto
    num=$((num+1))
done
```
### for
O bucle `for` é outro tipo de bucle, este bucle generalmente utilizamolo par recorrer unha lista. É similar a un foreach en php. A estructura de este bucle é a siguiente:
```bash
#!/bin/bash

for elemento in lista_de_valores
do
    # Comandos
done
```

No seguinte bloque de código vemos como podemos aplicar un bucle for que mostra por pantalla todos os argumentos que se lle pasaron ao scritp.
```bash
#!/bin/bash

# recordamos que $@ conten toda a lista de argumentos que lle pasas ao script
for argumento in $@
do
    # imprimimos un a un o argumento da lista
    echo $argumento
done
```
# Interacción co usuario
En bash non só podemos crear scripts que o usuario sexa pasivo, é decir que o usuario vexa información por pantalla, senon que podemos crear scripts no que lle solicitemos información ao usuario e o script faga cousas en función de esto. Para recibir información do usuario utilizamos o comando `read`.

Un exemplo en un script sería un script que solicite o nombre do usuario e o solicite.
```bash
#!/bin/bash

# pedimoslle ao usuario que nos diga o seu nombre
# o -p utilizamolo para poñerlle un texto á hora de pedir a informacion
read -p "introduce o teu nombre: " nombre

# mandamos de volta no nombre do usuario
echo "hola $nombre"
```

Grazas a esta información, podemos saber como podríamos crear un script que tivese un menú e en función da opción que escolla o usuario realizar unhas opcións ou outras. No seguinte exemplo vemos como podemos crear un menu.
```bash
#!/bin/bash

# mostramos as opcions que ten o menu
echo "1) opcion1"
echo "2) opcion2"
echo "3) opcion3"

# pedimoslle ao usuario que escolla unha opcion
read -p "escolle opcion: " opcion

# coa opcion quen os mandou o usuario metemola nun case para facer cousas coa opcion que nos introduciu
# en este caso devolvemoslle por pantalla o que nos introduciu
case $opcion in
    1)
    echo "escolleches a opcion1"
    ;;
    2)
    echo "escolleches a opcion2"
    ;;
    3)
    echo "escolleches a opcion3"
    ;;
esac
```
# Traballando con ficheros
Un dos casos máis comúns á hora de facer scripts en bash, é a de leer ficheros e tratalos para automatizar tarefas do sistema en función de estos. Diferenciamos dous tipos de ficheros os que son básicos e os que son csv, ou que conteñen algún tipo de campo separado.
## Leer ficheros texto plano
Este tipo de ficheros é como ter unha lista, un elemento está encima do outro, por exemplo, traballamos co seguinte fichero:
```bash
jano@DESKTOP-OI7MJLM ~ % cat palabras.txt
hola
jano
texto
```

Ahora creamos o seguinte script que o que fai é leer o fichero e decir o texto que se leeiu:
```bash
#!/bin/bash  

fichero="palabras.txt"  
  
# leemos o fichero linea a linea  
while read linea  
do  
    echo "liuse a linea do fichero: $linea"
done < $fichero # metemoslle o fichero ao bucle
```

Almacenamos na variable "fichero" a ruta na que se encontra o fichero, como no ejemplo o fichero de texto está na misma ruta que o script non fai falta indicar nada máis que o nombre. Co bucle [[03 - Scripting con Bash#while|while]] leemos linea a linea o contido do fichero e coa función `read` damoslle un nombre á variable na que almacenamos o valor da línea.
## Leer ficheros con separador de campos
Este é un dos casos máis interesantes á hora de traballar con ficheros, xa que así, por exemplo, podemos crear un script que reciba un csv con usuarios e passwords para crear esos ususarios no sistema. 

Por exemplo, creamos o seguinte fichero csv cos seguintes usuarios:
```bash
jano@DESKTOP-OI7MJLM ~ % cat usuarios.csv
pancho;abc123.
jano;abc123.
bad bunny;abc123.
```

E ahora creamos uns script que nos mostre por pantalla o valor do nombre do usuario e a password que tería o usuario no caso de que o quixeramos crear no sistema.
```bash
#!/bin/bash  

fichero="usuarios.csv"  
 
while IFS=";" read nombre_usuario password  
do  
    echo "no fichero hai o usuario: $nombre_usuario con $password"
done < $fichero # metemoslle o fichero ao bucle
```

Este caso é similar ao anterior, pero aquí ao bucle while añadimoslle a opción `IFS=` que sirve para indicar o delimitador dos campos. No noso caso os campos están delimitados por `;`. No `read` creamos tantas variables como campos teña o noso csv que almacenan o valor dos campos.
# Debugging
Cando queremos debuggear un script de bash podemos crear a seguinte escturctura ao principio do scritp:
```bash
#!/bin/bash

trap 'echo "[${BASH_SOURCE}:${LINENO}] $BASH_COMMAND"; read -p "Continue?"' DEBUG

echo "hola mundo!"

touch "fichero.txt"

rm "fichero.txt"
```

O que fai a linea esta de `trap` é imprimir cada liñea e preguntarnos se queremos executala.
