<br>
Title: Working With More Complex Versions Of State<br>
Duration: 1hr + <br>
Creator:  Joe Keohan<br>

---

# Working With More Complex Versions Of State

## Learning Objectives

After this lesson you will be able to:

- Create multiple instances of state
- Work with objects and arrays as state values
- Use `Object Destructuring` to copy data from a previous version state

## Framing

We've all had to learn new skills in our lives. The fact that your sitting in the class right now is an example of just that.

At first, learning something new involves keeping track of small bits of information. Take for instance learning a skill like karate. A new student must first learn the basics of how to punch straight forward or block the same punch. As they develope the techniques become more advanced with need to keep track of more and more information.

Soon single moves are combined into a sequence of move and then into larger sequences called Kata's. In the end there is a need to aggregate and organize multiple pieces of information.  

Building our app falls along the same path. At first we might only need to keep track of a number. But then we may need to keep track of how many times that number has been incremented/decremented or how many times the user has reset the value back to 0. We may need to keep track of what time and day the resets happened.


## More Than One State

So far, the code we've only leveraged a single instance of useState to keep track of a single number. 

Were are now going to keep track of how many times the reset button was clicked and color code an elements background based on if the current count value is positive or negative.

There are several ways that we can keep track of additional state values:

- create new instances of useState
- use an object that contains the key:value pairs for our state.

### Multiple Instances of useState

Let's continue to work through the Counter Component and add another instance of state.

Here is the [CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-counter-starter-more-state-zxx5w?file=/src/Counter.js) code.

We need to follow the same steps as before:

- create a another instance of `useState`
- update the `JSX` to include a new HTML element to show the state value
- calls the `setState` function to increment that value

Let's start with creating a new instance of useState

```js
const [resetCount, setResetCount] = useState(0);
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now that we have added a new instance of useState let's take a look at the `React DevTools Components` tab and see what state looks like now.

 If you highlight `Counter` it should look like the following:

<img src="https://i.imgur.com/HvD9hbo.png" />

Try incrementing the value a 4x times and you should both values eventually update.

<img src="https://i.imgur.com/qMRuN3L.png" />

One thing to note here is that each instance of state is merely represented by the word `State` and not which state it represents. 

<hr>


Now let's call the `setResetCount` function in `handleReset`

```js
const handleReset = () => {
	setCount(0);
	setResetCount(resetCount + 1);
};
```

And finally add some JSX to display the value in the DOM.

```html
<span>Current Count: {count}</span> 
<span>Reset Count: {resetCount}</span>
```

The Counter app should look like the following now:

<img src="https://i.imgur.com/zTDYKVe.png" width=200/>

Try clicking on the `+/-` buttons a few times and then the `Reset` button. Confirm that the functionality is working as expected.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's try a quick activity that should help you apply some of these concepts.

- Add another instance of state called `color` and set it's initial value to `white`
- Set color to `lightgreen` when the user increments the counter
- Set color to `pink` if the user decrements the counter
- Add in inline style to the span that will apply the background color based on the current value assigned to `color`

Here is the basic syntax of writing an inline style.

```html
<span style="{{" css-property-name: value }}></span>
```

- Click on the thumbs up :thumbsup: when you've implemented the solution

<hr>

<details>
<summary>Solution</summary>

```js
```

</details>

### Using an Object as the State Value

Adding another instance of useState works in this example and it seems like an intuitive way to go. 

There is however one small flaw in our design but it won't become evident until we try and call `setColor` 2x in a row, once via `handleIncrement/handleDecrement` and then again in `handleReset`.

Let's add `setColor` to `handleReset` and see this in action, or better yet, not in action.

```js
setCount(0);
setResetCount(resetCount + 1);
// add setColor
setColor('white');
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

- Try incrementing the value more than 3x
- This should do the following:
  - reset count to 0
  - increment the reset counter by 1
  - reset the background color to white....or does it?

<hr>

The issue is that we are calling `setColor` in 2 different functions in sequence and React will ignore the second update call.  

So having multiple unique instances of useState can work but it also has it's limits.  Also, having multiple instances starts to make the code seem more bloated. 

A better approach would be to create one single instance of useState that contains all the values.  The best data type to do this is an `object`.  

#### One Object To Rule Them All

Let's organize all our data into one object and comment out the previous single instance useStates.

:star: Name the initial state based on what it contains

For the sake of this demo I'm calling it `counterObj` but only to convey that this state is now set to an object.  If this was a real app we would probably call it `counter` or `counterState`.  

```js
const [counterObj, setCounterObj] = useState({
    count: 0,
    resetCount: 0,
    color: 'white'
});
```

Of course this requires some refactoring to use the new object.  

Let's start with `handleIncrement`.

```js
counterObj.count === 3 ? handleReset() : setCounterObj({
    color: 'lightgreen',
    count: counterObj.count + 1
});
```

And now update the JSX with the following:

```js
<span style={{ background: counterObj.color }}>Current Count: {counterObj.count}</span>
<span>Reset Count: {counterObj.resetCount}</span>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now that we have updated useState to use an object let's take a look at the `React DevTools Components` tab and see what state looks like now.

 If you highlight `Counter` it should look like the following:

<img src="https://i.imgur.com/0CtvajS.png" />

Try incrementing the value just once and you should see state update to the following:

<img src="https://i.imgur.com/1zcgDuK.png" />

:question: **Question:** What change has occurred to our object?

<hr>

### The ...Spread Operator

So it seems that state lost one of its keys.  This is due to the following rule:

:oncoming_police_car: State is never directly edited it must always be overwritten with a new value 

In this instance when we call `setCounterObj` and assign it a new object we excluded one of the keys. In order to guarantee that all the previous keys are present in the new object we must use the `...spread` operator. 

:star: Always use `...spread` operator to copy object and array values to the new state

Let's update our code to the following:

```js  
counterObj.count === 3 ? handleReset() : setCounterObj({
    ...counterObj,
    color: 'lightgreen',
    count: counterObj.count + 1
});
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Now it's your turn to update both `handleIncrement` and `handleRest` to use the new implementation of state. 

<hr>

<details>
<summary>Solution</summary>

```js
```

</details>


### Using an Array as the State Value

So we were just informed that the owner of the app would like to capture, not only how many times each increment/decrement button was clicked but the time it was clicked as well.  

Now we have the following 2 options to implement this design

-  add a new key:value to our existing state 
- create a new instance of state

Since the goal of this section is to demo how to set an array as the value for state let's opt to create a new instance of state. 


```js
const [buttonClicks, setButtonCLicks] = useState([])
```

#### Small Refactors

It makes sense to call the `setButtonClicks` function in both handler functions and add a new object that contains the buttonType and date.

```js
const handleIncrement = () => {
    // rest of code...
    setButtonCLicks([
        {buttonType: 'increment', date: new Date()}
    ])
};

const handleDecrement = () => {
    // rest of code...
    setButtonCLicks([
        {buttonType: 'decrement', date: new Date()}
    ])
};
```

If we examine React DevTools we should see the new state in place. 

<img src="https://i.imgur.com/r7CTmiE.png">

Let's click `increment` and see state update.

<img src="https://i.imgur.com/4ucdMci.png">

And now `decrement`

<img src="https://i.imgur.com/01Lvjls.png">

Hmmm...It seems we've lost the previous value. This has to do with the fact that were overwritting the previous array with a new one that only contains the last instance of a button click.

So just like the `counterObj` we need to copy the previous elements in the array to the new array.  For that we can use the `...Spread` operator again.

```js
const handleIncrement = () => {
    // rest of code...
    setButtonCLicks([
        ...buttonClicks,
        {buttonType: 'increment', date: new Date()}
    ])
};
```

Let's increment several times and see if this works. 

<img src="https://i.imgur.com/XeZDVvS.png">

## Recap

You've learned quite a bit about React state.  Let's take a minute to review the `rules` and `best practices`

:oncoming_police_car: - Rules 

Here are some of the rules that govern the useState Hook:

- never update the state value directly
- always use the `setState` function to update state
- since state is never directly edited it must always be overwritten with a new value 

:star: - Best Practices

A few best practices when assigning variable names are:

- Use `Array Destructuring` when initializing the state variables
- Name the initial state based on what it contains
- Use the same name for the function but precede it with `set`
- Use a the callback function version of useState if you need to reference the previous version of state
- Give thought as to what needs to be in state and how that state should be organized and structured

<hr>