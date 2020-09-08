# Intro to React.js



<img src="https://i.imgur.com/yt8BVNj.png" width=500/>

## Learning Objectives

* Explain what a frontend framework is and why they can be helpful in writing more complex applications.
* Explain what React.js is and where it fits in our applications' stack.
* Explain the component model of web development.
* Create and render React components in the browser.

## Framing

### The Birth of the Frontend Frameworks

As the world of web development and software engineering grows in complexity so does the need to introduce new tools that facilitate development and increase the efficiency and performance our our codebase. 

I'm sure everyone here has heard of jQuery, which was first introduced in 2006. It filled a gap for front end developers for some time, and still does but it's considered just a ibrary and falls short of carrying the label of `framework`.

Some of the front end frameworks you might of heard and even worked with are:

| Framework | Year Introduced |
| :---: | :---: | 
| Angular | 2009 |
| Backbonne | 2010|
| Ember | 2011 |



<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

- Think about what a front end framekwork is and answer the following questions:
  - How it's different than a JavaScript library like jQuery, Lodash, Underscore or Ramda? 
  - Why would we opt to use it?
- Write our your answer in a slack thread to yourself
- When asked slack your answer in the thread created by the instructor

<hr>

### Front End Frameworks

A framework is a library that provides generic functionality and structure that serves as foundation to build and deploy applications.  The following are just a few of the front end frameworks mentioned in [https://2019.stateofjs.com](https://2019.stateofjs.com/front-end-frameworks/)

- React
- Vue
- Angular
- Ember



Frameworks can help standardize code, give you additional functionality and performance, and can help get your code off the ground faster.  

There is a lot of debate over whether frontend frameworks count as frameworks at all -- some people say that they are just libraries and should be referred to as such.

### Sites Built On React

First, let's think about where you might see a React.js app. Here are two of the most popular web sites built in React and that should give some 

*   Facebook - They actually built React! It needed web pages that could change quickly based on a user's interaction. 
*   Instagram - It's public feed and internal system are entirely built on React.


As you can imagine they are not the only popular sites built in React.  


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at this article  [32 Web Sites Built In React](https://medium.com/@coderacademy/32-sites-built-with-reactjs-172e3a4bed81)

- Look over the sites and determine which ones you might use on a daily or weekly basis
- When asked slack your answer in the thread created by the instructor

<hr>

### What Is React.js


React is a JavaScript framework used to craft modern day UI and views for the front-end in web applications.

> **Selling Point:** By modeling small compatible components that focus on just rendering a view, we can move business logic out of the DOM, and therefore improve our app's performance, maintainability, modularity and readability.

React is "agnostic" to other tools in your front end. This means that React can 
co-exist with other Javascript frameworks, letting the other frameworks handle 
the models and controllers while having React handle the views.

### The History of React

The first thing most people hear about React is "Facebook uses it".  As mentioned before Facebook actually created React to meet the demands of the most popular social media platform of it's day. 

*   First used by Facebook in 2011.
*   Adopted by Instagram in 2012.
*   Made open source in May 2013.
*   Not long after React was embraced by the dev community. 

React was born out of Facebook's frustration with the traditional MVC model and:

  * how re-rendering something meant re-rendering **everything** (or just a lot).
  * how it had negative implications on processing power and ultimately user experience, which at times became glitchy and laggy.


### React in MVC

Here is what the MVC architecture represents:

- `M stands for Model`
- `V stands for Views` 
- `C stands for Controller.` 

 The View is the presentation layer, it’s what the user sees and interacts with in the browser. The Controller makes the decisions based on requests and then controls what happens in response, like clicking on links and submitting forms. It controls the interaction with the Models and Views (passing data from one to the other). The model refers to the database

 React is now the View in this model. 

<img src="https://i.imgur.com/t779Jw9.png" width=600/>

React will work with any back-end language such as Node/Express, Rails, Django, ect. 


## The Virtual DOM For Efficiency

The Virtual DOM is a Javascript representation of the actual DOM, which looks like the following:

<img src="https://i.imgur.com/qB0cznr.png" width=500/>

The virtual DOM is a staging area for changes that will eventually be implemented. Because of that, React can keep track of changes in the actual DOM by
  comparing different instances of the Virtual DOM.

  <img src="https://i.imgur.com/xTxgF0b.png" width=500/>

React then isolates the changes between old and new instances of the Virtual
  DOM and then only updates the actual DOM with the necessary changes as opposed to re-rendering an entire
  view altogether, it's significantly more efficient.


  <img src="https://i.imgur.com/RmHCcDu.png" width=500/>




### Getting Started With React

So now it's time to get started with React.  Let's open the following starter code and install the required libraries:

[CodeSandbox Starter](https://codesandbox.io/s/rctrr-9-8-20-getting-starter-yryf6)

**NOTE:** In order to easily share code, submit homeowrk and work through errors we will be using `CodeSandbox` for this remote course.

So a few things have been removed from this CodeSandbox and need to be readded on our part to get our React app up and running properly.  For this demo we will focus on:

- Add the required libraries (react & reactDOM)
- Import the libraries into index.js
- Use ReactDOM to render some initial content. 


#### Adding Dependencies

Let's add the following dependencies first.  On the left side click on `Add dependency` 

<img src="https://i.imgur.com/Q9aLHqN.png" width=300/>

And then add the following:

- `react` - used to create Components
- `react-dom` - used to manage the Virtual DOM
- `react-scripts` - used to transpile the code

Once they have been added it should look like the following.  Take note of the react version which in this case is `16.13.1`.  As of `16.8` React introduced `Hooks` which has changed that way we write our React Components and will be the focus of this course. 


<img src="https://i.imgur.com/ksZIMRm.png" width=300/>

#### Setting Up index.js

In the left pane we should see the following.  This is essentially the default folder structure for React App however, as mentioned earlier, it is missing a few things. 

Both the `public` and `src` folders are important with the `public` folder being sent to the end user and the `src` used to write all our React code. 

<img src="https://i.imgur.com/pHKE3l4.png" width=300/>

#### Importing The Libraries
First we need to import the libraries into `index.js`.

```js
// IMPORT React
import React from "react";
// IMPORT ReactDOM
import ReactDOM from "react-dom";
```

#### ReactDOM.render()
With our libraries in place we can use ReactDOM.render() to render data to the screen, in our basic starter app we will render some basic `JSX` for now. 

`ReactDOM.render()` It takes the following two arguments:

1. The HTML or Component name
2. The DOM element we want to append it to.

```js
// GRAB THE ELEMENT WITH AN ID OF ROOT AND STORE IN A VARIABLE CALLED rootElement
const rootElement = document.getElementById("root");
// USE ReactDOM TO RENDER SOME HTML
ReactDOM.render(<h1>Hello World</h1>, document.getElementById("root"));
```

We should see our app update to show the following:

<img src="https://i.imgur.com/3xze8jL.png" width=300/>


We only have to use `ReactDOM.render()` when `mounting` react to our html and this happens only once.  That's why we do it at the root of the page, so that the rest of our site can be built using react components.

**Question:** We know that `Hello World` is being rendered from `index.js` but where is the element with a className of `App` coming from?

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min


Let's take a moment to examine `public/index.html`


- Look for an element with an `id=root`
- Does it have any HTML directly inside of it? 
- Investigate the same element in Chrome Developer Tools and we should see the following:

<img src="https://i.imgur.com/ka5Pd4F.png" width=300/>

Now cut the entire element with `className=App` and paste it over our `<h1>` in `index.js`. 

<img src="https://i.imgur.com/y2l6la8.png" width=400/>

React will re-render and our page should display the content.   Take note that it also renamed `className` to `class`.

<img src='https://i.imgur.com/LViMzXN.png' width=500/>

<hr>


### Resources

- For an intro to React, watch [this video](https://generalassembly.wistia.com/medias/lr8idjxtx8).
