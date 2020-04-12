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
