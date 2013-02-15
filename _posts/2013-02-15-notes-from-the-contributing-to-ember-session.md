---
layout: post
title: "Notes from the 'Contributing to Ember' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

### Peter Wagenet

* [Twitter profile](https://twitter.com/wagenet)
* [Github profile](https://github.com/wagenet)
* [Lanyrd profile](http://lanyrd.com/profile/wagenet/)

## We love contributors

Contributing is **really** important to us. We thrive on contributions. There
are over 200 people who have a contribution.

## Questions are encouraged...elsewhere

Don't ask questions about your app on Github. Ask questions like that on
Stackoverflow. There's a great ember tag there.

We want to help you but make sure to ask in the correct place.

## Reporting bugs

The #1 way to contribute to Ember is by filing bugs.

### What happened?

What exactly is the bug?

###  What to expect? 

Error message would be great

### Browser and other relevant information

The more you can tell us the quicker we can help you. 

### Failing [JSBin](http://jsbin.com/), [JSFiddle](http://jsfiddle.net/), or test case

We want to be able to show this issue happening. Apps are complicated and we
can't really help you unless you can reduce it down to something simple that
shows it in a test case it gives us a great place to start with regards to
helping you.

Sometimes when you reduce the problem it fixes itself and you realize that the
problem wasn't what you thought it was.

### Double check in HEAD

Any bugs that we fix we're fixing in Master branch. Please do test against
Master to confirm that your bug hasn't already been fixed.

## Suggesting features

### Full explanation of proposed change

Information is key here. We want to know what you have in mind. 

### Detailed proposal for complex features 

The more complex the feature request the more we would like a thought out proposal from you.

### Consider side-effects

See the big picture and how your change fits into it.

### Don't break APIs in minor releases

We only break APIs in major releases per our new Semantic Versioning

## Sending pull requests

### Simple fixes

Typos, assertions, tests, and/or anything thats simple and straight forward just
edit it directly on Github

### API

#### Inline Documentation

* [YUIDoc](http://yui.github.com/yuidoc/syntax/index.html)

#### Test more complex changes

* Clone website repo to the same direcotry as the ember repo
* `bundle exec rake preview`
* View changes at `localhost:4567/api`

### The environment

#### Set up Ruby 1.9

* [Vagrant](http://www.vagrantup.com/) - see * [`CONTRIBUTING.md`](https://github.com/emberjs/ember.js/blob/master/CONTRIBUTING.md)

#### Install dependancies

#### Running tests

##### CLI

* `rake test`
* `rake test[standard]`
* `rake test[ember-views]`

##### Browser
 * `rackup`
 * `htp://localhost:9292`
 * `htp://localhost:9292/?package=ember-views`

### PR Requirements

* Test are required
* Follow coding style
* Write documentation

### Development tips

#### Use a branch, don't develop on master

* Consider cross-browser compatibility

* Ember.EnumerrableUtils

#### Maintain hygiene

* Keep your commits clean
* Squash and edit with `git rebase -i`
* Rebasing on master

### Submitting

#### Push to a branch on your fork

#### Submit a PR via Github

* Pick the right branch

## Following up

### Answer questions

Please be around to answer any follow up questions we have. We understand that
you're busy but please be available or we might just close your ticket without
merging your code.

### For Pull Requests

* Watch for merge conflicts
* Make sure the Travis tests pass

### Close resolved issues

## What can I do?

### Review open issues

This might be more challenging but checkout the open issues and see if there is
something that you understand and could fix.

* Tackle ones with close milestones. The next milestone is `1.0 Final`

### Write API documentation

If you notice there isn't any or isn't enough documentation on something then
create it.

### Write more unit tests

If you see bugs write unit tests to catch and document bugs.

### Contribute to guides

If it's anything too complex talk with someone from Ember Core first to confirm
that we're on the same page. We don't want you to waste your time.

## Location of Issues

[Ember.js's issues](https://github.com/emberjs/ember.js/issues) live on github. Please check them out and see what you can
contribute!
