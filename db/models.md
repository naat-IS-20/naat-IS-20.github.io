---
layout: default
title: Clases como tablas
parent: DB
nav_order: 1
---

# Clases como tablas

## Entidades

Usando anotaciones, JPA permite definir tablas en bases de datos usando clases normales de _Java_.

Cada atributo se mapea a una columna en la tabla. Para configurar las columnas existen anotaciones más específicas.

Esta clase debe incluir métodos para acceder y modificar todos los atributos.

Una manera sencilla de implementarlos es usando anotaciones de _Lombok_ para generarlos.

Algunas comunes son

* `@Id`: indica la llave de la tabla

* `@GeneratedValue`: valor manejado por la base de datos.

* `@NotNull`: exactamente lo que parece

En el caso más sencillo, tenemos por ejemplo

```java
...
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
...
```

## Relaciones

Definir relaciones se hace a través de anotaciones.

Las relaciones en _JPA_ constan de dos entidades, una de ellas siendo la dueña de la relación.

La dueña debe indicar cualquier detalle extra sobre como se va a comportar la llave foránea.

La otra entidad únicamente tiene que indicar el nombre del atributo al que se mapea.

Algunas anotaciones para relaciones

* `@JoinColumn`: indica una llave foránea. Tiene algunos parámetros

  * `name`: indica el nombre de la llave foránea en la tabla. Es necesaria cuando la llave foránea tiene el mismo
    nombre que un atributo de la clase actual.
  * `nullable`: lo que parece
  * `unique`: lo que parece

  Se pueden consultar el resto de los [atributos][jcol].

* `@JoinColumns`: define una llave foránea compuesta

* `@InverseJoinColums`: defina una llave foránea para la entidad que no es la dueña de la relación.

* `@JoinTable`: indica la tabla que representa la relación. Esto es para las relaciones de muchos a muchos.

  * `name`: nombre de la tabla en la base de datos.

  El resto de los atributos se puede [consultar][mtm].

### Uno a uno

`@OneToOne` tiene varios atributos

* `cascade`: indica como reaccionará la tabla antes modificaciones en la llave foránea.
* `mappedBy`: en la parte no dueña, indica el nombre del atributo en la entidad dueña.
* `optional`: como `nullable`.

Más información en la [documentación][oto].

Una entidad dueña

```java
...
@Data
@Entity
class User {
  @Id
  private String mail;

  @OneToOne
  @JoinColumn(name="cart_id")
  private Cart cart;
}
...
```

Y la otra entidad.

```java
...
@Data
@Entity
class Cart {
  @Id
  @GeneratedValue
  private long id;

  @OneToOne(mappedBy="cart")
  private User user;
}
...
```

### Uno a muchos / muchos a uno

En este caso, creo que tendría más sentido que la entidad única sea la dueña.

Las anotaciones son `@OneToMany` y `@ManyToOne`. La lista de parámetros se puede consultar [aquí][otm] y [aquí][mto]
respectivamente.

Por ejemplo

```java
@Data
@Entity
public class Order {
  @Id
  @GeneratedValue
  private long id;

  @ManyToOne
  @JoinColumn(name="status")
  private Status status;
}
```

Y la entidad de muchos

```java
...
@Data
@Entity
public class Status {
  @Id
  private Long name;

  @ManyToOne(mappedBy="status")
  private List<Order> orders;
}
...
```

### Muchos a muchos

La anotación es `@ManyToMany`. En este caso, se tiene que definir una tabla en la parte de la entidad dueña.

En este caso, las llaves se llaman igual, por lo que hay que renombrarlas en la nueva tabla.

Los demás atributos se puede encontrar [aquí][mtm].

La entidad dueña

```java
...
@Data
@Entity
public class Food {
  @GeneratedValue
  @Id
  private Long id;

  private String name;

  @ManyToMany
  @JoinTable(
    name="food_order",
    joinColumns=@JoinColumn(name="food_id")
    inversJoinColumns=@JoinColumn(name="order_id")
  )
  private List<Order> orders;
}
...
```

Y la otra entidad

```java
@Data
@Entity
public class Order {
  @Id
  @GeneratedValue
  private long id;

  @ManyToMany(mapperBy="orders")
  private List<Food> foods;
}
```

## Algunos tipos de datos

### Fechas

Usar  `LocalDate` del paquete `java.time`.

Para definir una fecha de creación, existe la anotación `@CreationTimestamp`.

```java
...
import java.time.LocalDate;
import org.hibernate.annotations.CreationTimestamp;
...
@CreationTimestamp
private LocalDate delivery_date;
...
```

También existe una fecha de modificación `@UpdateTimestampo` que funciona de la misma manera.

### Dominios específicos

Para restringir valores, usar `Enumerate`. No necesita tener nada especial.

Al poner el atributo en la entidad, debe estar anotado con `@Enumerated`.

Por ejemplo, si se define una enumeración `DeliveryStatus`,

```java
...
import javax.persistence.Enumerated;
import javax.persistence.Enumerated;
...
@Enumerated(EnumType.STRING)
private DeliveryStatus status;
```

## Referencias

* <https://www.baeldung.com/spring-data-rest-relationships>
* <https://www.objectdb.com/api/java/jpa>

[jcol]: https://www.objectdb.com/api/java/jpa/JoinColumn
[oto]: https://www.objectdb.com/api/java/jpa/OneToOne
[otm]: https://www.objectdb.com/api/java/jpa/OneToMany
[mto]: https://www.objectdb.com/api/java/jpa/ManyToOne
[mtm]: https://www.objectdb.com/api/java/jpa/ManyToMany
