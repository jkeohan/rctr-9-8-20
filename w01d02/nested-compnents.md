<br>
Title: Nested Components<br>
Duration: 45min+ <br>
Creator:  Joe Keohan<br>

---

# Nested Components

## Learning Objectives

*   Create and nest multiple Components

## Components

As we've explained Components are the fundamental building blocks of React and let you split the UI into independent, reusable pieces, and be able to use each one in isolation.  

This is very similar to the way we write JavaScript functions in general.  They are meant to be `independent` and `reusable`.  By passing in `standardized` input they will return `standardized output`.  

 Components behave under the same premise and, if configured to accept input, will return UI that is either includes the input or has influenced how the input is displayed. 
 
 The input we will pass to a Component is called a `prop` and we will use them extensively in any React app we build.  

### Nested Components

Let's revisit the Bootstrap card example.  It provides all the HTML needed to produce a standard `card` and, along with Bootstrap css, styles the card quite nicely. 

Here is the HTML provided by Bootstrap:

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

In order to bridge the gap of what defines a Component we will be creating a custom React Card Component that uses the Bootstrap HTML. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Open and fork the following [CodeSandbox Card Starter](https://codesandbox.io/s/rctrr-8-8-20-bootstrap-starter-o2ry1).

You should see the following:

<img src="https://i.imgur.com/NaGIt48.jpg" width=400/>

- Take a moment to examine the code.  
- See if you can determine where the `H1` is being rendered as well as the 2 cards
- The instructor will ask you to post your answer in a thread

:thumbsup: Click on the thumbs up when your done.

<hr>

Our investigation should have determined the following:

- `App` Component - renders the H1
- `public/index.html` - renders the cards

#### Creating A Component

So let's take a moment to create a new `Functional Component` to contain all the Bootstrap code which we will allow us to create the Components needed to produce each card individually. 

In the `src` folder create the following files:

- Card1.js
- Card2.js

:thumbsup: Click on the thumbs up when your done.

We will start with Card1.js for now. Inside of Card1.js let's do the following for now:

- Import React
- Create the Component
- Export the Component

```js
// IMPORT REACT
import React from 'react'

// CREATE THE COMPONENT
const Card1 = () => {
  return (
    <div>Card1</div>
  )
}

// EXPORT THE COMPONENT
export default Card1
```

#### Nesting A Component

Nesting Components is merely calling one Component within the `return` statement of a parent Component.

Now let's import `Card1` into App.js and nest it so that it renders. .

```js
// IMPORT CARD1
import Card1 from './Card1'

export default function App() {
  return (
    <div className="App">
      <h1>Bootstrap Cards To Component Example</h1>
      <Card1 />
    </div>
  );
}
```

If successful you should see the following:

<img src="https://i.imgur.com/jHnPLLv.png" width=150/>

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

**NOTE:** Before you perform the steps we ask that you do not copy/paste at this time and write everything from scratch.  In time copy/paste will be the most efficient way to create Components however you are just learning how to create Components so the additional manual work will help solidfy the concepts.

- Perform the same steps as you did for Card1
- Only change it's HTML output to be `Card2`
- Make sure to render Card2

Your code should produce the following:

<img src="https://i.imgur.com/MOiPdAA.png" width=200/>

<hr>

Now it's time to output the HTML that represents each Component.  This we discovered earlier is found in `public/index.html`

Cut the entire `<div class='card>...</div>` for the first card and place it inside of `Card1`

```js
const Card1 = () => {
  return (
    <div class="card" style="width: 18rem;">
    <img
      src="https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60"
      class="card-img-top"
      alt="..."
    />
    <div class="card-body">
      <h5 class="card-title">Card 1</h5>
      <p class="card-text">
        Some quick example text to build on the card title and make up the
        bulk of the card's content.
      </p>
      <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
  </div>
  )
}

```

We should be immediately met with the following error:

<img src="https://i.imgur.com/u9Uvwg9.png" />

This has to do with the rules of JSX which states that the `style` prop must be written in the following format:

```js
style={{key: value}}
```

Let's update our Component to include the proper syntax

```js
<div class="card" style={{width:'18rem'}}>
```

The other JSX rule we must follow is to rename every instance of `class` to `className` and although it's not a make or break rule as was style we must adhere otherwise we will certainly run into issues later. 

Here is our Component as it stands:

```js
const Card1 = () => {
  return (
    <div className="card" style={{width:'18rem'}}>
    <img
      src="https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60"
      className="card-img-top"
      alt="..."
    />
    <div className="card-body">
      <h5 className="card-title">Card title</h5>
      <p className="card-text">
        Some quick example text to build on the card title and make up the
        bulk of the card's content.
      </p>
      <a href="#" className="btn btn-primary">Go somewhere</a>
    </div>
  </div>
  )
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

- Perform the same steps to Card2 as you did for Card1 
- Make sure to render Card2
- Refesh the page to see the changes

Your code should produce the following:

<img src="https://i.imgur.com/MOiPdAA.png" width=150/>

<hr>

In the original design they were sitting next to eachother.  The reason they are no longer doing that is because we did not include the parent `<section class="cards">` so let's add that to the App Component.

```js
export default function App() {
  return (
    <div className="App">
      <h1>Bootstrap Cards To Component Example</h1>
      <section className="cards">
        <Card1 />
        <Card2 />
      </section>
    </div>
  );
}
```

If everything worked we should now see our original design in place.

<img src="https://i.imgur.com/nsN0Cro.jpg" width=400/>
