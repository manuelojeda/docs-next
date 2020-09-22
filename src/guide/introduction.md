# Introducción

## ¿Qué es Vue.js?

Vue (pronunciado /viuː/) es un **framework progresivo** para construir interfaces de usuario. A diferencia de otros frameworks monolíticos, Vue esta diseñado desde cero para ser incrementalmente. La librería núcleo se enfoca unicamente en la capa de la vista, y es fácil de adaptar con tros librerías o proyectos ya existentes. Por el otro lado, Vue es perfectamente capaz de dar poder a sofisdticadas Aplicaciones de una Sola Página cuando se usa una combinación con [herramientas modernas](../guide/single-file-component.html) y [librerías que tienen soporte](https://github.com/vuejs/awesome-vue#components--libraries).

Si quieres aprender más sobre Vue antes de entrar a fondo, hemos<a id="modal-player"  href="#">creado un video</a> repasando a traves de los principios centrales y en un proyecto simple.

Si eres un desarrollador frontend con experiencia y quieres saber como Vue se compara con otras librerias/frameworks, mira la [Comparación con Otros Frameworks](TODO:comparison.html).

## Iniciando

<p>
  <ActionLink class="primary" url="installation.html">
    Instalación
  </ActionLink>
</p>

::: tip
La guía oficial asume que cuenta con un conocimiento intermedio de HTML, CSS, y JavaScript. Si eres un desarrollador frontend totalmente nuevo, puede que no sea la mejor idea iniciar con un framework como primeros pasos - aprende las bases y entonces vuelves! La experiencia con otros frameworks ayuda, pero no es requerido.
:::

La manera más fácil de probar Vue.js es usando el [ejemplo de Hola Mundo](https://codepen.io/team/Vue/pen/KKpRVpx). Sientete libre de abrirlo en otra pestaña y continua a través de otros ejemplos básicos.

La página de [Instalación](installation.md) provee más opciones de como instalar Vue. Nota: **No** recomendamos que principiantes inicien con el `vue-cli`, especialmente si no estás familiarizado con herramientas basadas en Node.js.

## Renderizado Declarativo

El núcleo de Vue.js es un sistema que nos habilita renderizar declarativamente datos al DOM utilizando una sintaxis de template:

```html
<div id="hello-vue">
  {{ message }}
</div>
```

```js
const HelloVueApp = {
  data() {
    return {
      message: 'Hello Vue!'
    }
  }
}

Vue.createApp(HelloVueApp).mount('#hello-vue')
```
Ya hemos creado nuestra primer app en Vue! Esto se parece en renderizar un string template, pero Vue ha hecho bastante trabajo bajo el capo. Los datos y el DOM ahora están vínculados, y ya todo es **reactivo**. ¿Cómo lo sabemos? Cambia la propiedad `message` en el snippet que se encuentra debajo con algún valor diferente y el ejemplo se renderizará con la debida actualización:

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="js,result" data-user="Vue" data-slug-hash="KKpRVpx" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Intro-1">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/KKpRVpx">
  Intro-1</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Además de la interpolación de texto, también podemos vincular el atributo del elemento así:

```html
<div id="bind-attribute">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound
    title!
  </span>
</div>
```

```js
const AttributeBindingApp = {
  data() {
    return {
      message: 'You loaded this page on ' + new Date().toLocaleString()
    }
  }
}

Vue.createApp(AttributeBindingApp).mount('#bind-attribute')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="KKpRVvJ" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Attribute dynamic binding">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/KKpRVvJ">
  Attribute dynamic binding</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Nos hemos encontrado con algo nuevo. El atributo `v-bind` qu es estamos viendo es llamado como una **directiva**. Las Directivas son prefijos con `v-` para indicar que son atributos especiales provistos por Vue, y como habrás adivinado, ellos aplican un comportamiento de reactividad especial al DOM renderizado. Aquí basicamente estamos diciendo "_manten el atributo `título` de este elemento title` actualizado con propiedad `mensaje` de esta instancia de Vue._"

## Condicionales y Ciclos

También es muy fácil cambiar la presencia de un elemento:

```html
<div id="conditional-rendering">
  <span v-if="seen">Ahora me ves</span>
</div>
```

```js
const ConditionalRenderingApp = {
  data() {
    return {
      seen: true
    }
  }
}

Vue.createApp(ConditionalRenderingApp).mount('#conditional-rendering')
```

Este ejemplo demuestra que podemos vincular datos no solo en atributos y textos, si no tambien en ***estructuras* del DOM. Además, Vue también provee un sistema de efectos de transición que aplica dichos efectos automáticamente cuando el elemento es insertado/actualizado/removido por Vue.

Puedes cambiar `seen` de `true` a `false` in el siguiente sandbox para mirar su efecto:

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="js,result" data-user="Vue" data-slug-hash="oNXdbpB" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Conditional rendering">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/oNXdbpB">
  Conditional rendering</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Existen algunas otras directivas, cada una con una funcionalidad especial. Por ejemplo, la directiva `v-for` puede ser utilizada para mostrar una lista de elementos usando los datos desde un arreglo:

```html
<div id="list-rendering">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```

```js
const ListRenderingApp = {
  data() {
    return {
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' }
      ]
    }
  }
}

Vue.createApp(ListRenderingApp).mount('#list-rendering')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="mdJLVXq" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="List rendering">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/mdJLVXq">
  List rendering</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Manejando la Interacción del Usuario

Para dejar que el usuario interactue con tu app, podemos usar la directiva `v-on` para escuchar eventos que invocan metodos de nuestra instancia de Vue:

```html
<div id="event-handling">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

```js
const EventHandlingApp = {
  data() {
    return {
      message: 'Hello Vue.js!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}

Vue.createApp(EventHandlingApp).mount('#event-handling')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="dyoeGjW" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Event handling">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/dyoeGjW">
  Event handling</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Notemos que con este método actualizamos el estado de nuestra app sin tocar el DOM - todas las manipulaciones del DOM son manejadas por Vue, y el código que tu escribes se concentra la lógica subyacente.

Vue también provee la directiva `v-model` que es la bindeo de dos-caminos entre el input de nuestro formulario y el estado de la aplicación:

```html
<div id="two-way-binding">
  <p>{{ message }}</p>
  <input v-model="message" />
</div>
```

```js
const TwoWayBindingApp = {
  data() {
    return {
      message: 'Hello Vue!'
    }
  }
}

Vue.createApp(TwoWayBindingApp).mount('#two-way-binding')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="poJVgZm" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Two-way binding">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/poJVgZm">
  Two-way binding</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Componer con Componentes

El sistema de componentes es otro concepto importante en Vue, porque la abstracción que nos permite construit aplicaciones a gran escala compuestas de componentes pequeños, auto contenidos y reutilizables. Si lo pensamos, casi cualquier tipo de interfaz puede ser abstracto en un arbol de componentes:

![Component Tree](/images/components.png)

En Vue, un componente es en esencia otra instancia de Vue con opciones predefinidas. Registrar un componente en Vue es sencillo:  creamos un objeto componente tal como lo hicimos con `App`y definimos que el parte de los componentes del padre:

```js
// Create Vue application
const app = Vue.createApp(...)

// Define a new component called todo-item
app.component('todo-item', {
  template: `<li>This is a todo</li>`
})

// Mount Vue application
app.mount(...)
```
Ahora lo componemos en el template de otro componente:

```html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```
Pero esto haría el render del mismo texto para cada `todo`, lo cual no es nada interesante. Debemos de ser capaces de pasar los datos desde el padre al componente hijo. Modifiquemos la definición del componente para que acepte una [propiedad](component-basics.html#passing-data-to-child-components-with-props):

```js
app.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})
```

Ya podemoss pasar el `todo` en cada iteración del componente usando `v-bind`:

```html
<div id="components-app">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```

```js
const ComponentsApp = {
  data() {
    return {
      groceryList: [
        { id: 0, text: 'Vegetables' },
        { id: 1, text: 'Cheese' },
        { id: 2, text: 'Whatever else humans are supposed to eat' }
      ]
    }
  }
}

const app = Vue.createApp(ComponentsApp)

app.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})

app.mount('#components-app')
```

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="result" data-user="Vue" data-slug-hash="VwLxeEz" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Intro-Components-1">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/VwLxeEz">
  Intro-Components-1</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Este es un ejemplo artificioso, pero hemos separado nuestra aplicación en dos unidades pequeñas, y el hijo está desacoplado de manera razonable desde el padre a través de la interfaz de propiedades. Ya podemos mejorar nuestro componente `<todo-item>` con un template más complejo y con otra lógica sin afectar la aplicación del padre.

En una aplicación más grande, es necesario dividir toda la app en componentes para tener un desarrollo más manejable. Hablaremos más de componentes [después en la guía](component-basics.md), pero aquí tenemos un ejemplo (imaginario)  de como se miraría una app a través de la separación de componentes:

```html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Relación de Elementos Personalizados

Habrás notado que los componentes de Vue son similares a **Elementos Personalizados**, el cual son parte de [Web Components Spec](https://www.w3.org/wiki/WebComponents/). Eso es porque la sintaxis de componentes de Vue está modelado desde esta especificación. Por ejemplo, los componentes de Vue implementan el [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md)  y el atributo especial `is`. Sin embargo, tenemos algunas diferencias claves:

1. La Especificación de Componentes para la Web ha sido finalizada, pero no ha sido implementada nativamente en cada navegador. Safari 10.1+, Chrome 54+ y Firefox 63+ tienen dicho soporte nativo. En comparación, los componentes de Vue no requieren de polyfills y de trabajo constante para dar soporte a cada navegador (IE9 y superior). Cuando lo necesitamos, los componentes de Vue también pueden contener otros elementos personalizados de forma nativa.

2. Los componentes de Vue proveen características importantes que no están disponibles en elementos personalizados de forma plana, mayormente el flujo de información entre componentes, eventos de comunicación personalizada y herramientas de integración.

Claro está que Vue no utiliza elementos personalizados de manera interna, el cual tiene una [gran interoperabilidad](https://custom-elements-everywhere.com/#vue) cuando se trata de consumir o distribuir dichos elementos. El Vue CLI también da soporte a la creación de componentes de Vue que se registran como elementos personalizados de forma nativa.

## ¿Listo para más?

Te hemos introducimos de forma resumida las características base de Vue.js - el resto de la guía los cubre así como el resto de características avanzadas con mayor detalle, así que asegurate de leerlos!
