---
layout: default
title: Clases como tablas
parent: DB
nav_order: 1
---

# Clases como tablas

## Entidades

Usando anotaciones, JPA permite definir tablas en bases de datos usando clases normales de _Java_.

Las clases deben estar anotadas con `@Entity`. Cada atributo se mapea a una columna en la tabla. Para configurar las
columnas existen anotaciones más específicas.

Esta clase debe incluir métodos para acceder y modificar todos los atributos.

Una manera sencilla de implementarlos es usando anotaciones de Lombok para generarlos.

Algunas comunes son

* `@Id`: indica la llave de la tabla

* `@GeneratedValue`: valor manejado por la base de datos.

* `@NotNull`: exactamente lo que parece

En el caso más sencillo, tenemos por ejemplo

```java
package com.example.demo.models;

import lombok.Data;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.NotNull;

@Data
@Entity
public class Food {
  @GeneratedValue
  @Id
  private Long id;

  private String name;

  @NotNull
  private int price;
}
```

## Relaciones

Definir relaciones se hace a través de anotaciones.

Las relaciones en _JPA_ constan de dos entidades, una de ellas siendo la dueña
de la relación.

La dueña debe indicar cualquier detalle extra sobre como se va a comportar la
llave foránea.

La otra entidad únicamente tiene que indicar el nombre del atributo al que se
mapea.

### Uno a uno

### Uno a muchos / muchos a uno

### Muchos a muchos
