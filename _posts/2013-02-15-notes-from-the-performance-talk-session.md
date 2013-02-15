---
layout: post
title: "Notes from the 'Performance Talk' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

Kristofor Selden

* [Twitter profile](https://twitter.com/krisselden)
* [Lanyrd profile](http://lanyrd.com/profile/krisselden/)
* [Github profile](https://github.com/kselden)

## setProperties

run loop

* Does not matter if multiple componets respond to an event and change stuff
* Waterfall: sync, actions, render, afterRender, destroy, timers

## What are Bindings in Ember?

* Ember.Binding
* fooBinding
* {{foo}}
* Ember.computed

## View Bindings

`{{foo}}`

Observes changes, schedules work later on the run loop

    observer = function(){
      Ember.run.scheduleOnce(
        'render', bindView, 'rerenderIfNeeded'
      );
    };

## Bindings vs Computed Properties

> Having watched people devlop o nEmber for the last year, one thing...

## Two-way vs one-way bindings

* Installs two observers vs one on create
* Two way sync invloves suspending the other direction's observer

## 2-way vs 1-way computer properties

* none

## Computed proeprties vs bindings

* CP can be setup on the prototype
* Bindings can't be setup until create
* Bindings have ordering issues
* Conputed proeprties are lazy
* Unfotunately CP notify changes synchronously (for now)

## Computed properties are Lazy

## Observing Property Paths Affect CP Laziness

* CP will fire a change when they are invalidated regarless if they will compute to a different value
* Property paths will fire a change if their parent node change sregardless if they resolve to the same value

## Array Observers are Synchronous

### ArrayProxy eagerly consumes 'content'

  App.PricesController = Em.ArrayController.extend{{
    // ...
    content : function(){
      return this.get('fruitsController.@each.price');
    }.property('fruitsController.@each.price');
  }};

## Dangers of Binding through viewName

Views are like the rendering trees behind things. It's unstable to be adding
bindings between siblings. Be wary of using the viewName to bind.

## autorun

If you do something that needs to defer and you haven't started dqing it we'll
set it to flush and give it a timeout.

On the willChange a view will tear something down. 

Try not to have these in your normal flow.

## Observer memory leaks

* Only case you need to teardown an observer added in init on willDestroy: `addObserver(otherObj, 'prop', this, 'something')`
* Use `willClearRender` to teardown stuff installed on render
* Use `willDestroyElement` to teardown stuff isntalled on `didInsertElement`

## Future Concerns

* Garbage during rendering
