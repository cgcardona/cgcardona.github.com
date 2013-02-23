---
layout: post
title: ".contains, .startsWith, and .endsWith"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

## Intro

ECMAScript 5 brought some much needed attention to the `Array` and `Object`
Objects so it's nice to see `String` get some focus with ECMAScript 6.

There are 3 `String` instance methods that caught my eye this evening:
`.contains`, `.startsWith`, and `.endsWith`.

Earlier this evening I had the following exchange on Twitter.

### [@cgcardona](https://twitter.com/cgcardona/status/305199575348678656):

> Javascript Devs—in #Firefox check out: `'carlos'.contains('los');`
> `'carlos'.startsWith('car');` `'carlos'.endsWith('los');` Harmony

### [@oscargodson](https://twitter.com/oscargodson/status/305203583505285120)

> why not indexOf?

### [@cgcardona](https://twitter.com/cgcardona/status/305204878890897408)

> Just because I was showing 3 methods that are coming in ES6 and
> indexOf is old school.

### [@oscargodson](https://twitter.com/oscargodson/status/305205385252438017)

> yea but what's the benefit other than "its cool"? Contains is equal
> to -1, and startsWith is 0 and endsWith is str.length, right?

### [@oscargodson](https://twitter.com/oscargodson/status/305205440239792128)

> is it faster? More peformant?

## Good point

That's a totally valid point which got me thinking&mdash;is it worth the overhead of adding 3 new methods in
order to get the added semantic clarity?

After all as we show below the functionlity of `.contains`, `.startsWith`, and
`.endsWith` can all be achieved using `.indexOf`.

## Pros

Traditionally one of Javascript's strengths has been it's lightweight standard
library. As Douglas Crockford famously says Javascript is the one language that
no one feels that they need to learn before they dive in and start programming.

And for the most part it's true&mdash;Javascript and HTML are pretty forgiving.
But it's clear to everyone involved that Javascript has grown up and now is
expected to do some relatively heavy lifting. 

As such the standard library can seem small and advanced functionality can be
hidden behind cryptic method names like `.indexOf`.

The Pro would be beginning to expose more functionlity of the language through
meaningful names with the side effect of fleshing out the standard library.

## Cons

The Con would be abandoning Javascript's traditionally lightweight standard
library. Adding more methods means adding overhead to any developer hoping to
pick up the language. This can all be mitigated to some degree with good
documentation and a community of developers both of which Javascript thankfully has.

## Code

Based on the Twitter conversation I decided to see how easy it would be to write ECMAScript 6's proposed `.contains`, `.startsWith`, and `.endsWith` methods using good ole `.indexOf`.

### .contains

```javascript
'carlos'.contains('car');
// true
'carlos'.indexOf('car') >= 0;
// true
```

### .startsWith

```javascript
'carlos'.startsWith('car');
// true
'carlos'.indexOf('car') === 0;
// true
```

### .endsWith

This one looks a little dirty to me because I needed to know the `fname` and
`arg` in advance. It would be best to wrap it in some type of function.

```javascript
'carlos'.endsWith('los');
// true
var fname = 'carlos';
var arg = 'los';
fname.indexOf(arg) == fname.length - arg.length;
// true
```

[Oscar Godson](https://github.com/OscarGodson) recommended the following on
[this gist](https://gist.github.com/cgcardona/5018788#comment-779783):

```javascript
String.prototype.endsWith = function (suffix) {
  return this.indexOf(suffix, this.length - suffix.length) !== -1;
};
```

## Summary

My personal opinion is that it is a **good** thing to add these methods even
though the functionality is already available with `.indexOf`.

My thoughts are that the Pros outweigh the cons in the sense of the only con I
see being extending the standard library at the expense of making it harder for
newcomers to grasp the full language.

But I would argue that the language is actually helped by having methods which
are self documenting by their names. 

As a new Javascript developer comes on the scene they can use `.endsWith` when
that is what they mean.

## Write what you think

This all plays into why I enjoy writing Ruby and why I think Coffeescript is a
pleasant abstraction on top of Javascript. I want my programs to read like my
thoughts.

If the method names sound or read like what I'm trying to accomplish then all
the better. And I think that's what high level languages are all about.
