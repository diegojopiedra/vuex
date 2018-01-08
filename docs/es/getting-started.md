# Primeros Pasos

En el centro de cada aplicación Vuex está la  **tienda**. Una "tienda" es básicamente un contenedor que almacena los **estados** de su aplicación. Hay dos cosas que hacen que una tienda Vuex sea diferente de un simple objeto global:

1. Las tiendas Vuex son reactivas. Cuando los componentes de Vue obtienen el estado de la tienda, se actualizarán de manera reactiva y eficiente si cambia el estado de esta.

2. No puedes cambiar directamente el estado de la tienda. La única forma de cambiar el estado de una tienda es mediante **llevar a cabo explícitamente las mutaciones**. Esto garantiza que cada cambio de estado deje un registro de seguimiento y habilite herramientas que nos ayuden a comprender mejor nuestras aplicaciones.

### La tienda más simple

> **NOTA:** Usaremos la sintaxis de ES2015 en los ejemplos de código para el resto de la documentación. Si aún no lo has visto [¡debieras!](https://babeljs.io/docs/learn-es2015/)!

Después de [instalar](installation.md) Vuex, creemos una tienda. Es bastante sencillo - solo definimos un objeto de estado inicial y algunas mutaciones:

``` js
// Asegúrese de llamar a Vue.use(Vuex) primero si usa un sistema de módulo

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

Ahora puede acceder al objeto de estado como `store.state` y activar un cambio de estado con el método `store.commit`:

``` js
store.commit('increment')

console.log(store.state.count) // -> 1
```

De nuevo, la razón por la cual estamos llevando a cabo una mutación en lugar de cambiar `store.state.count` directamente, es porque queremos rastrearla explícitamente. Esta sencilla convención hace que su intención sea más explícita, por lo que puede razonar mejor sobre los cambios de estado en su aplicación al leer el código. Además, esto nos da la oportunidad de implementar herramientas que pueden registrar cada mutación, tomar instantáneas de estado (snapshots), o incluso realizar el debugeo de viaje en el tiempo.

Usar la tienda de estados en un componente simplemente implica devolver el estado dentro de una propiedad calculada **(computed property)**, porque el estado de la tienda es reactivo. Desencadenar cambios simplemente significa llevar a cabo mutaciones en los métodos de los componentes.

Aquí hay un ejemplo de la aplicación de contador [Vuex más básica](https://jsfiddle.net/n9jmu5v7/1269/).

A continuación, discutiremos cada concepto central en detalle, empezando por el [Estado](state.md).
