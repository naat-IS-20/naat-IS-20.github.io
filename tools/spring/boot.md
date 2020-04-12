---
layout: default
title: Spring Boot
parent: Spring
grand_parent: Herramientas
nav_order: 1
---

# Spring Boot

Si bien _Spring_ provee varias soluciones, aún es necesario invocarlas e integrarlas en un proyecto funcional. Esto es
sí resulta algo complicado.

Para agilizar esto, se creó _Spring Boot_. Es una herramienta de configuración automática.

Entre otras cosas, _Boot_ busca en el árbol de dependencias e integra las bibliotecas encontradas al proyeco. Luego,
busca archivos de configuración dentro del paquete del proyecto. En caso de no encontrar nada, utiliza una configuración
por omisión.

Para habilitarlo, es suficiente incluir el plugin de _Boot_, como ya está hecho en el proyecto de ejemplo.

```kotlin
plugins {
  id 'org.springframework.boot' version '2.3.0.M4'
  id 'io.spring.dependency-management' version '1.0.9.RELEASE'
  ...
}
...
```

Y anotar la clase `main` como aplicación de _SpringBoot_.

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }
}
```

Como la aplicación está en blanco, al correrla no hace nada.

```console
$ ./gradlew build

BUILD SUCCESSFUL in 21s
5 actionable tasks: 5 executed
```

Dependiendo de las bibliotecas que se incluyan en el proyecto, esta acción
realiza tareas más complicadas.

## Starters

_Boot_ tiene como propósito agilizar el desarrollo. Así que existen ciertas bibliotecas que encapsulan casos de uso
frecuentes.

Se les conoce como _Boot Starters_.

Todos los projectos de ecosistema de _Spring_ tiene un starter. También varias bibliotecas que usualmente se integran
con _Spring_ suelen tener o varios estándares de arquitectura de software comunes.

### Spring Data _JPA_

Este _Starter_ incluye lo necesario para manejar bases de datos desde _Java_ usando el projecto _Spring JPA_.

Para habilitarla sólo hay que agregarla a las dependencias, junto con el driver de la base de datos a user. Para
desarrollo, creo que lo más sencillo es _H2_.

```kotlin
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
  runtimeOnly 'com.h2database:h2'
}
```

Además de manejar la base de datos, se pueden definir tablas como clases de _Java_ y el _DAO_ como una interfaz.
Todo este código generado agiliza el desarrollo general del proyecto.

### Spring Data _REST_

### Spring Security
