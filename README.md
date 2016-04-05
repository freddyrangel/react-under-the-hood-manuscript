# React Under the Hood

## Table of Contents

* Chapter 1: Introduction
  * What is React?
  * Development of React
  * Why Would I Want to Use React?
  * Why is React so popular?
* Chapter 2: Key Concepts
  * How Does React View the World?
    * How To Separate Concerns: Write Components, Not Templates
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

Most JavaScript developers today have heard of React by now. Many are already using it to build their web applications. React has quickly become the preferred JavaScript library for building client-side web applications. Its popularity quickly surpassed frameworks like Angular and Ember, forcing those projects to radically alter their APIs. Angular 2 and Ember 2 are really attempts at bringing in ideas popularized by React.

It's popularity has nothing to do with its newness. Other libraries/frameworks have come out since React was open sourced, as well as new editions of Angular and Ember, yet its popularity remains. This is due to React's much cleaner, simpler, and powerful API. React's architecture philosophy is also much better suited for managing stateful applications since it makes managing state very explicit. It is also easy and fun to learn. Once you learn how to use React, it will become clear that it's a huge leap forward toward a more perfect API for building JavaScript applications in the browser and beyond.

Surprisingly, very few engineers actually understand exactly how it works under the hood. In some ways, this is due to how well React's abstractions are designed. You do not need to understand exactly how it works because it's abstractions are not as leaky. You can build very large web applications without ever having to know how React works. In contrast, working with a framework like Angular requires deep understanding of how its internals work, because its abstractions often fail on non-trivial applications. You need to understand how $apply and $scope work, among a million of other inner workings of that particular framework. With React, understanding it's internals is not a show stopper.

That said, React's internals are very fascinating and worth learning. React's way of thinking is very different to what we're using to in other JavaScript projects. React's successfully arbitraged ideas from other industries such as gaming and early versions of Windows, bringing them to the DOM. Now, those ideas are being reapplied to other platforms with React Native, React Canvas, React-Three, and now React Native for OS X.

This book is meant for beginners. As such, it's very much an introduction to React. But in addition to being somewhat vocational, this book aims to dive much deeper into the ideas behind React. The idea is to avoid cargo-culting and really understand what makes React different and why you would want to use it in the real world.

After finishing this book, you should know the most important parts of React's API, its architectural philosophy, React patterns and antipatterns, and how to work with existing legacy code and third-party libraries such as jQuery plugins. The first half of the book will be mostly explanations, while the second book focuses on building a demo applications. Rather than doing the same old boring Todo app, we will be building a simple Star Trek video game. Games have much more state and interactivity that a Todo app, so it's the perfect way to demonstrate the power and flexibility of React. But most of all, it'll be fun!
