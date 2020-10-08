# Light Levels Using useReducer

## Working Version
Here is a [working version](https://o4noc.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 

<img src="https://i.imgur.com/yx9Z8M0.png" width=500/>

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/light-levels-usereducer-starter-hesji?file=/src/Components/App.js)

## Instructions
For this exercise you will do the following:

### App Component
- examine the working live solution and look over the Components in React DevTools
- look over the imported `lightData` object to determine the light level values
- import `useReducer`
- setup the `useReducer` logic
- pass the `dispatch` function to `Controls` Component

#### Controls Component
- update the `handleClick` to call the` dispatch` function

#### Ligth Component
- pass down a new prop called color that contains the current background color

#### Click Event

- Add a click event to the `Toggle Themes` button that will allow the user to toggle between the themes

<!-- [Solution Code](https://codesandbox.io/s/light-levels-usereducer-solution-8w6m8?file=/src/Components/App.js) -->
