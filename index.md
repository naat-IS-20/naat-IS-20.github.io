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

# Arquitectura

Se va a usar _MVC_.

Para implementar esto, se va a tener un servidor _REST_ desarrollado en _Spring_ y un cliente de _Angular_ para consumir
la _API REST_.

En términos generales, creo que las grandes partes del proyecto son

* [La base de datos](/db/)

* [Los usuarios](/auth/)

* [La interfaz gráfica](/ui/)

# Pasos

De acuerdo a la guía de construcción de software, hay que hacer lo siguiente.

1. Instalar las herramientas

    * [_MySQL_](/tools/mysql)

    * [_JDK_](/tools/jdk)

    * [_Gradle_](/tools/gradle)

    * [_NodeJS_](/tools/node)

    * [_Angular_](/tools/angular)

    Y en general leer la sección de [herramientas](/tools/) para tener una idea general de como funcionan las
    tecnologías que se van a usar.

2. Crear el repositorio.

    Esta tarea está explicada en parte en sección de [_multimódulos de Gradle_](/tools/gradle#multi-módulos), pero
    también requiere configurar un proyecto de [_Boot_](/tools/spring/boot) y un proyecto de [_Angular_](/tools/angular)
    que esté configurado con el plugin de [_Node para Gradle_](/tools/node#integración-con-gradle).
    Además, hay que realizar una inyección de dependencias para unir los dos proyectos. Como todo esto está tan
    disperso, se creó una [guía](/repo/) que lo junta todo.

3. Homologar la apariencia de la vista.

    Las generalidades de la vista se describen en su [sección](/ui/).

4. Crear la base de datos.

    La creación de las tablas, configuración de llaves foráneas se encuentran en la sección de [entidades](/db/models).

    Lo relacionado con los _CRUD_ de la base de datos está en la sección del [_DAO_](/db/dao).

5. Implementar cada caso de uso

6. Integrar todos los casos
