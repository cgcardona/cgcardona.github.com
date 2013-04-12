---
layout: post
title: "Keyword arguments in Ruby 2.0"
description: "Keyword arguments in Ruby 2.0"
category: 
tags: ['ruby', 'code']
---

## Intro

The first stable release of [Ruby 2.0](http://www.ruby-lang.org/en/news/2013/02/24/ruby-2-0-0-p0-is-released/) has
arrived and I'm checking out some of the added features.

With this post I'm checking out [keyword arguments](https://github.com/ruby/ruby/blob/2adb9fd4a51b054543cc40555718bd09901a324f/ChangeLog#L9627).
[Wikipedia defines](http://en.wikipedia.org/wiki/Named_parameter) as

> a computer language's support for function calls that clearly state the name of each parameter within the function call itself.

Before we get into that let's look at a couple other examples of Ruby methods
with parameters.

## Traditional method with parameters

First there's the traditional method with arguments.

```ruby
def create_profile(first_name, last_name)
  puts "first name: " + first_name
  puts "last name: " + last_name
end

create_profile 'Carlos', 'Cardona'
# first name: Carlos
# last name: Cardona
```

Nothing special here except to note if you pass in the wrong number of arguments
at the function call you'll get an error like so

```ruby
create_profile 'Cardona'
# ArgumentError: wrong number of arguments (1 for 2)
```

## Method with default parameter values

You can defend against that with default parameter values 

```ruby
def create_profile(first_name = "n/a", last_name = "n/a")
  puts "first name: " + first_name
  puts "last name: " + last_name
end

create_profile 'Cardona'
# first name: Cardona
# last name: n/a
```

Ok that prevented the `ArgumentError` but it incorrectly passed in `Cardona` as
the `first_name` argument and not the `second_name` argument. And that is where
keyword arguments really shine.

## Method with Keyword Arguments and default parameter values

Here you can see that we can pass in our arguments with a keyword. This allows
us to be more confident that our default parameter values will get assigned
correctly.

```ruby
def create_profile(first_name: "n/a", last_name: "n/a")
  puts "first name: " + first_name
  puts "last name: " + last_name
end

create_profile last_name: 'Cardona'
# first name: n/a
# last name: Cardona
```

At the same time it allows us to pass in arguments in a different order than
they were defined which makes the function call more fluid.

```ruby
create_profile last_name: 'Cardona', first_name: 'Carlos'
# first name: Carlos
# last name: Cardona
```
