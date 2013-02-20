---
layout: post
title: "Some handy new Javascript features"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

## TLDR

Introducing Javascript's [trim, trimLeft, and trimRight](#trim_trimleft_and_trimright) methods and [default
parameter values](#default_parameter_values).

## Intro

Javascript is a language which you either love or hate. But no matter how you
feel the web has grown into the world's plaform which has made javascript an undeniable force to be reckoned with.

One positive side of javascript is that the standard library is lightweight
which makes the language's API pretty easy to pick up. This is true but it has
the unfortunate side effect of leaving javascript without some pretty basic
functionality.

Fortunately the web is moving quickly and the multitude of preprocessors
([coffeescript]()), supersets ([typescript](http://www.typescriptlang.org/)),
and subsets ([asm.js](http://asmjs.org/spec/latest/)) as well as having
javascript now on the server with [node.js](http://nodejs.org/) has brought to
light the sore spots of javascript and has begun to show a clear path forward. 

Check out [altjs](http://altjs.org/) for a list of literally dozens of projects related to the future of Javascript.

## But why?

The functionality we're about to discuss seems pretty basic. Thankfully our kids
will grow up in a world where javascript supports this stuff. :p

All joking aside why does this matter? Can't we keep Javascript's standard library lightweight
and have 3rd party libraries polyfill this stuff?

Of course we could do that but at this point it's clear that the
web is the biggest development plaform of all time. The browser is the largest
and most forgiving of run times which means we can count on an ocean of
developers coming to this platform.

We can't count on all those developers learning about the correct libraries to
get this functionality. We can't count on the 3rd party library creators
standardizing on these features. And having native function calls tends to be
more performant than calling 3rd party libraries. 

I would expect the Javascript Standard Library to get larger going forward. Now
on to the code!

## trim, trimLeft, and trimRight

Introduced in `Javascript 1.8.1`

[trim()](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String/Trim),
[trimLeft](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String/TrimLeft),
and
[trimRight](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String/TrimRight) method supported in Firefox 19+, Chrome 24+, Safari 6.0.2

    console.log('   StringOne   '.trim() + 'StringTwo');
    console.log('StringOne' + '   StringTwo'.trimLeft());
    console.log('StringOne   '.trimRight() + 'StringTwo');
    // all of the above statements log 'StringOneStringTwo'

### Notes

Yea trimming. Like I said&mdash;we're talking about some pretty basic stuff
here.

The `trimLeft` and `trimRight` methods both say `Non-standard` in their docs as
well as `ECMAScript Edition None`.

Their sibling `trim` says `Introduced in JavaScript 1.8.1` in it's docs as well
as `ECMAScript Edition  ECMAScript 5th Edition`.

I'm not entirely sure the status of `trimleft` and `trimRight` with regards to
standards bodies and such but they appear to be implemented in the 3 desktop
browsers which I tested.

### Potential improvement

This could be improved by taking a second argument which is a list/range of
characters to trim similar to [PHP's trim implementation](http://php.net/manual/en/function.trim.php).

## Default parameter values

Supported in [Firefox
15+](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/default_parameters).

    function foobar(buz = 'baz'){
      console.log(buz);
     // logs 'baz'
    }
    foobar();

### Notes

This is far superior in readability to the current hack:

    function foobar(buz){
      buz = buz || 'baz';
      console.log(buz);
      // logs 'baz'
    }
    foobar();

### Potential improvement

Perhaps with a little added syntax we could have the default parameter value
assigned to `this`. Ex:

    function foobar(buz => 'baz'){
      console.log(this.buz);
     // logs 'baz'
    }
    foobar();

## Summary

`trim`, `trimLeft`, and `trimRight` as well as default parameter values are some
small additions which flesh out Javascript's API in places where it's badly needed. I
expect a lot more of this kind of thing going forward.
