---
layout: post
title:  "APIs and Webservices: Background and an Example"
date:   2018-03-13 13:37:05 +0100
categories: programming
---

About a year ago I familiarized myself with **web-services** and **API's** (*Application Program(ming) Interface*) more generally to get a better understanding of the technological background. My conclusion back then was that the terms are used in various contexts and depending on the exact context, everyone seemed to have a vague idea about what they actually mean and stand for.

# Many explanations, all somewhat related
In an introductory class about web development from [Colt Steele](https://www.linkedin.com/in/coltsteele/) which I had attended last year, he introduces APIs at some point in the course right after having moved from front-end technologies to back-end web development as follows: **API's are interfaces for code/computers to talk to one another.** He goes on to clarify that the term 'API' is actually a **broader term that refers to any type of code/interface that is made for other code to be used with/to communicated with**. Referring to the corresponding [Wikipedia-article](https://en.wikipedia.org/wiki/Application_programming_interface), the definition of an API undermines the very broad/vague definition that Colt used to introduce APIs by stating that **[a]n application programming interface (API) is a set of routines, protocols, and tools for building software and applications.** Hence, the term API comprises anything ranging from libraries, packages, modules, databases, web-APIs, etc.<br>
Building on all of the above, a fairly neat explanation is given by [Martin Gibbs](https://study.com/academy/lesson/application-programming-interface-api-definition-example.html) where he states that **APIs are a set of tools that programmers can use in helping them create software** and thereby **allow a programmer to deliver solid solutions fairly rapidly without having to rebuild everything from scratch every time.**  

But what people nowadays typically mean they refer to an API is a **web (application) API**, which are, strictly speaking, only a subset of the much broader definition of APIs from above. It is only that web-APIs have become so prevalent and common, that when people refer to an API they usually actually are referring to a **web API**, meaning any sort of generic interface to an application via the web.

Today a classical example where web APIs are exploited extensively are all kinds of travel search engines like Trivago, Expedia, Checkfelix, etc., that aggregate information from a number of other services via the corresponding web APIs and thereby make the respective data of the services whose web APIs they are consuming available on their platforms for customers to e.g., compare prices.

The above example already makes clear, that the way that applications get data from web APIs or access its interface is through the internet (or more precisely, via HTTP). Today almost all major (internet)-companies like Twitter, Facebook, Google, eBay, Amazon, etc. actively maintain various web-APIs that are all designed for specific purposes and audiences and have become part of these companies' standard product range/deliverables.

As an example and to distinguish a web API from a *normal* human-readable website, Colt refers to [reddit.com/r/aww](https://www.reddit.com/r/aww) which represents a subreddit for cute photos in a human-readable format (which our browser appropriately renders for us to have a look at). But there is also the corresponding web API-version for *code* to interact with of exactly this 'aww' subreddit available under [reddit.com/r/aww.json](https://www.reddit.com/r/aww.json). The JSON (Javascript Object Notation) - output is easier for computers/code/applications to handle as compared to the human-readable version as before.

As an interesting (not so ay funny) application of such web APIs, Colt mentions [ifttt.com/recipes](https://ifttt.com/recipes) which is a service that enables you to make apps and devices to work together by exploiting the connection/concatenation of web APIs (that are supported on this platform).

A great place that collects a comprehensive list of available web APIs (i.e., kind of like an API directory) is  [programmableweb.com](https://programmableweb.com).




A very intuitive explanation that I found was given by [Petr Gazarov](https://medium.freecodecamp.org/what-is-an-api-in-english-please-b880a3214a82) on his blog:


*When I think about the Web, I imagine a large network of connected servers. Every page on the internet is stored somewhere on a remote server. A remote server is not so mystical after all — it’s just a part of a remotely located computer that is optimized to process requests. When you type www.facebook.com into your browser, a request goes out to Facebook’s remote server. Once your browser receives the response, it interprets the code and displays the page. To the browser, also known as the client, Facebook’s server is an API. This means that every time you visit a page on the Web, you interact with some remote server’s API. An API isn’t the same as the remote server — rather it is the part of the server that receives requests and sends responses.*

So what is then the difference of an API as described above from what people actually mean when they are talking about API's? The difference is the *format* of the request and the response.

In the former example of facebook, a whole web page is rendered. What we actually mean when using the term API are services that return plain data that can then be easily integrated into other applications (i.e., allow A2A communication). Usually API's return their data in *JSON*  or *XML* - format. And this data-retrieval happens via dedicated URLs (URIs) that return the respective requested responses.

Often these requests can be executed directly via the browser but it is more common to fetch the data via the command-line (by using executables like `curl`) or apps like Postman or SOAP UI.

In the last years REST (Representational State Transfer) emerged as *the* standard architectural design for webservices and web APIs. Thereby the characteristics of a REST system are defined by six 'design' - rules (which we will not list here in detail). The decisive factor is that the REST architecture was originally designed to fit the HTTP protocol that the ww as we know it already uses. Clients that want to retrieve data from certain end-points (resources/URIs) or store data in certain end-points simply send HTTP requests to affect a given resource in one of the common ways (GET, POST, PUT, DELETE, etc.).

While the above all makes sense, I stumbled over [Miguel Grinberg's](https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask/page/0#comments) amazing tutorial that with just a few lines of code implements a simple REST API as follows:
