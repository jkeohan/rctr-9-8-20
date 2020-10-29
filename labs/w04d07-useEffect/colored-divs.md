# Colored/Responsive Divs


## Working Version
Here is a [working version](https://3iej1.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/useeffect-colored-divs-starter-uz3mr?file=/src/App.js)

## Instructions
For this exercise you will do the following:

#### App Component
- Examine the working live solution and look over the HTML elements
- Import and use `useEffect` and set it up to run only on ComponentDidMount
- It should register a window `resize` event that calls the `updateWidth` function
- Once this complete the current window width will dynamically be updated in the UI

Here is an example of adding and removing  a `resize` event listener to the window
```js
  window.addEventListener('resize', updateWidth)
  ```

#### ColoredDiv Component

- Examine the working live solution and look over the HTML elements
- Import and use `useEffect` and set it up to run only on ComponentDidMount
- It should register a window `resize` event that calls the `updateWidth` function
- `useEffect` should also remove the event listener when the Component is removed from the UI

Here is an example of removing  a `resize` event listener to the window
```js
  window.removeEventListener('resize', updateWidth)
```

- Add a conditional style that will set the flex property to 1 if the width is > 1023 or to 0 if its not

#### Bonus - Add New Color Button

- Add the functionality that will add a new color

#### Bonus - Remove Colored Div

- Add the functionality that will remove a ColoredDiv Component
