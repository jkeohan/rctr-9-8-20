# Traffic Light

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

The solution above was implemented using jQuery so there is no React code to inspect via DevTools.  It is meant to provide a working example of how the apps functionality. 

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/rctr-9-8-20-traffic-light-lifting-state-starter-q6elz)

## Instructions
For this exercise you will do the following:

#### TrafficLight Component
- Examine the working live solution and determine the functionality needed
- Examine the HTML provided in `src/index.html` as this contains the HTML elements needed for the design
- Examine the file called bulbData.js as it contains the data you need to create the elements
- Create a `TrafficLight` Component 
- Import bulbData.js into TrafficLight
- Import `useState` into `TrafficLight`
- Work out the remaining logic needed to implement the design

#### Bulb and Buttons Components

- Create a `Bulb` Component
- Import the Component into TrafficLight
- Loop over the array in bulbData and create 3 Bulb Components 

#### App Component
- Import the data into App.js
- Import the `TrafficLight` Component 
- Render a single `TrafficLight` Component and pass it the data it needs 

**Note:** App will render only a single instance of the TrafficLight Component.  Therefore, in App, do not loop over the array of data and create multiple instances. 

### Bonus - Bulb Component

- Create a new `Bulb` Component that will render the a single bulb
- Pass the `Bulb` Component the color it needs based the state of the application