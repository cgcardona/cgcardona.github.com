---
layout: post
title: ".contains, .startsWith, and .endsWith"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

## Summary

Writing ECMAScript 6's proposed `.contains`, `.startsWith`, and `.endsWith` methods using good ole `.indexOf`.

## .contains

```javascript
'carlos'.contains('car');
// true
'carlos'.indexOf('car') >= 0;
// true
```

## .startsWith

```javascript
'carlos'.startsWith('car');
// true
'carlos'.indexOf('car') === 0;
// true
```

## .endsWith

This one looks a little dirty to me because I needed to know the `fname` and `arg` in advance. Is there a way to do it so that I don't need those two variables?

```javascript
'carlos'.endsWith('los');
// true
var fname = 'carlos';
var arg = 'los';
fname.indexOf(arg) == fname.length - arg.length;
// true
```
