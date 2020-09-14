<br>
Title: Intro to State<br>
Duration: 1hr + <br>
Creator:  Joe Keohan<br>

---

# Intro to State

<img src="https://i.imgur.com/KRmlOo1.png" width=500/>

## Learning Objectives

After this lesson you will be able to:

- Explain what `state` is and how to implement it in React
- Use `Array Destructuring` to create variables from an array 
- Update `state` and re-render the Component

## Framing

The best analogy to understand React `state` is to start by answering the following question: How are you feeling this very moment?

- Are you happy to be in class learning a new topic?
- Are you frustrated to sit for the next 2hrs learning a new topic?
- Did some random person wish you a good evening and make you smile?

The answer to any one of those questions has a direct impact on the `state` of mind your in. A `happy` state will be reflected in your smile, your tone of voice, your being nice to others in return. An `unhappy` state will have the opposite reaction.

As with all human beings our `state` of mind changes on the fly which is reflected is all the ways you can imagine. React keeps track of the applications `state` and updates the UI to reflect any changes made to state.

Therefore updating `state` is our control mechanism for how we update the DOM.

## Props Recap

So far we've worked with `props` and used them to pass values from a `parent` to a `child` Component. Data in React is `unidirectional` and always flows down.

We also know that the props passed down to a child are organized, by React, into an object where every prop becomes a key:value pair.

Props are a great way to pass data but have the following limitations:

- Props are immutable
- React will ignore any attempt to reassign a prop value
- Reassigning a prop value will have no effect on the Component.

<hr>

#### :alarm_clock: Activity - 2min

Let's take a moment to edit our previous [Cards CodeSandbox]() and try to reassign a value to a prop.

**Note:** Feel free to fork this CodeSandbox if you missed last class or are havivngg issues with your version the last code along.

- Open the `Card` Component and add the following:

```js
console.log('current props.title', props.title);
props.title = 'Mykonos';
console.log('props.title', props.title);
```

Refresh the page and you should see the following:

<img src="https://i.imgur.com/Nmio71o.png" width=300/>

<hr>

#### :mag: Check for Understanding - 2min

- Take 2 minutes to think about and write your answers to the following questions:
  - What do we use `props` for?
  - What benefits do they provide when passing down multiple properties?
  - What limitations do they have?
- When asked slack your answer(s) in a thread created by the instructor

<hr>

## Intro To State

In our attempt to provide a coherent framing of React `state` the point was made that what you see on the page is current `state` of the application. Any changes to `state` , aka `data`, will then be reflected in the UI.

One important thing to note here is that any changes to state will cause the Component to `re-render`. This is essentially how the UI is updated. This is a very important concept to keep in mind as a `re-render` can also initiate additional function calls, something we will discuss as part of React `lifecycle methods`.

### Working With State

So updating state will, most often, require the user to interact with the application. Hence the user performs some action, like clicking a button, and the component responds by `doing a thing` and updating `state`.

We've done a fair amount of framing so far, so let's dive in to building our
application!

### A Simple Counter Component

We'll walk through a very simple `Counter` Component which provides the user 2 buttons to increment or decrement a counter.

#### Spin Up A New CodeSandbox

For this demo you will spin up a new CodeSandbox. To do this just click on the blue `Create Sandbox` button.

<img src="https://i.imgur.com/N0qsmdh.png" width=200/>

Now scroll down to the `Official Templates` section and choose `React by CodeSandbox`.

<img src="https://i.imgur.com/dgdr5A8.png" width=300/>

#### Creating The Counter Component

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Since you already have experience creating Components take a minute to perform the following activity.

- Create a new file in `src` called `Counter.js`
- Import `React`
- Return the following html:

```js
<>
    <span>Current Count: 0</span>
    <section>
        <button>+</button>
        <button>-</button>
    </section>
</>
```

- Export the Component
- Import the Component into `App.js`
- Replace all the html inside of `className="App"` with:

```js
<div className='App'>
	<Counter />
</div>
```

Once your done React should render the following:

<img src="https://i.imgur.com/fBEOYU0.png" width=300/>

That HTML looks like it could use a little styling so add the following css to `styles.css`

<details>
<summary>CSS</summary>


```css
.App {
	font-family: sans-serif;
	text-align: center;
	width: 160px;
	margin: auto;
	display: flex;
	flex-direction: column;
}

section {
	display: flex;
}

button {
	flex: 1;
}

span {
	font-size: 20px;
}
```

</details>

<br>


And now the design should look like:

<img src="https://i.imgur.com/jTh9SU2.png" width=200/>

<hr>

### Working With useState

In order to add state to the `Counter` Component we will first need to import `useState` from `React`. `useState` is one of the 3 Basic Hooks as per the Official React Doc.

#### A Word On Hooks

Hooks were introduced in React Version 16.8.

Before hooks, all state needed to be within a Class component. Class components come with a lot of boilerplate, which can feel bulky, especially when dealing with a simpler state. 

Hooks introduce state management to Function components, using a simpler and more flexible API. Here's an example of a Class component refactored to be a Function component with hooks:

> "Hooks let you split one component into smaller functions based on what pieces are related"



<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Since we will be working with `Hooks` solely in this class let's take a minute to review the following React Docs:

- [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html)
- [useState Hook](https://reactjs.org/docs/hooks-overview.html)  



<hr>

#### Importing useState

Now it's time to import `useState` into the Counter Component.

The react library has a key called `useState` that we elicit and store in a variable of the same name by using the `Object Destructuring` syntax: `{useState}`

```js
import React, { useState } from 'react';
```

Just so that we get a better idea of what `useState` actually is let's add a console.log.

```js
const Counter = () => {
  console.log('useState - ', useState)
  ...rest of code
}
```

The output should look like the following:

<img src="https://i.imgur.com/IZFNnbg.png" width=400/>

It appears that `useState` is a function that takes in in `initialState` and returns `dispatcher.useState()`. We won't get into the underlying code here but one thing I want to highlight is the keyword `dispatcher`. 

We will revisit this concept later when we cover the `useReducer` hook as it makes use of a `dispatch` function. 

<hr>

#### useState Rules and Best Practices

:oncoming_police_car: - Rules 

Here are some of the rules that govern the useState Hook:

- never update the state value directly
- always use the `setState` function (or whatever you named it) to update state
- since state is never directly edited it must always be overwritten with a new value 

:star: - Best Practices

A few best practices when assigning variable names are:

- Use `Array Destructuring` when initializing the state variables
- Name the initial state based on what it contains
- Use the same name for the function but precede it with `set`
- Use a the callback function version of useState if you need to reference the previous version of state.

<hr>

#### Creating An Instance Of State

With `useState` imported it's time to create an instance of state. To do this we will call `useState()` and pass it an initial starting value of `0`

```js
const countState = useState(0);
```

Once again let's add a console log and see what it returns.

```js
const countState = useState(0);
console.log('countState -', countState);
```

We should see the following:

<img src="https://i.imgur.com/0SIS9qZ.png" width=300/>

So it appears `countState` is set to an array that contains the following elements:

- 0 - the initial state value we defined
- a `function` - which we will be used to update state.

One way to create 2 new variables based on the array would be to manually elicit their values using bracket notation. 


⭐ Naming State Variables

In keeping with best practices we will name the initial state variable `count` as it will use it to increment/decrement a starting value essentially keeping `count`. Of course, the corresponding function that will be used to update state should be called `setCount`.

```js
const count = countState[0];
const setCount = countState[1];
```

#### Array Destructuring 

:star: 
A more convenient way of doing this is using ES6 [Array Destructuring](https://javascript.info/destructuring-assignment). 

This elicits the values from the array based on their position  and stores them in variables. 


```js
const [count, setCount] = useState(0);
```

#### Using State

Now that our initial value is been assigned to the `count` variable let's update the JSX to use that value instead of a current hard coded, static value of 0. 

Of course, as has been stated several times already, JSX requires that all JavaScript be surrounded in curly braces.


```js
return (
	<div>
		<span>Current Count: {count}</span>
		... rest of code
	</div>
);
```

#### Updating State

With our state value in place it's time to provide some functionality to the buttons so that we can provide the user a means to update state.

In the case of our Counter the only way to update  `count` is to call the `setCount` function and pass it a new value. 

There are 2 ways to perform this action:

```js
// update the current value directly
setCount(count + 1);

// OR

// use a callback function and pass the previous version of state
setCount((prevState) => prevState + 1);
```
In the second example React will call that updater function with the previous value of the state, and whatever you return will replace the state with a new value. The argument is called `prevState` in the example but you can name it anything.

There are scenarios when the callback function version is required such as when state is being updated within the callbacks of either a `setTimeout()` or `setInterval()`.  


#### Adding an onClick Event

In order to allow the user to interact with the buttons we will need to add an event listener.

React event listeners is an additional topic we will revisit again in future lessons. For now we will add an `onClick` event listener and call `setCount` to update state.

Also, as with plain JavaScript or jQuery we will use an anonymous callback to pause the execution until the click event has occurred.

```js
  return (
    <div>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={() => setCount(count + 1)}>+</button>
        <button onClick={() => setCount(count - 1)}>-</button>
      </section>
    </div>
  )
```

#### Event Handlers

Working with React certainly requires that we write code in very specific and opionated ways. That is a good thing in that we can quickly examine code and expect to find a consistent and reliable way as to how it is written.

But some React code is written soley based on the adoption of the community. One such pattern is creating `event handler` functions and preceding their name with `handle`.

Let's give that a try by creating the following supporting functions:

- `handleIncrement`
- `handleDecrement`

```js
const handleIncrement = () => {};

const handleDecrement = () => {};
```

Now let's move the `setState` function calls into their corresponding `handler` as well as replace the anonymous function call with our handlers

```js
const handleIncrement = () => {
	setCount(count + 1);
};

const handleDecrement = () => {
	setCount(count - 1);
};

<section>
	<button onClick={handleIncrement}>+</button>
	<button onClick={handleDecrement}>-</button>
</section>;
```

The other added benefits of using these supporting `handler` functions are:

- its a much better way to organize our code
- we now have a function that can be passed down to a child Component as `props`

#### State Update Delay

Although the updates to state appear immediate there is one thing to note.  After calling `setState` the new value assigned to state isn't available until the Component re-renders. 

So if we were to console.log `count` immediately after it's been updated in handleIncrement we would see it outputs the previous version of state. 

```js
const hanndleIncrement = () => {
    setCount(count + 1);
    console.log('handleIncrement - count:', count)
};
```

Here we can clearly see that `count` is now 2 but the console logs show that count is one value behind. 

<img src="https://i.imgur.com/V0agq9h.png" width=300/>

There will indeed be instances where we will need to run some logic based on the state change but in order to do this we must we must do so after after rendering and using the` useEffect()` hook. 

The `useEffect` hook is a much broader topic and delves into the React Component Lifecycle methods, something we will learn about in upcoming lectures. 


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's try a quick activity that should help you apply some of these concepts.  

- Add a new `Reset` button to the Component that, when clicked, will reset the counter back to 0. 
- Use the `handler` model that we used to setup the previous buttons. 
- Implement `setCount` using the callback function approach. 

<hr>

#### Final Solution

Here is the final version of the Counter Component.

<details>
<summary>Solution</summary>

```js
import React, {useState} from 'react'

const Counter = () => {

  const [count, setCount] = useState(0)

  const handleIncrement = () => {
   setCount(count + 1)
  };

  const handleDecrement = () => {
    setCount(count - 1)
   };

  const handleReset= () => {
    setCount(0)
  };

  return (
    <div>
      <span>Current Count: {count}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
        <button onClick={handleReset}>Reset</button>
      </section>
  )
}

export default Counter
```

</details>



<hr>

#### :mag: Check for Understanding - 2min

- Think about the following questions:
  - What do we use `props` for?
  - What do we use `state` for?
  - What is the difference between `state` and `props`?
- Take a moment to write out your best answer for each question, 3 answers in total.
- When asked slack your answer(s) in a thread created by the instructor

<hr>

### Bonus - Using Conditional Logic and Ternary Operators

Since React is all JavaScript we can use all of our previous JS expertise and knowledge when trying to implement or work out additional logic. 

Let's add some basic conditional logic to the handleIncrement/handleDecrement that will reset the count to 0 if it meets a specific threshold.  

**handleIncrement**
```js
const handleIncrement = () => {
  if(count === 3) {
      handleReset()
    } else {
      setCount(count + 1)
  }
}
```

**handleDecrement**
```js
const handleDecrement = () => {
  if(count === -3) {
      handleReset()
    } else {
      setCount(count - 1)
  }
}
```

#### Refactor To Use `Ternary` Operator

Most often React developers prefer to write a single if/else conditional as a `ternary` operator.  So let's refactor our code to do just that.

**handleIncrement**
```js
const handleIncrement = () => {
  count === 3 ? handleReset() : setCount(count + 1)
}
```

**handleDecrement**
```js
const handleDecrement = () => {
  count === -3 ? handleReset() : setCount(count - 1)
}
```


### Resources

- [React Docs - useState](https://reactjs.org/docs/hooks-overview.html)
- [The useState Hook - robinwieruch](https://www.robinwieruch.de/react-usestate-hook)
- [React useState Hook Guide - dmitirpavlutin](https://dmitripavlutin.com/react-usestate-hook-guide/)
- [React Event Handlers - robinwieruch](https://www.robinwieruch.de/react-event-handler)
<hr>
