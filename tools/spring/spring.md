---
layout: default
title: Spring
parent: Herramientas
has_children: true
nav_order: 5
permalink: /tools/spring
---

# Spring

_Spring_ es un ecosistema para desarrollo de aplicaciones en _Java_ (también tiene soporte para otros lenguajes basados
en la _JVM_).

Provee muchas soluciones para problemas de desarrollo de software comunes como configuración de servidores, manejo de
bases de datos, autentificación y seguridad, manejo de _URL_, diseño de micro-servicioes y pruebas unitarias y de
integración.

Consta de una gran cantidad de proyectos que se dedican a soluciones en diferentes ámbitos, cada uno con muchos módulos
aún más especializados.

Por ejemplo

* _Spring Framework_: funcionamiento base, como dependencias y manejo de datos.

* _Spring Boot_: configuración automática de proyectos

* _Spring Data_: manejo de bases de datos

* _Spring Security_: autorización e identificación

Necesitaremos estos en el desarrollo del proyecto.

Para ilustrar el funcionamiento de todos, se usará un proyecto demo mínimo.

## Creación de proyectos

La manera recomendada para iniciar proyectos con _Spring_ es _[Initializr]_.

![Spring Initializr](/assets/images/initializr.png)

Este permite especificar el manejador de dependencias (Gradle para nosotros), la versión de _Spring_(procurar elegir una
versión RELEASE o MILESTONE), la versión de _Java_ (11 para nosotros), las dependencias iniciales y el nombre y paquete
del proyecto de forma gráfica.

Después de descomprimir el proyecto generado, tiene la siguiente estrucutra.

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
├── HELP.md
├── settings.gradle
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── demo
    │   │               └── DemoApplication.java
    │   └── resources
    │       └── application.properties
    └── test
        └── java
            └── com
                └── example
                    └── demo
                        └── DemoApplicationTests.java

14 directories, 10 files
```

Que es una estructura común para proyectos de _Gradle_.

Este proyecto siempre es una aplicación de _Spring Boot_.

## Referencias

* <https://www.baeldung.com/spring-why-to-choose>
* <https://docs.spring.io/spring/docs/current/spring-framework-reference/>
* <https://spring.io/projects>

[Initializr]: https://start.spring.io/
