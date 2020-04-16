---
layout: default
title: Lombok
parent: Herramientas
nav_order: 6
---

# Lombok

[_Lombok_][lombok] una biblioteca de _Java_ que genera código en tiempo de compilación para agilizar el desarrollo.

_Boilerplate code_ es un término para describir código necesario pero que no requiere ningún ingenio humano.

Cosas como _Getters_ y _Setters_, constructores sin parámetros, o logs.

El propósito de _Lombok_ es sustituir este código con anotaciones.

Además, provee mecanismo para inferencia de tipos para variables locales.

## Depencencia

Se encuentra en los repositorios usados por _Gradle_. Además de incluirlo como dependencia, hay que indicar que se usará
como procesador de anotaciones.

```groovy
depenencies {
  compileOnly 'org.projectlombok:lombok'
  annotationProcessor 'org.projectlombok:lombok'
}
```

## `@Getter` y `@Setter`

Proveen acceso para atributos. Por omisión son públicos, pero se puede modificar.

Por ejemplo

```java
package com.example.demo.models;

import lombok.Getter;
import lombok.Setter;
import lombok.AccessLevel;

public class Flower {

  @Getter
  private String species;

  @Getter @Setter(AccessLevel.PROTECTED)
  private String name;

  @Getter @Setter
  private int price;
}
```

Es equivalente a

```java
package com.example.demo.models;

public class Flower {

  private String species;

  private String name;

  private int price;

  public String getSpecies() {
    return this.species;
  }

  public String getName() {
    return this.name;
  }

  protected void setName(String name) {
    this.name = name;
  }

  public int getPrice() {
    return this.price;
  }

  public void setPrice(int price) {
    this.price = price;
  }
}
```

Es posible aplicarlos a toda la clase, y excluir casos usando otra anotación.

```java
package com.example.demo.models;

import lombok.Getter;
import lombok.Setter;
import lombok.AccessLevel;

@Getter
@Setter
public class Flower {

  private String species;

  @Setter(AcessLevel.PROTECTED)
  private String name;

  @Setter(AccessLevel.NONE)
  private int price;
}
```

## `@Data`

Especifica que un objeto será usado para almacenar información.

```java
package com.example.demo.models;

import lombok.data;

@Data
public class Flower {

  private String species;

  private String name;

  private int price;
}
```

Se traduce a varias otras anotaciones.

* `@Getter` para todos los atributos.

* `@Setter` para todos los atributos no finales.

* `@ToString` incluye el tipo y la lista de atributos.

```java
"Type(param1=<val>,param2=<val>,...)"
```

* `@EqualsAndHash` que incluye igualdad por igualdad de atributos y una implemetanción de un algoritmo de dispersión.

* `@RequiredArgsConstrucutor` que genera un constructor con todos los atributos.

Con todo lo que provee, usarlo ahorra la imlementación de cualquier método al crea tablas como clases.

## Referencias

* [lombok]

* <https://www.baeldung.com/intro-to-project-lombok>

[lombok]: https://projectlombok.org
