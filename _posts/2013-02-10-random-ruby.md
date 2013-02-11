---
layout: post
title: "Random Ruby"
description: ""
category: 
tags: ['ruby', 'code']
---
{% include JB/setup %}

An initial impression that I've had of Ruby which has stayed true is that there
is often more than one way to do something. Just some random [Ruby](http://www.ruby-lang.org/en/) stuff I'm studying
tonight.

## Fun with Arrays

Two different ways to create an `Array`

    arr1 = Array.new # => []
    arr2 = []
    
Two different ways to push an item into an `Array`

    [].push 'foo' # => ['foo']
    [] << 'foo' # => ['foo']

Create an `Array` and push a `String` into it

    arr1 = Array.new.push 'Foobar' # => ['Foobar']
    arr2 = [] << 'Foobar' # => ['Foobar']
    arr3 = Array.new << 'Foobar' # => ['Foobar']

It's interesting to me that these are the same two statements

    Array.new << 'Foobar'
    Array.new.<<('Foobar')

Push all the contents of one array into another

    arr1 = [1,2,3]
    arr2 = [4,5,6]
    arr1.push *arr2 # => [1,2,3,4,5,6]

This is an interesting example from the homepage

    cities = %w[ Negril Bogota Caracas Paris Amsterdam Berlin]
    visited = %w[ Negril Amsterdam Caracas]
    puts "I still need to visit the following cities:", cities - visited

Split a `String` into an `Array`

    'foobar'.chars.to_a # => ['f','o','o','b','a','r']
    'foobar'.split(//) # => ['f','o','o','b','a','r']

## [String#<<](http://www.ruby-doc.org/core-1.9.3/String.html#method-i-3C-3C) and [Array#<<](http://www.ruby-doc.org/core-1.9.3/Array.html#method-i-3C-3C)

Both `Array` and `String` have a `<<` method. With regards to `Array` it's
basically like `push` and with `String` it's a concatenator. 

    [] << 'one' << 'two' << 'three' # => ['one', 'two', 'three']
    'one ' << 'two' # => 'one two'


## More info

* [Ruby Array](http://www.ruby-doc.org/core-1.9.3/Array.html)
* [Ruby String](http://www.ruby-doc.org/core-1.9.3/String.html)


