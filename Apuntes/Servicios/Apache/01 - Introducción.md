---
tags:
  - web_server
---
# Qué é?
Apache é un dos servicios de servidores web máis utilizados a nivel mundial.
# Instalación e configuración 
Dependendo do sistema operativo temos que instalar o paquete de `apache2` se estamos en un **_Debian_** e o paquete de `httpd` en un sistema **_RHEL_**.
## Debian
Para a instalación en Debian utilizamos o seguinte comando:
```bash
sudo apt install apache2
```
### Configuración Global
O fichero de confiruación global está ubicado dentro da seguinte ruta:
```bash
/etc/apache2/apache2.conf 
```
Este fichero controla a configuración principal do servidor.
### Módulos
Os modulos en apache agregan funcionalidades extra ao servidor. Os módulos están disponibles en:
```bash
/etc/apache2/mods-available/
```
Se queremos habilitar un modulo utilizamos:
```bash
sudo a2enmod <modulo>
sudo systemctl reload apache2
```

Para deshabilitar un módulo utilizamos:
```bash
sudo a2dismod <modulo>
sudo systemctl reload apache2
```
### SSL
En Ubuntu para habilitar o SSL é tan simple como habilitar o modulo encargado de esto:
```bash
sudo a2enmod ssl 
```

Unha vez feito eso, debemos reiniciar apache para que os cambios fagan efecto:
```bash
sudo systemctl restart apache2
```
## RHEL
Para a instalación en RHEL utilizamos o seguinte comando:
```bash
sudo dnf install httpd
```
### Configuración Global
O fichero de configuración principal de Apache está en:
```bash
/etc/httpd/conf/httpd.conf 
```
### Firewall
En RHEL é común que veña o firewall habilitado, para permitir o uso de este servicio cos portos 80 (HTTP) e 443 (HTTPS) temos que utilizar os seguintes comandos:
```bash
sudo firewall-cmd --permanent --add-service=http 
sudo firewall-cmd --permanent --add-service=https 
sudo firewall-cmd --reload
```
### SSL
En RHEL para habilitar SSL basta con instalar o módulo:
```bash
sudo dnf install mod_ssl
```

Unha vez temos este módulo habilitado, creasenos un fichero `ssl.conf` na ruta dos virtual hosts e ahí configuramos o SSL para o vhost por defecto. Se queremos en vhost alternos debemos configura os certificados dentro de cada fichero.
