---
layout: post
title: "Build a static site with Ember.js"
description: ""
category: 
tags: ['emberjs', 'javascript', 'code', 'handlebars']
---
{% include JB/setup %}

## Create a git repo

I've created a new repo on [Github](http://github.com) and clone it to my machine

   $ git clone git@github.com:user/app_name.git 
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

Now you want to edit the `Gemfile` to include the `ember-rails` gem. Open the
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
