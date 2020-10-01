# Random User API


## Working Version
Here is a [working version](https://tfj8s.csb.app/) of the app so you have a reference of the base functionality that you are being asked to implement. 

## Starter CodeSandbox
Here is our [Starter CodeSandbox](https://codesandbox.io/s/random-user-starter-xtpup?file=/src/App.js)

## Instructions
For this exercise you will do the following:

### App Component
- Examine the working live solution and look over the HTML elements

#### Importing Data on ComponentDidMount
- Import `useEffect` and set it up to run only on ComponentDidMount
- This `useEffect` will make the initial call to fetch call to retrieve data for a single random user 
- This `useEffect` will then update state with the data once it's been returned
- The `content` div will display by default the name of the user in the `bigtext` div

```html
<div id="content">
    <span id="smalltext">My name is</span>
    <span id="bigtext">William Petersen</span>
</div>
```

<img src="https://i.imgur.com/WYR7xv3.png" width=500/>

#### Click Event

- When any of the icons are clicked that info should be dynamically displayed in the `content` div
- Say for example the `email` icon is moused over then the app should update to show the following:

<img src="https://i.imgur.com/rISz9vU.png" width=500/>


#### Bonus - Add A Button To Pull A New User

- Add a button that will make another API call and pull another user
- The new users info will replace the previous user
- Consider consolidating the code to make the api call into a single function
- Consider refactoring `useEffect` to be ComponentDidUpdate where it only runs if a state value has changed

<img src="https://i.imgur.com/wOSW8hx.png" width=500/>
