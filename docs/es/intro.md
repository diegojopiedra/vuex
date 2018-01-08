# ¿Que es Vuex?

<<<<<<< HEAD
Vuex es un  **patrón de gestion de estados + librería** para aplicaciones Vue.js. Sirve como una tienda centralizada para todos los componentes de una aplicación, con reglas que garantizan que el estado solo se puede mutar de manera predecible. También se integra con [la extensión devtools](https://github.com/vuejs/vue-devtools) oficial de Vue para proporcionar características avanzadas como la depuración de viaje en el tiempo, el zero-config y la exportación / importación de instantáneas (snapshot) de estado.
=======
Vuex es un  **patrón de gestion de estados + librería** para aplicaciones Vue.js. Sirve como una tienda centralizada para todos los componentes de una aplicación, con reglas que garantizan que el estado solo se puede mutar de manera predecible. También se integra con [la extensión devtools](https://github.com/vuejs/vue-devtools) oficial de Vue para proporcionar características avanzadas como la depuración, el viaje en el tiempo, el zero-config y la exportación / importación de instantáneas (snapshot) de estado.

>>>>>>> a4c218b9416ebc0d1726269f5e56b08187f52939

### ¿Que es un "Patrón de Gestion de Estados"?

Comencemos con una simple aplicación de contador con Vue:

``` js
new Vue({
  // estado
  data () {
    return {
      count: 0
    }
  },
  // vista
  template: `
    <div>{{ count }}</div>
  `,
  // acciones
  methods: {
    increment () {
      this.count++
    }
  }
})
```

Esta es una aplicación autocontenida con las siguientes partes:

- El **estado**, que es la fuente de la verdad que conduce nuestra aplicación;
- La **vista**, que no es más que un mapeo declarativo del **estado**;
- Las **acciones**, las cuales son las formas en que el estado podría cambiar en relación con las entradas del usuario desde la **vista**.

Esta es una representación extremadamente simple del concepto de "one-way data flow" (flujo de datos unidireccional):

<p style="text-align: center; margin: 2em">
  <img style="width:100%;max-width:450px;" src="./images/flow.png">
</p>

Sin embargo, la simplicidad se rompe rápidamente cuando tenemos **varios componentes que comparten un estado común**:

- Varias vistas pueden depender de la misma pieza de estado.
- Las acciones desde diferentes vistas pueden necesitar mutar la misma pieza de estado.

Para el problema uno, pasar propiedades **(props)** puede ser tedioso para componentes profundamente anidados, y simplemente no funciona para componentes hermanos. Para el problema dos, a menudo nos encontramos recurriendo a soluciones como pasar referencias directas a instancias padre/hijo o intentando mutar y sincronizar múltiples copias del estado a través de eventos. Ambos patrones son frágiles y conducen rápidamente a un código inmanejable.

Entonces, ¿por qué no extraemos el estado compartido de los componentes y lo administramos en un singleton global? Con esto, nuestro árbol de componentes se convierte en una gran "vista", y cualquier componente puede acceder al estado o desencadenar acciones, ¡sin importar dónde se encuentren en el árbol!

Además, al definir y separar los conceptos involucrados en la administración del estado y hacer cumplir ciertas reglas, también le damos a nuestro código más estructura y capacidad de mantenimiento.

Esta es la idea básica detrás de Vuex, inspirada en [Flux](https://facebook.github.io/flux/docs/overview.html), [Redux](http://redux.js.org/) y [The Elm Architecture](https://guide.elm-lang.org/architecture/). A diferencia de los otros patrones, Vuex es también una implementación de librería diseñada específicamente para Vue.js para aprovechar su sistema de reactividad granular para actualizaciones eficientes.

![vuex](./images/vuex.png)

### ¿Cuándo debería usarlo?

A pesar de que Vuex nos ayuda a lidiar con la gestión compartida del estado, también viene con el costo de más conceptos y repeticiones. Es un balance entre la productividad a corto y largo plazo.

Si nunca ha construido un SPA a gran escala y entra directamente en Vuex le puede parecer verboso e intimidante. Vuex no es indispensable en un proyecto y si su aplicación es simple, lo más probable es que esté bien sin Vuex. Un simple [bus de eventos globales](https://vuejs.org/v2/guide/components.html#Non-Parent-Child-Communication) puede ser todo lo que necesita. Pero si está construyendo un SPA de mediana a gran escala, es probable que se haya topado con situaciones que lo hagan pensar sobre cómo manejar mejor el estado desde fuera de sus componentes de Vue, y Vuex será el siguiente paso natural para usted. Hay una buena cita de Dan Abramov, el autor de Redux:

> Las librerías Flux son como gafas: **usted sabrá cuándo las necesita.**
