---
layout: post
title: "Notes from the 'Testing Ember Apps' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

Jo Liss

* [Twitter profile](https://twitter.com/jo_liss)
* [Lanyrd profile](http://lanyrd.com/profile/jo_liss/)
* [Slides from the talk](http://www.slideshare.net/jo_liss/testing-ember-apps)
* [Blog](solitr.com/blog)

## Part 1 Full stack integration tests

### capybara

* 'Selenium for Rails'
* Performance issues are a problem
* Powerful but clunky
* Strategy: ONly test every model once DB-to-DOM, read and write
* Move finer-grained tests to client side

## Part 2 Client side integration tests

The idea is to limit the architectural complexity. You have no back end. You
have no DB. Test are run completely on the client.

### konacha

* Rails gem pachaging
* Mocha.js testing framework +
* Chai.js

## Mocha + Chai

Mocha is a testing framework but it doesn't do assertions so you combine it with Chai. All test run in an i-frame by default and it's really fast.

It's very helpful to see it visually.

## Konacha

### Why is it fast?

* No page loads 
* 100% synchronous
* No stack. The most expensive thing is the DOM manipulation that Ember does

## Unit vs Integration

Lot of simple layers ==> integration tests win.

## Ember setup

No 'official' support for testing. So we wing it!

## Router

AppRouter.reopen
  location: 'none'
beforeEach: -> 

Konacha by default clears out the body. Ember automatically schedules run loops
with `setTimeout`. That's bad for reliable tests.

## Model Fixtures

### Client-side fixtures

* easy
* goes out os sync with backend
* fragile
* server-side computed attributes

### Server-side fixtures

`rake test:fixtures`

1. Write fixtures to DB
2. Generate JSOn to fixtures.js. Load through RESTAdapter

* Covers models, serializers, adapters
* Easy to maintain
* Usability
* Complex to set up

## Bonus: JS-driven?

Capybara but in Javascript?

## Questions

Q: with sinatra do you see opportunity for TTD

A: Not quite TDD but continuous. When working with Konacha I wrote tests as I
went.

Q: Can you test views in isolation

A: it's really tricky to instantiate a view... It's too 'unit testy'. It might
be possible

Comment: We use 'Rosie' for Javascript factories. Have you tried VCR for server side
things? It's a Ruby library that will make the requests. We set up the tests
against a live production server.

Q: A lot of bugs come from asynchronicity. Have you tried to test that
specifically?

A: No I haven't. My hope is that a lot of these bugs dissapear. Mocha allows for
asynchronous tests where you set a call back for when your test is complete.
