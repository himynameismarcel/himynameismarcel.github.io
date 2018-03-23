---
layout: post
title:  "Visualizations Using D3.js"
date:   2018-03-16 20:37:05 +0100
categories: programming
---

- D3 stands for data-driven documents
- is a javascript libraray targeted towards making stunning visualizations
- official webpage: https://d3js.org/
- examples: https://github.com/d3/d3/wiki/Gallery (including the underlying code that actually generated those visualizations)
- in order to work with javascript, one should be lightly familiar with html, css (d3.js uses css-selectors for maniuplating the web-document); javascript-syntax itself is probably not terribly necessary to be able to work with d3.js
- also one should be familiar with the concept of the DOM (the document object model) which more or less stands for the hierarchical structure of a webpage
- on the official webpage of d3.js if you click on API-reference (https://github.com/d3/d3/blob/master/API.md), you'll get a long list of every method and object that is used in d3 (including a short explanation of each concept)
- if we want to include d3 javascript into our webpage, we have to fetch the library in the first place; this is done by including a script-tag in the header of our weg-page
- then, whenever we write js-code on our page, (in the body), we have to include it between script-tags
- important concept: svg: scalable vector graphics: you could call it a way to create 2-dimensional graphics on a webpage
- D3 allows us to create svg-shapes!
- svg is an image-format for displaying graphical elements on a webpage
