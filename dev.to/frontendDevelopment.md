# Frontend Development - How do the UI Applications work?

&emsp; So when I was surfing **Reddit**, I came across [what a framework like Vue does behind the scene.](https://www.reddit.com/r/vuejs/comments/1115jor/what_does_a_framework_like_vue_do_behind_the_scene/) that intrigued me. As there is a lot of information on how a framework/library handles the **Dynamic UI**, I thought to write up. This will serve as a starting point for anyone relatively new and trying to understand what is happening behind the code they type and a memory refresher for season veterans. 

## Intro

&emsp; Have you ever wondered how websites become interactive and dynamic, responding to user actions and displaying information seamlessly? A lot has changed since the early days of static HTML pages. Today, building a website requires a deep understanding of the design and the functionality that powers the user experience. Even though there are drag-and-drop website builders like *WordPress*, *SquareSpace*, etc., for people from non-IT backgrounds, yet building web applications by profession requires the developer to have profound knowledge of the same. To build dynamic and interactive websites that are more accessible and more efficient, frontend frameworks such as **Angular** and **VueJS** have been developed.

> <em> If you are wondering about **ReactJS**, it is not a full-blown **framework.** It is a **JavaScript library** to create UI. Still, it is **equivalent** to a framework as it gets the job done. </em>

<img src="https://i.postimg.cc/xTYZnJ1f/image.png" />

## Frontend Development

&emsp; Frontend development refers to creating and implementing a website or web application's **User Interface (UI)** and **User Experience** (**UX**). It involves working with technologies such as **HTML**, **CSS**, and **JavaScript** to create visually appealing and interactive web pages. The primary focus of front-end development is to enhance the user experience by making web pages visually appealing, interactive, and user-friendly.

&emsp; A front-end developer creates a website or web application's look, feel, and behavior. They work closely with designers to bring the design to life and with backend developers to ensure that the web application doesn’t provide outdated content by integrating it appropriately.

&emsp;There are a lot of frontend frameworks like **[Angular](https://angular.io)**, **[VueJS](https://vuejs.org)**, **[SvelteJS,](https://svelte.dev)** etc., and Libraries like **[ReactJS](https://reactjs.org)**, etc.,

## Frontend Frameworks

&emsp; As web applications grow in complexity, the need for efficient and scalable front-end development solutions has become increasingly apparent. Frontend frameworks provide tools and components that make developing complex and dynamic web applications easier. They offer a simplified and consistent way of working with **HTML**, **CSS**, and **JavaScript** and provide a range of functionalities, including state management, **DOM** manipulation, and component-based architecture.

&emsp; These frameworks/libraries handle many of the complex and repetitive tasks involved in front-end development, freeing up the developer to focus on the unique and creative aspects of the project.  They define both the **HTML** template and **JavaScript** behavior of **UI** elements, with templates providing the **HTML** structure and including variables, bindings, and expressions that are dynamically evaluated at runtime. Reactive data binding allows developers to bind the application state to the **UI** in a declarative manner, ensuring that changes in the state are automatically reflected in the **UI** and vice versa. State management is responsible for keeping track of the values of variables, user interactions, and other data affecting the application's behavior. Event handling handles user interactions and other events, while routing manages navigation between different pages or views.

<img src="https://miro.medium.com/v2/resize:fit:828/format:webp/0*AAUG5KTeZawlLRbP.png" />

## Working model of the Frontend frameworks

&emsp; So, now that we know what a frontend library or a framework is, let’s discuss the working model of the same. At its core, a frontend framework like **VueJS** is an intermediary between the user interface and the underlying data and logic. It provides a set of abstractions and tools that make it easier for developers to manage the **DOM (Document Object Model)**, which is the hierarchical representation of the content and structure of a web page.

&emsp; One can argue that a web application can be built with **HTML**, **CSS**, and **JavaScript** without external libraries or frameworks. Yes, it is possible. But, maintaining the codebase for an extensive application, better understanding, and debugging will become tedious. Consider a simple to-do list application that allows users to add, edit, and delete items. With a frontend framework like **VueJS**, instead of manipulating the **DOM** to update the list of items manually, the developer can update a **JavaScript** object that represents the state of the application, and the framework will take care of automatically update the **DOM**.

> Herein after, **VanillaJS** will refer to plain/pure **JavaScript**

### VanillaJS implementation for rendering a list of todos and adding a todo item

```javascript
<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript">
      var todoList = [];

      function addTodo() {
        var todoInput = document.getElementById("todoInput").value;
        todoList.push(todoInput);
        renderTodos();
      }

      function renderTodos() {
        var todoListElem = document.getElementById("todoList");
        todoListElem.innerHTML = "";
        for (var i = 0; i < todoList.length; i++) {
          todoListElem.innerHTML += "<li>" + todoList[i] + "</li>";
        }
      }
    </script>
  </head>
  <body>
    <input type="text" id="todoInput" />
    <button onclick="addTodo()">Add Todo</button>
    <ul id="todoList"></ul>
  </body>
</html>

```

### VueJS implementation of rendering a list of todos and adding a todo item

```vue
<div id="app">
  <input type="text" v-model="newTodo" />
  <button @click="addTodo">Add Todo</button>
  <ul>
    <li v-for="todo in todos">{{ todo }}</li>
  </ul>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
var app = new Vue({
  el: "#app",
  data: {
    newTodo: "",
    todos: []
  },
  methods: {
    addTodo: function() {
      this.todos.push(this.newTodo);
      this.newTodo = "";
    }
  }
});
</script>
```

&emsp; We can see from the above code the **VueJS** code is more concise and organized, making it easier to understand and maintain. With **VueJS**, we can bind data to the view using directives like `v-model` and `v-for`, making it easier to keep the view and data in sync. The code also uses an object-oriented approach to manage the state and behavior of the application, as opposed to using imperative code to manipulate the **DOM** in the **Vanilla HTML** and **Vanilla JS** examples.

&emsp; The **DOM API** is a low-level API that allows developers to interact with and manipulate the content and structure of a web page. It provides a set of methods for accessing and modifying the elements of a web page, such as adding and removing elements, changing the styles, and more. While the **DOM API** is powerful, it can also be complex and cumbersome, especially for more complex applications. This is where front-end frameworks like **VueJS** come in. They encapsulate the **DOM API** and provide a higher-level API that is more developer-friendly and abstracts away much of the complexity of working with the DOM. Let’s discuss some of the key concepts of the working model compared with the **Vanilla JS** approach.

- **Templating**:

&emsp;In **VueJS**, a template is a string or **HTML**-like syntax representing your application's structure. The template is compiled into a render function that generates a **Virtual DOM.** The **Virtual** **DOM** is a lightweight representation of the actual **DOM**, which **VueJS** uses to optimize updates and improve performance.

```vue
<!-- VueJS template -->
<div id="app">
  <h1>{{ message }}</h1>
</div>

```

In **VanillaJS**, we manually create and manipulate the actual **DOM** using APIs like `document.createElement()` and `appendChild()`. Here's an example of creating an element and appending it to the document using **VanillaJS**:

```javascript
// Vanilla JS code
const appDiv = document.createElement('div');
const h1 = document.createElement('h1');
const text = document.createTextNode('Hello, Vanilla JS!');
h1.appendChild(text);
appDiv.appendChild(h1);
document.body.appendChild(appDiv);
```

As you can see, the VanillaJS code is more verbose and requires more code to achieve the same result.

- **Reactive Data binding:**

&emsp; In **VueJS**, you can define reactive data properties in the `data` object. **VueJS** automatically updates the virtual DOM when reactive property changes and re-renders the affected components.

```javascript
// VueJS app
const app = new Vue({
  el: '#app',
  data: {
    message: 'Hello, VueJS!',
  },
});
```

&emsp; In **VanillaJS**, we manually create event listeners and update the DOM when a data property changes. Here's an example of creating an event listener and updating the DOM using **VanillaJS**:

```javascript
// Vanilla JS code
const h1 = document.querySelector('h1');
let message = 'Hello, Vanilla JS!';
h1.textContent = message;

const button = document.querySelector('button');
button.addEventListener('click', () => {
  message = 'Hello, Vanilla JS! (updated)';
  h1.textContent = message;
});
```

&emsp; As you can see, the vanilla JS code is more complex and requires more code to achieve the same result.

- **Components**

&emsp; In **VueJS**, you can define components as reusable building blocks for your application. Each component encapsulates its state, props, and behavior, making it easier to reason and test.

```vue
<!-- VueJS component -->
<template>
  <div>
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello, VueJS!',
      message: 'This is a VueJS component',
    };
  },
};
</script>
```

In **VanillaJS**, we manually define and organize our code into modules and use techniques like the Revealing Module Pattern to encapsulate state and behavior. Here's an example of defining a module using vanilla JS:

```javascript
// Vanilla JS code
const module = (function() {
  let title = 'Hello, Vanilla JS!';
  let message = 'This is a Vanilla JS module';

  function setTitle(newTitle) {
    title = newTitle;
    update();
  }

  function setMessage(newMessage) {
    message = newMessage;
    update();
  }

  function update() {
    const h1 = document.querySelector('h1');
    const p = document.querySelector('p');
    h1.textContent = title;
    p.textContent = message;
  }

  return {
    setTitle,
    setMessage,
  };
})();
```

- **Lifecycle Methods (Hooks)**

In VueJS, you can define lifecycle hooks to perform actions at specific stages of the component's lifecycle, such as when it is created, mounted, updated, or destroyed.

```javascript
// VueJS component with lifecycle hooks
export default {
  data() {
    return {
      message: 'Hello, VueJS!',
    };
  },
  created() {
    console.log('Component created');
  },
  mounted() {
    console.log('Component mounted');
  },
  updated() {
    console.log('Component updated');
  },
  destroyed() {
    console.log('Component destroyed');
  },
};
```

&emsp; To achieve this functionality, we can follow the below approach in VanillaJS.

```javascript
class MyComponent {
  constructor() {
    console.log('Component is constructed');
  }

  connectedCallback() {
    console.log('Component is connected');
    this.innerHTML = '<div>Hello, Vanilla JS!</div>';
  }

  disconnectedCallback() {
    console.log('Component is disconnected');
  }

  attributeChangedCallback(name, oldValue, newValue) {
    console.log(`Attribute "${name}" has changed from "${oldValue}" to "${newValue}"`);
  }

  adoptedCallback() {
    console.log('Component is adopted');
  }
}

// Define the new custom element
customElements.define('my-component', MyComponent);
```

> *We're creating a custom element using the `customElements` API, which allows us to define a new HTML element that can be used in our markup. The `MyComponent` class represents the implementation of the new custom element, and it defines various methods that are part of the custom element's lifecycle. To know more about the `customElements`, refer to https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements)*

Here are the **VanillaJS** lifecycle methods that are defined in the example above:

- `constructor`: This method is called when a new instance of the custom element is created. It's similar to the VueJS `beforeCreate` hook, allowing you to perform initialization and setup before the element is connected to the DOM.
- `connectedCallback`: This method is called when the custom element is added to the DOM. It's similar to the VueJS `mounted` hook, allowing you to perform a setup that requires DOM access, such as adding event listeners or updating the component's content.
- `disconnectedCallback`: This method is called when the custom element is removed from the DOM. It's similar to the VueJS `beforeDestroy` hook, allowing you to perform cleanup tasks, such as removing event listeners or freeing up resources.
- `attributeChangedCallback`: This method is called when an attribute of the custom element is changed. It allows you to respond to changes in the element's properties and update its content accordingly. This method is similar to the VueJS `updated` hook, but it only applies to changes in attributes rather than changes in the component's data.
- `adoptedCallback`: This method is called when the custom element is moved to a new document. It's similar to the VueJS `mounted` hook but only relevant in rare cases where the custom element moves between documents.

&emsp; These are a few important topics/concepts that help us understand what happens behind the code we write when we use a framework like **VueJS** and how the respective framework/library handles the dynamic nature of a front-end application. And I just took **VueJS** for a quick comparison. Generally, any framework or library might follow this approach to provide an easy, manageable, and scalable developer experience and architecture.

## Conclusion

&emsp; In conclusion, utilizing a front-end framework like **VueJS** can significantly simplify the development process and provide advanced features compared to writing everything in **Vanilla** **HTML** and **VanillaJS**. However, it is essential to understand the fundamental concepts and principles of front-end development to make the most out of these tools. Whether for personal or professional purposes, learning front-end development can lead to exciting and creative opportunities in the digital world.