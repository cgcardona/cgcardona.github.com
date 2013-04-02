---
layout: post
title: "Getters and Setters?"
description: ""
category: 
tags: ['code', 'php', 'ruby', 'javascript', 'objectivec', 'cocoa']
---
## Intro

Abstraction and encapsulation are two sides of the same coin. Abstraction
focuses on the outside fundamental characteristics which define and distinguish
and object while encpasulation focuses on hiding the implementation of an
object's functionality; thereby freeing the Object's methods client or consumer 
of the need to understand the underlying complexity.

As far as a client is concerned an object is just a black box. It has methods
which can retrieve and update internal data but the internal implementation of all functionality should be completely
hidden.

And this is the way we want it. Information hiding is one of the reasons that
object oriented design scales to programming-in-the-colossal. It allows us to
free our minds of so many lower levels of complexity and only focus on the
highest levels of abstraction.

## Thoughts on getters and setters

It's often said that in a properly encapsulated object no outside entity could
directly access and/or change any of the object's instance variables.

### Objective-C & Cocoa

In Objective-C and Cocoa for example when you are defining the class's interface you can
have the compiler synthesize getter and setter methods like so

```objectivec
@interface Profile : NSObject
@property NSString *name;
- (id) initWithName:(NSString *) name;
@end

// Now imagine there is an implementation file for this interface with property
// and custom init method. Now to create a Profile object
Profile *myProfile = [[Profile alloc] initWithName:@"carlos cardona"];
```

That will handle creating two methods which allow me to access (get) and change
(set) the value of `name` like so

```objectivec
NSLog(@"%@", [myProfile name]);
// logs "carlos cardona"
[myProfile setName:@"soljah cardona"];
// changes name from "carlos cardona" to "soljah cardona"
```

There are ways to be more restrictive and only synthesize a getter.

### Ruby

Ruby is similar in the sense that you'll get an error if you try to get or set
an instance variable without declaring a getter and/or setter.

```ruby
class Profile
  def initialize(name)
    @name = name
  end
end

# now create a new Profile object
newProfile = Profile.new "carlos cardona"
# #<Profile:0x007ffc042fb040 @name="carlos cardona">

# now notice the fail if I try to get the value of name
newProfile.name
# NoMethodError: undefined method `name' for #<Profile:0x007ffc042fb040 @name="carlos cardona">

# the same thing if I try to set the value
newProfile.name = 'soljah cardona'
# NoMethodError: undefined method `name=' for #<Profile:0x007ffc042fb040 @name="carlos cardona">
```

You can manually create the getters and setters

```ruby
class Profile
  def initialize(name)
    @name = name
  end
  def name
    @name
  end
  def name=(name)
    @name = name 
  end
end
```

This works but it's verbose. Ruby gives us a more pleasant way to do it.

```ruby
class Profile
  attr_reader :name
  attr_writer :name
  def initialize(name)
    @name = name
  end
end
```

But of course Ruby takes it one step further

```ruby
class Profile
  attr_accessor:name
  def initialize(name)
    @name = name
  end
end
```

The `attr_reader`, `attr_writer`, and `attr_accessor` methods leverage Ruby's terse yet expressive
syntax to get more done with less code.

## Intermission #1

So far Objective-C and Ruby have shown good **language enforced** abstraction
and encapsulation. By design a property cannot be directly accessed and
manipulated. Only through getter and setter methods explicitly provided by a
Class's designer can a client of the object get access to state values.

It's worth a quick note on a couple specifics for later reference. In
Objective-C and Cocoa when you have the compiler synthesize accessor methods for
a property `foo` it will automatically give the getter and setter names `foo`
and `setFoo` respectively.

In Ruby both the getter and the setter share the name of the property `foo`. Ex:
`Profile.foo`

Now let's look at how PHP and Javascript do it.

## PHP

PHP has poor language enforcement with regards to abstraction and encapsulation
in this context.

A PHP Object's instance variables (when the visibility is `public`) are
avaliable via the property name similar to Ruby.

What is not similar to Ruby is that this behavior is on by default as opposed to
being turned on by the `attr_accessor` method.

```php
<?php
class Profile{
  public $name = 'carlos cardona';
}

// Create a Profile Object
$profile = new Profile();

// getter
var_dump($profile->name);
// string(14) "carlos cardona"  

// setter
$profile->name = 'soljah cardona';
var_dump($profile->name);
// string(14) "soljah cardona"
?>
```

Javascript acts the same way.

## Javascript

Javascript exhibits the same behavior as PHP in this context. It allows an
object's properties to be accessed and updated via the property name out of the
box. 

```javascript
<script>
function Profile(){
  this.name = 'carlos cardona';
}

// create a Profile Object.
var profile = new Profile();

// getter
console.log(profile.name);
// carlos cardona

//setter
profile.name = 'soljah cardona';
console.log(profile.name);
// soljah cardona
<script>
```

## Final Thoughts

There are really two ways to consider this. 

### Side One

First is to say with regards to Abstraction and Encapsulation in the context of an Object's publicly visible
properties via accessor methods Objective-C and Ruby exhibit better default
behavior compared to PHP and Javascript.

This argument would be based on the fact that both Objective-C and Ruby require
the developer to explicitly allow the client of the Object to have access to
it's properties. Even then that access is only available via a method and never
directly as seen in Objective C's `setPropertyName` method.

PHP and Javascript on the other hand allow direct access and manipulation of an
Objects public properties by default thus they exhibit inferior behavior.

### Side Two

The other way to consider this is that the true expressive power of javascript
comes from it's dynamic nature. The ceremony that comes with allowing someone to
access a property is just baggage. 

After all doesn't Ruby just generate getter and setter methods which are the
name of the property? That's what both javascript and PHP do out of the box!

## More info

* [What is attr_accessor in Ruby?](http://stackoverflow.com/questions/4370960/what-is-attr-accessor-in-ruby)
