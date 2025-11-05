---
tags:
  - web_server/vhost
---
# Introducción
O término **VirtualHost** refierese a poder executar máis de un sitio web (por exemplo; sitio1.exemplo.com e sitio2.exemplo.com) no mesmo servidor web. Os VirtualHost poden ser **basados en IP** ou **basados por nombre**, esto quere decir que teremos varios sitios webs coa mesma IP.
# VirtualHost basados en nombres
Este é o caso máis común á hora de configurar un VirtualHost. Nestos casos o servidor depende de que o cliente reporte o nome do host como parte das súas cabeceiras HTTP.
## Exemplo de configuración
```apache
<VirtualHost *:80>
	DocumentRoot /var/www/html/sitio1
	ServerName sitio1.ejemplo.com
</VirtualHost>
```

En este exemplo empregamos un `*` para indicar que o VirtualHost pode recibir peticións en calquera das interfaces do servidor, pero tamén se podería especificar algunha delas.

No caso de só ter definidos VirtualHost baseados en nombres se nos chegase unha petición sen cabeceira de nome, ou que non coincide con ningún dos VirtualHost definidos respondería o **primeiro dos VirtualHost** que cargase ao arrancar Apache.
# VirtualHost baseado en IP
Os VirtualHost basados en IP é un método de aplicar diferentes directivas basadas na dirección IP ou puerto no que se recibe a petición. Desta maneira sirvense diferentes sitios en diferentes puertos e interfaces de rede.

Na maioría de ocasións os VirtualHost basados en nombre é máis conveniente porque nos permite crear moitos máis hosts ao compartir unha misma dirección e porto.

Se queremos crear un VirtualHost de este estilo podemos conseguilo de dúas maneiras:
- Varias interfaces de red físicas ou virtuales
- Empregando múltiples números de porto
## Exemplo de configuración
```apache
<VirtualHost 172.20.30.40:80>
    ServerAdmin webmaster@www1.exemplo.com
    DocumentRoot "/var/www/vhosts/www1"
</VirtualHost>
<VirtualHost 172.20.30.50:80>
    ServerAdmin webmaster@www2.exemplo.org
    DocumentRoot "/var/www/vhosts/www2"
</VirtualHost>
```

# Configuración
Á hora de crear os VirtualHosts debemos crear uns ficheros terminados en `.conf` que conterán a configuración dos nosos VirtualHost. Dependendo da distribución que utilicemos esta ruta e maneira de activalos será distinta. 
## Sistemas baseados en Debian
Os archivos de configuración dos VirtualHost en suelen estar na siguiente ruta:
```bash
/etc/apache2/sites-available/
```

Se queremos habilitar un virtual host temos que utilizar o seguinte comando:
```bash
sudo a2ensite sitio.conf
sudo systemctl reload apache2
```

No caso que queiramos deshabilitar o virtual host facemolo da seguinte maneira:
```bash
sudo a2dissite sitio.conf
sudo systemctl reload apache2
```
## Sistemas baseados en RHEL
En RHEL os VirtualHost configuranse con na seguinte ruta:
```bash
/etc/httpd/conf.d/
```

Para habilitar estos virtual hosts únicamente temos que recargar o servicio de httpd:
```bash
sudo systemctl reload httpd
```

No caso que queiramos deshabilitar un VirtualHost chega con cambiar a extensión do fichero a calquer cousa que non sexa `.conf`, por exemplo, `.dis`. Así faríamos o seguinte se queremos deshabilitar un VirtualHost
```bash
mv sitio.conf sitio.conf.dis
```

E despois recargamos httpd para que deshabilite o sitio.
```bash
sudo systemctl reload httpd
```
