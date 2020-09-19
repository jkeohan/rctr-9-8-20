

Title: Components And JSX<br>
Duration: 45min+ <br>
Creator:  Joe Keohan<br>

---

# Components and JSX

## Learning Objectives

*   Identify and define React components
*   Describe why we use components in React
*   Build a React component
*   Describe what JSX is transpiled into

## Components

The basic unit you'll be working with in React is a **Component**.  Components are pieces of our application that we define once and can reuse throughout.  They also can be extended to include additional functionality, including the following:

- all or part of the applications state (data)
- accept data from a parent component as props
- perform some action on initial render and subsequent re-renders

#### Components Are Used Every

If you are familiar with Bootstrap then you already understand the concept of a `Component`.  Bootstrap even has a section in their documentation dedicated to just components.  

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at [Bootstraps section on Components](https://getbootstrap.com/docs/4.5/getting-started/introduction/). 

On the left hand side you will see a link to `Components` and clicking on that will open the door to over 2 dozen Components. 

<img src="https://i.imgur.com/ORHHHpi.png" width=200/>

<hr>



Let's take this Bootstrap Card component for instance.  It's a common design that we have all seen on the web and perhaps have even used yourself in previous projects. 

<img src="https://i.imgur.com/oKyuaBn.png" width=200/>

It's essentially comprised of the following html.  All you would need to do is copy/paste the html and update the relevant content placeholders.  

It's essentially a grouping of elements that, as a Component, is reusable. 

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

Bootstrap essentially allows us to pick and choose from this reusable pool of Components and to implement any web page layout/design. 

<img src="https://i.imgur.com/CEDY0l6.png" width=800/>

<br>
<br>

### React Components

Although Boostrap comes with predefined Components out of the box, React does no such thing.  

React allows you to decide what constitues a Component and then provides the framework for you to add the required HTML and JS to create them. 

So instead of creating a few large files, you will organize your web app into small, reusable Components that encompass their own content, presentation, and business logic.

#### Train Station Schedule Example
Take for instance an example of a train station schedule. There are elements that repeat themselves in the html structure that essentially perform the same function. 

<img src="https://i.imgur.com/D6HngOk.png" />

These Components, much like the HTML used to render them, will be structured into various nested Components.
	
```
- TubeTracker
  - Network
      - Line
  - Predictions
      - DepartureBoard
          - Trains
```

- `TubeTracker` contains the application and will render 2 main elements: `Network` and `Predictions`
- `Network` displays each line on the network and renders a `Line` for each line that it contained in it's dataset
- `Line` displays a single station on a line
- `Predictions` controls the state of the departure board and renders `DepartureBoard`
- `DepartureBoard` displays the current station and platforms and renders a `Train` for each one in its dataset
- `Trains` displays the trains due to arrive at a platform

When using React, building Components will be a thing you will do quite often.


### Rules To Follow

From this point on we will be creating Components, more  than you ever imagined, so before we begin let's take a moment to discuss the `requirements` and `best practices` for creating Components.  

Some of the requirements are specific to `JSX`, short for `JavaScript And XML`, and will be reviewed again in a later section. 

:oncoming_police_car: - Rules
- They must import `React`
- They must be called within the JSX using an uppercase first letter
- They must return some form of UI (user interface) 
- They can return only one top level element but that element can contain numerous children. 
- They must be exported from the file to be imported into another Component 

:star: Best Practices
- Each Component should be in it's own file
- Each Component file should be in a separate folder 
- Each Component should reference it's own CSS

### Class vs Hook Components

As of `React 16.8` Components now come in 3 forms, all of which follow the same requirements and best practices. 

- Class Based (with or without state)
- Functional Using Hooks - leverages one or more `Hooks` and/or includes `state`
- Presentational - Renders UI only and is `stateless`

#### Class Based Components

We will introduce `Class Based` Components so that you have some grounding as to what they are, but the remainder of this class and all future lectures will be taught as `Functional Components` 

Let's continue working on the previous [CodeSandbox Starter code](https://codesandbox.io/s/rctrr-9-8-20-getting-started-yryf6). 

In `src` create a new file called `App.js`. 

<img src="https://i.imgur.com/RArVqwo.png" width=200/>

<br>
<br>

Inside `App.js` let's do the following:

 - import `React`
 - create the `Class Component` 
 - export the `Component`

```js
// IMPORT REACT
import React from 'react'
// CREATE THE CLASS BASED COMPOENT
class App extends React.Component {
  render(){
    return (
      <div>Class Based Component</div>
    )
  }
}
// EXPORT THE COMPONENT
export default App
```


Let's break down the things we see here:

:oncoming_police_car: `import React from 'react'`

This imports React methods from the React library.

:oncoming_police_car: `class App extends React.Component`

Since we are creating a `Class Component` we must include the keyword `class`, as well as `extend` which is used to inherit al the functionality provided via the default `React.Component`.  


ES6 classes and class inheritance are a much more extensive topic and something we will not cover in this class but expect to encounter them anytime you research how to do something in React. 

```js
render(){
  return (
    <div>Class Based Component</div>
  )
}
```

All Class Components must use the `render(){}` method to `return()` the UI.  The `render()` method is something that was inherited by extending the React.Component.

`export default App`

This allows other files to import the `App` Component. In our case, we'll be importing it into `index.js` using `import` keyword. 

##### Importing The Component Into index.js

In `index.js` let's import the `App` Component and render it.

```js
// IMPORT THE APP COMPONENT
import App from './App'
```

And now let's render it.  For this we are going to replace the existing code we copied earlier with the `<App />` Component.

```js
ReactDOM.render(
  <App />, 
document.getElementById("root"));
```

Once the page refreshes you should see the output.

**Final Note On Class Components**

There is much more to `Class Components` then was touched on here.  This was only meant to show the most minimum instantiation of a Class Component.  

Just keep in mind that the additional structure for defining state, handling props, calling lifecycle methods is much different than their `Hook` based counterparts. 

#### Functional Components

Being that you are familiar with JS functions writing a Functional Component is much easier to understand. 

For now let's just comment out the Class Component and write a new `Presentational Functional` Component.


```js
const App = () => (
    <div>Functional Component</div>
)
```

As we can see a `Functional` Component is more streamlined and concise. It's written using the `fat-arrow` syntax which allows it to take advantage of the `implicit` return.  

If we only need to return `JSX` then this way of writing the Component will suffice.  However if we needed to include additional functionality then we would need to write the Component as follows:

```js
const App = () => {
  return (
    <div>Functional Component</div>
  )
}
```

As we can see this requires curly braces `{}` and an `explicit` return statement. 


## JSX

One thing to note about Bootstrap is that there is a distinct separation between HTML, CSS and JS.  It takes the `separation of concerns` modality and requires the import of a separate css and js file.  So in order to fully work with Bootstrap not only do you need to include the Bootstrap specific HTML but also import the following files:
```html
<!-- BOOTSTRAP CSS -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
<!-- BOOTSTRAP JS AND REQUIRED DEPENDENCIES-->
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
```

React however brings the HTML and JS together into one file using `JSX`.  It can also include the CSS to make the Component self containing. 

JSX is [a language that compiles to Javascipt](http://blog.yld.io/2015/06/10/getting-started-with-react-and-node-js/#.V8eDk5MrJPN) and allows us to write code that strongly resembles HTML. It is eventually compiled to lightweight JavaScript objects. 

JSX is not not limited to `React` and can be implemented in other frameworks. 

#### Rules For Writing JSX

Much like writing Components there are some rules we must adhere to when using JSX. 

- They can render only one top level element but that element can contain numerous children. 
- As per CSS, the word `class` is replaced with `className`
- Any JavaScript code must be surrounding in opening/closing curly braces
- Any Component created via a loop must include a `key` prop


Keeping all these rules in mind let's see what happens if you try to render two top level elements.  

##### Single Top Level Parent
Let's add another `div`

```js
const App = () => {
  return (
    <div>Top</div>
    <div>Functional Component</div>
  )
}
```

We should get the following error regarding `Adjacent JSX elements...`

<img src="https://i.imgur.com/hheNsc3.png" width=400/>

<br>

We can fix that by wrapping all the HTML in a top level element, such as another `div` or by using a `React` fragment.

```js
const App = () => {
  return (
    <React.Fragment>
      <div>Top</div>
      <div>Functional Component</div>
    </React.Fragment>
  )
}
```

Which can also be writen as:

```js
const App = () => {
  return (
    <>
      <div>Top</div>
      <div>Functional Component</div>
    </>
  )
}
```

#### Replacing `class` with `className`

Although this won't cause the same fatal error as with trying to define two top level parents, it will produce a warning. 

Let's see that that warning in action by adding a `class`.

```js
const App = () => (
  <>
    <div class='top'>Top</div>
    <div>Functional Component</div>
  </>
)
```

In Chrome DevTools we should see the following warning in the `Console`

<img src="https://i.imgur.com/f28eP84.png" width=500/>

### Bonus - Modern Web Components

Components, React or otherwise,  are now becoming the standard for sharing small pieces of functionality.  

Let's take a look at [https://bit.dev/](https://bit.dev/) which is an environment developers can share their own custom Components or use those created by other devs. 

There are even hundreds of [React Components](https://bit.dev/components?q=react) being shared on the site as well. 

Much like the Train Station design we looked at earlier, Components are used organized to implement a design and can be built using several of the shared Components on bit.dev.

<img src="https://i.imgur.com/CnpxIFM.jpg" width=500/>


### Resource
- [Modern Web Components](https://bit.dev/)
- Watch: [Intro To Components](https://generalassembly.wistia.com/medias/h64z7lp1ir)  - official GA content