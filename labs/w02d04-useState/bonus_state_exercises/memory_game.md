# Intro To State Exercise

**Title:** Intro to State<br>
**Duration:** 15-30min <br>
**Creator:**  Joe Keohan<br>

So far you've learned the following about React:

- Creating and nesting Components
- Iteraring over an array and creating many instances of the same Component 
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. At a high level you will do the following:

> Iterate over an array and create a Card Component for each element in the array. Each card will be assigned the same background image.  When the user clicks on a card it will update and re-render the image assigned to the cardImage key for that card specifically. 

## Working Version
Here is a [working version](https://codepen.io/jkeohan/live/peZQaz) of the app so you have a reference of the base functionality that you are being asked to implement. 

Examine the working version of the app so you can see what element will be rendered as the actual card.  

## Starter CodeSandbox
Here is the [Starter CodeSandbox](https://codesandbox.io/s/rctr-9-8-20-memory-game-starter-hgp2t?file=/src/App.js)

## Instructions
For this exercise you will do the following:

#### Card Component
- Examine the working solution and determine what HTML element is being used to render as the card
- Create a `Card` Component that accepts props 
- Import and setup `state` in the Card Component
- State should be assigned an initial value of the `backgroundImage` key
- Update the Card Components JSX to use the value stored in state
- Add an `onClick` event to the Card that will set state for that Card to the value assigned in the `cardImage` key

#### App Component
- Import the data into App.js
- Import the `Card` Component into `App`
- Examine the data in the `cardData.js` file
- Iterate over the array and pass the `Card` Component the data it needs as props

#### Bonus 

- Add the logic needed that will allow the user to click the card and toggle between the background and card image