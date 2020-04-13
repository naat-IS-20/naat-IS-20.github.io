---
layout: default
title: NodeJS
parent: Herramientas
nav_order: 7
---

# NodeJS

_Javascript_ es un lenguaje que está implementado en los navegadores.

Tradicionalmente se usaba para manejar aspectos de la vista de las páginas.

Pero actualmente se puede usar para muchas cosas fuera del navegador.

_NodeJS_ es un ambiente donde se puede correr _Javascript_ sin la necesidad de
un navegador.

Al ser la versión 12.16.2 la más moderna que actualmente tiene soporte a largo
plazo, será la usada para el proyecto.

## Instalación

De manera similar a _Python_, las bibliotecas para _NodeJS_ requieren cierta
versión de _NodeJS_.

Así que de la misma manera que `venv` para _Python_, _NodeJS_ tiene un manejador
de versiones llamado `nvm` (_Node Version Manager_).

Para evitar problemas de compatibilidad, la forma más recomendada de instalar
_NodeJS_ es através de `nvm`.

Para _Mint_ y _Fedora_, hay que hacer la instalación manual.

Por suerte, los desarrolladores de `nvm` proveen un script que automatiza esa
instalación.

```console
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
...
```

Para _Manjaro_, `nvm` se encuentra en los repositorios de _AUR_.

```console
$ yay -Syu nvm
...
```

Pasa lo mismo para _MacOS_.

```console
$ brew update
...
$ brew install nvm
...
```

En cada caso, es necesario reiniciar la sesión de terminal o actualizar los
valores manualmente. Esto último depende del tipo de terminal.

Con `bash` sería

```console
$ source ~/.profile
...
```

Y para verificar la instalación

```console
$ command -v nvm
nvm
```

Ya con `nvm` instalado, instalar _NodeJS_ es sencillo.

```console
$ nvm install --lts
Installing latest LTS version.
Downloading and installing node v12.16.2...
Downloading https://nodejs.org/dist/v12.16.2/node-v12.16.2-linux-x64.tar.xz...
############################################################################################################# 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v12.16.2 (npm v6.14.4)
```

## Referencias

* <https://github.com/nvm-sh/nvm>

* <https://nodejs.org/en/>

* <https://formulae.brew.sh/formula/nvm>
