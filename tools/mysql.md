---
layout: page
title: MySQL
parent: Herramientas
nav_order: 3
---

# MySQL

## Versión

Se usará MySQL 8, al ser la más reciente y aún tener seis años de soporte
restante.

Al ser este software de Oracle, no se encuentra en la mayoría de los
repositorios para Linux.

Una alternativa para esto podría ser remplazarlo con MariaDB, una implementación
abierta de MySQL.

## Instalación

### Mint

No se encuentra en los respositorios, pero Oracle proporciona un
[APT](https://dev.mysql.com/downloads/repo/apt/).

Ingresando a esa página, se tiene que descargar manualmente el archivo de
configuración.

Luego hay que ejecutarlo

```console
$ sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb
...
```

Y se iniciará un programa para configurar algunas variables del repositorio APT.

Hasta donde entendí de momento, basta con dejar todas los campors con los
valores por omisión si no se está seguro de la configuración deseada.

Con el repositorio añadido, se prosigue como de constumbre.

```console
$ sudo apt-get update
...
$ sudo apt-get install mysql-server
...
```

### Fedora

De forma análoga, hay que ir a fepositorio de
[yum](https://dev.mysql.com/downloads/repo/yum/) que proporciona Oracle.

Y descargar la versión pertinente para el SO.

Luego, hay que añadir el paquete al sistema.

```console
$ sudo dnf localinstall mysql80-community-release-fc<OSv>-1.noarch.rpm
...
```

Donde `<OSv>` es la versión de Fedora.

Luego hay que actualizar e instalar.

```console
$ sudo dnf update
...
$ sudo dnf install mysql-community-server
...
```

### Manjaro

Se encuentra en los repositorios no oficiales de AUR.

```console
$ yay -Syu mysql
...
```

### MacOS

Se puede instalar directamente de Homewbrew.

```console
$ brew install mysql
...
```

Y probablemente sea útil instalar un administrador de procesos de sistema para
iniciar y detener MySQL.

```console
$ brew install homebrew/services
...
```

### Windows

Está en los repositorios de Chocolatey.

```powershell
> choco install mysql
```

## Revisar instalación

Antes de revisar la instalación, se debe iniciar el proceso.

En _Linux_

```console
$ sudo systemctl start mysqld
...
```

En _MacOS_

```console
$ brew services start mysql
...
```

En _Windows_

```powershell
> "C:\tools\mysql\mysql-<version>-winx64\bin\mysqld" --console
```

Al momentode esto guía, `<version>=8.0.19`

Revisar que el comando siguiente se ejecute correctamente

```console
$ mysql -v
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.4.12-MariaDB Arch Linux

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
```

En caso de esto ser problemático, se resolverá más adelante.
