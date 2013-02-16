---
layout: post
title: "Notes from the 'Ember in Action' talk"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}


## Speaker

* Justing Giancoloa 
* [Github profile](https://github.com/elucid)
* [Twitter profile](https://twitter.com/elucid)
* [Lanyrd profile](http://lanyrd.com/profile/elucid/)

## [Summary](http://lanyrd.com/2013/ember-camp/sccrwb/)

> What does an Ember app actually look like in practice? How do features like
> computed properties, data bindings, and state machine-based structure come
> together to make a real application?

> In this talk we will explore a medium-sized Ember app. We will go over
> high-level app structure and investigate specific techniques and idioms that
> commonly appear. The application source will be available on Github so that you
> can follow along in your favorite editor or dig in afterwards when you want to
> refresh your memory.

> By the end you should have a practical sense of what makes the framework useful
> and what makes writing apps with Ember so enjoyable.

## Goal
* Show what building an app feels like
* Focus on how things fit together
* Provide a roadmap for finding answers

This talk was very code heavy. Find the [code samples on github](https://github.com/elucid/ember-tunes)

## What are we building

* Clone of Peepcode's backbone I & II screencast app
* https://peepcode.com/products/backbone-js
* https://peepcode.com/backbone-ii

## Approach to building ember apps

### Models

* Domain logic
* Hold persistant data

### Controllers

* present model data to views
* hold transiet data

### Views

* Manage browser interaction
* Can be used for application level events

### Router

* Coordinates app state with URL
* Coordinates creation, connection of app components

## What I like to do

* Work from the outside in
* Start from UI
* Build downwards into internal components
* Following convenitions

## Steps

1. I missed the first 2 steps
2. I missed the first 2 steps
3. Pull in our data
4. Render library content
5. Add playlist controller
6. Queueing albums
7. Track listings
8. First computed property
9. Current Track
10. Current Track and current album styling
11. Add dequeue action
12. Prev and next
13. Music

## Recap

* Less than 200 SLOC (JS + templates)
* Better abstractions
* Harder to ruin apps
