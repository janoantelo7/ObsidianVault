---
tags:
  - linux
  - troubleshooting
---
# ping
`ping` é unha ferramenta critica cando se trata de facer "troubleshooting". Este comando permitenos comprobar a conectividade entre un host e a máquina objetivo.
```bash
ping [IP_OBJETIVO/HOSTNAME]
```
# traceroute
`traceroute` é unha ferramenta de diagnostico de rede. Mostra o recorrido que realiza un paquete dende o sistema onde se executa traceroute ata o destino. Utilizamolo para identificar problemas de enrutamento. 
```bash
traceroute [DESTINO]
```
# ss
O comando `ss` é unha ferramenta que se utiliza para mostrar información sobre sockets de rede de un sistema Linux. Remplazou en gran medida a `netstat` xa que é máis rápido e eficiente.

A sintaxis básica é a seguinte:
```bash
ss [OPCIONS] [FILTRO]
```
## Ejemplos
1. Listar todas as conexións que están e non están escoitando
```bash
ss -a
```
2. Mostrar todos os sockets tcp que están escoitando
```bash
ss -lt
```
3. Mostrar todos os sockets filtrado por estado `conectado`
```bash
ss state established
```
# dig
`dig` é un comando que utilizamos para facer consultas DNS. A consulta máis básica é:
```bash
dig ejemplo.com
```
## Ejemplos
1. Buscar IPs asociadas a un registro tipo A
```bash
dig +short ejemplo.com
```
2. Preguntar por un tipo de registro DNS especifico a un dominio
```bash
dig ejemplo.com [A|MX|TXT|CNAME|NS]
```
3. Especificar un servidor de DNS alternativo para a consulta
```bash
dig @8.8.8.8 ejemplo.com
```
4. Ejecutar unha busqueda de DNS inversa
```bash
dig -x [IP]
```
# Netcat
Podemos utilizar o comando `nc` para escanear se un servidor ten algún porto aberto co seguinte comando
```shell
nc -vz [hostname] [puerto]
```

