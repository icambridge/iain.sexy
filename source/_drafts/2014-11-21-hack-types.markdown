---
layout: post
title: "Hack: Types"
date: 2014-11-21 12:23
comments: true
categories: [development, hack, hacklang]
---
Facebook's Hack bring lots of features that a lot of other programming languages get to take advantage of. One of major advantages of Hack over PHP is a typing system. So here's a quick run over of the typing system as I understand it.

<!-- more -->

## Annotate


```php
<?hh
```

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

Classes and interfaces, if a class or interface exists in the code that's being executed then it's a type that you can use for type annotations.

Other basic types

* mixed - Will take anything
* void - Nothing it means there is no type, this is generally used
* resource -
* closure - syntax `(function(typeOne, typeTwo, ...): returnType)`
* tuples - syntax `tuple(typeOne, typeTwo)`

## Generics

Sometimes you want your code to work with any type. In those cases we can use type generics. Generics can be defined on a class or on a method. To define a generic you wrap the name of the generic with less than and greater than in either the class definition or the method definition.  

When naming it you should remember can't use the name of a type that already exists. It's a general rule of thumb that you start your generic type with `T` and for real simple use cases `T` alone is fine. With collections it's advised to use `Tk` for the key and `Tv` for the value.

```php
<?hh

namespace Examples;

class Value<T>
{
  public function __construct(private T $value) {}

  public function get(): T {
    return $this->private;
  }
}

class Constraint
{
    public function isEqual<T>(T $valueOne, T $valueTwo) {
      return ($valueOne == $valueTwo);
    }
}
```

## Overriding return type signature

## Type Aliases
