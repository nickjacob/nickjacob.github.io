---
layout: post
title: How to write a tiny client-side, compiled-template library
date: 2014-08-22 12:00:00
categories: javascript
author: Nick Jacob
---

In writing quick/one-off web apps, I often find myself really wanting some client-side templating. In general, I think it's a good idea to move all presentation to the client and let any front-end servers work mainly to proxy/authenticate requests to backend APIs, containing any scoping/formatting but not dictating presentation. This makes responsive presentation more flexible (you can limit display on smaller screens, or reeuse the same data across views without making extra backend calls. This also makes it easier to make a completely static site (e.g., hosted in s3) with a backend service using some scoped CORS--this is how [demo.mirador.im](http://demo.mirador.im) works. With the rise in popularity of client-side frameworks, it seems like this approach is pretty well accepted.

At the same time, I rarely need all of the features of a templating library like [handlebars.js](http://handlebarsjs.com), and I don't usually include [underscore](http://underscorejs.org) in simple apps, even though I do think it's pretty great.

I figured all I really need in client-side templating is string interpolation, possibly also with nested property access. So I put together a couple of javascript functions to create some compiled templates:

{% gist 7093743 %}

This can be represented in a lot fewer lines, although I have to admit it's still not really super readable. Just to break down the `compile` function.

On a high level, the function produces a new function that performs string interpolation using concatentation, dynamically looking at the object passed in (using `with` statement).  Ideally, this could be called with a context that would provide additional helpers:

There are a lot of improvements that could be made, but I'm a fan of this for its simplicity and the fact that it forces me to avoid pushing to much logic onto the actual view.
