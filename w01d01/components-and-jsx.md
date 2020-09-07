# Components and JSX

## Learning Objectives

*   Identify and define React components
*   Describe why we use components in React
*   Build a React component
*   Describe what JSX is transpiled into

## Components

The basic unit you'll be working with in React is a **Component**. 

Components are pieces of our application that we can define once and reuse throughout.

If you are familiar with Bootstrap then you already understand the concept of a Component.  Bootsrap even has a section in their documentation dedicated to just components.  

Take for instance this Bootstrap Card component.  It's a common design that we have all seen on the web. 

<img src="https://i.imgur.com/oKyuaBn.png" width=300/>

It's essentially comprised of the following html.  All you would need to do is copy/paste the html and update the content.  It's essentially a grouping of elements that is reusable. 

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

If you're used to writing out all of a page's view in a single HTML file, using components is a very different way of approaching web development.

Essentially you can pick and choose from this reuable pool of components that can be used to build any web page layout/design. 

<img src="https://i.imgur.com/CEDY0l6.png" width=800/>

<br>
<br>

### React Components

Although Boostrap comes with predefined Components out of the box, React does no such thing.  

React allows you to decide what constitues a Component and then provides the framework for you to add the required HTML and JS to create them. So instead of creating a few large files, you will organize your web app into small, reusable components that encompass their own content, presentation, and behavior.


Take for instance an example of a train stationn schedule. There are elements that repeat themselves in both html structure as well as functioanlity. 

<img src="https://i.imgur.com/HYp5VI2.png" />

These Components, much like the HTML used to render them, will be structured into various nested Components
	
```
- TubeTracker
    - Network
        - Line
    - Predictions
        - DepartureBoard
            - Trains
```

- `TubeTracker` contains the application
- `Network` displays each line on the network
- `Line` displays the stations on a line
- `Predictions` controls the state of the departure board
- `DepartureBoard` displays the current station and platforms
- `Trains` displays the trains due to arrive at a platform

When using React, building components will be your main front-end task.


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

**Indentify Components**

* The instructor will create breakout rooms of 3 or 4 students
* Each group will look at one of the following websites: `AirBnB, BBC, Bleacher Report, Flipboard, Imgur, Instagram, Khan Academy, Netflix, Postmates, and Reddit`
* Identify the visual "components" the website is comprised of. 
- Take a snapshot of the site and use Google Draw to add colored boxes around the Components

As you're drawing this out, think about the following questions:

* Where do you see `nested components`? Where do you not?
* Are there any components that share the same structure?
* Of these similar components, what is different about them?

<hr>

### Rules To Follow

From this point on we will be creating more and more Components that you ever imagined but before we begin let's discuss the requirments and best practices for creating Components.  Some of the requirements are specific to `JSX` and will be reviewed again in a later section. 

#### Requirements
- They must import `React`
- They must begin with an uppercase letter
- They must render some UI (user interface) as `JSX` (more on JSX later)
- They can render only one top level element but that element can contain numerous children. 
- As per CSS, the word `class` is replaced with `className`
- The Component must be exported from the file

#### Best Practices
- Each Component should be in it's own file
- Each Component file should be in a separate folder 
- Each Component should reference it's own CSS

### Class vs Hook Components

As of `React 16.8` Components now come in 3 forms, both of which follow the same requirements and best practices. 

- Class Based (with or without state)
- Functional Using Hooks - leverages one or more `Hooks`
- Presentational - Renders UI only and contains no state

#### Class Based Components

We will introduce `Class Based` Components so that you have some grounding as to what they are but for all future lectures will be taught using `Functional Components using Hooks` 

Let's continue working on the previous CodeSandbox. In `src` create a new file called `App.js`. 

<img src="https://i.imgur.com/RArVqwo.png" width=200/>

<br>
<br>
Inside `App.js` let's import `React`, create our `Class Component` and then export it.

```js
import React from 'react'

class App extends React.Component {
  render(){
    return (
      <div>Class Based Component</div>
    )
  }
}

export default App
```


Let's break down the things we see here:

`import React from 'react'`

This imports React methods from the React library.

`class App extends React.Component`

This is the Class Component we're creating which requires the keyword `class` and also must `extend` the default `React.Component`.  Essentially it is inheriting all the underlying functionality from the base React Component. 

```
 render(){
    return (
      <div>Class Based Component</div>
    )
  }
```

All Class Components must use the `render(){}` to `return()` the UI.  

`export default App`

This exposes the `App` component to other files. This means that other files can `import` from the `App.js` file in order to use the `App` component. In our case, we'll be importing it into `index.js` by calling an `import` to `App.js`.

When we try to import something from `App.js`, JavaScript will attempt to match a named export.

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

There is much more to `Class Componenents` then was demo'd.  This was only meant to show the most minimum and basic Class Compontent.  The structure for defining state, handling props, calling lifecycle methods is different than their `Hook` based counterparts. 

#### Functional Components

Functional Components are much easier to write. For now let's just comment out the Class Component and rewrite it as a `Functional` Component.


```js
const App = () => (
    <div>Functioanal Component</div>
)
```

As we can see a `Functional` Component is more in line with `Functional Programming`


## JSX

One thing to note about Bootstrap Components is that there is a distinct separation between HTML, CSS and JS.  It actually requires that you import the following links in order to get the full functionality that Bootstrap provides:

```html
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
```

React however brings the HTML and JS together into one file using `JSX`.  

JSX is [a language that compiles to Javascipt](http://blog.yld.io/2015/06/10/getting-started-with-react-and-node-js/#.V8eDk5MrJPN) and allows us to write code that strongly resembles HTML. It is eventually compiled to lightweight JavaScript objects. 

JSX is not not limited to `React` and can be implemented in other frameworks. 

#### Rules For Writing JSX

Much like writing Components there are some rules we must adhere to when using JSX. 

- They can render only one top level element but that element can contain numerous children. 
- As per CSS, the word `class` is replaced with `className`

Keeping that in mind let's see what happens if you try to render two top level elements.  


##### Single Top Level Parent
Let's add another `div`

```js
const App = () => (
  <div>Top</div>
  <div>Functional Component</div>
)
```

We should get the following error regarding `Adjacent JSX elements...`

<img src="https://i.imgur.com/hheNsc3.png" width=400/>

We can fix that by wrapping all the HTML in a top level element, such as another `div` or by using a `React` fragment which can be written in 2 ways:

```js
const App = () => (
  <React.Fragment>
    <div>Top</div>
    <div>Functional Component</div>
  </React.Fragment>
)
```

Or the shorthand:

```js
const App = () => (
  <>
    <div>Top</div>
    <div>Functional Component</div>
  </>
)
```

##### Using `className` instead of `class`

Although this won't cause the same fatal error as with trying to define two top level parents, it will produce a error. Let's see that that error in action by adding a `class`.

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

### Resource
- For an intro to components, watch [this video](https://generalassembly.wistia.com/medias/h64z7lp1ir) (Note: right click to open in a new tab).
