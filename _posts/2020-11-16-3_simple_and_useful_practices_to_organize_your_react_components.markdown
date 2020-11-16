---
layout: post
title:      "3 Simple and Useful Practices to Organize Your React Components"
date:       2020-11-16 15:01:41 -0500
permalink:  3_simple_and_useful_practices_to_organize_your_react_components
---


## 1) Keep your components small if possible
If you find that your class components are getting lengthy and you're possibly even re-using the same info in the same component, it's time to extract that info. Turn it into a functional component that your initial class component can use by simply having your class component render it as a child component. This results in an app that is cleaner and much easier to read.

## 2) Speaking of functional components, make sure to use them!
It's easy to get in the habit of making a component a class component just in case it ends up doing more than just displaying data. However, if you're reviewing your app and find that many of your class components aren't doing anything with that data other than displaying it, then you should convert it into a functional component. Doing this will result in a stateless component that has less code and, again, improves readability!

## 3) Use fragments instead of divs
React components require that you return an element. In many cases, you'll use a div tag to bypass this requirement. However, this can lead to unnecessary markup that is also poorly structured. To remedy this, you can use React fragments. Fragments allow you to fulfill React's requirement of returning an element while avoiding the addition of unnecessary nodes in the DOM.

I hope these three easy practices will help clean up your components so that they're more readable and easier to understand!
