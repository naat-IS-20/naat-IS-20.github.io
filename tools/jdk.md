---
layout: default
title: JDK
parent: Herramientas
nav_order: 2
---
# JDK

Es la herramienta necesaria y suficiente para compilar y correr cualquier código
de _Java_.

## Versión

En marzo del 2020, JDK14 será publicado. Entonces no vería mucho sentido usar
JDK13 directamente.

Al ser JDK11 la última versión con soporte a largo plazo, se me hace razonable
que sea la versión de Java que usemos.

De cualquier manera, como Java tiene compatibilidad hacia atrás, usar versiones
más recientes del JDK en el futuro probablemente no tendrá muchos problemas.

En caso de que surgan problemas de compatibildiad, se resolverán en su momento.

## Instalación

La manera más sencilla de instalarlo es usando manejadores de paquetes.

### Mint

```console
$ sudo apt-get update
...
$ sudo apt-get install openjdk-11-jdk
...
```

### Fedora

```console
$ sudo dnf update
...
$ sudo dnf install java-11-openjdk.x86_64
...
```

### Manjaro

```console
$ sudo pacman -Syu jdk11-openjdk
...
```

### MacOS

Hay que agregar el repositorio correspondiente antes de realizar la instalación.

```console
$ brew update
...
$ brew tap homebrew/cask-versions
...
$ brew cask install java11
...
```

### Windows

Como se indicó anteriormente, para Windows se utilizará _Chocolatey_.

```powershell
> choco install openjdk11
```

para OpenJDK o

```powershell
> choco install jdk11
```

para la versión oficial.

## Revisar instalación

En terminal correr

```console
$ java -version
openjdk version "13.0.2" 2020-01-14
OpenJDK Runtime Environment (build 13.0.2+8)
OpenJDK 64-Bit Server VM (build 13.0.2+8, mixed mode)
```

## Manejar versiones

En caso de que alguien ya tenga una versión diferente de Java que desee
conservar, es posible cambiar entre versiones de la JDK.

### Versiones en Mint y Fedora

Existe [`update-alternatives`](https://linux.die.net/man/8/update-alternatives)
que suele estar instalado por omisión.

Para seleccionar el JDK deseado, correr

```console
$ sudo update-alternatives --config java
...
```

### Versiones en Manjaro

Existe [`archlinux-java`](https://wiki.archlinux.org/index.php/Java) que
suele instalarse junto con cualquier JDK.

Para ver las versiones correr

```console
$ archlinux-java status
...
```

Y para asignar alguna de estas versiones, usar

```console
$ archlinux-java set <version>
...
```

### Versiones en MacOS

Una opción es [`jenv`](https://www.jenv.be/). Este se puede instalar con
```homebrew```.

```console
$ brew install jenv
...
```

Luego, para ver las versiones disponibles, usar

```console
$ jenv versions
...
```

Y para asignar la versión requerida, usar

```console
$ jenv global <version>
...
```

### Veriones en Windows

Para Windows no hay muchas opciones.

Se encontró [`jvms`](https://github.com/ystyle/jvms).

Este manejador es simplemente un ejecutable que reescribe vínculos simbólicos.

Basta con [descargarlo](https://github.com/ystyle/jvms/releases), y ejecutarlo
desde ``powershell``.

```powershell
> jvms.exe init
```

Para ver las versiones disponibles, correr

```powershell
> jvms.exe list
```

Y para cambiar la versión, usar

```powershell
> jvms.exe swith <version>
```
