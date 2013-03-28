---
layout: post
title: "Method naming oddness"
description: ""
category: 
tags: ['php', 'code']
---
{% include JB/setup %}

## Intro

Yesterday I got a new [Macbook](https://twitter.com/cgcardona/status/316707494510604290) Pro [w/ retina](http://www.apple.com/macbook-pro/features-retina/) display and while I was 'moving into'
it last night I noticed that it shipped with [PHP Version
5.3.15](http://www.php.net/releases/5_3_15.php). For several months I've been
meaning to checkout some features that shipped with [PHP 5.4](http://www.php.net/releases/5_4_0.php) and I figured that this would be the perfect time to upgrade.

After going to the PHP download page I noticed that the latest version of PHP is
currently [5.5.0](http://php.net/archive/2013.php#id2013-03-21-1). A couple of
stackoverflow threads pointed to [this package](http://php-osx.liip.ch/) as the easiest way to upgrade my
PHP version.

The upgrade was straight forward and painless and I am now running PHP version 5.5.0.

## You said something about oddness?

Oh yes I did didn't I? Well I noticed that if you create a class which with a
method name that is the same as the class and no constructor function then the
method with the same name as the class will get called when the object is
constructed. 

Let's look at some code to make it clearer.

## Code Example

```php
<?php
// example without constructor
class Base{
  public function base(){
    echo 'I was called!!!';
  }
}

$base = new Base();
// echos 'I was called!!!'
?>
```

It's easy to make it fail and to confirm that this is happening. Here we change
the function name to `ase`.

```php
<?php
// example without constructor
class Base{
  public function ase(){
    echo 'I was called!!!';
  }
}

$base = new Base();
// echos nothing
?>
```

Finally you can override this behavior by supplying a constructor method.

```php
<?php
// example with constructor
class Base{
  public function __construct(){
    echo 'constructor called';
  }
  public function base(){
    echo 'I was called!!!';
  }
}

$base = new Base();
// echos 'constructor called'
?>
```

## Summary

Ok I admit it's not the oddest behavior in the world. But it took me a minute to
debug exactly what was happening because my real world example Classes had many
more methods.

Obviously I can see this bug being annoying in cases like above where you have
no need of a constructor method but you accidentally have a poorly named method
in your class.
