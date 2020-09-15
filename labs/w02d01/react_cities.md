# Intro To State Exercise

So far you've learned the following about React:

- Creating and nesting Components
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. At a high level you will do the following:

> Using only a single App Component you will implement the logic that allows a user to click on one of 4 small images and then update the DOM to display that image as the large image.

<img src="https://i.imgur.com/ORYJpoM.png" width=200/>

## Working Version
Here is a [working version](https://codepen.io/jkeohan/pen/850f8454693590e9772f8d0f6c2f44c8?editors=1000) of the app so you have a reference of the base functionality that you are being asked to implement. 

The solution above was implemented using jQuery so there is no React code to inspect via DevTools.  It is meant to provide a working example of the apps functionality. 

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/rctr-9-8-20-react-cities-starter-kpsk5)


## Instructions
For this exercise you will do the following:

#### App Component
- Examine the working live solution and determine the functionality needed
- Examine the HTML provided in `src/index.html` as this contains the HTML elements needed for the design
- Determine how best to organize the data needed to render the images
- Create a file called imageData.js that contains the data needed, in this case images
- Using Array.map() loop over the data to create the small images based on the structure you decided
- Render the array of elements 
- Import `useState` into App
- Use one or more instances of `useState` to implement the logic
- Work out the remaining logic needed to implement the design
