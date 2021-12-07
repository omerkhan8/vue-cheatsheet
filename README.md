# Vue JS CheatSheet

## To Create an app:

    const vm = Vue.createApp({
		data(){
			return {
				firstName:"Omer",
				lastName: "Khan"
			}
		},
		methods: {
			fullName(){
				return `${omer} ${khan}`
			}
		}
	}).mount('#app')
data will go in data function's return method and methods will go in methods object you can then use them in your templete.

    <div id="app">
	    {{ firstName }}
	    {{ fullName() }}
    </div>
## Directives:
Uses to change the behaviour of an element.

 - **v-cloak**
		 - *dom will consider it as an attribute and vue will remove it from the element as soon as vue mounts, so we can use it to hide the elements from dom until vue initializes and can understand the templates.*
 - **v-model**
		- *used to two way data binding for your inputs with some data*
 - **v-bind:attribute**
		-  *uses to bind the attributes with data to make them dynamic can also use shorthand property with just :*
		 `eg: <a v-bind:href="url">Some link</a>`
		 or
		 `<a :href="url">Some link</a>`
 - **v-html**
		- *to output raw html in templates. equivalent to `innherHtml` dom api.*
 - **v-on:eventName**
		-	*to bind events to elements, also supports shorthand property @*
		`<button v-on:click="yourFn($event)">Click me</button>`
		or
		`<button @click="yourFn()">Click me</button>`
		for change events on input we use `@input`  event.
	
## Event Modifiers 
 -  `stop`
-   `.prevent`
-   `.capture`
-   `.self`
-   `.once`
-   `.passive`
-
shorthand way to call event modifiers like `preventDefault` , `stopPropogation` etc

``eg <input :value="lastName" @input.prevent="updateLastName()" />``

