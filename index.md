---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Home
permalink: /
nav_order: 1
---

# Nixtamal
{: .fs-9 }

Especificaciones de las herramientas y generalidades de las partes principales del proyecto.
{: .fs-6 }

# Pasos

De acuerdo a la guía de construcción de software, hay que hacer lo siguiente.

1. Instalar las herramientas

    * [_MySQL_](/tools/mysql)

    * [_JDK_](/tools/jdk)

    * [_Gradle_](/tools/gradle)

    Y en general leer la sección de [herramientas](/tools/) para tener una idea general de como funcionan las
    tecnologías que se van a usar.

2. Crear el repositorio.

     Requiere crear un proyecto de [_Spring_](/tools/spring) con las siguientes dependencias

     * _Spring Web_: servidor

     * _Spring Data JPA_: base de datos

     * _Spring Security_: usuarios

     * _MySQL Driver_: base de datos

     * _Thymeleaf_: vista

     * _Lombok_: optimiza descripción de la base de datos

3. Homologar la apariencia de la vista.

4. Crear la base de datos.

    La creación de las tablas, configuración de llaves foráneas se encuentran en la sección de [entidades](/db/models).

    Lo relacionado con los `CRUD` de la base de datos está en la sección del [_DAO_](/db/dao).

5. Implementar cada caso de uso

    Cada caso de uso debe ser implementado en el contexto de una caracterísitca del sistema.

    * Usuarios: esto requiere, además de los modelos, manejar sesiones. [_Spring Security_](/auth/) proporciona algunas
        soluciones al respecto.
    * Menu
    * Ordenes

    Y cada una debe tener completar las siguientes secciones

    * El [servicio](/service/): la lógica del caso de uso.
    * El [controlador](/controller/): mapear las peticiones _HTTP_ a las acciones del servicio.
    * Las [vistas](/layout/): como _HTML_ en conjunto con _Thymeleaf_.

    Para esto deben usar el _DAO_ proporcionado por los modelos. Puede modificarse de ser necesario.

6. Integrar todos los casos
