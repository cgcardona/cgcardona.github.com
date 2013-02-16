---
layout: post
title: "Notes from the 'Ember State of the Union' talk"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Opening comments by [Yehuda Katz](https://twitter.com/wycats) and [Tom Dale](https://twitter.com/tomdale)

* Ember.js is now 2 years old
* The new router at the end of 2012 caused the traffic to spike
* **Lots** of code contributions on [Github](https://github.com/emberjs)
* Ember 1.0 RC1 released today!
* Semantic Versioning
* PeepCode Integrations Tests
* one dot zero tests

## Updates to [docs](http://emberjs.com/guides/)

* Getting started
* Tutorial and video 
* Interactive code samples
* Full API Coverage
* Core team will be looking for old tutorials and will contact the creators to
ask them to add a disclaimer which says that the code **isn't** from the new 1.0
RC1 API.

## Future of the Web

### Web components

[Web
components](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/) are
*just HTML*. The ember team wants to make Web Components an integral part of the
framework.

### ES6 (Javascript.next)

How about making App Cache a more layered approach?

If there are ways that people are using JS today then the next version of JS
should attempt to use the language to pave existing ways that people are already
using the language.

#### Upward compatability

Changes in the language should have a targeted effect. For example `super`.
Noone likes `_super`.

[Object.observe](http://wiki.ecmascript.org/doku.php?id=harmony:observe#object.observe)

The team is paying a lot of attention to the future of the web platform. We want
to make sure that the ember code is structured to take max advantage of new
features in JS/HTML/CSS.

## URLs

### Example from Discourse

Yehuda is showing an example of URLs on
[discourse](http://meta.discourse.org/). Basically showing that `EmberJS` can
handle infinite scrolling and passing on deep state of the app via a url.

### URL-Driven Apps

When you build an Ember App you get URLs for free as a side effect of the ember
conventions.

### Native

Native apps don't have URLs. The intention is for ember to remind client side
app developers of the importance of passing app state around via URLS.


## More notes

* 200 contributors
* Dozens of companies using it in production
* Officially introducing the Ember Core Team.

1. Peter
2. Stephan
3. [Trek Glowacki](https://twitter.com/trek)
4. [Yehuda Katz](https://twitter.com/wycats)
5. [Kristofor Selden](https://twitter.com/krisselden)
6. Leah
7. Eric
8. Tom Dale

## Path to core

The idea is to be community driven. The idea isn't to make Yehuda and Tom
millionaires. They want to bring in other people and companies to distribute
ownership and responsibility of the app. 

If Yehuda and/or Tom get hit by a bus that shouldn't affect the framework in a major way.

Ember Core team is watching commits on Github. If they notice someone doing
great work and adding value they will consider ways to move that person to the
Core team.

### Companies that have helped Ember.js

* Yapp
* Addepar
* Living Social
* MHElabs

### Sponsors of the event

* Zendesk 
* Livenation
* Tilde
* Addepare
* Microsoft

## Meetups

* Atlanta
* Berlin
* Boston
* Dublin
* Chicago
* London
* New York
* Munich
* Orange County
* Paris
* Philadelphia
* Toronto
* San Francisco
* Seatlle

### People specifically thanked

* New York Meetup - This is basically a monthly Ember.js Conference. If you are in the New York area make sure to check it out.
* Matt Grantham - Dedicated time to designing the ember.js website.

## One More Thing...

### Ember Inspector

JS Inspector is great but [Ember Inspector](https://github.com/tildeio/ember-extension) provide a debugging tool that is on a higher level.  Lets you see whats happening in the code with regards to an Ember.js
perspective.

#### Features

* Hover over a controller
* Show and interact with computed properties
