---
layout: page
title: Herramientas
nav_order: 2
has_children: true
permalink: /tools/
---

# Herramientas

Breve presentación de las herramientas necesarias para el proyecto y su
configuración.

El proyecto está desarrollado en _Java_ usando el marco de trabajo _Spring_.

Para todo el manejo de dependenias se usará _Gradle_.

De _Spring_, se usan los proyectos de _Spring Boot_, _Spring JPA_, _Spring Security_ y _Spring Web_, además de
_Thymeleaf_ para las vistas.

_Spring JPA_ permite la integración sencilla de una base de datos, que en este caso será _H2_ para desarrollo y _MySQL_
para producción.

_Spring Web_ proporciona todo lo relacionado con servidores e interacción con _HTTP_.

_Spring Security_ maneja la seguridad de usuarios, sus sesiones, y el acceso restringido usando roles de usuario.

_Thymeleaf_ permite interactuar con objetos de los controladores y variables del proyecto. Por lo que permite mostrar
diferentes vistas dependiendo del usuario.

Y _Spring Boot_ junta todo en un proyecto compacto y sencillo de configurar.
