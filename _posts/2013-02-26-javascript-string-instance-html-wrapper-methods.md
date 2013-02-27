---
layout: post
title: "Javascript String Instance HTML Wrapper Methods"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

While digging around the `String` docs over on Mozilla I ran across 
[HTML Wrapper Methods](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String#HTML_wrapper_methods).

These are a suite of methods which quickly wrap a string in an HTML element. I've
not actually seen this in practice and the subset of elements (13 in total) are
outdated (I'm looking at you `<fontsize>`) which leads me to believe that though
perhaps this was how things were once done that is no longer the case.

The Mozilla docs lists HTML Wrapper Methods as `Non-standard` which further
backs up my suspicion. So I wouldn't recommend actually doing this in practice.
This is more just meant to shine some light on a strange feature of Javascript
`String` instances.

what do HTML Wrapper methods look like? Let's have a look.

## On to the code

### anchor

```javascript
'foo'.anchor(name);
// <a name='name'>foo</a>
```

### big

```javascript
'foo'.big();
// <big>foo</big>
```

### blink

```javascript
'foo'.blink();
// <blink>foo</blink>
```

### bold

```javascript
'foo'.bold();
// <b>foo</b>
```

### fixed

```javascript
'foo'.fixed();
// <tt>foo</tt>
```

### fontcolor

```javascript
'foo'.fontcolor(color);
// <fontcolor color='color>foo</fontcolor>
```

### fontsize

```javascript
'foo'.fontsize(size);
// <fontsize size='size'>foo</fontsize>
```

### italics

```javascript
'foo'.italics();
// <i>foo</i>
```

### link

```javascript
'foo'.link(url);
// <a href='url'>foo</a>
```

### small

```javascript
'foo'.small();
// <small>foo</small>
```

### strike

```javascript
'foo'.strike();
// <strike>foo</strike>
```

### sub

```javascript
'foo'.sub();
// <sub>foo</sub>
```

### sup

```javascript
'foo'.sup();
// <sup>foo</sup>
```

## Summary

HTML Wrapper Methods provide an easy way to wrap a `String` in an HTML element.
However this only offers a small subset of older HTML elements. Also it's non
standard and can easily be done in a standard way like so:

```javascript
var p = document.createElement('p');
p.innerText = 'foo';
// <p>foo</p>
```

or with [jQuery](http://jquery.org):

```javascript
$('<p></p>').text('foo');
// [<p>foo</p>]
```
