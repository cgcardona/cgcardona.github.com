---
layout: post
title: "Highlighting some Object functions in underscorejs"
description: ""
category: 
tags: ['javascript', 'underscorejs', 'code']
---
{% include JB/setup %}

As I [mentioned previously](/2013/02/20/some-handy-new-javascript-features/)
[javascript](https://developer.mozilla.org/en-US/docs/JavaScript) has a lightweight standard library. As I became more familiar with
[PHP](http://www.php.net/manual/en/index.php) I often became frustrated that
javascript didn't have an equivalent to PHP's `is_*` such as `is_array`,
`is_object`, etc.

Yet the browser is the biggest development environment in history so clearly I'm
not the only one who feels this pain point. The makers of the
[underscore.js](http://underscorejs.org/) have done a fine job of solving the
problem.

## is array?

### PHP

[is_array](http://www.php.net/manual/en/function.is-array.php)

Validates an `array`.

```php
<?php
$arr = array('one','two');
var_dump(is_array($arr));
// bool(true)
?>
```

### underscore.js

[isArray](http://underscorejs.org/#isArray)

Validates an `array`.

```javascript
<script>
console.log(_.isArray(['one','two']));
// true
</script>
```

## is boolean?

### PHP

[is_bool](http://www.php.net/manual/en/function.is-bool.php)

```php
<?php
var_dump(is_bool(true));
// bool(true)
?>
```

### underscore.js

[isBoolean](http://underscorejs.org/#isBoolean)

```javascript
<script>
console.log(_.isBoolean(true));
// true
</script>
```

## is a number?

### PHP

PHP has a few methods because it handles numbers different than javascript.

[is_numeric](http://www.php.net/manual/en/function.is-numeric.php) handles
numbers and numeric strings

```php
<?php
var_dump(is_numeric(42));
// bool(true)
var_dump(is_numeric('42'));
// bool(true)
?>
```

[is_float](http://www.php.net/manual/en/function.is-float.php) handles float
value validation.

```php
<?php
var_dump(is_float(3.15));
// bool(true)
?>
```

[is_integer](http://www.php.net/manual/en/function.is-integer.php) handles
validating integers.

```php
<?php
var_dump(is_integer(3));
// bool(true)
?>
```

### underscore.js

[isNumber](http://underscorejs.org/#isNumber)

`isNumber` handles checking for integers as well as floats. What it does not ddo
that it's PHP counterpart does is validate numeric string like '42'.

```javascript
<script>
console.log(_.isNumber(42));
// true

console.log(_.isNumber('42'));
// false

console.log(_.isNumber(3.15));
// true
</script>
```

## is null?

### PHP

[is_null](http://www.php.net/manual/en/function.is-null.php)

Checks if a value is `NULL` or `null` but not another bottom value like `false`, an empty string`

```php
<?php
var_dump(is_null(NULL));
// bool(true)
?>
```

### underscore.js

[isNull](http://underscorejs.org/#isNull)

```javascript
<script>
console.log(_.isNull(null));
// true
console.log(_.isNull(undefined));
// false
console.log(_.isNull(''));
// false
console.log(_.isNull(false));
// false
console.log(_.isNull(0));
// false
</script>
```

## is object?

### PHP

[is_object](http://www.php.net/manual/en/function.is-object.php)

This will validate PHP System objects as well as objects that you define yourself

```php
<?php
class FooClass{
  public function __construct(){}
}
var_dump(is_object(new FooClass()));
// bool(true)
var_dump(is_object(new stdClass()));
// bool(true)
?>
```

### underscore.js

[isObject](http://underscorejs.org/#isObject)

This will validate object literals, objects created with the constructor
pattern, and objects created with `Object.create()`.

```javascript
<script>
function FooClass(){}

var fooObject = new FooClass();
console.log(_.isObject(fooObject));
// true
console.log(_.isObject(Object.create(fooObject)));
// true
console.log(_.isObject({}));
// true
</script>
```

## is string?

### PHP

[is_string](http://www.php.net/manual/en/function.is-string.php)

Validates a `string`.

```php
<?php
var_dump(is_string('this is a string'));
// bool(true)
?>
```

### underscore.js

[isString](http://underscorejs.org/#isString)

Validates a `string`.

```javascript
<script>
console.log(_.isString('this is a string'));
// true
</script>
```
