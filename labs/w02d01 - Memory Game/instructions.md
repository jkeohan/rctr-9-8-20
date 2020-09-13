# Intro To State Exercise

So far you've learned the following about React:

- Creating a single Component
- Iteraring over an array and creating many instances of the same Component 
- Passing props and how to use them in JSX
- Adding and Updating State

Now it's time to put it all together. At a high level you will do the following:

> Create a separate Card Component for each element in the array of data provided. Each card will be assigned the same background image.  When the user clicks on a card it will update and re-render the image assigned to that card specifically. 

## Working Version
Here is a [working version](https://codepen.io/jkeohan/live/peZQaz) of the app so you have a reference of the base functionality that you are being asked to implement. 

## Instructions
For this exercise you will do the following:

#### Card Component
- Examine the data in the cardData.js file
- Create a Card Component that accepts props 
- Import and setup state in the Card Component
- State should be assigned the value of the background image
- Update the Card Components JSX to work with the props passed and state value
- Add an onClick event to the card image that will update the state to the card image

#### App Component
- Import the data into App.js
- Iterate over the array and pass the Card Component the data it needs as props

#### Bonus 

- Add a toggle feature that will allow the user to click the card again and keep toggling the images