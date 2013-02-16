---
layout: post
title: "Notes from the 'ClientSideValidations for Ember' session"
description: ""
category: 
tags: ['emberjs', 'embercamp']
---
{% include JB/setup %}

## Speaker

### Brian Cardarella

* [Twitter profile](https://twitter.com/bcardarella)
* [Github profile](https://github.com/bcardarella)
* [Lanyrd profile](http://lanyrd.com/profile/bcardarella/)

[Summary](http://lanyrd.com/2013/ember-camp/sccrwp/)

> The ClientSideValidations gem for Rails has been the best way to extract
> validations for the client. Recently Brian has been porting the code over to use
> with Ember apps. This effort includes building out a FormBuilder base and
> similar syntactic sugar as SimpleForm. He'll walk you through what he's been up
> to, and what's coming next.

## Experience

Been working with client side validations for a couple of years.

## [Client side validations](https://github.com/bcardarella/client_side_validations)

* Rails gem
* Supports custom calidations
* Renders client side same as server side
* When in doubt prefer server side

## [Ember-data-validations](https://github.com/dockyard/ember-data-validations)

## [Ember-formbuilder](https://github.com/dockyard/ember-formBuilder)

## [Client side validations ember](https://github.com/dockyard/client_side_validations-ember)

Bootstraps your ember app modles with server side validations

## Challenges

### Ember-formbuilder

* Support more input types (on Ember?)
* How errors are rendering
* i18n support for labels

### Ember-data validations

* Don't block, use promises
* i18n error messaging
* Don't overwrite pre-defined validations
* Framework (Rails) specific

### Ember-data

* Add 'validating' state to DS.StateManager prior to 'inFlight'
* `inFlight.becameInvalid` should not blow away `model.errors` object

## Ideal validation workflow

1. Client validations pass
2. Send to server
3. Server side validations fail and notifies client

## Ideal validation workflow + 1

1. Client validations pass
2. Send to server
3. Server side validations pass
4. Record attempts to save, database contraints fail, validation bubbles up and
notifies client
