---
layout: page
title: Manejadores de Software
parent: Herramientas
nav_order: 1
---
# Manejadores de software

Las distribuciones de _Linux_ proveen manejadores de software para facilitar la instalación y actualización de software,
entre otras cosas.

Para _MacOS_ y _Windows_ hay alternativas similares para hacer la instalación de las herramientas necesarias lo más
sencillo posible.

## Homebrew

_[Homebrew]_ es uno de los manejadores de paquetes de software más populares para MacOS.

Es lo que se utilizará para la instalación de todas las herramientas.

Requiere _[Ruby]_.

Hay que correr el comando

```console
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
...
```

Y para verificar la instalación, correr

```console
$ brew help
...
```

## Chocolatey

_[Chocolatey]_ es un manejador de software para Windows que funciona de manera similar a los manejadores para Linux o
_Homebrew_ para MacOS.

Es lo que se usará en la instalación en Windows de todas las herramientas necesarias para el proyecto.

En `powershell` correr el siguiente comando

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
```

Y para verificar la instalación, correr

```powershell
choco
```

[Homebrew]: https://brew.sh/
[Ruby]: https://www.ruby-lang.org/en/
[Chocolatey]: https://chocolatey.org
