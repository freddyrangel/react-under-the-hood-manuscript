# Chapter 1: Introduction

React is gaining a lot of attention in the JavaScript community. Today, React powers applications such as Netflix and Facebook. Combined, these two companies take up over 30% of all US internet traffic. The level of React's adoption is amazing, especially how recently is has been open sourced. Some consider React the prefered JavaScript library for building dynamic client-side web applications. Its popularity influenced the direction of other JavaScript projects, which are now starting to incorporate some of React's ideas and design decisions.

Its success is partly due to its simple API, which made it easy to get up and running. It is simple, easy to use, and lightning fast. React as a library is also effective in other environments outside of the DOM. Implementations of React now exist in native application development with [React Native](https://facebook.github.io/react-native/), for HTML canvas via [React Canvas](https://github.com/Flipboard/react-canvas), and even in the terminal via [React Blessed](https://github.com/Yomguithereal/react-blessed). You can also render React on the server with [React DOM Server](https://facebook.github.io/react/docs/top-level-api.html#reactdomserver).

Developers with intimate knowledge of React are in very high demand. As of the writing of this book, the average salary for a React developer in San Francisco is [$153,000](http://www.indeed.com/salary?q1=React+Js+Front+End+Engineer&l1=San+Francisco%2C+CA). Many companies are making huge bets on React. Therefore, spending the time to learn React now will pay dividends in the future. By reading this book, you are off to a very good start!

## Why This Book Was Written

Developers using React rarely understand exactly how it works under the hood. In some ways, this is due to how well designed React is when compared to other projects. You do not need to understand how React works in order to get a non-trivial web application up and running. You can build large web applications effectively without ever having to know how React works under the hood. With React, lack of understanding of its internals is not a show stopper.

Still, the internals of React are fascinating and worth learning. React's way of thinking is different from what we are used to in other JavaScript frameworks. React introduced ideas from gaming and early versions of Windows to the DOM, along with some of their own ideas. These concepts changed the way we think about how to build scalable and performant web applications.

## What This Book Is About

This book is an introduction to React, but also dives much deeper into the ideas behind React. There are many excellent introductions to React which are worth looking into, but by and large, they are vocational in nature. There is nothing wrong with that, but what is needed is a resource that puts React in context with other JavaScript frameworks/libraries. Rather than cargo-culting on what is popular, the goal is to show the reader how React works under the hood, as well as go over how to use it. The idea is to explain how React works and how it fits into modern web development, instead of assuming the reader knows why it's great. This book will explain what React does well, as well as point out where the library fails and how to fix it. In addition, we will be going over why React is great for working with existing legacy code and third-party libraries such as jQuery plugins. By the end of this book, the reader should fully understand React's architectural philosophy and design decisions. At the end of this book, the reader will be well on their way to being able to build real world applications with react.

To achieve this, the book will be a mixture of explanations and a practical exercise. Instead of building a typical Todo app, the book will walk the reader through how to build a simple Star Trek video game.

## What This Book Is Not About

While intended for beginners, this book is not an introduction to JavaScript. You do not need to be an expert, but the reader should be somewhat familiar with the language. ES2015 is gaining more adoption and works really well with React but we will not cover that in this book either. We are going to use ECMAScript 5 for the majority of the book, but after reading this book the reader should learn more about ES2015 with React. Also, this book is not about related libraries such as Flux, Relay, or Falcor. Those libraries deserve their own book. Flux in particular is constantly changing so by the time a book is written on the topic, it will most likely already be obsolete.

## Who Should Read This Book

You should read this book if you are interested in learning how to write web applications in React and want a deep understanding of how the library works. This book is intended for absolute beginners to React. That said, this book will go over the internals of React, which is beneficial for those already familiar with React. Anyone interested in building rich web applications in the browser can benefit from this book.
