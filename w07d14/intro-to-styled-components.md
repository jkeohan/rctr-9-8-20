[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# React Styling

## Learning Objectives

- Compare and contrast the four ways that styling is done in React
- Use objects to add dynamic inline styles
- Identify the ES6 tagged template literal syntax
- Use styled components and polished to create a simple component

## Framing

As with all things `coding` there are many ways to accomplish the same thing. Take for instance the need to run a simple conditional logic statement. It could be performed using the following approaches:

- if/else
- switch statement
- ternary operators

What about the need to iterator and filter an array of data. The following approaches could be taken:

- for loop
- Array.forEach()
- Array.filter()
- Array.reduce()

Styling is no different and, although we are free to take the most basic approach such a single CSS file for the entire app there are several more options to consider as per organization and third party tools in the React ecosystem.

<hr>

:question: How would you define a Compponent and it's place in React and the React Ecosystem? 

<hr>

## Components As Self-Contained

The first concept we need to keep in mind is that `Components` are meant to be **self-contained** and **reusable**.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Components, React or otherwise,  are now becoming the standard for sharing small pieces of functionality.  

Let's take a look at [https://bit.dev/](https://bit.dev/) which is an environment developers can share their own custom and reusable [React Components](https://bit.dev/components?q=react). 

<hr>

Controlling behaviors internally is what the promise of components offers. When our CSS _behaviors_ are an integrated as part of our code, we can use `props` and `state` to thoroughly control the view, including styling, versus swapping out classes.

Fortunately, lots of techniques, frameworks, tooling and other open source projects have been built an popularized to fill the gaps. Four popular ways that you'll likely encounter are:

- CSS Stylesheets
- Inline Styles
- CSS-in-JS (CSS Modules & Styled Components)

## Starter Code

Here is the [Starter Code](https://codesandbox.io/s/styles-4-ways-starter-13qy5?file=/src/App.js) we will be using for this lecture. 

## CSS Stylesheet

The first and most basic approach is importing CSS files directly into our components.

```js
import './styles.css';
```

We can import a single `css` file at the highest level in the app or create separate `css` files that target a specific Component. A great way to organize your app would be to place `Components` into separate folders along with the `css` file.

<img src="https://i.imgur.com/8WUzfcr.png" />

#### Benefits

- Anyone working in front end design knows how to use them
- Smaller subset of css files
- Full access to all CSS specifications (animations, pseudo-classes, pseudo-elements, etc.)

#### Drawbacks

- CSS may be overridden by more specific rules

## Inline Styling

The term `separation of concerns` is a design principle in CS that refers to separating programs into distinct sections to make it modular. Under `SoC`, it's logical that since our CSS, HTML and JS all do different jobs, they should be separate and independent of one another, and for many years the web dev community preached this approach (vociferously :smiley:).

As a result, [inline styles were considered bad practice](https://stackoverflow.com/questions/2612483/whats-so-bad-about-in-line-css).

Inline styles, particularly in the context of components, does make a lot of sense though and is inline with the idea that `what goes together should stay together`.

### Style Object

When using `inline-styles` we might opt to assign the style directly in the JSX which works best for a single style.

```html
<div style={{color: primary}}></div>
```

Or create a `styles` object that includes several styles and then assign the object.

```js
export default function InlineStyle() {
  const buttonStyles = {
    backgroundColor: primary,
    color: '#fff',
    padding: '7px 14px',
    margin: '0 5px',
    borderRadius: '5px',
    border: '1px solid transparent',
  };

  return (
  <div style={{ color: 'red' }}>
    <h2>Inline Styles</h2>
    <button>Primary</button>
  </div>
  );
}
```
#### Conditional Logic
We can also used conditional logic to determine which values should be assigned to specific css rules.  

```js
const buttonStyles = {
  backgroundColor: props.primary ?  primary : danger ,
  // ...rest of styles
};
```

This works well enough for the most basic logic of a single button.  But when multiple buttons are introduced that require different background colors and `hover` effects then the code can get messy very quickly. 

#### Benefits

- No special tools and takes advantage of existing toolchain
- Access to `props` and `state`
- Component level styles stay with the component
- Locally scoped with access to external values

#### Drawbacks

- Limited support of CSS specification (no animations, pseudo-classes, pseudo-elements, etc.)
- Hard to read and difficult to override
- Hard to document and maintain

## CSS in JS

CSS in JS lets you you style your presentation with JavaScript instead of CSS. Then, when your application is run, the JavaScript is parsed and generates CSS, which is attached to your DOM directly.

### CSS Modules

One major issues of standard CSS or Sass is that there is no concept of true encapsulation and requires that the developer to choose unique class names. 

And this is exactly what CSS modules did, it relied on creating a dynamic class names for each locally defined style and making sure there styles didn't conflict. 

It's creators very specifically designed it to be lightweight and not try to be everything to everyone. It really only supports a handful of features.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at a site like [Buffer](https://buffer.com/) which  uses CSS Modules.  

We will focus our attention specifically on the `header` element of their home page. 

<hr>

The basic premise is that the css classes are converted using a preprocessor into unique names in order to create `local scoping`. 

While additional tooling is needed to handle the processing of the files, `create-react-app`, which `CodeSandox` uses, includes this tooling by default.

The actual css file must include `.module` in it's name.  So if you are using standard css then the name might be `styles.module.css` but your using SCSS then it would be `sytles.module.scss`.  The rule written will then be dependent on which one you are using. 

<img src="https://i.imgur.com/FWdD5YU.png" />


#### Importing styles

The file is then imported, but this time we store the import in a variable as it returns an object.  

Let's also add a console log and see what that import looks like.
```js
import styles from './styles.module.css';
console.log('styles', styles);
```

From the console log it's clear that the css rules are assigned as keys and the values are `module` specific.

<img src="https://i.imgur.com/q2tirlw.png" />

The rules are then applied to the elements using dot notation.

```html
<div className={styles.container}>
  <h2>Modules</h2>
  <button className={styles.primary}>Primary</button>
  <button className={styles.secondary}>Secondary</button>
  <button className={styles.success}>Success</button>
</div>
```

If we take a look at the `button` element in the `Elements` Tab in in DevTool we will see the following:

<img src="https://i.imgur.com/kDWUghQ.png" />

Since this isn't a standard CSS name there is no way these styles would conflict with another elemnent in the global scope that has been assinged a class of `.button` as well. 

#### Benefits

- Component level styles stay with the component
- Import/Export styles between files
- Access to full CSS specification including support of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) for variable support

#### Drawbacks

- Limited access to `props` and `state`
- No Sass like features except `composes`


## Styled Components 

One of the most popular and advanced CSS-in-JS libraries is [Styled Components](https://www.styled-components.com/).

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Now that were jumping into styled components let's take a look at a [Vimeo](https://vimeo.com/) and see styled components in action

<hr>




Since `styled components` in an npm package, and therefor a dependency, it must first be installed.

<img src="https://i.imgur.com/zCX1cFF.png" />

Then we must import the library. 

```js
import styled from 'styled-components';
```

Styled Components do a great job of taking advantage of a feature an ES6 feature called a `Tagged Template Literal`.


Let's create two styled components for the `container` and the `buttons`. 

```js
const Container = styled.div`

`;

const Button = styled.button`

`;
```

And now we add some styles.  

First to the `Container`.  We can add a color by name or reference a variable. 

```js
const Container = styled.div`
  color: red;
  // or
  color: ${warning}
`
```
Now the `Button`.  Since we are also adding a `hover` effect , which is a `pseudoclass` we must include `&:hover`.

```js
const Button = styled.button`
  background-color: ${primary}
  color: #fff;
  padding: 7px 14px;
  margin:0 5px;
  border-radius: 10px;
  border: 1px solid transparent;

  &:hover {
    background-color: red;
  }
`
```

If we take a look at those elements in the `Elements` Tab in in DevTool we will see that the class names begin with `sc-` and then end with a mix of difference characters.  

<img src="https://i.imgur.com/BDJ3rOR.png" />

### Conditional Logic
Just as we did with inline styles we can use conditional logic to determine which css values be assigned to a component.  Conditional logic can be added in a vew ways:

- a sinlge ternary operator
- a callback function based on a style component specific prop

#### Ternary Operator
Being that were using `back ticks` when creating the component we must include `${}` when running the evaluation. 

Let's try and set the color based on passing in a `primary` prop. This requires that the parent element pass down the prop as well.

```js
const Button = styled.button`
  background-color: ${props.primary ?  primary : secondary };
  // ...rest of css
`
```

Here is what the rendered Components look like in React DevTools

<img src="https://i.imgur.com/ZuqZizF.png" width=700/>

### Passing Styled Components Props

Once the `styled component` is rendered we can pass it props of it's own just as we would do with any Component. 

It doesn't actually need a value assigned and will set that property to `true` being that it just exists. 

```js
<ButtonTwo primary>Customized</ButtonTwo>
```

Now within the `styled component` we can pass that value via an anonymous function and run additional JS conditional logic. 

```js
border-radius: ${props => {
    console.log('props', props)
    if (props.primary) return '20px'
    return '0'
}};
```

Here is what the console log looks like

<img src="https://i.imgur.com/JvgqV1F.png" />

We can also pass the prop a value as well. 

```js
<ButtonTwo primary={'blue'}>Customized</ButtonTwo>
```

```js
border-radius: ${props => {
    console.log('props', props)
    if (props.primary == 'blue') return '20px'
    return '0'
}};
```

#### Helpers

Styled components come with several [Helper function](https://styled-components.com/docs/api#helpers) such as:

- css
- keyframes
- many more

Let's take a look at `css` and use it to create and share css between multiple components. 


The functions need to be imported.  

```js
import styled, {css} from 'styled-components';
```

Then we create our shared styles.

```js
const sharedStyles = css`
  color: ${props => (props.standard ? white : warning)};
`
```

And include this in the styled components that need it. 

```js
const Button = styled.button`
  ${props =>  sharedStyles}
  //...rest of css
`
```

#### Benefits
- Full access to `props` and `state`
- Component level styles stay with the component
- Access to full CSS specification including support of [CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) for variable support
- Sass-like features (such as nesting) and much more if you add [Polished](https://polished.js.org/)

#### Drawbacks

- dependency required
- learning curve

### Solution Code

Here is the [Solution Code](https://codesandbox.io/s/styles-4-ways-starter-10-22-20-gpf9t?file=/src/StyledComponents/index.js)

### Bonus -  Sass/SCSS

Both Sass (Syntactically Awesome Style Sheets) and SCSS (Sassy CSS) are extensions to CSS and provide a robust set of functionality. 

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

Let's take a look at the [Sass](https://sass-lang.com/guide) documentation

<hr>

## Additional Resources

- [CSS Modules](https://github.com/css-modules/css-modules#composition).
- [Styled Components](https://styled-components.com/docs/faqs)
- [Building a reusable Component System with React.js and styled-components](https://levelup.gitconnected.com/building-a-reusable-component-system-with-react-js-and-styled-components-4e9f1018a31c)
- [React Styling Options](https://www.sitepoint.com/react-components-styling-options/)
