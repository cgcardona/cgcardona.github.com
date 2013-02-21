---
layout: post
title: "Use Ember.js as a cross plaform javascript library pt2"
description: ""
category: 
tags: ['emberjs', 'javascript']
---
{% include JB/setup %}

## Previously

See [Use Ember.js as a cross platform javascript library pt1](http://cgcardona.github.com/2013/02/18/use-emberjs-as-a-cross-plaform-javascript-library/)
for the previous episode.

As with previously this code is [Version: v1.0.0-rc.1](https://raw.github.com/emberjs/ember.js/release-builds/ember-1.0.0-rc.1.js)

## Ember.js Object model, KVO, and CPs

After posting previously this afternoon I got the following tweet from Ember.js
Core member [@wagenet](https://twitter.com/wagenet/status/303660277797376000):

> Looks like a nice start. However, I see the main benefits of
> `ember-runtime` as being KVO support and CPs.

KVOs meaning Key/Value Observation and CPs being Computed Properties.

You don't have to dig in too deep to the Ember.js Object Model before you start
to hear about [Computed Properties](http://emberjs.com/guides/object-model/computed-properties/).

So in the context of just using ember-runtime let's take a look at the Object
Model, Key/Value Observations, and computed properties.

## The Object Model

Ember.js brings some sanity to Javascript's Prototypal nature by offering a
syntax to create classes, instances of classes, and extend classes. It also
offers a simple `this._super()` sytax for calling a parent's method.

### Base class

First create a simple `HumanClass`. The fname and lname properties are both null
and will get set with `create()`. The `fullName` is a Computed Property. By
setting it to the value of this.get('fname') and this.get('lname') `fullName` will
be dynamic to whatever properties `fname` and `lname` have at a later time.

```javascript
var HumanClass = Ember.Object.extend({
  fname : null,
  lname : null,
  fullName : function(){
    return this.get('fname') + ' ' + this.get('lname');
  },
  say : function(){
    console.log('called via super!');
  }
})
```

### Extend the base class

Next create a `ManClass` which extends the `HumanClass`. Notice `this._super()`.  Sweet.
    
```javascript
var ManClass = HumanClass.extend({
  say : function(){
    this._super();
  }
})
```

### Create an instance

Now use the `create()` method to create an instance of your class. The values
that you pass in via an object literal will be assigned to the properties that
you defined on your class.

```javascript
var manInstance = ManClass.create({
  fname : 'Carlos', 
  lname : 'Cardona' 
});
```

To test out `this._super()` call the `say()` method.

```javascript
manInstance.say(); // demonstrates this._super();
```

## Add Key/Value Observers

One of the cool things about Ember.js is Key/Value observers. You can tie
objects together based on fluctuating values of properties.

Here we want to create a `PropertyObserverClass` which will have a `propertyDidChange` method. The method will take `sender`, `key`, `value`, and
`rev` per the docs for the [addObserver
method](http://emberjs.com/api/classes/Ember.Object.html#method_addObserver).
The method will just log to the console the name of the property that changed
and its new value.

```javascript
var PropertyObserverClass = Ember.Object.extend({
  propertyDidChange : function(sender, key, value, rev){
    console.log(key + ': ' + sender.get(key));
  }
});

var propertyObserverInstance = PropertyObserverClass.create();

Object.keys(manInstance).forEach(function(el, ind){
  // add an observer for both of the manInstance's properties
  manInstance.addObserver(el, propertyObserverInstance, propertyObserverInstance.propertyDidChange);
});
```

## Run it

Now that we've got an object with a couple of properties with another object
observing those properties let's see what happens when the values change.

```javascript
manInstance.set('fname', 'Soljah');
manInstance.set('lname', 'Cardona-Edwards');
console.log(manInstance.fullName());

manInstance.set('fname', 'Second');
manInstance.set('lname', 'Name');
console.log(manInstance.fullName());
```

And in the console we see:

```javascript
fname: Soljah 
lname: Cardona-Edwards 
Soljah Cardona-Edwards 
fname: Second 
lname: Name 
Second Name 
```

Twice you can see `fname` and `lname` get called from within the
`propertyDidChange` method that gets called via Ember's Key/Value Observation.

You also see the full name get logged which is created dynamically with Ember's
computed properties.

## Summary

This was meant to show that `ember-runtime.js` still supports Ember.js's Object
Model, Key/Value Observation, and Computed Properties. 
