---
layout: post
title: "irb require shortcut"
description: ""
category: 
tags: ['ruby', 'irb']
---
## Intro

I've been doing more work with ruby so therefore I've been spending more time in
[irb](http://en.wikipedia.org/wiki/Interactive_Ruby_Shell).

`irb` is Ruby's interactive shell. It allows you to quickly bang out some Ruby
code from the command line.

This is just a quick note on a shortcut I found to `require` all your files from
one master file which cuts down on the number of manual `require`s.

## My standard work flow

First imagine that you have a couple of classes such as

### base.rb

```ruby
class Base
  def initalize
    puts "base class!!!!"
  end
end
```

### child.rb

```ruby
class Child < Base 
end
```

As you can see these classes are nothing special. For the sake of this example
they don't need to be.

Now imagine that you are firing up `irb` from your command line like so

`$ irb`

That will drop you into an interactive Ruby Shell. From there you could imagine
requiring each of your files and then creating an instance of the Child class

```ruby
irb(main):001:0> require "/Path/To/base.rb"
 => true
irb(main):002:0> require "/Path/To/child.rb"
 => true
irb(main):003:0> child = Child.new
base class!
 => #<Child:0x006e62cb2fbda2>
```

Of course that isn't too brutal but you can imagine a case where you have many
files that you want to `require` for your `irb` session. In this case the simple
solution is to create a file which as all the desired files required in it and
then simply `require` that one file in your `irb` session.

## Updated work flow

To start off we have the same two classes as before&mdash;`Base` and `Child`.
However now we're adding a third file called `requires.rb`.

This file acts as a wrapper that we include all of our other requires in like so

```ruby
require "/Path/To/base.rb"
require "/Path/To/child.rb"
```

Then from within your `irb` session just `require` your `requires.rb` file

```ruby
irb(main):001:0> require "/Path/To/require.rb"
 => true
irb(main):003:0> child = Child.new
base class!
 => #<Child:0x006e62cb2fbda2>
```

## Summary

So yeah I actually took the time to write up a post about requiring files for
`irb`. But the truth is it actually proves to be a really nice work flow when
working with a bunch of `require` statements in `irb`.
