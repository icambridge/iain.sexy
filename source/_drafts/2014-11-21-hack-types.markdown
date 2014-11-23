---
layout: post
title: "Hack: Types"
date: 2014-11-22 12:23
comments: true
categories: [development, hack, hacklang]
---
Facebook's Hack bring lots of features that a lot of other programming languages get to take advantage of. One of major advantages of Hack over PHP is a typing system. So here's a quick run over of the typing system as I understand it.

<!-- more -->

## Annotate

Annotating when you define which type is going to be used. You can type the follow:

* function arguments
* function return
* class variable
* constants

To define the types in function arguments you just put the type before the variable name for the argument.

```php
<?hh

function example(TypeOne $typeOne, int $anInteger){}

```

To define the return type you just put `: type` in between the function definition and the function body.

```php
<?hh

function returnsTrue(): bool { return true; }
```

Constants you just put the type in between the `const` keyword and the constant name.

```php
<?hh

const int NUMBER_NINE = 9;
```

Class variables you just put the type in between the scope keyword and the variable name.

```php
<?hh

class Example {
  private int $numberNine = 9;
}

```

## List of basic types

Primitive are one most basic types that are used in most programming languages.

* `string`
* `int` - Integer
* `float` - Floating point
* `bool` - Boolean (True or False)
* `array`

Primitive Unions are types that can be used to describe other Primitive types that go together.
* `num` - integer or float
* `arraykey` - string or integer

Arrays while being a primitive type can be expanded to show what type of data they hold. You can also define the array key type. Instead of typing arrays like this you may want to look at using collections.

* `array<string>` - An array of strings
* `array<string,int>`  - An array of integers indexed by a string

Classes and interfaces, if a class or interface exists in the code that's being executed then it's a type that you can use for type annotations.

Other basic types

* `mixed` - Will take anything
* `void` - Nothing it means there is no type, this is generally used
* `resource` 
* closure - syntax `(function(typeOne, typeTwo, ...): returnType)`
* tuples - syntax `tuple(typeOne, typeTwo)`

A full list can be found in [hack annotations docs](http://docs.hhvm.com/manual/en/hack.annotations.usingtypes.php).

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
    return $this->value;
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

When you extend a class you are able to override the return type for methods you override. However the new type must be compatible with the original type. So in other word the type must be a child type of the original type.

So say you originally typed it `Foo` you couldn't then change the type to `bool`. As that's not a compatable type of `Foo`. However if you created a child class of `Foo` called `Fooable` you would be able to use that as a type. So your code still actually follows the orignal return signature it's just more detailed.
