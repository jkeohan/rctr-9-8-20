<br>
Title: Working With More Complex Versions Of State<br>
Duration: 1hr + <br>
Creator:  Joe Keohan<br>

---

# Working With More Complex Versions Of State

## Learning Objectives

After this lesson you will be able to:

- Create multiple instances of useState
- Work with objects and arrays as state values
- Use `Object Destructuring` to copy data from a previous version state

## Framing

We've all had to learn new skills in our lives. The fact that your sitting in the class right now is an example of just that.

At first, learning something new involves keeping track of small bits of information. Take for instance learning a skill like riding a bike. A child often starts with training wheels so that they can focus on developing the skills to peddle and steer. They might even attempt standing up to provide more downward force into the peddle. 

Soon the training wheels are removed and they must learned to balance which requires that they adjust their steering and how they peddle while all the while paying attention to their surroundings. 

Building our app falls along the same path. At first we might only need to keep track of a single number. But then we may need to keep track of how many times that number has been incremented/decremented or how many times the user has reset the number back to 0. We may need to keep track of what time and day each event occurred. 

All of it requires a more organized approach to aggregating the data. 

## More Than One State

So far,  we've only leveraged one instance of useState to keep track of a single number. 

Several requirements has been introduced to the app that require:

- keeping track of how many times the reset button was clicked 
- color coding an elements background based on which button was clicked
- keeping a record of which button was clicked and when

There are several ways that we can keep track of additional state values:

- create an additional instances of useState
- aggregate all state values into a single object 

### Multiple Instances of useState

Let's continue to work through the Counter Component and take the first approach of adding an additional instance of state.

Here is the [Counter CodeSandbox Starter](https://codesandbox.io/s/rctr-9-8-20-w02d04-counter-starter-71oc2?file=/src/Counter.js) code with the changes from the previous lecture. 

**Note:** Feel free to fork this CodeSandbox if you missed last class or want a fresh codebase to start with.

Just as a quick review here is what we need to do: 

- create a new instance of `useState`
- update the `JSX` to include a new HTML element to show the state value
- calls the `setState` function to increment that value

Let's start with creating a new instance of useState that will keep track of how many times the reset button was clicked. 

```js
const [resetCount, setResetCount] = useState(0);
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now that we have added a new instance of useState so let's take a look at `React DevTools` and confirm state is present and accounted for.

 If you highlight `Counter` it should look like the following:

<img src="https://i.imgur.com/HvD9hbo.png" />

Try incrementing the value a 4x times and you should both values eventually update.

<img src="https://i.imgur.com/qMRuN3L.png" />

One thing to note here is that each instance of state is merely represented by the word `State` and not which specific state it represents. 

<hr>


Since we will be keeping track of how many times the reset button is clicked it makes sense to call `setResetCount` in `handleReset`. 

```js
const handleReset = () => {
	setCount(0);
	setResetCount(resetCount + 1);
};
```

And finally let's add some JSX to display the current value in the DOM.

```html
<span>Current Count: {count}</span> 
<span>Reset Count: {resetCount}</span>
```

The Counter app should look like the following now:

<img src="https://i.imgur.com/zTDYKVe.png" width=200/>

Try clicking on `+/-` a few times and then the `Reset` button. Confirm that the functionality is working as expected.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's try a quick activity that should help you apply some of these concepts.

- Add a third instance of state called `color` and set it's initial value to `white`
- When the user increments the counter set color to `lightgreen` 
- When the user decrements the counter set color to `pink` 
- Add an inline style to the `Current Count` span that will apply the background color assigned in state.

Here is the basic syntax of writing an inline style.

```html
<span style={{ css-property-name: value }}></span>
```

:thumbsup: Click on the thumbs up when you've implemented the solution

<hr>

<details>
<summary>Solution</summary>

```js
const Counter = () => {
  const [count, setCount] = useState(0);
  const [resetCount, setResetCount] = useState(0);
  const [color, setColor] = useState('white');

  const handleIncrement = () => {
    count === 3 ? handleReset() : setCount(count + 1);
    setColor('lightgreen');
  };

  const handleDecrement = () => {
    count === -3 ? handleReset() : setCount(count - 1);
    setColor('pink');
  };

  const handleReset = () => {
    setCount(0);
    setResetCount(resetCount + 1);
  };

  return (
    <>
      <span style={{ background: color }}>Current Count: {count}</span>
      <span>Reset Count: {resetCount}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
        <button onClick={handleReset}>Reset</button>
      </section>
    </>
  );
};
```

</details>

### Using an Object as the State Value

Adding another instance of useState works in this example and it seems like an intuitive way to go. 

There is however one small flaw in our design but it won't become evident until we try and call `setColor` in both `handleIncrement/handleDecrement` and then again in `handleReset`.

Let's add `setColor` to `handleReset` and see this in action, or better yet, not in action.

```js
setCount(0);
setResetCount(resetCount + 1);
setColor('white');
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

- Try incrementing the value more than 3x
- This should do the following:
  - resets count to 0
  - if clicked 3x increments the reset counter by 1
  - reset the background color to white...`or does it?`

<hr>

As our testing would have confirmed the color is not reset to white. 

The issue is that we are calling `setColor` in 2 different functions in sequence and React will ignore the second update call.  

In order to set the value to white React would need to first `re-render` and then call `setColor`.  This requires the help of an additional hook called `useEffect` and something that we will cover in a future lecture. 

So having multiple unique instances of useState can work but it also has it's limitations.  

Also, having multiple instances starts to make the code seem more bloated. 

A better approach would be to create one single instance of useState that contains all the values.  The most optimal data type to use for this is an `object`.  

#### One Object To Rule Them All

Let's organize all our data into one object and comment out the previous instances of useState.

:star: Name the initial state based on what it contains

For the sake of this demo I'm calling it `counterObj` and only to convey that this state is now set to an object.  If this was a real app we would probably call it something more like `counter` or `counterState`.  

```js
const [counterObj, setCounterObj] = useState({
    count: 0,
    resetCount: 0,
    color: 'white'
});
```

Of course this requires some refactoring to use the new object.  

Let's start with `handleIncrement`.  Since it's only responsible for incrementing the count and assigning the color let's make sure it updates those two values.

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

Now that we have updated useState to use an object let's take a look at `React DevTools` and see what state looks like now.

 If you highlight `Counter` it should look like the following:

<img src="https://i.imgur.com/0CtvajS.png" />

Try incrementing the value just once and you should see state update to the following:

<img src="https://i.imgur.com/1zcgDuK.png" />

:question: **Question:** What change has occurred to our object?

<hr>

### The ...Spread Operator

So it seems that state lost one of its keys.  In this instance when we called `setCounterObj` and assigned it a new object we excluded one of the keys.

This is due to the following rule:

:oncoming_police_car: State is never directly edited and must always be overwritten with a new value 

 In order to guarantee that all the previous keys are present in the new object we must use the `...spread` operator. 

:star: Always use `...spread` operator to copy object and array values to the new state

Let's update our code to use the `...spread` operator:

```js  
counterObj.count === 3 ? handleReset() : setCounterObj({
    ...counterObj,
    color: 'lightgreen',
    count: counterObj.count + 1
});
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now it's your turn.

- Update both `handleIncrement` and `handleRest` to use the new implementation of state. 
- Click on the thumbs up :thumbsup: when you've implemented the solution

<hr>

<details>
<summary>Solution</summary>

```js
const Counter = () => {
  const [counterObj, setCounterObj] = useState({
    count: 0,
    resetCount: 0,
    color: 'white'
  });

  const handleIncrement = () => {
    counterObj.count === 3 ? handleReset() : setCounterObj({
      ...counterObj,
       color: 'lightgreen',
       count: counterObj.count + 1
    });
  };

  const handleDecrement = () => {
    counterObj.count === -3 ? handleReset() : setCounterObj({
      ...counterObj,
       color: 'pink',
       count: counterObj.count - 1
    });
  };

  const handleReset = () => {
    setCounterObj({
      color:'white',
      count: 0,
      resetCount: counterObj.resetCount + 1
    })
  };

  return (
    <>
      <span style={{ background: counterObj.color }}>Current Count: {counterObj.count}</span>
      <span>Reset Count: {counterObj.resetCount}</span>
      <section>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
        <button onClick={handleReset}>Reset</button>
      </section>
    </>
  );
};
```

</details>


### Using an Array as the State Value

So we were just informed that the owner of the app would like to capture, not only how many times each increment/decrement button was clicked but the time it was clicked as well.  

Now we have the following 2 options to implement this requirement: 

- add a new key:value to our existing state 
- create a new instance of state

Since the goal of this section is to demo how to set an array as the value for state let's opt to create a new instance of state. 


```js
const [buttonClicks, setButtonCLicks] = useState([])
```

#### Update Handlers

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

If we examine `React DevTools` we should see the new state in place. 

<img src="https://i.imgur.com/r7CTmiE.png">

Let's click `increment` and see state update.

<img src="https://i.imgur.com/4ucdMci.png">

And now `decrement`

<img src="https://i.imgur.com/01Lvjls.png">

Hmmm...It seems we've lost the previous value. This has to do with the fact that were overwriting the previous array with a new one that only contains a single object based on the last instance of a button click.

So just like the `counterObj` we need to copy the previous elements in the array to a new array.  For that we can use the `...spread` operator once again.

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

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

Way back machine time...

Before the introduction of the ES6 `...spread` operator what other techniques did you use to create a copy of an array?

Slack you answer in a thread created by the instructor.

<hr>

### Bonus - Using A Style Object

So we've used inline styles to assign the background color property 

```js
 <span style={{ background: counterObj.color }}>Current Count: {counterObj.count}</span>
```

This works best if there is only a single value to assign but if there are more properties then it will start to bloat the JSX and make it harder to read.  Another way to structure the css is to use an object. 

```js
const styles = {
  background: counterObj.color
}
```

Let's use the styles object.

```js
<span style={styles}>Current Count: {counterObj.count}</span>
```

Let's keep in mind that `background` is short for several properties in css so let's be very specific about which rule we are targeting, which is `background-color`.  

Let's update the property name to target that rule specifically. 

```js
const styles = {
  background-color: counterObj.color;
}
```

That however won't work and we should get the following:

<img src="https://i.imgur.com/hIzbE5L.png" width=500/>

We must keep in mind that there are other rules, JavaScript specific, that React must follow as well. And in the case of css property names they must be written in camel case.  

Let's update the previous rule and add one more to drive the point home. 

```js
const styles = {
  backgroundColor: counterObj.color,
  fontFamily: 'cursive'
}
```

We should end up with the following error:

<img src="https://i.imgur.com/ahgAR8a.png" width=200/>

```js
const styles = {
  backgroundColor: counterObj.color,
  fontFamily: 'cursive'
}
```

## Recap

#### Here is the solution code from our in-class build

[Solution Code](https://codesandbox.io/s/rctr-9-8-20-w02d04-counter-startersolution-gybkx?file=/src/Counter.js)

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

### Resources

- [ES6 Tutorial](https://www.javascripttutorial.net/es6/)
