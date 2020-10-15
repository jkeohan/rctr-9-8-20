# React Router

<img src="https://i.imgur.com/UcmwbaK.png" width=300/>

## Learning Objectives

### React Bitcoin Currency

Here is what we are looking to build:  [Bitcoin Solution Code](https://9esbr.csb.app/)

Here is our [Starter Code](https://codesandbox.io/s/rctr-router-p2-bitcoin-starter-8e2vp?file=/src/components/App/App.js)

## Currencies component 

If we look at this component we see a long list of links. Note that the links are using regular `<a>` tags.

What happens if we click on a link? It works, but the whole page reloads which is a poor choice of UI. 

Lets go ahead and replace the `a` tag with a `<Link>` component. Make the `to` prop value equal to the `href` value.

```jsx
// src/Components/Currencies/Currencies.js
import { Link } from 'react-router-dom'

//...

  render() {
    let list = listOfCurrencies.map(item => {
      return (
        <div className="currency" key={item.currency}>
          <p><Link to={"/currencies/"+ item.currency}>{item.currency}</Link>: {item.country}</p>
        </div>
      )
    })
  }

```

Great! Now go back to the page and click the link again, what happens?

It changes the route for us (notice the URL changing) but we don't have any
routes set up to match that url so it `Redirects` us back to the home page. 


### Currency Component 

If we take a moment to examine the `Currency` Component we will see that there is the following variable with the url to the `conidesk` api.

```js
const coindeskURL = "https://api.coindesk.com/v1/bpi/currentprice/";
```

If we copy/paste the url into the browser and append a bitcoin currency we should see that it returns the data. 

```js
https://api.coindesk.com/v1/bpi/currentprice/AFN
```

<img src="https://i.imgur.com/ADE1k6U.png" width=400/>

This is the data we will use to render the info dynamically for the currency each time the user clicks to see a currency. 

### Currency Route

In order to active this route we need  add another `<Route>` component in `App`. 

This time though we want to include a `parameter`.

Look at the URL that we're on after clicking on a currency and we should see the following:

```js
https://vthmi.csb.app/currencies/AFN
```

It seems as though the info we need to make the API call is already in the route. We can use that as part of our routing logic. 

Let's create a new route that includes a `url parameter`. This is done by appending a `:paramName` after the path.

```html
 <Route path="/currency/:currency" component={Currency}/>
```

Clicking on a currency should take us to the following:

<img src="https://i.imgur.com/orCqpXN.png" width=500/>

And if we examine the `Currency` Component in React DevTools we should see the following: 

<img src="https://i.imgur.com/dKFS5G8.png" width=500/>

So it looks like `props.match.params.currency` contains the value that we need to make the API call. 

## Adding useState and useEffect to Currency

Knowing that we need to make the API call and then update state with the data means we need both `useState` and `useEffect` so let's import them. 

```js
import React, {useState, useEffect} from "react";
```

Of course let's setup our state. 

```js
const [currency, setCurrency] = useState(null);
```


Since the Currency component will be responsible for making the API call to coindesk to retrieve the current price of the currency we will need to make the call within a  `useEffect` and have it run  when the component is first mounted.  

```js
  useEffect(() => {
    const currency = props.match.params.currency;
    const url = `${coindeskURL}${currency}.json`
    const makeApiCall = async () => {
      const res  =  await fetch(url)
      const json = await res.json()
      let currencyPrice = json.bpi[currency].rate;
      setPrice(currencyPrice)
    }
    makeApiCall()
  },[])
```

## New Feature Request

The client has just asked that we now include a new feature.  They would like to display the currency name in the header.  The header will look like this when no currency is selected: 

<img src="https://i.imgur.com/guMrAJb.png" width=500/>

And then update to include the currency name when a currency is active.

<img src="https://i.imgur.com/ukBuPSI.png" width=500/>

This means that we need to pass, or better yet lift the currency name from `Currency` to `App`.  In order to to this we need to pass down the `setCurrency` function defined in state. 

```js
 const [currency, setCurrency] = useState('');
```

Here is the thing though.  The way our route is configured we can't pass down props. 

```html
 <Route path="/currencies/:currency" component={Currency}/>
```

This requires that we use the `render` method in the route. 

```html
<Route path="/currencies/:currency" render={() => <Currency setCurrency={setCurrency}/>} />
```

Let's see if that works.  

Hmmmm...it looks like we broke it. 

<img src="https://i.imgur.com/A2TZ8Lb.png" width=400/>

Let's comment out that link in `Currency` and then take a look at the `Currency` Component in DevTool. 

```js
  {/* <h1>Bitcoin price in {props.match.params.currency}</h1> */}
```

It seems as though we have lost all of the previous router props that we had access to just moments before. 

<img src="https://i.imgur.com/XielcdH.png" width=500/>

We need to get them back and can do so by manually passing them down. 

We could spread the routerProps object, we'll get something like this:

```js
<Currency
  history={ /* stuff in here */ }
  location={ /* stuff in here */ }
  match={ /* stuff in here */ }
>
```

Or a much better way would be to pass them all down using the `...spread` operator. 

> The `...` (spread operator) is allowing us to "destructure" the props object
> being passed by `Router` and apply each of its key/value pairs as props on the
> `Currency` component.


```html
<Route path="/currencies/:currency" render={(routerProps) => 
  <Currency 
    setCurrency={setCurrency}
    {...routerProps}
  />} 
/>
```

Confirm in DevTools that those props are back and uncomment out the code. 

### Update Navigation

Add the following in `App`

```js
<Link to="/currencies">{
      currency ? `Currencies List > ${currency}` : 
      `Currencies List > `
  }</Link>
```

We still have some weird issue where both the `currencies` and `currencies/:currency` routes display today. Let's work on those now.

## Using Switch 

Switch works just like the switch/case statements in javascript. We're comparing
string values (in this case, routes) and executing conditions (rendering
components) based on what matches turn out true.

Since we're not using switch right now the two components are stacked on top of each other! The Home and the
Currencies component. That's silly.

> Why does this happen?

There are two ways to handle this: using the Switch component, or specifying
`exact` on routes.

Let's look at our routes in `App.js` again:

```jsx
<Route path="/"
  component={Home}
/>
<Route
  path="/currencies/:currency"
  render={(routerProps) => <Currency setCurrency={setCurrency} {...routerProps}/> }
/>
<Route path="/currencies"
  component={Currencies}
/>

Try putting `exact` on the `/` path route component.

```js
<Route path="/" exact component={Home} />
```

> Note: this is equivalent to putting `exact=true`

Beautiful! this is a great solution, unless we have many different routes.

If we had a list of routes like:

- `/currencies`
- `/currencies/new`
- `/currencies/:id` etc

we would have to put `exact` on `/currencies` or else, any time we went to
`/currencies/something` it would match both the root (`/currencies`) AND the
`/currencies/something` routes and both would be rendered.

We can avoid all this by just using `<Switch />`.

Back in `App.js`, let's import the `<Switch />` component and then wrap all of
our routes in it.

```jsx
import { Route, Link, Switch } from 'react-router-dom'

  return(
    <div>
      <nav>
        <Link to="/">
          <img src="https://en.bitcoin.it/w/images/en/2/29/BC_Logo_.png" alt=""/>
          <h1>Bitcoin prices</h1>
        </Link>
        <Link to="/currencies">Currency List</Link>
      </nav>
      <main>
        <Switch>
          <Route path="/"
            exact
            component={Home}
          />
          <Route
            path="/currencies/:currency"
            render={(routerProps) => <Currency setCurrency={setCurrency} {...routerProps} /> }
          />
          <Route path="/currencies"
            component={Currencies}
          />
     
        </Switch>
      </main>
    </div>
  )
```

### You Do: The Coindesk API 

We will be using `fetch` to query the Coindesk API in this exercise. Take 5 minutes to read the [Coindesk API](https://www.coindesk.com/api/) documentation and test viewing the current currency rate for a `AED` and using just the browswer.  Do not try and make a fetch call yet. 




## Redirects

Redirects using react router are incredibly easy. Redirect is just another
component we can import and use by passing it a few props.


- Add another route called `/currency`
- Instead of rendering one of our components, put the `Redirect` component.

```js
<Route path="/currency" render={() => <Redirect to="/currencies" />} />
```

Redirect only requires a `to` prop which tells it what path to redirect to.

## Bonus - Working With `History` 

We can make use of the the `history.push` method to push routes into the browsers url.

Let's create a `handleClick` button that when called will navigate the user back to the `currencies` route.

```js
  const handleClick = () => {
    props.history.push('/currencies')
   }
```

Let's add a button and assign it the `handleCLick` function. 

```js
 <button onClick={handleClick}> Home</button>
```
