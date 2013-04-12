---
layout: post
title: "Globally scoped methods in Ruby"
description: ""
category: 
tags: ['ruby', 'code']
---

## Intro

Just reading the [Wikipedia entry on Ruby](http://en.wikipedia.org/wiki/Ruby_(programming_language#Semantics) and
found out this interesting bit of semantics.

> Every function is a method and methods are always called on an object. Methods
> defined at the top level scope become members of the Object class. Since this
> class is an ancestor of every other class, such methods can be called on any
> object. They are also visible in all scopes, effectively serving as "global"
> procedures.

That's a pretty interesting concept&mdash;that any globally scoped methods get
encapsulated in the `Object` class.

## Globals Considered Harmful

We learned long ago that Globally accessable data is a fail. Abstraction and
encapsulation give us the tools we need to properly implement information
hiding.

So having it cooked into the language that any globally scoped function is just
a method on the `Object` class is good out of the box Object Oriented behavior
of which I approve.

## Code Example

```ruby
def globally_scoped_method
  puts "This is a globally scoped method."
end

class MyClass < Object
  def initialize
    globally_scoped_method
  end
end

myClass = MyClass.new
# Logs: This is a globally scoped method.
```

It's important to note that `globally_scoped_method` is added as a `private`
method of the `Object` class. Therefore it would be impossible to call it like
so

```ruby
def globally_scoped_method
  puts "This is a globally scoped method."
end

class MyClass < Object
  def initialize
  end
end

myClass = MyClass.new
myClass.globally_scoped_method
# NoMethodError: private method `globally_scoped_method' called for #<MyClass:0x016ff23dc23832>
```
