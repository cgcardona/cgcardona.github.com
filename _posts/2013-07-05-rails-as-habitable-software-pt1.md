---
layout: post
title: "Rails as Habitable Software pt1"
description: ""
category: 
tags: ['rails', 'Richard Gabriel']
---
{% include JB/setup %}

## Software good enough to live with

In [Patterns of Software](http://www.dreamsongs.com/Files/PatternsOfSoftware.pdf) LISP expert [Richard Gabriel](http://en.wikipedia.org/wiki/Richard_P._Gabriel) speaks about the habitability of codebases. In comparing a sprawling codebase which has been predesigned by architects with a codebase which has grown organically piecemeal over many years he makes the comparison of a large industrial complex and a small farmhouse.

He says that the large industrial complex has been designed beforehand by a team of engineers. They thought long and hard about the specifications and the needed materials. They knew the timetable down to the second and they could quote you the projected price down to the penny. However many times these planning commissions forget to factor the most important element--the human equation. 

These industrial buildings lack a sense of life and all too often people working in them feel like cogs in a machine--totally powerless and lacking any personal ownership of the project. The buildings themselves tend to dictate what happens inside because the rooms are prefabricated and can't be molded to fit the occasion.

He contrasts this with a small country farmhouse. At first it's just a small building and a barn. But over years as grandma moves in and a couple of children are added to the family a couple of extra rooms are added. Then one winter it's cold so the barn is connected to the house to make it easier for grandma to get what she needs.

In the end you have a much more organic and piecemeal growth. The people who live there have an affection and sense of ownership of the place because every time they added something they did it to solve a personal problem. 

The industrial building's rooms are prefabricated and offer no flexibility. Inversely the farmhouse's rooms are an extension of the living situation. 

## Umm... Wasn't this supposed to be about rails?

What we are ultimately supposed to draw from this metaphor is that the best software systems are the systems which are the most habitable. They grow organically in a piecemeal fashion over many years as opposed to being designed before hand from the top down.

Each peice of code which is added is like a room being added for grandma. It serves a critical function. Each new abstraction is like the hall connecting the barn and the house. They take the common and repetitive and make it simple and predictable.

And perhaps most importantly habitable software encourages better programming and maintanance. People who are new to the codebase instantly feel at home thanks to common patterns. The code is self documenting and there is a full test suite to run as soon as any changes are made to confirm non-borkage.

In this environment the programmer feels comfortable taking ownership and maintanence. She is confident in making changes and adding new features. This is habitable software at it's finest.

I think that the actual source code of Ruby on Rails is highly habitable. I also think that the Ruby on Rails framework encourages the production of software that is highly habitable.

## Convention over configuration

Perhaps my favorite feature of rails is also the feature which I think makes it most habitable--and that is [convention over configuration](http://en.wikipedia.org/wiki/Convention_over_configuration). 

There are tasks that we're all gonna do if we're setting up a web CRUD app. We all need routes. We all need some type of [datastore](http://en.wikipedia.org/wiki/SQLite). We're gonna need templates. Oh yea and we're gonna need a [webserver](http://en.wikipedia.org/wiki/WEBrick). And while we're at it we should separate our concerns into an [MVC pattern](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller). Oh and also we should have a sane naming convention so that the Models, Views, and Controllers are naturally tied together. And finally let's put it all into a standard directory structure.

Add all that together and you have the perfect recipe for a new developer to come onto a project and instantly know their way around the code base. If you want to check out the views code you **always** know where that is in a rails project. Things like that speed up developer productivity **big time**.

## Best Practices

I have several things that I can reply with when someone asks me why I primarily use rails for development and one of those replies is 'Rails takes the industry best practices and folds them into the framework.'

Separation of concerns through Model, Views, and Controllers? Yeah we got that. Full test suites? [Of course](http://guides.rubyonrails.org/testing.html). REST is gonna be a big deal? Don't worry--[we're covered](http://guides.rubyonrails.org/routing.html). Loading the head section and assets each page refresh slowing down the mobile clients? How about [turbolinks](https://github.com/rails/turbolinks/)! And on and on and on...

By taking industry best practices and rolling them into the framework rails makes it easy to do the right thing. It start beginners out on solid footing and ensures that the farmhouse has a solid foundation and is built with the highest quality building materials.

## Rails source code

The two previous points were related to how rails encourages production of habitable software. Now I'd like to look at the [rails source code](https://github.com/rails/rails) and explore how it is quite habitable.

The first thing to note about Rails is that the framework is itself made up of several minor frameworks--ActionMailer, ActionPack, ActiveRecord, ActiveModel, and ActiveSupport. Each of these frameworks are themselves further broken down. For example ActionPack is made up of ActionDispatch, ActionView, AbstractController, and ActionController.

This illustrates the first way in which the rails source code is habitable--it's highly modular. At the same time the modules make logical sense and give the layout of the land so to speak.

## Directory Patterns

If you open any of the rails sub-frameworks you'll notice that they all share a few common features. First they are packaged as independant gems such that they can be used outside of rails and they can be swapped out for something else in the context of rails. That is another trait of habitable software. Rails is encouraging programmers to swap out/in the bits they need in order to feel at home and get the job done.

Notice that they all have the following

* Changelog
* License
* README
* TESTS_README
* Rakefile
* Gemspec
* test/
* lib/

In the `lib/` directory each framework has a single file which lists all the Modules contained within. There is also a directory named after the framework which holds all the individual modules in their own files. 

This directory pattern is an extremely powerful habitable trait of the rails source code. By breaking up the Modules and Classes into frameworks which are logically grouped and highly modular the rails source code has a sort of map which the programmer can mentally navigate in order to get to the code that matters in that moment.

## Summary

I've listed a few ways in which I think rails both encourages the production of habitable software as well as has highly habitable souce code itself. In part 2 I'll look at how rails uses idiomatic ruby to create code which is pleasant to live with.