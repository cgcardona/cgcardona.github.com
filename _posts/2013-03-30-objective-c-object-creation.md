---
layout: post
title: "Objective C Object Creation"
description: ""
category: 
tags: ['objective c', 'code']
---
{% include JB/setup %}

## Intro

I'm learning Objective C for a native OSX project that I'm working on. Here are
some quick notes about creating objects.

## The way that I don't prefer

The first way is to call two `NSObject` methods

1. `(id)alloc`
2. `(id) init`

This best way is to nest them so that you can be sure you're calling the `init`
method on the newly allocated object.

```objectivec
CustomObject customObject = [[CustomObject alloc] init];
```
Some Objects accept a variation on the `init` method:

```objectivec
- (id)initWithBool:(BOOL)value;
- (id)initWithFloat:(float)value;
- (id)initWithInt:(int)value;
- (id)initWithLong:(long)value;

CustomObject customObject = [[CustomObject alloc] initWithBool:YES];
```

However that seems really nasty to me. Thankfully there is a shortcut `(id)new`
method on `NSObject` which is better suited to my javascript tastes.

```objectivec
CustomObject customObject = [CustomObject new];
```

## The way that I prefer

Some Objects have factory methods which I much prefer. They allow you to both
allocate memory for an Object as well as initialize it with variables.

`NSNumber` is a good example. 

```objectivec
+ (NSNumber *)numberWithBool:(BOOL)value;
+ (NSNumber *)numberWithFloat:(float)value;
+ (NSNumber *)numberWithInt:(int)value;
+ (NSNumber *)numberWithLong:(long)value;

NSNumber *myNum = [NSNumber numberWithInt:32];
```

This accomplishes the same think as nesting the `alloc` and `initWithInt`
messages but is much more readable.

## More info

[Apple Developer
Docs](http://developer.apple.com/library/ios/#documentation/cocoa/conceptual/ProgrammingWithObjectiveC/WorkingwithObjects/WorkingwithObjects.html#//apple_ref/doc/uid/TP40011210-CH4-SW1)
