# Notes from the Vue complete course

## The Basics of Vue

1. [Creating a Vue app](#creating-a-vue-app)
2. [Event Handling](#event-handling)
3. [Data Binding](#data-binding)
4. [Computed Properties](#computed-properties)
5. [Watchers](#watchers)
6. [Shortcuts](#shortcuts)

### Creating a Vue app

```javascript
const app = Vue.createApp({
    data() {
      return {};
    },
    watch: {

    },
    computed: {

    },
    methods: {

    }
});

app.mount('#assignment');
```

### Event Handling

### Data Binding

In this example, we want to add a reset button that will reset the contents of the textbox. Rather than using JavaScript to access the textbox directly, we use data binding to bind the textbox to a property and then let the button also access the same property to reset it.

Use the v-bind property to have the textbox value filled from the name property.
```javascript
<input type="text" v-bind:value="name" v-on:input="setName($event, 'Schwarzmüller')">
```

Bind the button to a new resetInput method
```javascript
<button v-on:click="resetInput">Reset Input</button>
```

Add the new method in the app.js file. This method will reset the same property that is now bound to the textbox (it is also bound to the paragraph so that will reset as well)
```javascript
resetInput() {
    this.name = '';
}
```

The textbox shows a very common pattern where you are binding a property to an input AND setting the property on input. All of this can be replaced with a shorter form:
```javascript
v-model="name"
```
This is called Two-way binding. We are listening for the event AND writing the value back to the element. Thus, these two elements shown below do the exact same thing.
```javascript
<input type="text" v-bind:value="name" v-on:input="setName($event)">
<input type="text" v-model="name">
```

### Computed Properties

Next we look at using a method in the paragraph to format the content rather than using binding. 
```javascript
outputFullName() {
    if (this.name === '') {
    return '';
    }
    return this.name + ' ' + 'Schaefer';
},
```

This pattern creates an inefficiency because Vue must execute this method whenever anything on the message changes. Rather than using methods, computed properties know the dependencies and will only execute when those dependencies change.

Computer properties add a new section to the Vue app. They are methods but they should be named like properties. When called they are called WITHOUT (), they are used like variables.
```javascript
computed: {
    fullname() {
        if (this.name === '') {
            return '';
        }
            return this.name + ' ' + 'Schaefer';
    }   
},
```

### Watchers

This is a function that executes when a dependency changes. Very similar to computed properties. Watcher methods are connected to a property name by being named the same. 

This is also a new section
```javascript
data() {
    return {
      counter: 0,
      name: '',
      fullname: ''
    };
  },
  watch: {
    name(value) {
      this.fullname = value + ' ' + 'Schaefer';
    }
  },
```

The difference between watchers and computed properties is that watchers are bound to a single field whereas a computed field can work with more complex situations. Watchers are best used when you are validating or enforcing threshholds. Like having a maximum on the counter field.

### Shortcuts

v-on: can be replaced with @
v-bind: can be replaced with just the :

### Dynamic Styling

This is an approach that uses in-line styles

```html
<section id="styling">
  <div 
    class="demo"
    :style="{borderColor: boxASelected ? 'red' : '#ccc'}"
    @click="boxSelected('A')"></div>
  <div class="demo" @click="boxSelected('B')"></div>
  <div class="demo" @click="boxSelected('C')"></div>
</section>
```

A better approach is to use a css class dynamically

```css
.active {
  border-color: red;
  background-color: salmon;
}
```

Note in this code that the :style has been removed and now :class in its place

```html
<div 
  :class="boxASelected ? 'demo active' : 'demo'"
  @click="boxSelected('A')">
</div>
```
Vue supports a shorthand for css styles
```html
<div
  class="demo"
  :class="{active: boxASelected}"
  @click="boxSelected('A')">
</div>
```