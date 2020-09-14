# Intro To State Exercise

So far you've learned the following about React:

- Creating and nesting Components
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. At a high level you will do the following:

> Create a TrafficLight Component that will implement the functionality based on the working solution. 

## Working Version
Here is a [working version](https://codepen.io/jkeohan/live/bYYpLN) of the app so you have a reference of the base functionality that you are being asked to implement. 

The solution below was implement using jQuery so there is no React code to inspect via DevTools.  It is meant to provide a working example of how the apps functionality. 

## Instructions
For this exercise you will do the following:

#### TrafficLight Component
- Examine the working live solution and determine the functionality needed
- Examine the HTML provided in `src/index.html` as this contains the HTML elements needed for the design
- Determine how best to organize the data needed to create the control panel and traffic bulbs
- Create a file called bulbData.js that contains the above data
- Create a `TrafficLight` Component 
- Import `useState` into `TrafficLight`
- Work out the remaining logic needed to implement the design

#### App Component
- Import the data into App.js
- Import the `TrafficLight` Component 
- Render a single `TrafficLight` Component and pass it the data it needs 

**Note:** App will render only a single instance of the TrafficLight Component.  Therefore do not loop over the array of data and create multiple instances. 

#### Bonus 

- Add the logic needed that will allow the user to click the card toggle and between the background and card image