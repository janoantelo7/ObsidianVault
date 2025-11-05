# Instalación
Para instalar Go debemos acceder á seguinte web que nos explica os pasos necesarios dependendo do noso sistema operativo: [Download and install - The Go Programming Language](https://go.dev/doc/install).

A continuación pondrei os pasos de como instalar Go (1.24.0) en unha distribución de **linux**. O primeiro paso é descargarse o fichero comprimido desde a seguinte web: [All releases - The Go Programming Language](https://go.dev/dl/).

Unha vez temos o link, movemonos á carpeta `/tmp` do sistema.
```bash
cd /tmp
```

Dentro de este directorio, procedemos coa descarga do fichero comprimido.
```bash
wget https://go.dev/dl/go1.24.0.linux-amd64.tar.gz
```

Cando remate a descarga do fichero, o seguinte será borrar calquer instalación previa de Go e instalar a nova versión.
```bash
sudo  rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.24.0.linux-amd64.tar.gz
```

> [!WARNING] 
> Non descomprimir o fichero no path `/usr/local/go`, onde xa haxa unha instalación de Go. Esto rompe a instalación de Go.

Finalmente, añadimos o path `/usr/local/go/bin` ao PATH do sistema.
```bash
export PATH=$PATH:/usr/local/go/bin
```

Esta linea podese engadir en `$HOME/.{config_shell}` ou ben `/etc/profile` se queremos unha instalación en todo o sistema. Os cambios vanse ver reflexados unha vez reiniciemos o sistema ou cando recarguemos a terminal.

Podemos verificar a instalación de Go oc seguinte comando.
```bash
go version
```
