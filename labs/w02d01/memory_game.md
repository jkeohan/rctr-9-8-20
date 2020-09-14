# Intro To State Exercise

So far you've learned the following about React:

- Creating and nesting Components
- Iteraring over an array and creating many instances of the same Component 
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. At a high level you will do the following:

> Create a separate Card Component for each element in the array of data provided. Each card will be assigned the same background image.  When the user clicks on a card it will update and re-render the image assigned to that card specifically. 

## Working Version
Here is a [working version](https://codepen.io/jkeohan/live/peZQaz) of the app so you have a reference of the base functionality that you are being asked to implement. 

Examine the working version of the app so you can see what element will be rendered as the actual card.  

## Instructions
For this exercise you will do the following:

#### Card Component
- Examine the data in the `cardData.js` file
- Create a `Card` Component that accepts props 
- Import and setup `state` in the Card Component
- State should be assigned an initial value of the background image
- Update the Card Components JSX to work with the props passed and the initial state value
- Add an `onClick event` to the card image that will set state to the card image

#### App Component
- Import the data into App.js
- Import the `Card` Component into `App`
- Iterate over the array and pass the `Card` Component the data it needs as props

#### Bonus 

- Add the logic needed that will allow the user to click the card toggle and between the background and card image