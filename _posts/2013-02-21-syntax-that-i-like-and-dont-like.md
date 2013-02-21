---
layout: post
title: "Syntax that I like and don't like"
description: ""
category: 
tags: ['code']
---
{% include JB/setup %}

## Syntax that I like

I really like dot notation. I like it when methods are encapsulated within objects. 

### Pseudo code 

`Object.method` 

### Examples in languages:

#### [Javascript](https://developer.mozilla.org/en-US/docs/JavaScript)

```javascript
console.log('foobar'.length);
// 6
 ```

#### [Ruby](http://www.ruby-lang.org/en/)

```ruby
puts 'foobar'.length
// 6
```

## Syntax that I don't like

I dislike functions which are global in nature. PHP has over 5000 of such
functions. These are problematic because that is over 5000 chances that a
developer will write over that global function name. 

Thankfully PHP will at least give you a fatal error: `Fatal error: Cannot
redeclare is_array()` but there is still too high of a chance that a new dev
might not have the `error_reporting` and `display_errors` options configured
correctly in their `php.ini` file.

BTW you can replace a built in PHP function definition with a new implementation
with [runkit function define](a function definition with a new implementation)
from [the runkit extension](http://no2.php.net/manual/en/book.runkit.php).

### Pseudo code 

`function_name(Object);` 

### Examples in a language:

#### [PHP](http://www.php.net/manual/en/index.php)

```php
echo strlen('foobar');
// 6
```
