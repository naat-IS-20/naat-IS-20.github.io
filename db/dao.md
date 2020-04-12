---
layout: default
title: DAO
parent: DB
nav_order: 2
---

# DAO

_Spring JPA_ provee varias interfaces que en tiempo de compilación se usan para
crear una clase con los métodos necesarios para el DAO.

La que nos es relavante es `CrudRepository<T, ID>`.

Esta declara los siguientes método a implementar.

```java
public interface CrudRepository<T, ID> extends Repository<T, ID> {

  <S extends T> S save(S entity);

  <S extends T> Iterable<S> saveAll(Iterable<S> entities);

  Optional<T> findById(ID id);

  boolean existsById(ID id);

  Iterable<T> findAll();

  Iterable<T> findAllById(Iterable<ID> ids);

  long count();

  void deleteById(ID id);

  void delete(T entity);

  void deleteAll(Iterable<? extends T> entities);

  void deleteAll();
}
```

Para usar esta interfaz, basta con extenderla indicando la clase que representa
la tabla y el tipo de la llave.

```java
package com.example.demo;

import org.springframework.data.repository.CrudRepository;

import com.example.demo.models.Flower;

public interface FlowerRepository extends CrudRepository<Flower, Long>{}
```

Al momento de compilación, _Spring Boot_ encontrará esta interfaz, y generará
una clase concreta encargada de manipular la entidad.
