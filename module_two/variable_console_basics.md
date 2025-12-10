# Variable and Console Basics

## Exploring a Hello-world Project

Let's start by exploring the following program.

```c#
// Program.cs

namespace HelloWorld;

internal static class Program
{
    private static void Main()
    {
        Console.WriteLine("Hello, world!");
    }
}
```

This program prints "Hello, world!" to the console, but there's so much code here, it's hard to believe that's all 
it does. Nearly all of this code is *boilerplate code*. Boilerplate code is code that we have to write because we're 
required to, not because it does anything specific for our project. In modern C#, we can actually use what are 
called *top-level statements* to avoid writing all of this boilerplate code. This is to make it easier to create 
simple applications. This doesn't mean C# no longer needs the boilerplate code, it means C# generates it for us. 
In this course, we're always going to write this boilerplate code since this is how C# really works, so it's 
important to see it.

Since we'll be writing it for all our projects, let's go through each part and figure out what it's doing at a basic 
level. We'll learn about each of these constructs in more detail as we move throughout the course.

```c#
namespace HelloWorld;
```

This declares that the entities in the current file are part of the `HelloWorld` namespace. Namespaces are a way to 
group entities under one name. C# doesn't allow for two entities to have the same name, so namespaces help qualify 
names so we don't have to worry about potentially using the same name as something else in C# or in someone else's 
library.

Let's say we have some entity `Entity` in one file and another entity also called `Entity` in another file. If we 
put the first entity in a namespace called `A` and the second in a namespace called `B`, we won't have a problem 
since the first entity is now `A.Entity` and the second entity is now `B.Entity`.

The general convention when it comes to naming namespaces is that they should reflect the project structure. Since
the above code is from a project called `HelloWorld`, the namespace is also called `HelloWorld`. Rider will
automatically create the correct namespace declaration for you, so you don't have to worry about getting it right.
It's worth noting that namespaces are not required to follow this convention. This convention is generally a good
convention to follow, but there may be reasons to not follow it in certain circumstances, so you may see some
libraries not following it.

```c#
internal static class Program {}
```

This declares a class called `Program`. It's not important to understand classes right now, or what the other 
keywords do, but you should know that all code aside from top-level declarations must go inside a class.

```c#
private static void Main() {}
```

This is the main method for your program, and it serves as the entry point. All C# executables must have a `Main` 
method of some kind. We'll learn about methods later in the course, so don't worry about understanding them just yet.

```c#
Console.WriteLine("Hello, world!");
```

This is a C# print statement. It prints the text "Hello, world!" to the console followed by a newline. This is the 
print statement you'll use most of the time.

C# requires semicolons at the end of all statements. This tells the compiler when a thought is complete.

## Comments

```c#
// Single-line comment.
/*
Multi-line
comment.
*/
```

The above code shows how to write single-line and multi-line comments. Multiline are only used in a few select 
situations, so you should stick to single-line comments. Single-line comments last from `//` to the end of the line. 
Multi-line comments last from `/*` to `*/`.

## Basic Data Types

The following table shows the basic C# data types and some information about them.

| Type      | Alias     | Size in Bits | Zero Value | Classification                      |
|-----------|-----------|--------------|------------|-------------------------------------|
| `Boolean` | `bool`    | 8            | `false`    | Integral                            |
| `Byte`    | `byte`    | 8            | `0`        | Integral                            |
| `SByte`   | `sbyte`   | 8            | `0`        | Integral                            |
| `Char`    | `char`    | 16           | `'\0'`     | Unicode (UTF-16)                    |
| `Int16`   | `short`   | 16           | `0`        | Integral                            |
| `UInt16`  | `ushort`  | 16           | `0`        | Integral                            |
| `Int32`   | `int`     | 32           | `0`        | Integral                            |
| `UInt32`  | `uint`    | 32           | `0U`       | Integral                            |
| `Single`  | `float`   | 32           | `0.0F`     | Binary Floating-point (binary32)    |
| `Int64`   | `long`    | 64           | `0L`       | Integral                            |
| `UInt64`  | `ulong`   | 64           | `0UL`      | Integral                            |
| `Double`  | `double`  | 64           | `0.0`      | Binary Floating-point (binary64)    |
| `Decimal` | `decimal` | 128          | `0.0M`     | Decimal Floating-point (decimal128) |
| `String`  | `string`  | Unspecified  | `""`       | Unicode Sequence (UTF-16)           |

Each of the above types has an alias. These aliases are simply other names for the types. These aliases allow us to 
use more common names for these types, so they are preferred. For example, `int` should be preferred over `Int32`.

The following table includes newer basic types that extend the existing basic types. While these types are still 
basic types, you won't really use them much. This table is mainly for completion so you know what they are if you 
see code that uses them.

| Type      | Size in Bits | Zero Value     | Classification                   |
|-----------|--------------|----------------|----------------------------------|
| `Half`    | 16           | `(Half)0.0F`   | Binary Floating-point (binary16) |
| `Int128`  | 128          | `(Int128)0L`   | Integral                         |
| `UInt128` | 128          | `(UInt128)0UL` | Integral                         |

Let's go over the type classifications

### Integral

Integral types are used for storing integers. If there is a "u" in a type, it means *unsigned*. Unsigned integral 
types don't allow for negative numbers. These types are useful because you double the number of positive numbers you 
can store for the same size. If you don't care about negatives, this can reduce the size of the data type you need.

### Floating-point

Floating-point types are used for representing rational and irrational numbers (approximated). C# follows the 
IEEE-754 standard for floating-point numbers, which is what most languages follow. In this course, we won't worry about 
how floating-point numbers are stored, but you are welcome to investigate this if you want to!

#### Binary Floating-point

Binary floating-point types store values in binary. These types are subject to errors due to the conversion from 
decimal to binary. These types should not be used when accuracy is critical.

#### Decimal Floating-point

Decimal floating-point types store values in decimal. These types are used where accuracy matters. The most common 
type of value these types are used to represent is a monetary value like a balance or a price.

### Unicode

Unicode is how computers encode characters. Unicode replaced ASCII when computers started needing to be able to 
represent more than 128 unique characters. There are four versions of Unicode: UTF-8, UTF-16, and UTF-32. We won't 
be getting into Unicode in this course, but it's worth noting that C# uses UTF-16, which means characters are 
represented using either 16 bits or 32 bits.

### Primitive vs. Non-primitive Types

Except for `string`, the above types are all considered *primitive types*. Primitive types represent numbers. These 
are the foundational building blocks of other types. These other types are considered *non-primitive types* since 
they are built out of primitive types. `string` is an example of a non-primitive type since it's a sequence of `char`s.

C# doesn't meaningfully distinguish between primitive and non-primitive types, however. They are both equally 
supported by the language. Instead, C# distinguishes types based on whether they have *value semantics* or 
*reference semantics*. All above types besides `string` have value semantics; `string` has reference semantics. We 
will discuss these concepts later, so it's good enough for now to know the semantics for the above types.

## Variables

The syntax for variables in C# is as follows.

```c#
<type> <name> = <value>;
```

Let's say we want to declare an `int` variable. The following code shows how to do this.

```c#
int number = 5;
```

### Naming Conventions

C# uses camelCase for naming local variables. C# also prefers using full words over abbreviations. That's why the 
above variable was named `number` instead of `num`. When it comes to acronyms and initialisms, they should only be
used when widely recognized. They should also act like words when it comes to capitalization. The following code
demonstrates proper capitalization of acronyms and initialisms in C#.

```c#
uint idNumber = 1; // all lowercase at beginning
uint studentId = 2; // first letter capitalized when in middle or at end
```

### `var` keyword

The `var` keyword can be used in place of a type to have C# deduce the type from the right-hand side. You should use 
the `var` keyword whenever the type is obvious, or when the readability of your code can be enhanced. This means the 
following is preferred.

```c#
var number = 5;
```

This keyword will also allow us to avoid repeating data types later on when we start using other data types.

## Constants

Constants are variables whose values are known at compile-time and whose values won't change. This essentially means 
you can only assign literal values to constants. Some computation can be done at compile-time as long as the 
arguments are also constants. The following code demonstrates creating a local constant.

```c#
const double g = 9.81;
```

Type deduction is not allowed when declaring a constant, so `var` can't be used. When C# compiles your code, it will 
copy the values in each constant and paste them wherever the constants are used. This is why constant values have to 
be known at compile-time. The following code shows how C# processes constants.

```c#
// This is the code as written.
const double g = 9.81;
Console.WriteLine(g);

// This is the code C# will compile.
Console.WriteLine(9.81);
```

Constants should be used whenever possible since they won't actually exist at runtime.

## Console Output

The following code demonstrates the two methods we can use to output text to the console.

```c#
Console.WriteLine("Hello, world!");
Console.Write("Hello, ");
Console.WriteLine("world!");
```

The above code produces the following output.

```text
Hello, world!
Hello, world!
```

The `Console.WriteLine` method outputs text followed by a newline character. The `Console.Write` method outputs text 
with no trailing newline.

## Interpolated Strings

It's very common to want to insert values into strings. C# supports string concatenation, so we could output the 
value of a variable as shown in the following code.

```c#
const int luckyNumber = 7;
Console.WriteLine("I think " + luckyNumber + " is my lucky number!");
```

While this works, it can be hard to keep track of where to put spaces to make sure the output looks right. It can 
also become fairly unreadable when a lot of concatenation is used. To solve this problem, C# offers *interpolated 
strings* which are strings that can process code expressions. The following code shows how to use string 
interpolation to do the same thing as the above code.

```c#
const int luckyNumber = 7;
Console.WriteLine($"I think {luckyNumber} is my lucky number!");
```

Interpolated strings are created by prepending a `$` to a string literal. C# expressions can then be put inside 
curly brackets.

We can also do formatting with interpolated strings which we'll look at later. Interpolated strings should be 
preferred over string concatenation.

## Console Input

### Getting String Input

We use the `Console.ReadLine` method to get input in C#. The following code demonstrates how to use this method.

```c#
Console.Write("Enter your name: ");
string name = Console.ReadLine()!;
Console.WriteLine($"It's nice to meet you, {name}!");
```

The `Console.ReadLine` method will pause the program until the user types something into the console and presses the 
RETURN key. The code will the proceed as normal.

You may notice the strange `!` at the end of the call to `Console.ReadLine`. This is to silence a warning about 
converting a possible null value to a non-nullable type. We'll learn about nullable types a little later in the course,
so for now, add `!` after any call to `Console.ReadLine` where you get this warning.

### Getting Input of Other Types

`Console.ReadLine` always returns `string`, so what do we do if we want to accept an integer? We use C# conversion 
methods to convert string input to other types. The following code shows how to accept integer input.

```c#
Console.Write("Enter your age: ");
var age = Convert.ToByte(Console.ReadLine());
Console.WriteLine($"You're {age} year(s) old");
```

There are conversion methods for converting from a string to every other basic type. Note that the method names use 
the actual names of the types, not the aliases. Additionally, each conversion method will throw an exception if it's 
not possible to convert the string to the requested type. This is a problem if we want our code to handle bad input. 
We'll learn how to deal with this in a later module, so for now, assume the user always enters input perfectly.

You now know enough to create a basic chatbot!
