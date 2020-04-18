<!---
layout: default
title: Angular
parent: Herramientas
nav_order: 8
--->

# Angular

_Angular_ es un marco de trabajo para desarrollo de interfaces gráficas para sitios web.

Utiliza _TypeScript_, _HTML_ y _CSS_ para definir las vistas.

Provee también provee módulos para ruteo.

## Instalación

_Angular_ provee una herramiento de línea de comandos `ng` para manejar sus proyecos. Se puede instalar con `npm`.

```console
$ npm install -g @angular/cli
[ .................] - loadDep:readable-stream: sill resolveWithNewModule stream-shift@1.0.1 checking installable st
[ .................] - loadDep:readable-stream: sill resolveWithNewModule stream-shift@1.0.1 checking installable st
...

+ @angular/cli@9.1.1
added 272 packages from 207 contributors in 57.725s
```

## Proyectos

Se crea un nuevo proyecto

```console
$ ng new app-ui
? Would you like to add Angular routing? Yes
? Which stylesheet format would you like to use? CSS
...

✔ Packages installed successfully.
    Successfully initialized git.
```

Y para correrlo, desde el directorio recien creado,

```console
$ ng serve

chunk {main} main.js, main.js.map (main) 60.7 kB [initial] [rendered]
...
Date: 2020-04-16T06:12:49.830Z - Hash: 142456302bd17297637d - Time: 10716ms
** Angular Live Development Server is listening on localhost:4200, open your browser on http://localhost:4200/ **
: Compiled successfully.
```

Que inicia el proyecto por omisión de _Angular_.

![DefulatAngular](/assets/images/angular_default.png)

## Referencias

* <https://angular.io/guide/setup-local>
