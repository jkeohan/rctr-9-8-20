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
- Use `Array Destructuring` and `Object Destructuring` to copy values from state

## Framing

We've all had to learn new skills in our lives. The fact that your sitting in the class right now is an example of just that.

At first, learning something new involves keep track of small bits of information. Take for instance learning a skill like karate. A new student must first learn the basics of how to punch straight forward or block the same punch. As they develope the techniques become more advanced with need to keep track of more and more information.

Soon moves are combined into a sequence and then into large sequences called Kata's. In the end a student needs to be aggregate and organize multiple pieces of information.

Building our app falls along the same path. At first we might only need to keep track of a number. But then we may need to keep track of how many times that number has been incremented/decremented or how many times the user has reset the value back to 0. We may need to keep track of what time and day the resets happened.

## More Than One State

So far, the code we've written only leveraged a single instance of useState that was set to a number. Now let's say that we now need to keep track of how many times the reset button was clicked and display that on the screen and then perhaps color code the background based on if the current count value is positive or negative.

There are several ways that we can keep track of additional state values:

- create new instances of useState
- use an object that contains the key:value pairs for our state.

### Multiple Instances of useState

Let's continue to work through the Counter Component and add another instance of state.

Here is the [CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-counter-starter-more-state-zxx5w?file=/src/Counter.js) code.

We need to follow the same steps as before:

- create a another instance of useState
- update the JSX to include a new HTML element to show the state value
- calls the setState function to increment that value

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
<span>Current Count: {count}</span> <span>Reset Count: {resetCount}</span>
```

Our Counter app should look like the following now:

<img src="https://i.imgur.com/zTDYKVe.png" width=200/>

Try clicking on the +/- buttons a few times and trigger reset along with clicking on the `Reset` button. Confirm that the functionality is working as expected.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's try a quick activity that should help you apply some of these concepts.

- Add another instance of state called `color` and set it's initial value to `white`
- Set color to 'lightgreen' if the user increments the counter
- Set color to 'pink' if the user decrements the counter
- Add in inline style to the span that will apply the background color based on the current value assigned to `color`

Here is the basic syntax of writing an inline style.

```html
<span style="{{" css-property-name: value }}></span>
```

- Click on the thumbs up :thumbsup: when you've implemented the solution

<hr>

### Using an Object as the State Value

No new concepts were introduced were really introduced yet except adding another instance of useState.

There is however one small flaw in our design but it won't become evident until we try and reset the background to white when `handleReset` is called.

Let's add `setColor` to `handleReset` and see this in action, or perhaps not in action.

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

A better approach would be to create one single instance of useState that contains all the values.  What better data type to do this than an `object`.  

#### The All In One Approach

Let's organize all our data into one object and comment out the previous single instance useStates.

```js
const [counterObj, setCounterObj] = useState({
    count: 0,
    resetCount: 0,
    color: 'white'
});
```

Of course this requires additional refactoring to use the new object.  Let's start with `handleIncrement`.

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

Try incrementing the value just once times and you should see the following:

<img src="https://i.imgur.com/1zcgDuK.png" />

:question: **Question:** What happened to our object in state?

<hr>

### The ...Spread Operator

So it seems that state lost one of its keys.  This is due to the following rule:

:oncoming_police_car: State is never directly edited it must always be overwritten with a new value 

In this instance when we call `setCounterObj` as assign it a new object we did so but excluded one of the keys. In order to guarantee that all the previous keys are present in the new object we must use the `...spread` operator. 

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