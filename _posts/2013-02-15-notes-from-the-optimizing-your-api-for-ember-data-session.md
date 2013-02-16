---
layout: post
title: "Notes from the 'Optimizing Your API for Ember Data' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

### Dan Gebhardt

* [Twitter profile](https://twitter.com/dgeb)
* [Github profile](https://github.com/dgeb)
* [Lanyrd profile](http://lanyrd.com/profile/dgeb/)
* [Blog](http://www.cerebris.com/blog/)

## [Summary](http://lanyrd.com/2013/ember-camp/sccrwm/)

> We don't always have the luxury of designing an application's front and back
> ends together. However, when we do, it makes sense to mesh them as closely as
> possible. This talk will focus on optimizing a backend API for use with Ember
> Data.

> Ember Data has been steadily expanding its capabilities in the past year. It now
> supports a number of different data relationships, embedded and "side loaded"
> data, and even bulk commit operations. Serializers and mappings help translate
> between your API and your Ember models. This talk will explore front and back
> end code that illustrates these capabilities.

> Because Ember Data features "out-of-the-box support for Rails apps that follow
> the active_model_serializers gem's conventions", the examples in this talk will
> utilize active_model_serializers to build an API. However, the examples will
> focus on API endpoints and therefore be easily translatable to other tech
> stacks.

## Convention over configuration

> Trivial choices are the enemy
> - Yehuda Katz

My making our API as conventional as possible we can reduce friction on our team
and make our APIs easier to consume.

## Tech stack

### Client

`Ember.js`

### Server

`Rails` with `ActiveModel::Serializers`

## ActiveModel::Serializers

* "what" not "how"
* DRY
* Customizable

## Ember Data

* In memory store
* Canonical records
* Multi-layered architecture
* Customizable adapters/serializers

## AM::S Conventions

* underscore_naming
* include `root` element
* id: 1, fk_id: 1, fk_ids: [1]
* conventions for including related data

## DS.RESTAdapter Conventions

* underscore_naming
* include `root` element
* id: 1, fk_id: 1, fk_ids: [1]
* conventions for including related data

Identical to ActiveModel::Serializers

## A sprinkle of configuration

    class ApplicationSericalizer < ActiveModel::Sericalizer
      # sideload related data by default
      embed :ids, include: true
    end

## Relationships

### One-to-Many relationships

`... code Ember.js, rails, and JSON examples`

### One-to-None relationships

`... code Ember.js, rails, and JSON examples`

### Many-to-Many relationships

`... code Ember.js, rails, and JSON examples`

### Many-to-None relationships

`... code Ember.js, rails, and JSON examples`

## Embedded Relationships

### Serialized Embedded Data

`... code rails, and JSON examples`

### Embedded Read-only Data

`... code Ember.js example`

## Customizations

### Custom Pluralization

`... code JSON example`

### Custom Keys

`... code JSON example`

### Custom Sideloading

`... code Ember.js and JSON examples`

### Custom Transforms

Let you define your own types of data.

`... code Ember.js example`

### Custom URLs

`... code Ember.js example`

### Buld Commits

`... code Ember.js example`

## Edge of Convention

Each of these is easy for us to solve in our own domain but hard to standardize on.

* Pagination
* Authentication
* Sparse fieldsets
* Custom icnludes
* Polymorphism

## Resources

* [Ember data example](https://github.com/dgeb/ember_data_example)
* [Rails ative model serializers](https://github.com/rails-api/active_model_serializers)
