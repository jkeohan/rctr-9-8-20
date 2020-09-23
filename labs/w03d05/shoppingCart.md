# Shopping Cart

So far you've learned the following about React:

- Creating and nesting Components
- Passing props and how to using them in JSX
- Importing and setting up state
- Updating state and re-rendering the Component
- Adding and calling event listeners

Now it's time to put it all together. 

## Working Version
Here is a [working version](https://1prws.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/react-shopping-cart-starter-e2km4?file=/src/App.js)

## Instructions
For this exercise you will do the following:

#### App Component
- Examine the working live solution and look over the HTML elements
- Examine the file called products.js as it contains the data you need to create the elements
- Examine React Developer Tools and see how this App has been configured

#### AllTheThings Component

- Render a full list of the products with name and price
- When an item is clicked the value will be lifted to App
- App will update state and place the item 

#### MyShoppingCart Component

- Render the list of products in your shopping cart
- When an item is clicked the value will be lifted to App
- App will remove the item from state and pass down the new data set to MyShoppingCart
