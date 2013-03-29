---
layout: post
title: "Traits and Shortened Array Syntax"
description: ""
category: 
tags: ['php', 'code']
---
{% include JB/setup %}

## Intro

Just a quick post to introduce two new features that got introduced with [PHP Version 5.4.0](./_posts/2013-03-28-traits-and-shortened-array-syntax.md). Namely
traits and shortened array syntax.

## Traits

[Traits](http://php.net/traits) are a code reuse mechanism for single
inheritance languages like PHP. It allows a developer to share code between
classes which aren't in the same class hierarchy. It's similar in concept to
modules or mixins in other languages.

Let's see some code:

```php
<?php
// A trait shares the same sytax as a class.
trait Base{
  public function run(){
    echo 'Generic running!!!';
  }
}

class Human{
// include a trait in a class with the `use` keyword
  use Base;
}

class Car{
  use Base;
// including a method of the same name as a method in the trait will cause the
// local method to override the trait's method. 
  public function run(){
    echo 'Running like a car';
  }
}

$human = new Human();
$human->run();
// echos 'Running!!!'

$car = new Car();
$car->run();
// echos 'Running like a car'
?>
```

## Shortened Array Syntax

Creating an array by using the `Array` keyword has always seemed a little dated
to me. Ex:

```php
<?php
$arr = Array('one', 'two', 'three');
// array(3) { [0]=> string(3) "one" [1]=> string(3) "two" [2]=> string(5) "three" }
?>
```

As of PHP 5.4.0 there is a javascriptesque array literal syntax. Ex:

```php
<?php
$arr = ['one', 'two', 'three'];
// array(3) { [0]=> string(3) "one" [1]=> string(3) "two" [2]=> string(5) "three" }
?>
```
It's only a saving of 5 characters but it feels much nicer.
