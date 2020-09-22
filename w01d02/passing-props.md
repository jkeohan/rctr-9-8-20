<br>
Title: Passing Props<br>
Duration: 1.5hrs+ <br>
Creator:  Joe Keohan<br>

---

# Passing Props

## Learning Objectives

*   Create and pass props to Components
*   Loop over an array of data and pass multiple props
*   Work with additional JSX rules. 

## Framing

Having worked with functions we know that they are meant to be reusable.  Part of the reusability is the being able to accept arguments, perform some action and return something.  

Now consider that our application will have data and parts of the data will need to rendered in the UI.  Doing so means passing the Components the data they need and then performing whatever action is needed to render all or parts of the data in the UI. 

The data we pass to Components are called: `props`.

### Props

Every Component has `props` and they are how we pass data from a parent to a child Component. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's revisit `React Developer Tools` and take a look at a few Components and see if anything `props` related pops out. 

If we highlight the `Card1` Component we will see something called `props` to the right. 

<img src="https://i.imgur.com/qzpnB0y.png" /><br>

Since we haven't yet passed any data to these Components there is nothing to show. But once we do start passing data React Dev Tools will display something more like this: 

<img src="" alt="props data"/>

<hr>

:oncoming_police_car: Props are how we pass data from one Component to another and adhere to the following rules:

- Data is unidirectional in React passed down from a `parent` > `child` Component
- Props are immutable which means you can't reassign them within the receiving Component
- All Props passed to a child are organized into a single object in the child Component


### Passing Props

Say for instance we wanted to render the name of the place that the image represents in our cards example. We could go directly to `CardBody` and do the following: 

```html
<h5 class="card-title">Santorini</h5>
```

But this isn't actually passing props but more so just adding the value manually. So let's add a `prop` to CardBody and pass it the value of `Santorini`.

A `prop` is written in a `name=value` format like the other html attributes your used to writing such as: 

```html
<!-- The src property of a image tag -->
<img src="" />
<!-- The class property assigned to any element -->
<div class="blue"></div>
<!-- The href property assigned to an anchor tag -->
<a href="someurl"></a>
```

Since the `Card1` component is the parent that renders  `CardBody` than it must pass the prop to it's child.

:oncoming_police_car: - Data is unidirectional in React passed down from a `parent` > `child` Component

Let's add the following prop.

```js
<CardBody title="Santorini"/>
```

Nothing should really change as we have already updated CardBody with that title name. So we need to update the CardBody Component to accept props.

#### Accepting Props
The first thing we need to do is add the keyword `props` as a parameter. So inside CardBody.js make the following change. 

Let's make sure that our Component is being passed the `title` prop by adding a console.log.

```js
const CardBody = (props) => {
   console.log('this is props:', props)
   // ...rest of the code
}
```

In DevTools you should see the following in the console.

<img src="https://i.imgur.com/HlrtO2T.png" width=300/>

We can see here that `props` is an object and that `title` is a key.  This will be the same pattern when we start passing in multiple props.  Each one will be assigned a key:value pair. 

<hr>

#### :alarm_clock: Activity - 3min

Let's take a moment to edit our previous `Bootstrap Cards CodeSandbox` and try to reassign props.
- Open the `CardBody` Component and add the following:

```js
console.log('current props.title', props.title);
// ATTEMPT TO REASSIGN PROPS A NEW VALUE
props.title = 'Mykonos';
console.log('props.title', props.title);
```

Refresh the page and you should see the following:

<img src="https://i.imgur.com/Nmio71o.png" width=300/>

So it looks like props was not changed and so we have confirmed that once a Component has been passed props that any attempt to change those props directly will have no effect. 

:oncoming_police_car: - Props are immutable which means you can't reassign them within the receiving Component

<hr>


#### Using Props

Now that we have confirmed we are being passed the value let's use it to replace the hard coded value. 

Another JSX rule that we need remember is that any JavaScript code that needs to be executed must be enclosed in opening/closing curls braces `{}`

```js
<h5 className="card-title">{props.title}</h5>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 1min

Confirm in React Dev Tools that CardBody is now being passed a prop

<img src="" alt="image of props being passed"/>

:thumbsup: Click on the thumbs up when your done.

<hr>

### Passing Mulitple Props

We could do the same for all the additional values we wish to pass but as you can imagine if we had 10, 20, 100+ cards this manual method becomes completely inefficient. 

Also we should expect that the data we will be using to render the cards will be imported either via a file or returned from an API call. 

Either way we should expect the if we will need to create multiple cards that the data will be stored as an array of objects:  `[{}, {}]`


<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 3min

Let's use some real data and replace the generic placeholder text.

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

:thumbsup: Click on the thumbs up when your done.

<hr>


#### Creating Multiple Cards

Now that we have the data we can now loop over it and render as many `Card Components` as we need and pass the data down to from parent > child as many levels deep as needed. 

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

One thing to note here is that the object contains a key called `key`.  

It is currently set to `null` however React will warn us later when we render the Cards as it needs to assign a unique key to each Component rendered via a loop. 

Before we render the Cards we first need to update `Card1` to pass the data down to it's children.

```js
const Card1 = (props) => {
  console.log('this is props:', props)
  return (
    <div className="card" style={{width:'18rem'}}>
    <CardImage img={props.img} />
    <CardBody title={props.title} text={props.text} url={props.url} />
  </div>
  )
}
```

**CardBody**

Let's update `CardBody` to make use of the props.

```js
const CardBody = (props) => {
  return (
     <div className="card-body">
      <h5 className="card-title">{props.title}</h5>
      <p className="card-text">{props.text}</p>
      <Button url={props.url}/>
    </div>
  )
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min

Now it's your turn. 

Take a moment to update the following Components to accept and use props:

- CardImage
- Button

Keep in the mind the following: 

- Both Components need to include a parameter which we will always call `props`. 
- Any JS rendered in JSX must be wrapped in {}

:thumbsup: Click on the thumbs up when your done.

<hr>

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

Since the goal of a Component is to be reusable we could now use Card1 as our base template for rendering as many cards as we need. 

Let's rename the `Card1.js` to `Card.js` and update both the import statement and the Component name in the map.  

Below includes the updates.

<img src="https://i.imgur.com/SLtYu9d.png">
<br>
<br>

And there you have it.  Multiple Components rendered with each being passed multiple props.  

### Final React Architecture

As we have made some design changes let's take a look at our final React Architecture design that takes into account all Components used in this app.  

<img src="https://i.imgur.com/WlfxS7X.png" width=600/>

The above was created using [Google Draw](https://docs.google.com/drawings/d/1pG32gpXhkLqtBR2g_SrXWVeX6sza3TAq3zpP0Sjq3QM/edit?usp=sharing)

The architecture represents all the Components and the props that are being passed to each one.  This makes it much easier to understand the flow of data in our app. 

### Bonus - The ...spread Operator and Object Destructuring

Since passing props is a requirement in React there are a few shortcuts we can make when passing them.  

#### Using The ...spread Operator
The first is that we can use the `...spread` operator when passing them down.  In `Card.js` let's replace all those hard coded props with the `...spread` operator. 

```js
 const cards = cardsArr.map((ele, index) => {
    return (
      <Card1 
        {...ele}
        key={index}
     />
    );
  })
```

#### Using Object Destructuring 

The other shorthand we can use is to update the Child component to create variables based on the key:value pairs in the `props` object. 

Let's update `CardBody` to make use of Object Destructuring.  Here we use an object as parameter that includes all the prop key names that are being passed down. 


```js
const CardBody = ({title, text, url}) => {
  return (
     <div className="card-body">
      <h5 className="card-title">{title}</h5>
      <p className="card-text">{text}</p>
      <Button url={url}/>
    </div>
  )
}
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Take a moment to update the `CardImage` Component to make use of Object Destructuring. 

:thumbsup: Click on the thumbs up when your done.

<hr>

[Final Solution]() - (link provided after full codealong)
<!-- [Final Solution](https://codesandbox.io/s/rctrr-8-8-20-bootstrap-solution-uyvmg?file=/src/App.js) -->

### Lab Time

The instructor will provide the lab