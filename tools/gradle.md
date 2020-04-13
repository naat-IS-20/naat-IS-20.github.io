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
$ wget https://gradle.org/next-steps/?version=<version>&format=bin
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

### Manjaro

```console
$ sudo pacman -Syu gradle
...
```

### MacOS

```console
$ brew install gradle
...
```

### Windows

```powershell
> choco install gradle
```

## Revisar instalación

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

## Projectos

### Creación

Existe `gradle init` para iniciar proyectos.

```console
$ gradle init
Starting a Gradle Daemon (subsequent builds will be faster)

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 1

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Project name (default: demo):

> Task :init
Get more help with your project: https://guides.gradle.org/creating-new-gradle-builds

BUILD SUCCESSFUL in 27s
2 actionable tasks: 2 executed
```

Dependiendo del tipo de proyecto, elegir las opciones adecuadas genera ligeramente diferentes archivos, pero nada
que no se pueda hacer fácilmente de forma manual.

Este es el proyecto más básico.

```console
$ tree
.
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── settings.gradle

2 directories, 6 files
```

`setting.gradle` es la configuración local de _Gradle_ y `build.gradle` son las tareas del projecto.

`gradlew` significa _Gradle Wrapper_. Son archivos ejecutables. Esto se debe a que para construir un proyecto no es
necesario tener _Gradle_ instaldao. Se captura la configuración en los archivos ejecutables.

Para verificar que todo funciona bien, es mejor usar siempre estos ejecutables en lugar de `gradle` directamente.

Nunca se modifican manualmente, por lo que sólo hay que ignorarlos.

### Tareas

_Gradle_ usa un dialecto de _Groovy_(también puede usar _Kotlin_), un lenguje similar a _Python_ que corre en la _JVM_.

En contraste con _Maven_, que usa _XML_, esto significa que los archivos de configuración de _Gradle_ son
_Turing-Completos_.

Cada proyecto define _tareas (tasks)_, que se ejecutan por medio de línea de comandos.

Estas tareas son implementadas como funciones de _Groovy_.

Un ejemplo de la guía es crear una tarea que copie un archivo del directorio `src` al directorio `dst`.

```groovy
task copy(type: Copy, group: "Custom", description: "Copies sources to the dest directory") {
    from "src"
    into "dest"
}
```

Las tareas disponibles en el proyecto se pueden ver con `.\gradlew tasks`.

En el projecto recien creado, se tienen

```console
$ ./gradlew tasks

> Task :tasks

------------------------------------------------------------
Tasks runnable from root project
------------------------------------------------------------

Build Setup tasks
-----------------
init - Initializes a new Gradle build.
wrapper - Generates Gradle wrapper files.

Help tasks
----------
buildEnvironment - Displays all buildscript dependencies declared in root project 'demo'.
components - Displays the components produced by root project 'demo'. [incubating]
dependencies - Displays all dependencies declared in root project 'demo'.
dependencyInsight - Displays the insight into a specific dependency in root project 'demo'.
dependentComponents - Displays the dependent components of components in root project 'demo'. [incubating]
help - Displays a help message.
model - Displays the configuration model of root project 'demo'. [incubating]
outgoingVariants - Displays the outgoing variants of root project 'demo'.
projects - Displays the sub-projects of root project 'demo'.
properties - Displays the properties of root project 'demo'.
tasks - Displays the tasks runnable from root project 'demo'.

To see all tasks and more detail, run gradlew tasks --all

To see more detail about a task, run gradlew help --task <task>

BUILD SUCCESSFUL in 1s
1 actionable task: 1 executed
```

### Plugins

Para reciclar tareas comunes, se pueden incluir algo similar a bibliotecas de tareas. Se denominan plugins.

Por ejemplo, el plugin `java` agrega funcionalidad para construir archivos `jar`.

_Spring_ tiene diferentes plugins que son de mucha ayuda para generar gran parte de los proyectos.

### Multi módulos

Es posible que uun mismo archivo de _Gradle_ se encargue de manipular varios proyectos a la vez.

Con los dos proyectos ya configurados en _Gradle_, basta con agregar ambos a un nuevo proyecto que los contenga.

En este la carpeta que los contenga, se debe inicializar un projecto en blanco.

Se modifica `setting.gradle`

```groovy
include 'project1', 'project2', ...
```

Pero tener varios projectos no implica nada más. En general esto se hace por depedencia entre diferentes partes del
proyecto. Esto se puede hacer agregando un proyecto como dependencia de otro.

Por ejemplo, si `project2` requiere de `proyect1`, entonces `proyect2/build.gradle` tendría la siguiente dependencia.

```groovy
dependencies {
  compile project('project1')
}
```

La sintaxis de `project` indica que se debe obtener de otro módulo de _Gradle_ en el mismo multi-proyecto.

## Referencias

* <https://gradle.org/>

* <https://guides.gradle.org/creating-new-gradle-builds/>

* <https://guides.gradle.org/creating-multi-project-builds/>