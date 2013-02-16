---
layout: post
title: "Notes from the Panel QA' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## 1

Q: Will the docs evolve to document internal features to make it easier to
contribute internally

A: That would be great. It's more of a priority to getting people to use the
public API correctly. But I'd love to get to a point where internals are
documented in that way.

Nearly 100% of the internal apis are documented in the comments of the source
code.

There is definetily a learning curve to figureing out how the internals work. 

## 2

Q: Will ember-data always going to be a seperate component. If so will others
stuff be a seperate compenent?

A: No ember-data won't always be a seperate componenet. However we hope to have
other seperate components.

If you check out the source of ember you'll see that there is already a bunch of
components. We want all our components 'ember-metal' etc to be reusable across
other frameworks like node.

`ember-runtime` is already a seperate component. If you clone ember and
`rake:dist` ember-runtime.js comes out with people are using in node for example
when they just want the object model.
