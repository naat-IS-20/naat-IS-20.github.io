---
layout: default
title: Gradle
parent: Herramientas
nav_order: 4
---

# Gradle

Es un manejados de dependencias y constructor de proyecto principalmente para
_Java_.

## Versión

Al ser la versión más reciente estable, se utilizará Gradle 6.

## Instalación

Está disponible en todos los manejadores que se utilizarán excepto por `apt`.

Sin embargo, en los repositorios de Fedora la versión está desactualizada.

### Mint

Este programa no está en los repositorios oficiales, pero existe en forma de
[PPA](https://launchpad.net/~cwchien/+archive/ubuntu/gradle).

Así que primero hay que añadirlo, luego actualziar los registros de `apt`
y finalmente instalarlo.

```console
$ sudo add-apt-repository ppa:cwchien/gradle
...
$ sudo apt-get update
...
$ sudo apt-get install gradle
...
```

### Fedora

Se tiene que instalar [manualmente](https://gradle.org/install/). Se usa la
versión más reciente, pero sólo habría que cambiar el vínculo de descarga
[pertinente](https://gradle.org/releases/) para instalar otra versión.

Para esto, primero se descargan los binarios.

```console
$ wget https://gradle.org/next-steps/?version=6.2.1&format=bin
...
```

Luego hay que descomprimir los archivos. Como se está instalando sin apoyo del
manejador de versiones, lo recomendado es poner todos los archivos en un
directorio dentro de `/opt`.

```console
$ mkdir /opt/gradle
...
$ unzip -d /opt/gradle gradle-6.2.1-bin.zip
...
```

Para poder ejecutarlo utilizando sólo el comando `gradle`, hay que añadirlo
al `PATH` de la sesión.

```console
$ export PATH=$PATH:/opt/gradle/gradle-6.2.1/bin
...
```

Para hacer estos cambios permanentes, habría que añadir esta línea al final del
archivo `~/.profile` y reiniciar la sesión o correr

```console
$ source ~/.profile
...
```

## Manjaro

```console
$ sudo pacman -Syu gradle
...
```

## MacOS

```console
$ brew install gradle
...
```

## Windows

```powershell
> choco install gradle
```

# Revisar instalación

En terminal correr

```console
$ gradle --version
...
```

Y debería imprimir datos sobre la instalación de Gradle.

En mi caso imprime

```console
------------------------------------------------------------
Gradle 6.1.1
------------------------------------------------------------

Build time:   2020-01-26 12:47:38 UTC
Revision:     <unknown>
...
```
