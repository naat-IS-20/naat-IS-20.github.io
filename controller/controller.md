---
layout: default
nav_order: 8
permalink: /controller/
---

# Controlador

Atiende las peticiones _HTTP_ que lleguen a la página. Debe ser lo más sencillo posible. Culquier tipo de procesamiento
no trivial debe ser transiferido al servicio correspondiente.

Utilizan la anotación `@Controller`.

## Peticiones

Se pueden especificar las direcciones que se van a atender con la anotación `@RequestMapping`. Puede ser usada tanto en
clases como en métodos.

También se pueden especificar el tipo de petición por método usando `@GetMapping`, `@PostMapping` o su análogo del tipo
de petición necesaria.

Usando la anotación `@RequestBody` antes de un parámetro en la firma de un método, se puede deserializar el cuerpo de la
petición en el tipo adecuado.
