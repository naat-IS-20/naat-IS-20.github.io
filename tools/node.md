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

[_NodeJS_][node] es un ambiente donde se puede correr _Javascript_ sin la necesidad de
un navegador.

Al ser la versión 12.16.2 la más moderna que actualmente tiene soporte a largo
plazo, será la usada para el proyecto.

## Instalación

### _Linux_ y _MacOS_

De manera similar a _Python_, las bibliotecas para _NodeJS_ requieren cierta
versión de _NodeJS_.

Así que de la misma manera que `venv` para _Python_, _NodeJS_ tiene un manejador
de versiones llamado `nvm` ([_Node Version Manager_][nvm]).

Para evitar problemas de compatibilidad, la forma más recomendada de instalar
_NodeJS_ es através de _NVM_.

Para _Mint_ y _Fedora_, hay que hacer la instalación manual.

Por suerte, los desarrolladores de _NVM_ proveen un script que automatiza esa
instalación.

```console
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
...
```

Para _Manjaro_, _NVM_ se encuentra en los repositorios de _AUR_.

```console
$ yay -Syu nvm
...
```

Pasa lo mismo para _MacOS_.

```console
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

Ya con _NVM_ instalado, instalar _NodeJS_ es sencillo.

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

### _Windows_

_NVM_ no ofrece soporte para _Windows_. Pero existe [_NVM for Windows_][nvm_win].

```powershell
> choco install nvm
```

Y para instalar _NodeJS_.

```powershell
> nvm install 12.16.2
...
> nvm use 12.16.2
...
```

## _NPM_

_Node Package Manager_ es una manejador de dependencias para _NodeJS_.

Viene incluido al instalar _NPM_.

## Integración con _Gradle_

Existe un [plugin][node_grd] de para ejecutar comandos de `node` como tareas de _Gradle_.

Dentro de un projeco de _Gradle_, se agreda el plugin.

```groovy
plugins {
  id "com.moowork.node" version "1.3.1"
}
```

Para ejecutar programas de _Javascript_, se definen tareas de tipo `NodeTask`.

```groovy
task script(type: NodeTask) {
  script = file('src/script.js')
  args = ['arg1', ...]
  options = ['--option1', ...]
}
```

Es posible configurar algunos parámetros de `node`

```groovy
node {
  version = '12.16.2'

  // Versión de NPM
  npmVersion = '6.14.4'

  // Donde se van a guardar los archivos de node
  workDir = file("${project.buildDir}/nodejs")

  // Donde estás los módulos a usar
  nodeModulesDir = file("${project.projectDir}")
}
```

Hay una interfaz de tareas para correr comandos _NodeJS_, con la sintaxis `node_<command>`.

Por ejemplo `/.gradlew npm_run_build` o `/.gradlew npm_install`.

## Referencias

* [nvm]

* [node]

* [brew_nvm]

* [nvm_win]

* [node_grd]

* [nvm_win_st]

[nvm]: <https://github.com/nvm-sh/nvm>

[node]: <https://nodejs.org/en/>

[brew_nvm]: <https://formulae.brew.sh/formula/nvm>

[nvm_win]: <https://github.com/coreybutler/nvm-windows>

[nvm_win_st]: <https://docs.microsoft.com/en-us/windows/nodejs/setup-on-windows>

[node_grd]: <https://github.com/srs/gradle-node-plugin>
