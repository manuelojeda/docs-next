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

## Conditionals and Loops

It's easy to toggle the presence of an element, too:

```html
<div id="conditional-rendering">
  <span v-if="seen">Now you see me</span>
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

This example demonstrates that we can bind data to not only text and attributes, but also the **structure** of the DOM. Moreover, Vue also provides a powerful transition effect system that can automatically apply [transition effects](TODO) when elements are inserted/updated/removed by Vue.

You can change `seen` from `true` to `false` in the sandbox below to check the effect:

<p class="codepen" data-height="300" data-theme-id="39028" data-default-tab="js,result" data-user="Vue" data-slug-hash="oNXdbpB" data-preview="true" data-editable="true" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Conditional rendering">
  <span>See the Pen <a href="https://codepen.io/team/Vue/pen/oNXdbpB">
  Conditional rendering</a> by Vue (<a href="https://codepen.io/Vue">@Vue</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

There are quite a few other directives, each with its own special functionality. For example, the `v-for` directive can be used to display a list of items using the data from an Array:

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

## Handling User Input

To let users interact with your app, we can use the `v-on` directive to attach event listeners that invoke methods on our Vue instances:

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

Note that in this method we update the state of our app without touching the DOM - all DOM manipulations are handled by Vue, and the code you write is focused on the underlying logic.

Vue also provides the `v-model` directive that makes two-way binding between form input and app state a breeze:

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

## Composing with Components

The component system is another important concept in Vue, because it's an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components. If we think about it, almost any type of application interface can be abstracted into a tree of components:

![Component Tree](/images/components.png)

In Vue, a component is essentially a Vue instance with pre-defined options. Registering a component in Vue is straightforward: we create a component object as we did with `App` objects and we define it in parent's `components` option:

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

Now you can compose it in another component's template:

```html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

But this would render the same text for every todo, which is not super interesting. We should be able to pass data from the parent scope into child components. Let's modify the component definition to make it accept a [prop](component-basics.html#passing-data-to-child-components-with-props):

```js
app.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})
```

Now we can pass the todo into each repeated component using `v-bind`:

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

This is a contrived example, but we have managed to separate our app into two smaller units, and the child is reasonably well-decoupled from the parent via the props interface. We can now further improve our `<todo-item>` component with more complex template and logic without affecting the parent app.

In a large application, it is necessary to divide the whole app into components to make development manageable. We will talk a lot more about components [later in the guide](component-basics.md), but here's an (imaginary) example of what an app's template might look like with components:

```html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Relation to Custom Elements

You may have noticed that Vue components are very similar to **Custom Elements**, which are part of the [Web Components Spec](https://www.w3.org/wiki/WebComponents/). That's because Vue's component syntax is loosely modeled after the spec. For example, Vue components implement the [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) and the `is` special attribute. However, there are a few key differences:

1. The Web Components Spec has been finalized, but is not natively implemented in every browser. Safari 10.1+, Chrome 54+ and Firefox 63+ natively support web components. In comparison, Vue components don't require any polyfills and work consistently in all supported browsers (IE9 and above). When needed, Vue components can also be wrapped inside a native custom element.

2. Vue components provide important features that are not available in plain custom elements, most notably cross-component data flow, custom event communication and build tool integrations.

Although Vue doesn't use custom elements internally, it has [great interoperability](https://custom-elements-everywhere.com/#vue) when it comes to consuming or distributing as custom elements. Vue CLI also supports building Vue components that register themselves as native custom elements.

## Ready for More?

We've briefly introduced the most basic features of Vue.js core - the rest of this guide will cover them and other advanced features with much finer details, so make sure to read through it all!
