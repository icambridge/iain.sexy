---
layout: post
title: "Hack: Types"
date: 2014-11-21 12:23
comments: true
categories: [development, hack, hacklang]
---
Facebook's Hack bring lots of features that a lot of other programming languages get to take advantage of. One of major advantages of Hack over PHP is a typing system. So here's a quick run over of the typing system as I understand it.

<!-- more -->

## List of basic types

Primitive are one most basic types that are used in most programming languages.

* string
* int - Integer
* float - Floating point
* bool - Boolean (True or False)
* array

Primitive Unions are types that can be used to describe other Primitive types that go together.
* num - integer or float
* arraykey - string or integer

Arrays while being a primitive type can be expanded to show what type of data they hold. You can also define the array key type. Instead of typing arrays like this you may want to look at using collections.

* array<string> - An array of strings
* array<string,int> - An array of integers indexed by a string




```php
<?hh
```

## Union Types

## Overriding return type signature

## Generics

## Type Aliases
