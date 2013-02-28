---
layout: post
title: "The Object Model"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I'm reading [Object-Oriented Analysis and Design with Applications](http://www.amazon.com/Object-Oriented-Analysis-Design-Applications-3rd/dp/020189551X)
and just wanted to get down a few quotes from **Chapter 2 The Object Model**.

## Foundations of The Object Model

### OOP

> **Object-oriented programming** is a method of implementation in which programs are
> organized as cooperative collections of objects, each of which represents an
> instance of some class, and whose classes are all members of a hierarchy of
> classes united via inheritance relationships.

### OOD

> **Object-oriented design** is a method of design encompassing the process of
> object-oriented decomposition and a notation for depicting both logical and
> physical as well as static and dynamic models of the system under design.

### OOA

> **Object-oriented analysis** is a method of analysis that examines requirements
> from the perspective of the classes and objects found in the vocabulary of the
> problem domain.

## Four major elements

There are four major elements of The Object Model

### Abstraction

> An **abstraction** denotes the essential characteristics of an object that
> distinguish it from all other kinds of objects and thus provide crisply defined
> conceptual boundaries, relative to the perspective of the viewer.

### Encapsulation

> **Encapsulation** is the process of hiding all of the details of an aobject that do
> not contribute to its essential characteristics.

### Modularity

> **Modularity** is the property of a system that has been decomposed into a set of
> cohesive and loosely coupled modules.

### Hierarchy

> **Hierarchy** is a ranking and ordering of abstractions.

## Three minorelements

There are three minor elements of The Object Model

### Typing

> **Typing** is the enforcement of the class of an object, such that objects of
> different types may not be interchanged, or at most, they may be interchanged
> only in very restricted ways.

### Concurrency

> **Concurrency** is the property that distinguishes an active object from one that
> is not active.

### Persistence

> **Persistence** is the proeprty of an object through which its existence trancends
> time (i.e. the object continues to exist after its creator ceases to exists)
> and/or space (i.e. the object's location moves from the address space in which
> it was created).
