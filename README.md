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
there are also some keyboard modifiers for listening to keystrokes like `@keyup.enter` will listen to enter key press.

## Computed Properties
much like `useMemo` in react if computed value needs to be rendered in UI add that function in `computed` object and it will only called whenever references used inside that function will be changed otherwise an cached value will be returned.

    const vm = Vue.createApp({
     data(){
      return {
       firstName:"Omer",
       lastName: "Khan"
      }
     },
     methods: {},
     computed:{
		 fullName(){
	       return `${omer} ${khan}` 
	     }
	 }
    }).mount('#app')
   
   ## Watchers
   used to watch some data property or computed property whenever that property will change it will run with new and old value.
   

    watch:{
		age(newVal,oldVal){
		// runs whenever age property's value changes.
		}
	}

## Binding Classes
same like `ngClass` in angular or `classnames` library in react. will take object as value whos key will be class and value will be boolean condition
eg: `<div :class="{red:true}"></div>`

## Binding Styles
same like `ngStyle` in angular
eg: `<div :style={width: size + 'px'}></div>`

## Conditional Rendering
we use `v-if` directive for conditionally rendering items.
`v-else-if`
and 
`v-else`
`v-show` *there is another directive but it will not remove the element from html will just add display hidden property to the component.*

## Rendering Template
the alternate to `Fragment` in react and `ng-container` in angular is 
`<template></template>` in vue.

## List Rendering
`v-for` directive will be used for this
eg: 

    <ul>
	    <li v-for="let bird in birds">
		    {{ bird.name }}
	    </li>
    </ul>
  to get the index from loop 
  `<li v-for="let (bird, index) in birds"></li>`
  in Vue you can also loop through objects
  

    <li v-for="let (value, key, index) in person">
    </li>
   **adding key for performance improvement**
	   `<li v-for="let bird in birds" :key="bird.id">`
	   
## LifeCycle Methods
- `beforeCreate`
- `created`
- `beforeMount`
- `mounted`
- `beforeUpdate`
- `updated`
- `beforeDestroy`
- `destroyed`
- `activated`
- `deactivated`

## Child Components
To use a component we need to register it inside components property. then we can use it inside our template

    <template>
	    <profile></profile>
    </template>

	<script>
    export default{
	    name: "App"
	    components: {
			Profile
		}
    }
    </script>
## Styles Encapsulation:
while adding styles you can pass `scoped` attribute then it will only adds styles to that particular component and other components having same css classes won't be effected
`<style scoped></style>`

## Props
to pass down data as props from parent component simply send properties like attribute bindings: `<div :age="age"> </div>`
and in child component defined that in props object.

    props:["age"]
  or
  

    props:{
		age: Number
	}
or

    props:{
		age:{
			type: Number,
			required: boolean,
			default: any, /* will have to be a function 
							returning value incase of Array or 
							Object as type */
			validator(value:any):boolean
		}
	}

   

## Emitting Events
to send functions to child components, define the function name in child component in `emits:['someFn']` property then call it by using `this.$emit('someFn',arguments)`
and send the function from parent component same way `@someFn="handleFn"`
***this can be also achieved by passing functions as props to child component and calling them with data just like react.*** 

## Slots
slots are like `props.children` in react or `ng-content` in angular whatever passed between opening / closing tags of component from parents can be used as 
`<slot></slot>`

**Named Slot**
if you want to add multiple parts you use named slots
`<slot name="header"></slot`
and in parent component

    <template v-slot:header> // should be always used with templates.
	    // your content
	</template>
	
## Dynamic Components
Dynamic components can be rendered by writing
 `<component :is="componentName"></component>` tag and `is` attribute should be named as name of component you want to render..
 also on changing the name of `is` the old components will be destroyed and unmounts if you want it to be mounted you can use wrap it with `<keep-alive></keep-alive>`

