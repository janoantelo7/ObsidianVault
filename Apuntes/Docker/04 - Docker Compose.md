---
tags:
  - docker
  - contenedores
---
# Qué é?
Docker Compose é unha ferramenta para definir e executar aplicacións multicontenedor en [[Apuntes/Docker/01 - Introducción#Qué é?|Docker]]. Utiliza un fichero YAML para configurar os servicios, redes e [[Apuntes/Docker/01 - Introducción#Volumen|volúmenes]] dunha aplicación Docker, o que facilita a xestión e a execución de múltiples contenedores que traballan xuntos. Por defecto o comando `docker compose` busca un fichero chamado `docker-compose.yml`.
# Conceptos clave
- **Servicios (services)**: Son os contenedores que forman parte da aplicación. Cada servicio é unha instancia de un contenedor Docker basado nunha imágen específica.
- **Redes (networks)**: Definen cómo se comunican os contenedores entre sí. Docker Compose crea redes automáticamente, aunque tamén se poden definir explícitamente nun fichero YAML.
- **Volúmenes**: Son directorios compartidos entre o host e os contenedores, ou entre os propios contenedores, para persistir datos. 
# Contido fichero
Cando traballamos con Docker Compose, debemos definir un fichero chamado `docker-compose.yml`. Podemos chamalo de outra maneira e indicamos o nombre do fichero co seguinte comando: `docker compose -f <nombre_fichero>`. A estructura básica de un fichero Docker Compose é a seguinte.
```docker
services:
  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```

En este ejemplo, podemos ver como se configuran dous servicios, un para un **wordpress** e outro a base de datos que vai utilizar este wordpress. En el ademáis podemos ver que se crean dous volumenes que almacenaran os datos do wordpress e do contenedor mysql.
# Comandos básicos
Levantar os servicios definidos no fichero.
```bash
docker compose up

# tamén podemos levantar os servicios de maneira dettached
docker compose up -d
```

Detener e eliminar os contenedores, redes e volúmenes.
```bash
docker compose down
```

Mostrar o estado dos contenedores administrados por Docker Compose.
```bash
docker compose ps
```

Detener os servicios do Docker Compose.
```bash
docker compose stop
```

Iniciar os servicios do Docker Compose.
```bash
docker compose start
```
