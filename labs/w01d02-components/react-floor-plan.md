# Assignment: React Floorplan

## Learning Goals

So far, you've seen the following React basics:

* How to defining components as functions
* How to return a function component's UI defined using JSX
* How to pass props to components
* How to access the properties on props within a component

And that's what we'll practice in this assignment!

---

# React Floor Plan

## Minimum Requirements

1. Use `CodeSandbox` to generate a new React app, titled `react-floorplan` or something similar. 

1. Define the following components and code them such that they fulfill their responsibilities:

	| Component | Responsibilities |
	|---|---|
	| `<FloorPlan>` | Rendered by `<App>`<br>Renders the following components:<br>- A `<Kitchen>` component<br>- A `<LivingRoom>` component<br>- Three `<Bedroom>` components<br>- Two `<Bath>` components<br>**Render the components in any order you wish to make the floor plan more interesting** |
	| `<Kitchen>` | Renders the text "Kitchen" and the following components:<br>- A `<Oven>` component<br>- A `<Sink>` component |
	| `<LivingRoom>` | Renders the text "Living Room" |
	| `<Bedroom>` | Accepts a `bedNum` prop and renders the text "Bedroom [bedNum]" (substituting the value of the `bedNum` prop) |
	| `<Bath>` | Accepts a `size` prop and renders the text "[size] Bath", i.e., "Half Bath", "Full Bath" |
	| `<Oven>` | Renders the text "Oven" |
	| `<Sink>` | Renders the text "Sink" |

1. Define each component in its own file. The naming convention to use for a component's file is UpperCamelCase, for example, a `<SomeComponent>` component's file would be named `SomeComponent.js`

1. Export each component from its module. For example:

	```js
	import React from 'react';
	
	function SomeComponent(props) {
	  return (
	    <div>
	      <h1>SomeComponent</h1>
	    </div>
	  );
	}
	
	export default SomeComponent;
	```

1. Add the following CSS inside of **index.css** to style each component's wrapping `<div>` to make it easier to visualize the components:

```css
div {
  border: 1px solid grey;
  margin: 5px;
  padding: 5px;
}
```

With the minimum requirements complete, the output should resemble:

<img src="https://i.imgur.com/g0T8RNK.png">

### Hints

* If a component accepts a prop, that prop must be passed to it by the component that renders it, in other words, parent components pass props to their children components.

## Bonus

Style the components to make the output look like a floor plan:

<img src="https://i.imgur.com/NhRcNrk.png">

### Hints

* Use `className` and/or `id` on React Elements (`<div>`, `<p>`, `<span>`, etc.) to apply CSS styling using CSS rules in the **index.css** module.
* Styling the `<FloorPlan>` component as a CSS Grid is a great way to layout its children (grid items).
* Use props being passed in to generate a unique `id` on an element that can be used to target that element for custom styling. For example:

   ```js
   <div className='bedroom' id={`bed-${props.bedNum}`}>
   ```
   Would result in this `<Bedroom>` having a wrapping `<div>` like:

   ```js
   <div class="bedroom" id="bed-2">
   ```
   if it was rendered as:

   ```js
   <Bedroom bedNum={2} />
   ```

---

# Yay! All done!

