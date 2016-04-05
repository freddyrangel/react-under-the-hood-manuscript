# Chapter 5: Advanced topics

## Relevant Libraries & Concepts

React is perhaps Facebook's most popular open source library, but it is not the only one. They have released quite a few interesting libraries lately. We should point out 4 libraries/concepts they have introduced since they are often mentioned in the same breath as React. This tutorial is mostly about React, but we should briefly talk about these other libraries. 

### Flux

More of an architecture pattern than a library, Flux provides a more robust solution to organizing your data and business logic. As a React application grows, it can be useful to separate your core business logic from your UI components. Without MVC, Facebook needed another paradigm that adheres to React's unidirectional data flow. Flux works in tandem with React's unidirectional data flow.

Flux has 4 major parts: actions, dispatchers, stores, and views (React components). Actions are dispatcher helper methods used to create a more semantic API. When a user interacts with the view, an action is propagated to a central dispatcher that knows which stores it needs to call. Stores hold the application's data and business logic, which when called will update views that are dependent to a store's state. This helps clean out data and business logic from React components.

This is a step in the right direction but the overhead complexity of Flux is not worth the effort until you start having problems reasoning about your data and business logic. Only once you start reaching a certain level of complexity in a React application that you should consider taking a look at Flux.

### GraphQL

REST is not dead, but for some kinds of applications REST is not expressive enough to serve many application's data requirements without a lot of API calls to the server. For an application as large as Facebook, making individual API calls to RESTful endpoints is just not efficient.

A GraphQL query is a string interpreted by a server that returns data in a specified format. Here is an example query:

```
{
  user(id: 3500401) {
    id,
    name,
    isViewerFriend,
    profilePicture(size: 50)  {
      uri,
      width,
      height
    }
  }
}
```

This is much more expressive than regular REST. REST is much more imperative compared to GraphQL. When designing an API for native or web based clients, the API designer often needs to know a lot about the requirements of the client in order to prevent multiple calls to the server. REST is just too rigid for large client-side or native applications. With GraphQL, you can just make one call to the server asking for your data requirements. 

That said, REST is not dead. REST has been a great step forward for the web, but it is not the end of history. It is very imperative compared to GraphQL. Still, REST is tried and true but in no way should it be the final word for how to build scalable APIs.

We as programmers should be trying to prevent problems, but making premature optimizations will lead us into trouble. Just like with Flux, it is better to stick with REST unless it really does not make sense for your applications.

### Relay

While GraphQL can help limit the amount of calls to the server, various components have differing data requirements, which can result in multiple calls to the server. Relay, among other things, helps batch together all data requirements into one request. Relay is built on top of GraphQL.

Again, just like Flux and GraphQL, you don't need to worry about using Relay unless data fetching becomes a problem.

### Immutable.js

React's core philosophy is avoiding state, data that changes over time. Immutable data is a powerful concept that helps avoid some of the problems of data changing over time. When you have a collection that you know can never change, it is much easier to reason about that data. You no longer have to do expensive comparisons or observe for changes since you are absolutely guaranteed that a collection will never change.

Immutable.js provides a powerful way to create immutable collections in JavaScript. It aligns very well with the philosophy of React and Flux.

## Performance Optimization

On the surface, re-rendering an entire tree of components seems like a detriment to performance. As we demonstrated in a prior chapter, React's diff algorithm is very sophisticated and fast. This is all done in JavaScript, which is very fast. For the vast majority of cases, manipulating the DOM is going to be your biggest performance bottleneck by far and not JavaScript.

That said, there are ways to improve performance even further. React allows you to tell the Virtual DOM to skip calling `render()` on a particular component and its children via the lifecycle method `shouldComponentUpdate()`. This method is called before the re-rendering starts. By default, this method returns `true` but you can use it to check certain conditions and determine whether or not to return `false`. Keep in mind that this method gets called very frequently, so the code here needs to be pretty fast.

At first glance, the most obvious place to attempt performance optimization is in the `Stars` component. After all, star system data does not change at all between re-renders. No matter what happens to `state`, star system data does not change at all. However there is a problem with this line of thinking: we do not actually know if that is true. We do not have any data to back up our assumption. How do we know that is actually impacting performance?

The good news is: React provides handy add-on performance tools. It is only available in development and should not be included in a production environment, but it is very useful to find easy performance improvements. It is already included for you in `package.json` but normally you would install it via `npm i react-addons-perf -D`.

Let's make this available for us in the browser's dev tools. Let's temporarily add the performance tools to the browser global object so that we can access it for performance testing purposes. Open `unfinished/app/index.jsx` and add the following:

```javascript
// unfinished/app/index.jsx

require('./main.css');
window.Perf = require('react-addons-perf')

var React    = require('react');
var ReactDOM = require('react-dom');
var Game     = require('./components/Game.jsx');

var appNode = document.createElement('div');
appNode.className = 'react-game';
document.body.appendChild(appNode);
ReactDOM.render(<Game />, appNode);
```

Now we can go to the browser and use `Perf` in the dev tools. `Perf` is fairly simple to use. We want to start and stop the measurement using `Perf.start()` and `Perf.stop()`, and then use a measurement utility. React provides 4 measurement utilities: `Perf.printInclusive()`, `Perf.printExclusive()`, `Perf.printWasted()`, and `Perf.printDOM()`. `Perf.printWasted()` is by far the most useful utility since it tells us the amount of time spent on components that did not actually render anything. We can take the worst offenders and apply `shouldComponentUpdate()` to those components.

Open up the browser to `localhost:4000` and open the dev tools. Start the measurement with `Perf.start()`. Then, set a course and speed to a star system. Remember the course and speed so we can accurately compare the performance improvements. Then engage the engines and wait until the starship reaches its destination. Then in the dev console type `Perf.stop()` to stop the measurement. Now type `Perf.printWasted()`. You should see the following:

![First Performance Check](images/10_performance_3.png)

We have a problem with the measurement. The "Owner > component" column is not giving us a descriptive name for our components. That is because React does not know what we called our components once it has reached the browser. We need to tell React what the names of our components are.

To do that, we need to add `displayName` to our components so we can get better logging information. Let's start with `Game.jsx`:

```javascript
// unfinished/app/components/Game.jsx

module.exports = React.createClass({

  ...

  displayName: "Game",

  getInitialState: function() {
  
  ...
  
});
```

It is a good idea to set the value of `displayName` to the name of your component, making it easier to identify in the dev tools console. You will need to go into every component and add a unique display name before you can do further performance testing.

Once you have added `displayName` to all the components, refresh the browser and run through all the stops to measure performance. Once you have done so, you should see the following:

![Second Performance Check](images/08_performance_1.png)

Surprisingly, it is not the `Stars` component that is the biggest detriment to performance, despite the size of star system data. The component with the most wasted time is `ShipInfo`. Now we can optimize it with `shouldComponentUpdate()`. Let's do that now:

```javascript

...

module.exports = React.createClass({

  displayName: "ShipInfo",

  shouldComponentUpdate: function(nextProps, nextState) {
    return this.props.info !== nextProps.info;
  },
  
  ...
  
});
```

`shouldComponentUpdate()` receives `nextProps` and `nextState` which allows you to compare that with the component's current `props` and `state` with the next `props` and `state`. Since `ShipInfo` is stateless, we do not need to check for a change in `state`. What we will do is check if `props` has changed at all. If it has not changed, we want to return `false`, telling React to skip re-rendering this component and all of its children.

There is one problem here however. `updateInfo()` updates the reference to the ship directly even before `setState()` gets called. What this means is, under `shouldComponentUpdate()`, `this.props` and `nextProps` will always equal eachother, because we inadvertantly updated `this.props.info`. This means `shouldComponentUpdate()` will always return false, so `ShipInfo` will never be re-rendered even when ship info has changed.

There are a few ways we can fix this problem. We can clone the object we need using a utility library such as [lodash](https://lodash.com/) and [clone](https://lodash.com/docs#clone) the `info` object, then pass the cloned `info` object to update the ship state. We can similarly use the ES2015 feature [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) to copy `this.props.info` into a new object, and then pass that new object to update the ship state. Or, we can use immutable data structures with [Immutable.js](https://facebook.github.io/immutable-js/) throughout the game, ensuring we can never update an existing data structure.

For simplicity's sake, we will go with `Object.assign`. Let's update `updateInfo` in `#unfinished/app/components/ShipInfo.jsx`:

```javascript
// unfinished/app/components/ShipInfo.jsx

var React            = require('react');
var EditableElement  = require('./EditableElement.jsx');
var PureRenderMixin = require('react-addons-pure-render-mixin');

module.exports = React.createClass({

  ...

  updateInfo: function(key, newValue) {
    var info = Object.assign({}, this.props.info);
    info[key] = newValue;
    this.props.updateShipInfo(info);
  },
  
  ...

});
```

Now when we run the same performance text, we should see this:

![Final Performance Check](images/09_performance_2.png)

This pattern is so common, there is a React addon called [PureRenderMixin](https://facebook.github.io/react/docs/pure-render-mixin.html) which does everything we just did under `shouldComponentUpdate()`. We can use it to remove our `shouldComponentUpdate()` method and use `PureRenderMixin`

```javascript
// unfinished/app/components/ShipInfo.jsx

...

var PureRenderMixin = require('react-addons-pure-render-mixin');

module.exports = React.createClass({

  // Remove shouldComponentUpdate() and put this mixin
  mixins: [PureRenderMixin],
  
  ...
  
});
```

As a final note, don't forget to remove `Perf` from `index.jsx` when you are finished with performance optimization.

## More About Props

React components are easily reusable because in many ways they act like UI functions. However, just like functions, you can run across type errors or forget to pass in a particular argument. React has a few built in solutions for these problems, which you should use as much as possible.

React provides a way to validate the type of `props` that are passed into a component called `propTypes`. It is a method of adding type checking to your React component. This helps to ensure that you are passing in the correct type to your components `props`.

We can see how this looks like in action with `EditableElement` since this is intended to be highly reusable.

```javascript
// unfinished/app/components/EditableElement.jsx

var React = require('react');

module.exports = React.createClass({

  displayName: "EditableElement",

  propTypes: {
    value: React.PropTypes.string.isRequired,
    onEdit: React.PropTypes.func.isRequired
  },
  
  ...
  
});
```

`React.PropTypes` gives you a wide range of validations for your components, including ways to create your own. It supports JavaScript primitives via `React.PropTypes.[array, func, bool, number, object, string]` as well as others available in the [documentation](https://facebook.github.io/react/docs/reusable-components.html). These `PropTypes` are optional by default, so you have to call `isRequired` to make it required. When an invalid value is passed in as a `prop`, React will log a warning to the dev tool console in the browser. However, this is only available in development for performance reasons. 

Taking a look at the console, we get the following error: "Warning: Failed propType: Invalid prop `value` of type `number` supplied to `EditableElement`, expected `string`. Check the render method of `WarpDriveControls`". That is because we are passing in a number to `EditableElement` inside of `WarpDriveControls`. One way to fix this is to allow `value` in `EditableElement` to take a `number` type with `React.PropTypes.oneOfType()`:

```javascript
var React = require('react');

module.exports = React.createClass({

  displayName: "EditableElement",

  propTypes: {
    value: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
    ]).isRequired,
    onEdit: React.PropTypes.func.isRequired
  },
  
  ...

});
```

Now `value` will take a `string` or a `number`, and `onEdit` will always be a required function.

One other feature of functions in many languages is the ability to set default values to an argument. React gives us a way to do this via `getDefaultProps()`:

```javascript
var React = require('react');

module.exports = React.createClass({

  displayName: "EditableElement",

  propTypes: {
    value: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
    ]).isRequired,
    onEdit: React.PropTypes.func.isRequired
  },

  getDefaultProps: function() {
    return {
      value: 'Enter New Value'
    }
  },
});
```

`getDefaultProps()` functions very similarly to `getDefaultState()` in that the function needs to return an object with the values you would like to set for `props`. This is useful in the cases where a `prop` value is not passed in or is not needed to be passed in for every case. 

## Inline Styles

In normal HTML, inline styles are specified as a string. That will not work for React. Rather we need to pass an object to a `style` property with keys that are camelcase style names in order to be consistent with the DOM JavaScript API (similar to why `className` is camelcase). React will automatically add "px" to pixel values, allowing you to pass `number` type for certain style properties. Here is an example:

```javascript
var divStyle = {
  height: 10, // rendered as "height:10px"
  color: 'blue'
}; 
ReactDOM.render(<div style={divStyle}>Hello World!</div>, someNode);
```

Now we have the option of modularizing our styling within our components instead of using a global CSS style sheet. This is handy to help scope CSS and style our components in a more declarative way. However, making quick changes across the application can be much more difficult now. So far, the community has not adopted this approach, perhaps because we have nearly two decades of experience dealing with the pain of CSS. There are a few projects aiming to make this approach even easier with React, such as [React Style](https://github.com/js-next/react-style). This project is somewhat consistent with how React Native deals with styling in native applications that do not use CSS. At this point we are probably used to the way we have been doing thing as far as styling goes. Still, this is an approach that is worth exploring in the future.
