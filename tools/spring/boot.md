---
layout: default
title: Spring Boot
parent: Spring
grand_parent: Herramientas
nav_order: 1
---

# Spring Boot

Si bien _Spring_ provee varias soluciones, aún es necesario invocarlas e integrarlas en un proyecto funcional. Esto
puede resultar complicado.

Para agilizar esto, se creó _Spring Boot_. Es una herramienta de configuración automática.

Entre otras cosas, _Boot_ busca en el árbol de dependencias e integra las bibliotecas encontradas al proyeco. Luego,
busca archivos de configuración dentro del paquete del proyecto para configurar las bibliotecas encontradas. En caso de
no encontrar nada, utiliza una configuración por omisión.

Para habilitarlo, es suficiente incluir el plugin de _Boot_, como ya está hecho en el proyecto de ejemplo.

```gradle
plugins {
  id 'org.springframework.boot' version '2.3.0.M4'
  id 'io.spring.dependency-management' version '1.0.9.RELEASE'
  ....
}
....
```

Hay que notar que este plugin no se encuentra en el repositorio por omisión de plugins para _Gradle_. Así que hay que
agregarlo explícitamente.

Por razones que no comprendo bien, los plugins deben ser cargados antes de la ejecución de todos los demás bloques. Por
lo que el repositorio de plugins debe especifcarse en un bloque especial en `settiings.gradle`.

```gradle
pluginManagement {
  repositories {
    maven { url 'https://repo.spring.io/milestone' }
    gradlePluginPortal()
  }
}
```

Y finalmente, hay que anotar la clase `main` como aplicación de _SpringBoot_.

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

_Spring JPA_ es una especificación sobre un sistema de _ORM_ (_Object Relational Mapping_). Esto permite definir y
manejar bases de datos y todo lo relacionado con manejo de datos persistentes por medio de clases de _Java_. Esto es
para poder usar cuaquier _DBMS_ sin tener que modificar la definición de la base de datos.

La implemetación que se usa por omisión es [_Hibernate_][hib].

Para habilitarla sólo hay que agregarla a las dependencias, junto con el driver de la base de datos a user. Para
desarrollo, creo que lo más sencillo es _H2_.

```gradle
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
  runtimeOnly 'com.h2database:h2'
}
```

Además de manejar la base de datos, automatiza la creación de tablas como clases de _Java_, provee implementaciones
generadas de _DAO_ a través de interfaces, provee implementación automática de operaciones _CRUD_ y también provee una
interfaz sencilla para definir comandos de _SQL_ directamente.

Y se puede definir un script poblar la base de datos agregando el archivo `src/main/resources/data.sql`.

Todo estás acciones automáticas agilizan el desarrollo general del proyecto.

Como se van a usar estas características está explicado en la sección de la [base de datos](/db/).

### Spring Security

## Referencias

* [hib]

[hib]: https://hibernate.org/
