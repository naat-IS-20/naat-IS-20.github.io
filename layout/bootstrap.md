---
layout: default
title: Bootstrap
parent: Vista
---

# Bootstrap

[_Bootstrap_][boot] es una biblioteca de _HTML_, _CSS_ y _JavaScript_.

Provee de varios estilos y componentes comunes para usar directamente en la creación de sitios web.

En internet, encontré que está basada en _jQuery_, lo cuál no está recomendado por razones de seguridad a nivel del
_DOM_.

Pero encontré una implementación de _Bootstrap_ que no lo utiliza. Es [_Bootstrap Vue_][boot-vue]. Provee casi las
mismas funcionalidades de _Bootstrap_ pero sin usar _jQuery_. En su lugar utiliza [_VueJS_][vue].

## Instalación

Normalmente se debería incluir como dependencia dentro de un proyecto de desarrollo de interfaz gráfica, pero por el
tiempo creo que preferirían hacer todo en _HTML_ directamente.

Para esto se necesita incluir referencias a los archivos de _Bootstrap al final de la sección de `<head>`.

```html
...
<head>
  ...
  <!-- Load required Bootstrap and BootstrapVue CSS -->
  <link
    type="text/css"
    rel="stylesheet"
    href="//unpkg.com/bootstrap/dist/css/bootstrap.min.css"
  />
  <link
    type="text/css"
    rel="stylesheet"
    href="//unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.min.css"
  />

  <!-- Required scripts -->
  <script src="https://unpkg.com/vue@latest/dist/vue.js"></script>
  <script src="https://unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.js"></script>

</head>
...
```

En _Bootstrap_, al final del código se incluyen scripts de _jQuery_ para renderizar todo. Aquí también es necesario
hacerlo, pero más bien se tienen que inicializar los componetes como componentes de _VueJS_.

Dentro de este componentes, se puede incluir todos los datos necesarios para el componente, así como los scripts
para darle funcionalidad.

```html
...
<body>
  <script>
      window.app = new Vue({
        el: '#<id>',
        data: {<var>: <value>, ...},
        computed: { <func>, ...}
      })
    </script>
</body>
...
```

Esta última sección se puede aislar en un archivo de código a parte para más limpieza.

## Ejemplo

Se crea una carta con una imagen, texto y un botón.

Proviene de la documentación de _Bootstrap vue_.

```html
<!DOCTYPE html>

<html>

  <head>
    <!-- Load required Bootstrap and BootstrapVue CSS -->
    <link
      type="text/css"
      rel="stylesheet"
      href="//unpkg.com/bootstrap/dist/css/bootstrap.min.css"
    />
    <link
      type="text/css"
      rel="stylesheet"
      href="//unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.min.css"
    />

    <!-- Required scripts -->
    <script src="https://unpkg.com/vue@latest/dist/vue.js"></script>
    <script src="https://unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.js"></script>

  </head>

  <body>
    <div id = "card">
      <b-card
        title="Flores"
        img-src="https://picsum.photos/600/300/?image=25"
        img-alt="Image"
        img-top
        style="max-width: 20rem;"
        class="mb-2"
      >
        <b-card-text>
          Texto de ejemplo
        </b-card-text>
        <b-button href="#" variant="primary">Click</b-button>
      </b-card>
    </div>

    <script>
      new Vue({
        el: '#card'
      })
    </script>
  </body>
</html>
```

Que se renderiza a lo siguiente

![flower card](/assets/images/bootstrap_vue_card.png)

Más ejemplos y explicaciones más profundas se pueden encontrar en la [documentación][vue-docs].

## Referencias

* [boot]
* [boot-vue]
* [vue]
* [vue-start]
* [vue-docs]

[boot]: https://getbootstrap.com/
[boot-vue]: https://bootstrap-vue.js.org/
[vue]:https://vuejs.org/
[vue-start]: https://bootstrap-vue.js.org/docs/reference/starter-templates/
[vue-docs]: https://bootstrap-vue.js.org/docs/components/
