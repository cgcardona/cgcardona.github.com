---
layout: post
title: "Intro to Ember.js"
description: ""
category: 
tags: ['emberjs', 'javascript', 'code', 'handlebars']
---
{% include JB/setup %}

[Ember.js](http://emberjs.com) is an MVC framework for rich client side applications. It evolved out of SproutCore 2.0.  

## Let's dive in

### Create a new `rails` app

    rails new ember_tutorial --skip-bundle 

I'm telling `rails` to `--skip-bundle` because I'm going to be updating the
`Gemfile` in the next step and then running `bundle install`

### Update the `Gemfile`

I'm getting access to Ember.js with the `ember-rails` [gem](https://github.com/emberjs/ember-rails). Add the following
to your `Gemfile`:

    gem 'ember-rails', '~> 0.9.2'

Run `bundle install` which will pull down the dependancies from RubyGems. Then
add the following line to `app/assets/javascripts/application.js`

    //= require ember

`Ember-rails` will correctly use the production or development build of `ember.js`
depending on what environment you're in.

### Generate the directory structure

`ember.js` doesn't require a certain directory structure but there seems to be a
convention forming around the following:

    controllers/
    helpers/
    models/
    routes/
    templates/
    views/

If you're coming from `rails` that might look familiar. Within the `app`
directory `rails` has (amongst others):

    controllers/
    helpers/
    models/
    views/

[Yehuda Katz](https://twitter.com/wycats) is a member of both the `rails` core
and `ember.js` core teams. I'm not sure if this convention stems directly from
that relationship or not but it's certainly not the only simularity between the
two frameworks that I've spotted.

`ember-rails` comes with a handy generator that allows us to bootstrap the
desired directory stucture in `app/assets/javascripts`. Run `rails g ember:bootstrap` 

### What did that get us?

That command did a few things. First it updated
`app/assets/javascripts/application.js` to include to include the following

    //= require ember-data
    //= require appName
    AppName = Ember.Application.create();

Second it created `app/assets/javascripts/appName.js` which includes the
following lines:

    //= require ./store
    //= require_tree ./models
    //= require_tree ./controllers
    //= require_tree ./views
    //= require_tree ./helpers
    //= require_tree ./templates
    //= require ./router
    //= require_tree ./routes
    //= require_self

This basically encapsulates all the ember.js javascript files within this appName.js file.

Third it created two more files in `app/assets/javascripts/`:

    router.js
    store.js

### And what is in all those files?

Let's inspect each one to find out.

#### Quick tangent #1 - `.extend()`

`Ember.js` allows extending/subclassing Objects in an attempt to bring sanity to
javascript's prototypal nature. When you see `.extend({})` that's what's
happening.

Now back to what's in the files.

#### app/assets/javascripts/controllers/application_controller.js

    appName.ApplicationController = Ember.Controller.extend({});

#### app/assets/javascripts/routes/application_route.js

    appName.ApplicationRoute = Ember.Route.extend({});

#### app/assets/javascripts/templates/application.handlebars
    
    <h1>Application</h1>
    <p>Your content here.</p>
    {{outlet}}

#### app/assets/javascripts/views/application_view.js

    appName.ApplicationView = Ember.View.extend({});

#### app/assets/javascripts/router.js

    appName.Router.map(function() {});

#### app/assets/javascripts/store.js

    appName.Store = DS.Store.extend({
        revision: 11
    });

#### Quick tangent #2 - `Router`

`Ember.js` adds a new element to the traditional MVC makeup. They call this a
`Router`. 

The idea is that human visible/editable URLs are a strength of webapps that
native apps do not enjoy. Users are able to share URLs to friends which
basically let's them share the state of their app. 

Using a `Router` you map every single state of your app to a URL which allows
the sharing of deep state.

### What does it all mean?

The main take away is that we're getting a controller, route and view which extend
come core `ember.js` objects. We're also getting stub handlebars template,
router, and store.
