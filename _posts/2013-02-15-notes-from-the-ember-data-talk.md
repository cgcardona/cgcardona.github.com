---
layout: post
title: "Notes from the 'Ember Data Talk' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

 Igor Terzic

* [Twitter profile](https://twitter.com/terzicigor)
* [Lanyrd profile](http://lanyrd.com/profile/terzicigor/)
* [Github profile](https://github.com/igorT)


## Intro

* Why can't I call commit ona  model
* Why can't I reorder elements in a many array
* Why can't I rollback a single model

## Plot

* Try doing simple thinggs
* Fail 
* Uncover some ember-data functionality to help us
* Framework authors are not clowns writing code.

## Meet our Models: `App.Post` and `App.Comment`

    App.Post = DS.Model.extend({
      title : DS.attr('string');
    });

## What do we want to happen?

* `Comment.get('post')` is set correctly
* Comment and post are dirtied correctly

    var oldParent = store.find(App.Post, 1), newParent = store.find(App.Post, 2)

## What do we expect to happen?

* `post1.get('comments')` doesn't contain comment
* Objects are dirtied correctly

## It is 2013

* People have solved this before
* ActiveRecord, Django, etc

Ember data is more complex than traditional ORM. It's more complex to use
Ember-data because you don't know how your objects will be stored.

## Ember-data to the rescue

* one to one
* one to many
* many to many
* ... more

## Encode our own constraints

* Cannot be empty 
* Can't have more than 4 elements

if you modify data.

## What to send to the server?

* It depends
* Rails adapter - saved on the child
* node.js and mongo - saved on the parent
* If embedded need to go up the  chain

## Other gotchas

Because Ember-data has to work with so many apis there are other gotchas

* Transactions
* `HasMany` is not really an array

There are plenty of issues where I tried to so something that should be simple
but after working it through for an hour or two it totally blows up. Trying to
work within Ember-data conventions and not fighting it totally helped my sanity.

## Future

* `isDirty` and `shouldCommit`
* `applyingChanges` to the future
