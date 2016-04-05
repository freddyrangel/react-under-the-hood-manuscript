# React Under the Hood

## Table of Contents

* Chapter 1: Introduction
  * What is React?
  * Developement of React
  * Why Would I Want to Use React?
  * Why is React so popular?
* Chapter 2: Key Concepts
  * How Does React View the World?
    * How To Seperate Concers: Write Components, Not Templates
    * All Data Binding Abstractions Leak
    * How React Manages State
  * React's Design Under the Hood
    * Virtual DOM Diff Algorithm
    * Event Delegation and Autobinding
    * Rendering
* Chapter 3: Relevant Libraries & Concepts
  * Flux
  * GraphQL
  * Relay
* Chapter 4: Star Trek Video Game Tutorial
* Chapter 5: Advanced topics
  * Prop types
  * Patterns and Antipatterns
  * Testing
  * Optimization

Any developer working in the modern web has mostly likely heard of React by now and perhaps are already using it to build web applications. Among front-end developers, React has quickly becoming the preferred JavaScript library for building dynamic client-side web application. It's popularity is quickly surpassing that of rival projects such as Angular and Ember, forcing those projects to adopt some of the concepts React helped introduce to web development. React provides a very simple API making it very easy to get up and running. It's beauty comes from it's simplicy, easy of use, and lightnight fast performance.

That said, very few React developers actually understand exactly how it works under the hood. In some ways, this is due to how well designed React is compared to other projects. Unlike Angular or Ember, you don't really need to understand how React works in order to get a non-trivial web application up and running. You can build large web applications effectively without ever having to know how React works under the hood. In contrast, every Angular developer need to understand how $apply and $scope work, amoung a million of other inner workings of that particular framework. With React, understanding it's internals is not a show stopper.

Still, the internals of React are fascinating and worth learning. React's way of thinking is completely different from what we're used to in other JavaScript frameworks. React essentially has arbitraged successful ideas from the gaming industry and early versions of Windows to the DOM and creating some of their own ideas, completely changing the way we think about how to we should build scalable and performant web applications.

This tutorial/free ebook is meant to be an introduction to React, but it dives much deeper into the ideas behind React. Rather than cargo-culting on what's popular, the aim here is to how just tell you how to use React, but exactly how it works and why you should use it. React's API footprint is actually pretty narrow, so if you're looking for a quick tutorial there are resources probably better suited for you out there. We're also going to go over why React is great for working with existing legacy code and third-party libraries such as jQuery plugins, and how to go about doing so. We're going to learn all this with a mixture of explanations and building a Star Trek video game using React to render all the components. By the end of this book you should fully understand React and it's architectural philosophy, and know how to test and debug a React application, as well as learn React patterns and anti-patterns. You should also know how React works great with third party libraries and frameworks and know how to do so.
