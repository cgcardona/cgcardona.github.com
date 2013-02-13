--- 
layout: post
title: "Build a static site with Ember.js"
description: ""
category: 
tags: ['emberjs', 'javascript', 'code', 'handlebars']
---
{% include JB/setup %}

## TLDR

This is how to set up an **extremely** simple and static site with Ember.js and
Ruby on Rails using the `ember-rails` gem.

It shows how to set up a basic Route and points out that routes map to
controllers and templates.

This uses the [Ember.js Version: v1.0.0-pre.4](https://raw.github.com/emberjs/ember.js/release-builds/ember-1.0.0-pre.4.js) API.

Check out a live example: [http://ember-static.herokuapp.com/](http://ember-static.herokuapp.com/)

## Create a git repo

I've created a new repo on [Github](https://github.com/cgcardona/ember_static) and clone it to my machine

    $ git clone git@github.com:cgcardona/ember_static.git 
    Cloning into 'ember_static'...
    remote: Counting objects: 65, done.
    remote: Compressing objects: 100% (48/48), done.
    remote: Total 65 (delta 3), reused 62 (delta 3)
    Receiving objects: 100% (65/65), 20.94 KiB, done.
    Resolving deltas: 100% (3/3), done.

## Create a new rails app

Next I create a new rails app and tell it to `--skip-bundle`
    
    $ rails new ember_static --skip-bundle
    create  
    create  README.rdoc
    create  Rakefile
    create  config.ru
    create  .gitignore
    create  Gemfile
    create  app
    create
    app/assets/images/rails.png
    create
    app/assets/javascripts/application.js
    create
    ...

I tell rails to skip running `bundle install` because I'm going to be editing
the `Gemfile` in the next step.

## Edit the Gemfile

Now you want to edit the `Gemfile` to include the [ember-rails](https://github.com/emberjs/ember-rails) gem. Open the
`Gemfile` in your favorite text editor and add the following lines.

    gem 'ember-rails', '~> 0.9.2' 

Once you've updated your `Gemfile` run

    $ bundle install
    Fetching gem metadata from https://rubygems.org/...........
    Fetching gem metadata from https://rubygems.org/..
    Using rake (10.0.3) 
    Using i18n (0.6.1) 
    Using multi_json (1.6.0) 
    Using activesupport (3.2.12)
    ...

## Create a controller and route for the root url

    $ rails g controller welcome index
    create  app/controllers/welcome_controller.rb
     route  get "welcome/index"
    invoke  erb
    create    app/views/welcome
    create    app/views/welcome/index.html.erb
    ...

Once rails generator has stubbed out your controller edit `config/routes.rb` to
set the root url to point to `welcome#index` (the `welcome` controller and
`index` action)
    
      root :to => 'welcome#index'
      get "welcome/index"

Also because this is rails you'll need to remove the public/index.html file

    $ rm public/index.html

## Stub out your ember.js directories

Edit `config/environments/development.rb` and add 

    config.ember.variant = :development

Also edit `config/environments/production.rb` and add 

    config.ember.variant = :production

Using the handy `ember-rails` generator bootstrap the client side MVC directory
structure.

    $ rails g ember:bootstrap
    insert  app/assets/javascripts/application.js
    create  app/assets/javascripts/models
    create  app/assets/javascripts/controllers
    ...

At this point if you can remove any content from `app/views/welcome/index.html.erb`. All templating is going to be done on the Ember.js side.

## We have a stub ember app!!

Before we go on I must say that I prefer the `.hbs` extension to the overly
verbose `.handlebars` so I go ahead and change the name of the one stub
handlebars file.

    $ mv app/assets/javascripts/templates/application.handlebars app/assets/javascripts/templates/application.hbs

Ah, that's better. Onward. 

## Set up your overall application markup

Open `app/assets/javascripts/templates/application.hbs`. This is similar
conceptually to `app/views/layouts/application.html.erb`.

Remove `<p>Your content here.</p>`. We'll be adding per route specific content
to the templates in a moment.

The `{{outlet}}` is similar to `<%= yield %>`. It's where your different
templates for each route will get inserted.

## Set up your index controller/template

Ember.js is rails like in the sense that there is a certain convention over
configuration. In this case without setting up a route the root url maps to an
index controller and index template

Create the index controller `app/assets/javascripts/controllers/index_controller.js`

    emberStatic.IndexController = Ember.Controller.extend({
        name : 'carlos cardona'
    });

Notice that it's just an IndexController which extends Ember.Controller. Also
notice that we've added a `name` property which we'll display in our template
next.

Now create the index template `app/assets/javascripts/templates/index.hbs` and
add handlebar template variables for the `name` that we added in the controller.
Also add a link to an `about` route that we are going to create.

   Hello {{name}}!
   {{#linkTo 'about'}}About page{{/linkTo}}

## Set up a Route

To see how routing works open up `app/assets/javascripts/router.js` and add a
route to an `about` page

    EmberStatic.Router.map(function() {
      this.route("about", { path : "/about" });
    });

## Create an `about` controller and template

Start by create an `about` controller at `app/assets/javascripts/controllers/about_controller.js`

    emberStatic.AboutController = Ember.Controller.extend({
      about : 'This is some about text'
    });

Next create an `about` template at `app/assets/javascripts/templates/about.hbs`

   About: {{name}}
   {{#linkTo 'index'}}Index page{{/linkTo}}

## Thats all folks!

And that's an extremely simple and static site built with ember.js and rails.
There are some pretty critical things missing such as:

* Binding
* Generated Properties
* Ember Data

Let's not kid ourselves. Ember.js is capable of **way** more. This was simply
meant to be a demonstration of how routes work and how each route is mapped to a
controller and template. We also looked at how to pass a value from a controller
to a template.

Check this example live at [http://ember-static.herokuapp.com/](http://ember-static.herokuapp.com/)

Clone the code at: [https://github.com/cgcardona/ember_static](https://github.com/cgcardona/ember_static)

## More info

* [Official Ember.js site](http://emberjs.com/)
* [Official Handlebars site](http://handlebarsjs.com/)
