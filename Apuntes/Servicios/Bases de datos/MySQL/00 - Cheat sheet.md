---
tags:
  - utilidades/mysql
---
# Usuarios
## Crear usuario
```mysql
create user 'admuser'@'localhost' identified by 'pwd-admuser';
```
## Listar usuarios
```mysql
select user,password,host from mysql.user;
```
## Borrar un usario
```mysql
drop user 'admuser'@'localhost';
```
## Asignar permisos adm
```mysql
grant all privileges on *.* to 'admuser'@'localhost' with grant option;
```
## Dar permisos sobre una base de datos
```MySQL
grant all privileges on {database}.* to 'user'@'%';
```
## Ver permisos usuario
```MySQL
show grants for {user}@'localhost';
```
## Eliminar permisos sobre una base de datos
```MySQL
REVOKE ALL PRIVILEGES ON {database}.* FROM 'user@'%';
```
se tamén queremos quitar o permiso de dar permisos ejecutamos a seguinte query: 
```MySQL
revoke grant option on *.* from 'admuser'@'localhost';
```
## Cambiar contraseña usuario
```mysql
ALTER USER 'user'@'hostname' IDENTIFIED BY 'newPass';
```
## Permitir crear
```mysql
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE ON *.* TO 'user'@'%' IDENTIFIED BY 'pwd-user';
```
## Ver todos os usuarios
```mysql
SELECT User, Host FROM mysql.user ORDER BY User;
```
# Tamaños
## Tamaño bases de datos
Podemos utilizar a seguinte [[01 - Introducción a SQL#Consulta (query)|query]] para obter o tamaño que ocupan todas as [[01 - Introducción a SQL#Base de datos|bases de datos]] que hai en un sistema xestor de bases de datos.
```sql
SELECT table_schema "DB Name", ROUND(SUM(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" FROM information_schema.tables GROUP BY table_schema; 
```
## Tamaño tablas de una base de datos
Podemos utilizar a seguinte query para obter o tamaño que ocupan as [[01 - Introducción a SQL#Tabla|tablas]] de unha base de datos.
```sql
SELECT TABLE_NAME AS 'Table', ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS 'Size (MB)' FROM information_schema.TABLES WHERE TABLE_SCHEMA = '{nombre_base_datos}' ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC;
```
# Backups
## Exportar base de datos
Para exportar unha base de datos podemos utilizar o seguinte comando
```bash
mysqldump -u {username} -p {dbname} | gzip > {outputfile}_$(date +"%Y%m%d").sql.gz
```
## Importar base de datos
Para importar unha base de datos utilizamos
```bash
zcat /path/file.sql.gz | mysql -u {username} -p {dbname}
```
## Exportar tabla
```shell
mysqldump -u {username} -p {dbname} {table_name} | gzip > {outputfile}_$(date +"%Y%m%d").sql.gz
```
## Importar tabla
```shell
zcat /path/file.sql.gz | mysql -u {username} -p {dbname}
```
