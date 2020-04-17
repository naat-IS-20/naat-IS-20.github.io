---
layout: default
title: DB
has_children: true
permalink: /db/
nav_order: 3
---

# Base de datos

En el proyecto, _Spring JPA_ se encarga de manipular la base de datos, por lo que rara vez se tendrá que modificar
directamente.

Lo único necesario es configurar su conexión.

Fuera de esto, más bien es necesario aprender a usar la _API_ de _JPA_ para definir entidades persistentes.

## DBMS

_Spring JPA_ intenta ser agnóstico respecto a los manejadores. Esto es que ninguna funcionalidad implementada en código
tenga que ver directamente con la base de datos usada.

Las propiedades de la base de datos están en el archivo `src/main/resources/application.properties`.

Algunas propiedades comunes son

```properties
#Indica donde está la base de datos
spring.datasource.url

#Indica el driver
spring.datasource.driverClassName

#Usuario de la base de datos
spring.datasource.username

#Constraseña del usuario
spring.datasource.password

#Indica como se inicia la base de datos.
spring.jpa.hibernate.ddl-auto
```

`spring.jpa.hibernate.ddl-auto` puede tener varios valores

* `create` crea la base de datos cada vez que se corre el proyecto

* `update` añade lo necesario a la base existente

* `crate-drop` igual que `create`, pero la base de datos es eliminada al cerrar el proyecto

* `none` no hace nada

### H2

El _DBMS_ más sencillo de usar con _Spring_ es _H2_.

Es una base de datos relacional implementada en _Java_. Es muy ligera y puede correr totalmente en memoria.

Por esto, no requiere configuración de usuarios, controladores ni permisos de ningúnn tipo. Así que es perfecta para
pruebas y desarrollo.

Sólo se debe declara como dependencia en un proyecto de _Boot_ que tenga el starter de _Data JPA_, y será configurada
automáticamente.

```gradle
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
  runtimeOnly 'com.h2database:h2'
}
```

Y con esto se tiene una base relacional de prueba.

Por omisión el sistema corre en memoria, pero es posible usar una base de datos persistente.

```properties
#spring.datasource.url=jdbc:h2:mem Indica que la base de datos está en memoria y es privada

# Para guardar la base de datos en un archivo
spring.datasource.url=jdbc:h2:file:<path>
```

Y también provee una consola. Es necesario definir `spring.datasource.url` para acceder a ella.

```gradle
spring.datasource.url=jdbc:h2:mem:testdb
spring.h2.console.enabled=true
```

Se encuentra en `localhost:<port>/h2_console`. Por omisión, `<port>=8080`.

Por omisión, el usuario es `sa` y no tiene contraseña. Se debe especificar la `url` de la base de datos.

![H2 Login](/assets/images/h2_login.png)

![H2 Console](/assets/images/h2_console.png)

### MySQL

Hay que agregar la dependencia

```gradle
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
  runtimeOnly 'mysql:mysql-connector-java'
}
```

Y configurar la conexión

```gradle
spring.datasource.url=jdbc:mysql://<host>:<port>:<dbname>
spring.datasource.username=<user>
spring.datasource.password=<password>
spring.jpa.hibernate.ddl-auto=update
```

Por lo general, `<host>=localhost` y `<port>=3306`.

## Referencias

* <https://www.h2database.com>
* <https://www.baeldung.com/spring-boot-data-sql-and-schema-sql>
* <http://www.h2database.com/html/features.html>
* <https://www.baeldung.com/spring-boot-h2-database>
* <https://www.baeldung.com/the-persistence-layer-with-spring-data-jpa>
* <https://spring.io/guides/gs/accessing-data-mysql/>
