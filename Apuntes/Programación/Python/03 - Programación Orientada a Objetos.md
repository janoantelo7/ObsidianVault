---
tags:
  - python
---
# Introducción
A Programación Orientada a objetos (POO) é un paradigma de programación introducido nos anos 70 pero popularizado máis tarde. Organiza o código de forma semellante ao humano, empregando clases que agrupan variables (atributos) e funcións (métodos).

Por exemplo, un can pode representarse cunha clase, tendo atributos como idade ou raza e métodos como andar ou ladrar. Cada can concreto, como Toby ou Laika, sería un objeto baseado nesa clase.

A POO básase en seis principios funcamentales:
- herencia
- cohesión
- abstracción
- polimorfismo
- acoplamiento
- encapsulamiento

# Definindo clases
En este apartado vamos a ver como podemos crear unha clase. O primeiro exemplo que veremos é como crear unha clase vacía. Para esto utilizaremos o exemplo de can.
```python
class Can:
    pass
```

Unha vez temos a **clase**, podemos crear un **objeto* da misma. Podemos facelo como se fose unha variable normal. Nome da variable igual á clase con `()`. Dentro dos paréntesis irían os parámetros de entrada se os houbese.
```python
class Can:
    pass

pancho = Can()
```

## Añadindo atributos á clase
En este apartado vamos añadir alguns atributos a nosa clase. Antes de nada é importante distinguir entre dous tipos de atributos:
- **Atributos de instancia**: Pertenecen á instancia da clase ou obxeceto. Son atributos particulares de cada instancia.
- **Atributos de clase**: Tratase de atributos que pertenecen á clase, polo tanto serán comúns para todos os obxetos.
### Atributos de instancia
A continuación, vamos crear un par de atributos de instancia para o noso can, o `nombre` e a `raza`. Para eso creamos un método `__init__` que será chamado automáticamente cando creemos un objeto. Tratase do constructor.

```python
class Can:
    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        #atributos de instancia
        self.nombre = nombre
        self.raza = raza
```

Ahora podemos crear o objeto pasando o valor dos atributos.
```python
class Can:
    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        #atributos de instancia
        self.nombre = nombre
        self.raza = raza


pancho = Can("pancho", "can")
print(type(pancho))
```

Resultado da execución:
```python
creado o can pancho, can
<class '__main__.Can'>
 ```

O `self` que lle pasmos como parámetro de entrada ao método, é unha variable que representa a instancia da clase, e deberá estar sempre ahí.

O uso de `__init__` e o doble `__` non é unha coincidencia. Esto significa que está reservado para un uso especial do lenguaje. Neste caso sería o que se conoce como **constructor**.

Podemos acceder aos atributos do objeto usando o objeto e `.`:
```python
class Can:
    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        #atributos de instancia
        self.nombre = nombre
        self.raza = raza


pancho = Can("pancho", "can")

print(pancho.nombre)
print(pancho.raza)
```

Resultado da execución:
```python
creado o can pancho, can
pancho
can
```
### Atributos de clase
Os **atributos de clase** son aqueles que son comúns **para todos os objetos** da clase. Por ejemplo, a especie dos cans é algo común para todos os objetos can.
```python
class Can:
    # atributo de clase
    especie = "mamifero"

    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        # atributos de instancia
        self.nombre = nombre
        self.raza = raza
```

Dado que é un atributo de clase, non é necesario crear un objeto para acceder aos atributos. Podemos facer o seguinte:
```python
class Can:
    # atributo de clase
    especie = "mamifero"

    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        # atributos de instancia
        self.nombre = nombre
        self.raza = raza

print(Can.especie)
```

Resultado da execución:
```python
 mamifero
```

Podese acceder tamén ao atributo de clase desde o objeto.
```python
class Can:
    # atributo de clase
    especie = "mamifero"

    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        # atributos de instancia
        self.nombre = nombre
        self.raza = raza

pancho = Can("pancho", "perro")
print(pancho.especie)
```

```python
creado o can pancho, perro
mamifero
```

Desta maneira, todos os objetos que se creen da clase can compartirán ese atributo de clase, xa que pertenecen á mesma.
## Añadindo métodos á clase
En realidade cando usábamos `__init__` xa estábamos definindo un método, só que un especial. A continuación vamos ver como definir métodos que lle dean algunha funcionalidade á nosa clase.
```python
class Can:
    # atributo de clase
    especie = "mamifero"

    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        # atributos de instancia
        self.nombre = nombre
        self.raza = raza

    def ladra(self):
        print("guau")
    
    def andar(self, pasos):
        print(f"andando {pasos} pasos")


pancho = Can("pancho", "perro")
```

Polo tanto se creamos un objeto `pancho`, podemos facer uso dos seus métodos chamandoos con `.` e co nombre do método. Como se de unha [[01 - Datos e operadores#Funcions|función]] se tratasen, poden recibir e devolver argumentos.
```python
class Can:
    # atributo de clase
    especie = "mamifero"

    # o método __init__ é chamado ao crear o objeto
    def __init__(self, nombre, raza):
        print(f"creado o can {nombre}, {raza}")

        # atributos de instancia
        self.nombre = nombre
        self.raza = raza

    def ladra(self):
        print("guau")
    
    def andar(self, pasos):
        print(f"andando {pasos} pasos")


pancho = Can("pancho", "perro")

pancho.ladra()
pancho.andar(10)
```

Resultado da execución:
```python
creado o can pancho, perro
guau
andando 10 pasos
```

