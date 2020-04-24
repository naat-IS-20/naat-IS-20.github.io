---
layout: default
nav_order: 6
permalink: /service/
---

# Servicios

Contienen la lógica del caso de uso.

Hace uso de repositorio de las entidades para proveer de funcionalidad al
controlador que maneja los _URLs_.

Por buena práctica de programación, deben ir marcados como `@Service`, aunque esta anotación no genera ninguna
modificación de parte de _Spring_.

## Injección de atributos

Con la anotación `@Autowired` se inicializan los atributos sin necesidad de especificarlo en el constructor.
