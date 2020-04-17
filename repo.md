---
layout: default
title: Repositorio
permalink: /repo/
nav_order: 6
---

# Crear el repositorio

## Estrucutura

El proyecto va a constar de un cliente de _Angular_ que consume una _API_ de
_Spring_. Estos deben estar contenidos dentro de un proyecto multimódulo de
_Gradle_.

En necesario tener instalado el [_JDK_](/tools/jdk), [_Gradle_](/tools/gradle), [_NodeJS_](/tools/node) y
[_Angular_](/tools/angular).

Primero, se crea el multimódulo como un proycto básico de _Gradle_.

```console
.
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── settings.gradle
```

Luego, se crean las dos carpetas.

```console
.
├── nix-app <--
├── nix-ui <--
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── settings.gradle
```

## Condfiguración de la _UI_

En `nix-ui` se inicia un proyecto de _Angular_. Y se crea un archivo `build.gradle` para configurar el proyecto desde
_Gradle_.

```console
.
├── angular.json
├── browserslist
├── build.gradle <--
├── dist
├── e2e
├── karma.conf.js
├── node_modules
├── package.json
├── package-lock.json
├── README.md
├── src
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.spec.json
└── tslint.json
4 directories, 11 files

```

En ese archivo, se debe indicar que se usará el plugin de `node`.

```groovy
plugins {
  id 'com.github.node-gradle.node' version '2.2.3'
}
```

Y la configuración de `node`.

```groovy
node {
  version = '13.11.0'
  npmVersion = '6.14.4'
  download = true
}
```

Finalmente, hay que asegurarse de que al momento de generar los ejecutables desde _Gradle_, el proyecto esté construido.

```groovy
build.dependsOn npm_run_build
```

## Configuración de la API

En `nix-app` se agrega un nuevo proyecto de _Spring Initializr_. Los ejecutables son innecesarios al ya estar presentes
en el proyecto raíz.

```console
.
├── build.gradle
├── HELP.md
└── src
    ├── main
    └── test
```

## Configuración del proyecto raíz

Se tiene que especificar la versión de _JDK_ a usar. Como tiene que coincidir en ambos proyectos, se usa `subprojects`.

```groovy
subprojects {
  apply plugin: 'java'
  sourceCompatibility = '11'
}
```

Luego, hay que inyectar un par de dependencias.

Primero, se va a introducir al proyecto compilado de _Angular_ al projecto de _Spring_ para que se genere un sólo
ejecutable final.

```groovy
project(':nix-app') {
  dependencies {
    implementation project(':nix-ui')
  }

  build.dependsOn ':nix-ui:build'
}
```

Además, por omisión, _Angular_ compila sus archivos en `dist/<project>`. Pero _Spring_  lee los archivos desde `static`.
Así que se copian los archivos.

```groovy
project(':nix-ui') {
  jar {
    from 'dist/nix-ui'
    into 'static'
  }
}
```

Por último, resulta que los plugins de _Spring_ no se encuentras en el repositorio por omisión de _Gradle_.

Estos ya vienen añadidos en el proyecto de _Spring Inializr_, pero como también se va a correr este proyecto desde la
raíz, también hay que habilitat los repositorios extra en el proyecto raíz.

Se tiene que agregar lo siguiente a `settings.gradle` del proyecto raíz.

```groovy
pluginManagement {
  repositories {
    maven { url 'https://repo.spring.io/milestone' }
    gradlePluginPortal()
  }
 }
```

Y por supuesto, no hay que olvidar declara explícitamente los subproyectos en ese mismo archivo.

```groovy
include 'nix-ui', 'nix-app'
```

## Correr proyectos

Para la interfaz

```console
$ ./gradlew npm_start

> Task :nix-ui:npm_start

> nix-ui@0.0.0 start
> ng serve

chunk {main} main.js, main.js.map (main) 60.7 kB [initial] [rendered]
...
Date: 2020-04-16T07:07:29.743Z - Hash: 142456302bd17297637d - Time: 9833ms
** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **
: Compiled successfully.
<========-----> 66% EXECUTING
> :nix-ui:npm_start
```

Para la _API_

```console
$ ./gradlew bootRun

> Task :nix-app:bootRun

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::             (v2.3.0.M4)

...
2020-04-16 02:08:33.404  INFO 381889 --- [main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page: class path resource [static/index.html]
2020-04-16 02:08:33.481  INFO 381889 --- [main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-04-16 02:08:33.485  INFO 381889 --- [main] com.example.app.AppApplication           : Started AppApplication in 1.835 seconds (JVM running for 2.334)
<===========--> 87% EXECUTING
> :app:bootRun
```

Y para construir el ejecutable

```console
$ ./gradlew build

> Task :nix-app:test
2020-04-16 02:11:12.181  INFO 387226 --- [extShutdownHook] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'

> Task :nix-ui:npm_run_build

> nix-ui@0.0.0 build
> ng build

Generating ES5 bundles for differential loading...
ES5 bundle generation complete.

...

BUILD SUCCESSFUL in 24s
10 actionable tasks: 4 executed, 6 up-to-date
```

Que genera un ejecutable en `nix-app/build/libs`.

Que se puede ejecutar como

```console
$ java -jar nix-app/build/libs/nix-app-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::             (v2.3.0.M4)

2...
2020-04-16 02:14:12.119  INFO 393367 --- [main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-04-16 02:14:12.128  INFO 393367 --- [main] com.example.app.AppApplication           : Started AppApplication in 3.69 seconds (JVM running for 4.45)

```

Este ejecutable está corriendo tanto la interfaz gráfica como la _API_ al mismo tiempo de forma optimizada.

Es lo que al final será lo que se desplegará en un servidor.
