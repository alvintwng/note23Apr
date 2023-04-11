Note on Vue learning

- [Essentials](#essentials))
- [Components In Depth](#components-in-depth)
- [from Tutorial](#from-tutorial)

---

#### note on start keys
* npm init vue@latest
* cd <vue-project>
* npm install
* npm run dev
* `http://localhost:5173/`

[top]: topOfThePage
####  reference notes

* installed Node.js node-v18.15.0-x64.msi
, with Chocolatey (should not install, for python & visualStudio)
* reference:
	- https://vuejs.org/guide/introduction.html#what-is-vue
	- https://www.tutorialspoint.com/vuejs/vuejs_tutorial.pdf
	- https://vuejs.org/guide/quick-start.html#creating-a-vue-application
	- https://www.tutorialspoint.com/nodejs/nodejs_environment_setup.htm
* Verify installation:
	- Executing a File hello.js
	``` js
	/* Hello, World! program in node.js */
	console.log("Hello, World!")
	```
	- execute
	``` console
	AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/vueWk28/230330WhatIs
	$ node hello.js
	Hello, World!

	AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/vueWk28/230330WhatIs
	$ npm --version
	9.5.0

	AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/vueWk28/230330WhatIs
	$ node --version
	v18.15.0
	```


### Quick Start
``` console
npm init vue@latest
```
``` console
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/vueWk28/230330WhatIs
Need to install the following packages:
  create-vue@3.6.1
Ok to proceed? (y) y

Vue.js - The Progressive JavaScript Framework

√ Project name: ... vue-project
√ Add TypeScript? ... No / Yes
√ Add JSX Support? ... No / Yes
√ Add Vue Router for Single Page Application development? ... No / Yes
√ Add Pinia for state management? ... No / Yes
√ Add Vitest for Unit Testing? ... No / Yes
√ Add an End-to-End Testing Solution? » No
√ Add ESLint for code quality? ... No / Yes

Scaffolding project in C:\Users\AlvinNg\vueWk28\230330WhatIs\vue-project

Done. Now run:

  cd vue-project
  npm install
  npm run dev

npm notice
npm notice New minor version of npm available! 9.5.0 -> 9.6.2
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.6.2
npm notice Run npm install -g npm@9.6.2 to update!
npm notice

```
- cd vue-project
- npm install
- npm run dev
``` console
  VITE v4.2.1  ready in 565 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h to show help
```
- show `You did it!` in browser, `http://localhost:5173/`

---
### default code
index.html
``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```
src/main.js
``` js
import { createApp } from 'vue'
import App from './App.vue'

import './assets/main.css'

createApp(App).mount('#app')

```
src/App.vue
``` vue
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
```



### Introduction
#### Single-File Components
https://vuejs.org/guide/introduction.html#single-file-components

just revised App.vue
#### Options API
``` vue
<script>
  export default {
    // Properties returned from data() become reactive state
    // and will be exposed on `this`.
    data() {
      return {
        count: 0
      }
    },

    // Methods are functions that mutate state and trigger updates.
    // They can be bound as event listeners in templates.
    methods: {
      increment() {
        this.count++
      }
    },

    // Lifecycle hooks are called at different stages
    // of a component's lifecycle.
    // This function will be called when the component is mounted.
    mounted() {
      console.log(`The initial count is ${this.count}.`)
    }
  }
</script>
```
#### Composition API
``` vue
<script setup>
import { ref, onMounted } from 'vue'

// reactive state
const count = ref(0)

// functions that mutate state and trigger updates
function increment() {
  count.value++
}

// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

---
vue-intor.html. https://vuejs.org/guide/quick-start.html#using-the-global-build
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>VueJs Introduction</title>
</head>
<body>
    <div id="app">{{ message }}</div>
    <script type="module">
        import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        createApp({
            data() {
                return {
                    message: 'Hello Vue!!'
                }
            }
        }).mount('#app')
    </script>
</body>
</html>
```

Using JavaScript Expressions
``` js
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div :id="`list-${id}`"></div>
```

Dynamically Binding Multiple Attributes
``` js
data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```
can bind them to a single element by using v-bind without an argument:
``` html
<div v-bind="objectOfAttrs"></div>
```

Calling Functions
``` js
<span :title="toTitleDate(date)">
  {{ formatDate(date) }}
</span>
```

Arguments
``` js
<a v-bind:href="url"> ... </a>
<!-- shorthand -->
<a :href="url"> ... </a>

<a v-on:click="doSomething"> ... </a>
<!-- shorthand -->
<a @click="doSomething"> ... </a>

<a v-bind:[attributeName]="url"> ... </a>
<!-- shorthand -->
<a :[attributeName]="url"> ... </a>

<a v-on:[eventName]="doSomething"> ... </a>
<!-- shorthand -->
<a @[eventName]="doSomething">

<!-- This will trigger a compiler warning. -->
<a :['foo' + bar]="value"> ... </a>
```

---

## Essentials
### Reactivity Fundamentals	
Declaring Reactive State
``` js
import { reactive } from 'vue'

const state = reactive({ count: 0 })	
```
ref: https://vuejs.org/guide/extras/reactivity-in-depth.html

To use reactive state in a component's template, declare and return them from a component's setup() function:
``` js
import { reactive } from 'vue'

export default {
  // `setup` is a special hook dedicated for composition API.
  setup() {
    const state = reactive({ count: 0 })

    // expose the state to the template
    return {
      state
    }
  }
}
```
``` html
<div>{{ state.count }}</div>
```
Similarly, we can declare functions that mutate reactive state in the same scope and expose them as methods alongside the state:
``` js
import { reactive } from 'vue'

export default {
  setup() {
    const state = reactive({ count: 0 })

    function increment() {
      state.count++
    }

    // don't forget to expose the function as well.
    return {
      state,
      increment
    }
  }
}
```
``` html
<button @click="increment">
  {{ state.count }}
</button>
```
#### `<script setup>`
using Single-File Components (SFCs), we can greatly simplify the usage with `<script setup>`:
``` js
<script setup>
import { reactive } from 'vue'

const state = reactive({ count: 0 })

function increment() {
  state.count++
}
</script>

<template>
  <button @click="increment">
    {{ state.count }}
  </button>
</template>
```
#### Deep Reactivity
In Vue, state is deeply reactive by default. This means you can expect changes to be detected even when you mutate nested objects or arrays:
``` js
import { reactive } from 'vue'

const obj = reactive({
  nested: { count: 0 },
  arr: ['foo', 'bar']
})

function mutateDeeply() {
  // these will work as expected.
  obj.nested.count++
  obj.arr.push('baz')
}
```
#### Reactive Proxy vs. Original (Composition Api)

#### Reactive Variables with `ref()`
`ref()` takes the argument and returns it wrapped within a ref object with a .value property:
``` js
import { ref } from 'vue'

const count = ref(0)

console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```
A ref containing an object value can reactively replace the entire object:
``` js
const objectRef = ref({ count: 0 })

// this works reactively
objectRef.value = { count: 1 }
```
Refs can also be passed into functions or destructured from plain objects without losing reactivity:
``` js
const obj = {
  foo: ref(1),
  bar: ref(2)
}

// the function receives a ref
// it needs to access the value via .value but it
// will retain the reactivity connection
callSomeFunction(obj.foo)

// still reactive
const { foo, bar } = obj
```
#####	Ref Unwrapping in Templates
``` js
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">
    {{ count }} <!-- no .value needed -->
  </button>
</template>
```
	
	

---
#### Reactive Proxy vs. Original (Options Api)
	https://vuejs.org/guide/essentials/reactivity-fundamentals.html#reactive-proxy-vs-original-1
	
``` js
export default {
  data() {
    return {
      someObject: {}
    }
  },
  mounted() {
    const newObject = {}
    this.someObject = newObject

    console.log(newObject === this.someObject) // false
  }
}
```
	
---
Declaring Methods
``` js
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    // methods can be called in lifecycle hooks, or other methods!
    this.increment()
  }
}
```
``` html
<button @click="increment">{{ count }}</button>
```

Deep Reactivity (Options Api)
``` js
export default {
  data() {
    return {
      obj: {
        nested: { count: 0 },
        arr: ['foo', 'bar']
      }
    }
  },
  methods: {
    mutateDeeply() {
      // these will work as expected.
      this.obj.nested.count++
      this.obj.arr.push('baz')
    }
  }
}
```

### Computed Properties
``` js
<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})
</script>

<template>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
</template>
```
Writable Computed
``` js
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
</script>
```
	
---
### Class and Style Bindings
Binding to Objects
``` js
const activeColor = ref('red')
const fontSize = ref(30)
```
``` html
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

### Conditional Rendering
``` js
  <button @click="awesome = !awesome">Toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
  
  <h1 v-show="ok">Hello!</h1>
```

### List Rendering
``` js
<li v-for="{ message } in items">
  {{ message }}
</li>

<!-- with index alias -->
<li v-for="({ message }, index) in items">
  {{ message }} {{ index }}
</li>
```

### Form input Bindings
``` js
	const checkedNames = ref([])
```
``` html
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
```
Options Api
``` js
...
  data() { return {
      newItem2: '', } </script>
<template>
  <input v-model="newItem2" type="text" placeholder="edit me" />
  {{ newItem2 }}
</template>
```

### Lifecycle Diagram
[https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram]

### Watchers
``` js
const x = ref(0)
const y = ref(0)

// single ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

// getter
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// array of multiple sources
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})
```
Option Api
``` js
  watch: {
    // whenever question changes, this function will run
    question(newQuestion, oldQuestion) {
      if (newQuestion.includes('?')) {
        this.getAnswer()
      }
    }
  },
```

### Template **Refs**, Accessing the Refs
``` html
<script setup>
import { ref, onMounted } from 'vue'

// declare a ref to hold the element reference
// the name must match template ref value
const input = ref(null)

onMounted(() => {
  input.value.focus()
})
</script>

<template>
  <input ref="input" />
</template>
```

### Components Basics
ref: https://vuejs.org/guide/essentials/component-basics.html
	
#### Using a Component
App.vue
``` js
<script setup>
import ButtonCounter from './ButtonCounter.vue'
</script>

<template>
	<h1>Here are many child components!</h1>
	<ButtonCounter />
	<ButtonCounter />
	<ButtonCounter />
</template>
```
ButtonCounter.vue
``` js
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">
    You clicked me {{ count }} times.
  </button>
</template>
```

#### Dynamic Components
App.vue
``` js
<script setup>
import Home from './Home.vue'
import Posts from './Posts.vue'
import Archive from './Archive.vue'
import { ref } from 'vue'
 
const currentTab = ref('Home')

const tabs = {
  Home,
  Posts,
  Archive
}
</script>

<template>
  <div class="demo">
    <button
       v-for="(_, tab) in tabs"
       :key="tab"
       :class="['tab-button', { active: currentTab === tab }]"
       @click="currentTab = tab"
     >
      {{ tab }}
    </button>
	  <component :is="tabs[currentTab]" class="tab"></component>
  </div>
</template>
<style> ... </stype>
```
Home.vue
``` js
<template>
  <div class="tab">
    Home component
  </div>
</template>
```
Posts.vue
``` js
<template>
  <div class="tab">
    Posts component
  </div>
</template>
```
Archive.vue
``` js
<template>
  <div class="tab">
    Archive component
  </div>
</template>
```

[:point_up: Top](#top)
	
---
## Components In Depth
### Props
Binding Multiple Properties Using an Object.

If you want to pass all the properties of an object as props, you can use v-bind without an argument (v-bind instead of :prop-name). For example, given a post object:
``` js
const post = {
  id: 1,
  title: 'My Journey with Vue'
}
```
The following template:
``` html
<BlogPost v-bind="post" />
```
Will be equivalent to:
``` html
<BlogPost :id="post.id" :title="post.title" />
```
I tested by adding `ref="title"` in <>, and `console.log(this.$refs.title)` at mounted()


### Component v-model
`v-model` can be used on a *component* to implement a two-way binding.

App.vue
``` js
<script setup>
import { ref } from 'vue'
import CustomInput from './CustomInput.vue'
  
const message = ref('hello')
</script>

<template>
  <CustomInput v-model="message" /> {{ message }}
</template>
```
CustomInput.vue
``` js
<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
```

#### `v-model` arguments
By default, `v-model` on a component uses `modelValue` as the prop and `update:modelValue` as the event. 

#### Multiple `v-model` bindings
App.vue
``` js
<script setup>
import { ref } from 'vue'
import UserName from './UserName.vue'

const first = ref('John')
const last = ref('Doe')
</script>

<template>
  <h1>{{ first }} {{ last }}</h1>
  <UserName
    v-model:first-name="first"
    v-model:last-name="last"
  />
</template>
```
Username.vue
``` js
<script setup>
defineProps({
  firstName: String,
  lastName: String
})

defineEmits(['update:firstName', 'update:lastName'])
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>
```

### Fallthrough Attributes
fallthrough attributes will be automatically added to the root element's attributes.
``` html
<!-- template of <MyButton> -->
<button>click me</button>

<!-- And a parent using this component with: -->
<MyButton class="large" />

<!-- The final rendered DOM would be: -->
<button class="large">click me</button>
```

### Slots
 to pass a template fragment to a child component, and let the child component render the fragment within its own template.

#### Fallback Content
App.vue
``` js
<script setup>
import SubmitButton from './SubmitButton.vue'
</script>

<template>
  <!-- use fallback text -->
  <SubmitButton />
  
  <!-- provide custom text -->
  <SubmitButton>Save</SubmitButton>
</template>
```
SubmitButton.vue
``` js
<template>
  <button type="submit">
	  <slot>
    	Submit <!-- fallback content -->
  	</slot>
	</button>
</template>
```

#### Named Slots​
App.vue
``` js
<script setup>
import BaseLayout from './BaseLayout.vue'
</script>

<template>
  <BaseLayout>
    <template #header>
      <h1>Here might be a page title</h1>
    </template>

    <template #default>
      <p>A paragraph for the main content.</p>
      <p>And another one.</p>
    </template>

    <template #footer>
      <p>Here's some contact info</p>
    </template>
  </BaseLayout>
</template>
```
BaseLayout.vue
``` js
<template>
  <div class="container">
    <header>
      <slot name="header"></slot>
    </header>
    <main>
      <slot></slot>
    </main>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<style>
  footer {
    border-top: 1px solid #ccc;
    color: #666;
    font-size: 0.8em;
  }
</style>
```

### Provide / Inject
#### Inject, Working with Reactivity
* To inject data provided by an ancestor component, use the inject option:
* In order to make injections reactively linked to the provider, we need to provide a computed property using the computed() function:

App.vue
``` js
<script setup>
import { ref, provide } from 'vue'
import Child from './Child.vue'

// by providing a ref, the GrandChild
// can react to changes happening here.
const message = ref('hello')
provide('message', message)
</script>

<template>
  <input v-model="message">
  <Child />
</template>
```
Child.vue
``` js
<script setup>
import GrandChild from './GrandChild.vue'
</script>

<template>
  <GrandChild />
</template>
```
GrandChild.vue
``` js
<script setup>
import { inject } from 'vue'

const message = inject('message')
</script>

<template>
  <p>
    Message to grand child: {{ message }}
  </p>
</template>
```

### Async Components

### KeepAlive
App.vue
``` js
<script setup>
import { shallowRef } from 'vue'
import CompA from './CompA.vue'
import CompB from './CompB.vue'

const current = shallowRef(CompA)
</script>

<template>
  <div class="demo">
    <label><input type="radio" v-model="current" :value="CompA" /> A</label>
    <label><input type="radio" v-model="current" :value="CompB" /> B</label>
    <KeepAlive>
      <component :is="current"></component>
    </KeepAlive>
  </div>
</template>
```
CompA.vue
``` js
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <p>Current component: A</p>
  <span>count: {{ count }}</span>
  <button @click="count++">+</button>
</template>
```
CompB.vue
``` js
<script setup>
import { ref } from 'vue'
const msg = ref('')
</script>

<template>
  <p>Current component: B</p>
  <span>Message is: {{ msg }}</span>
  <input v-model="msg">
</template>
```

### Tooling > Try It Online

#### Try It Online
* Vue SFC Playground > https://sfc.vuejs.org/

#### IDE Support
* Visual Studio Code (VSCode) 
	* Volar is the official VSCode extension

#### Browser Devtools
* Added Vue.js devtools extension to Chrome 
	- manage extension 
	- allow access to file URLs 
	- can inspect the project page > Vue tab
	- can use the console to update `$vm0.data.firstName = "Hello"`

### Routing
App.vue
``` js
<script setup>
import { ref, computed } from 'vue'
import Home from './Home.vue'
import About from './About.vue'
import NotFound from './NotFound.vue'

const routes = {
  '/': Home,
  '/about': About
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
})
</script>

<template>
  <a href="#/">Home</a> |
  <a href="#/about">About</a> |
  <a href="#/non-existent-path">Broken Link</a>
  <component :is="currentView" />
</template>
```
Home.vue
``` js
<template>
  <h1>Home</h1>
</template>
```
About.vue
``` js
<template>
  <h1>About</h1>
</template>
```
NotFound.vue
``` js
<template>
  <h1>404</h1>
</template>
```

### State Management
#### Simple State Management with Reactivity API
App.vue
``` js
<script setup>
import ComponentA from './ComponentA.vue'
import ComponentB from './ComponentB.vue'
</script>

<template>
  <ComponentA />
  <ComponentB />
</template>
```
ComponentA.vue
``` js
<script setup>
import { store } from './store.js'
</script>

<template>
  <div>
    <button @click="store.increment()">
      From A: {{ store.count }}
    </button>
  </div>
</template>
```
store.js
``` js
import { reactive } from 'vue'

export const store = reactive({
  count: 0,
  increment() {
    this.count++
  }
})
```

### Render Functions & JSX
ref: https://vuejs.org/guide/extras/render-function.html
* `v-if`
* `v-for`
* `v-on`
* `v-model`

### Vue and Web Components


[:point_up: Top](#top)


---	  
## from Tutorial
The above example demonstrates the two core features of Vue:

- **Declarative Rendering**: Vue extends standard HTML with a template syntax that allows us to declaratively describe HTML output based on JavaScript state.

- **Reactivity**: Vue automatically tracks JavaScript state changes and efficiently updates the DOM when changes happen.

- https://vuejs.org/tutorial

Tutorial 2, Declarative Rendering
#### Options, SFC
App.vue
``` vue
<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 0
      }
    }
  }
}
</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</template>
```
#### Composition, SFC
App.vue
``` vue
<script setup>
import { reactive, ref } from 'vue'

const counter = reactive({ count: 0 })
const message = ref('Hello World!')
</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</template>
```
#### Composition, HTML
index.html
``` vue
<script type="module">
import { createApp, reactive, ref } from 'vue'

createApp({
  setup() {
    const counter = reactive({ count: 0 })
    const message = ref('Hello World!')

    return {
      counter,
      message
    }
  }
}).mount('#app')
</script>

<div id="app">
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</div>
```
#### Options, HTML
index.html
``` vue
<script type="module">
import { createApp } from 'vue'

createApp({
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 0
      }
    }
  }
}).mount('#app')
</script>

<div id="app">
  <h1>{{ message }}</h1>
  <p>Count is: {{ counter.count }}</p>
</div>
```

Tutorial 3, Attribute Bindings
``` vue
<script setup>
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <h1 :class="titleClass">Make me red</h1>
</template>

<style>
.title {
  color: red;
}
</style>
```
Tutotial 4, Event Listeners
``` vue
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">count is: {{ count }}</button>
</template>
```
Tutotial 5, Form Binding
``` vue
<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <input v-model="text" placeholder="Type here">
  <p>{{ text }}</p>
</template>
```
Tutorial 6, Conditional Rendering
``` vue
<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>
```
Tutorial 7, List Rendering
``` vue
<script setup>
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```
Tutorial 8, Computed Property
``` vue
<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```
Tutorial 9, Lifecycle and Template Refs
``` vue
<script setup>
import { ref, onMounted } from 'vue'

const p = ref(null)

onMounted(() => {
  p.value.textContent = 'mounted!'
})
</script>

<template>
  <p ref="p">hello</p>
</template>
```

Tutorial 10, Watchers
``` js
import { ref, watch } from 'vue'

const count = ref(0)

watch(count, (newCount) => {
  // yes, console.log() is a side effect
  console.log(`new count is: ${newCount}`)
})
```
Tutorial 11, Components
``` vue
<script setup>
import ChildComp from './ChildComp.vue'
</script>

<template>
  <ChildComp />
</template>
```
Tutorial 12, Props
``` vue
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const greeting = ref('Hello from parent')
</script>

<template>
  <ChildComp :msg="greeting" />
</template>
```
ChildComp.vue
``` vue
<script setup>
const props = defineProps({
  msg: String
})
</script>

<template>
  <h2>{{ msg || 'No props passed yet' }}</h2>
</template>
```
Tutorial 13, Emits
``` html
...
<template>
  <ChildComp @response="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>
</template>
```
ChildComp.vue
``` vue
<script setup>
const emit = defineEmits(['response'])

emit('response', 'hello from child')
</script>
...
```
Turorial 14, Slots
``` js
const msg = ref('from parent')
...
<template>
  <ChildComp>Message: {{ msg }}</ChildComp>
</template>
```
ChildComp.vue
``` vue
<template>
  <slot>Fallback content</slot>
</template>
```
Tutorial 15, You Did it!
``` vue
<script setup>
import JSConfetti from 'js-confetti'

const confetti = new JSConfetti()

function showConfetti() {
  confetti.addConfetti()
}

showConfetti()
</script>

<template>
  <h1 @click="showConfetti">🎉 Congratulations!</h1>
</template>

<style>
h1 {
  text-align: center;
  cursor: pointer;
  margin-top: 3em;
}
</style>
```

---
[:point_up: Top](#top)
[:top: Top](#top)
---
