<br>
Title: Passing Props<br>
Duration: 45min+ <br>
Creator:  Joe Keohan<br>

---

# Passing Props

## Learning Objectives

*   Create and pass props to Components
*   Loop over an array of data and pass multiple props
*   Work with additional JSX rules. 

### Props

Properties!  Every Component has `props` and they are how we pass data from a parent to a child Component. 

Props are a great way to pass data but have the following limitations:

- Props are immutable
- React will ignore any attempt to reassign a prop value
- Reassigning a prop value will have no effect on the Component.

### Passing Props

Say for instance we wanted to render the name of the place that the image represents in our cards example. We could go directly to Card1 and do the following: 

```html
<h5 class="card-title">Santorini</h5>
```

That isn't actually passing props but more so just adding the value manually. So let's add a `prop` to Card1 and pass it the value of `Santorini`.

Since the `App` component is actually rendering `Card1` that is where we pass it a prop.  A `prop` is written in a `name=value` format much like the other props your used to writing such as: 

```html
<!-- The src property of a image tag -->
<img src="" />
<!-- The class property assigned to any element -->
<div class="blue"></div>
<!-- The href property assigned to an anchor tag -->
<a href="someurl"></a>
```


Let's add the following prop.

```js
<Card1 title="Santorini"/>
```

Nothing should really change as we have already updated Card1 with that title name. So we need to update the Card1 Component to accept props.

#### Accepting Props
The first thing we need to do is add the keyword `props` as a parameter. So inside Card1.js make the following change. 

Let's make sure that our Component is being passed the `title` prop by adding a console.log.

```js
const Card1 = (props) => {
   console.log('this is props:', props)
   ...rest of the code
```

In DevTools you should see the following in the console.

<img src="https://i.imgur.com/HlrtO2T.png" width=300/>

We can see here that `props` is an object and that `title` is a key.  This will be the same pattern when we start passing in multiple props.  Each one will be assigned a key:value pair. 

#### :alarm_clock: Activity - 2min

Let's take a moment to edit our previous [Cards CodeSandbox]() and confirm these limitations of props. 

- Open the `Card1` Component and add the following:

```js
console.log('current props.title', props.title);
// ATTEMPT TO REASSIGN PROPS A NEW VALUE
props.title = 'Mykonos';
console.log('props.title', props.title);
```

Refresh the page and you should see the following:

<img src="https://i.imgur.com/Nmio71o.png" width=300/>

So it looks like props was not changed and so we have confirmed that once a Component has been passed props that any attempt to change those props directly will have no effect. 

<hr>


#### Using Props

Now that we have confirmed we are being passed the value and it's stored within an object let's replace the hard coded value.

Another JSX rule that we need remember is that any JavaScript code that needs to be executed must be enclosed in opening/closing curls braces `{}`

```js
<h5 className="card-title">{props.title}</h5>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

- Install [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) for Chrome
- In the DevTools you should see the following new tabs:
     - Components
     - Profiler
- Highlight the `Card1` component and you should see it's props displayed on the right pane.

<img src="https://i.imgur.com/1z614lc.png" />

<hr>

### Passing Mulitple Props

We could do the same for all the additional values we wish to pass but as you can imagine if we had 10, 20, 100+ cards this manual method becomes completely inefficient. 

Also we should expect that the data we will be using to render the cards will be imported either via a file or returned from an API call. 

Either way we should expect the if we will need to create multiple cards that the data will be stored as an array of object:s  `[{}, {}]`

This data has already been organized for us and will be imported in the activity below.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

- Create a new file in `src` called `data.js`
- paste the following code into the file

```js
export default [
  {
    img: "https://images.unsplash.com/photo-1536514072410-5019a3c69182?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=60",
    title: "Santorini",
    text: "This was one of the most amazing places I've ever seen. A must see for eveyrone",
    url: "https://unsplash.com/s/photos/santorini"
  },
    {
      img: "https://images.unsplash.com/photo-1498712964741-5d33ab9e5017?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=400&q=600",
      title: "Zakynthos",
      text: "This was like being a pirate and we were looking to bury our treasure. It was so isolated and beautiful. ",
      url: "https://unsplash.com/s/photos/santorini"
    }
]

```

- Import the data into `App.js` as `cardsArr` and add a console.log to confirm it was imported. 

```js
// IMPORT DATA
import cardsArr from './data'
console.log('this is cardsArr:', cardsArr)
```
<hr>

Now that we have the data we can now loop over it and render as many `Card Components` as we need. 

#### Creating Multiple Cards

Inside of the `App` Component we will now loop over the `cardsArr` array and create multiple Cards in one shot. 

Each prop is defined on it's own and passed it's corresponding value.

Let's also console the `cards` so see what React magic has been performed.

```js
 const cards = cardsArr.map((ele, index) => {
    return (
      <Card1 
        img={ele.img} 
        title={ele.title} 
        text={ele.text} 
        url={ele.url} 
        />
    );
  })

  console.log('this is cards:', cards);
  ```

Now take a look in DevTools and you should see the following:

<img src="https://i.imgur.com/gx42Kme.png" />

One thing to note here is the `key` key.  It is currently set to `null` however React will warn us later when we render the Cards as it needs to assign a unique key to each Component rendered via a loop. 

Before we render the Cards we first need to update `Card1` to make use of the new props being passed down. 

```js
const Card1 = (props) => {
  console.log('this is props:', props)
  return (
    <div className="card" style={{width:'18rem'}}>
    <img src={props.img} className="card-img-top" alt="..."
    />
    <div className="card-body">
      <h5 className="card-title">{props.title}</h5>
      <p className="card-text">{props.text}</p>
      <a href="#" className="btn btn-primary">Go somewhere</a>
    </div>
  </div>
  )
}
```

Now it's time to see all that code preparation in action. In App comment out `<Card1 />` and `<Card2 />` and add `{cards}`

```js
<section className="cards">
    {cards}
    {/* <Card1 title="Santorini" />
    <Card2 /> */}
</section>
```

#### The Key Prop

As you may recall it was mentioned earlier that the elements would render fine however React would present an error.  The following error to be exact:

<img src="https://i.imgur.com/Ofg12N1.png" >

This can easily be fixed by assigning a `key prop` to each element with a unique value.  Since each element in an array is assigned a unique index value we will opt to use that. 

```js
 const cards = cardsArr.map((ele, index) => {
    return (
      <Card1 
        img={ele.img} 
        title={ele.title} 
        text={ele.text} 
        url={ele.url} 
        key={index}
     />
    );
  })
```

The very last edit to make would be to rename the `Card1` Component to `Card` since we we now have a standard Card template. Below represents our codebase at the end of this lesson.

<img src="https://i.imgur.com/SLtYu9d.png">
<br>
<br>

And there you have it.  Multiple Components rendered with each being passed multiple props.  This is how we code in React. 

[Final Solution](https://codesandbox.io/s/rctrr-8-8-20-bootstrap-solution-uyvmg?file=/src/App.js)
