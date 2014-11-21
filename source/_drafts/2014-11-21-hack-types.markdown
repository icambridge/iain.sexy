---
layout: post
title: "Hack: Types"
date: 2014-11-21 12:23
comments: true
categories: [development, hack  hacklang]
---
Facebook's Hack bring lots of features that a lot of other programming languages get to take advantage of. One of major advantages of Hack over PHP is a typing system. So here's a quick run over of the typing system as I understand it.

<!-- more -->

List of basic types

Primitive, one most basic types that are used in most programming languages.

* string
* int - Integer
* float - Floating point
* bool - Boolean (True or False)
* array

Primitive Unions, types that can be used to describe other Primitive types that go together.
* num - integer or float
* arraykey - string or integer

Array types, to define an array type you define an array then you use less than and greater than to surround the type that array is going to contain. If you want to define what kind of key is used you put that in the that type and the value type seperated by a comma.

* array<string> - An array of strings
* array<string,int> - An array of integers indexed by a string




```php
<?hh
```
