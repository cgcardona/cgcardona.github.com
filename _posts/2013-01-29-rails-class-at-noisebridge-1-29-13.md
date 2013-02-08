---
layout: post
title: "Rails class at NoiseBridge 1 29 13"
description: ""
category: 
tags: ['ruby', 'rails', 'noisebridge']
---
{% include JB/setup %}

## Summary

My notes from the 1-29-13 [rails class](https://www.noisebridge.net/wiki/Backend_web_dev_in_Ruby_on_Rails) at noisebridge.

## Rails has two defaults

[Rails has two default stacks](http://words.steveklabnik.com/rails-has-two-default-stacks) by [Steve Klabnik](http://words.steveklabnik.com/rails-has-two-default-stacks)

What DHH uses at 37 Signals

* ERB for view templates
* MySQL for databases
* MiniTest for testing
* Fat Models, Skinny Controllers

The teacher prefers

* Haml for view templates
* PostgreSQL for databases
* Rspec/Cucumber for testing
* Skinny models, controllers, and a service layer

Brief mention of `rvm gemset create`

[rvm gemset docs](https://rvm.io/gemsets/basics/)

## Code time!

### Create a new app

`rails new appName`

### Add haml, rspec, and capybara

Open your Gemfile and add

  gem "haml-rails", '~>0.3.5'
	
	group :test, :development do
	  gem 'rspec-rails'
	end

	group :test do
	  gem 'capybara'
	end

Or do it this way

	rails generate rspec:install	

Create `.rvmrc` file

### create a test

Create a small test that checks if a user hits the root of the url and some text is returned.

Create a directory with `mkdir acceptance`

Go into the `acceptance` dir with `cd acceptance`

Create and edit a file called `welcome_page_spec.rb` (*spec file need to end in _spec.rb)

##### Contents of `welcome_page_spec.rb`

require spec_helper

## Notes on Postgres

### Up sides

* hstore for unstructured columns
* json-response queries
* geospatial indexing and pretty queries

### Down sides

* Pain in the ass to install on OSX (check out heroku [postgres.app](http://postgresapp.com/))

## Service Layer

Made up of PORO (plain old Ruby objects)

Fat Models, skinny controller breaks down after a while. The service layer idea is 'when all is said and done 95% of the problem can be solved with Ruby the language and without the assumptions of a framework' You can clean up your Model to just the data persistance stuff and move all the other code to PORO.

The Service Layer uses Ruby the language to solve problems which the framework introduces.

## Misc

### Lightweight Ubuntu that is super ruby/rails/postgres friendly

700MB Ubuntu server [12.04 x86_32 image](http://ubuntuone.com/6wvuy1oAoMwvv2wZOogj8j)

Recommended to use virtualbox

### Teacher's notes

[Teacher's notes from the class](http://www.railsschool.org/l/popular-alternative-rails-configurations/whiteboard)
