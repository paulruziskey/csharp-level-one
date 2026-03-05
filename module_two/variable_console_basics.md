# Variable and Console Basics

## Exploring a Hello-world Project

```c#
Console.WriteLine("Hello, world!");
```

This is a C# print statement. It prints the text "Hello, world!" to the console followed by a newline. This is the 
print statement you'll use most of the time.

## Comments

```c#
// Single-line comment.
/*
Multiline
comment.
*/
```

The above code shows how to write single-line and multiline comments. Multiline comments are only used in a few select 
situations, so you should stick to single-line comments. Single-line comments last from `//` to the end of the line. 
Multiline comments last from `/*` to `*/`.

## Basic Data Types

The following table shows the basic C# data types and some information about them.

| Type      | Alias     | Size in Bits | Zero Value | Classification                      |
|-----------|-----------|--------------|------------|-------------------------------------|
| `Boolean` | `bool`    | 8            | `false`    | Integral                            |
| `Byte`    | `byte`    | 8            | `0`        | Integral                            |
| `SByte`   | `sbyte`   | 8            | `0`        | Integral                            |
| `Char`    | `char`    | 16           | `'\0'`     | Integral, Unicode (UTF-16)          |
| `Int16`   | `short`   | 16           | `0`        | Integral                            |
| `UInt16`  | `ushort`  | 16           | `0`        | Integral                            |
| `Int32`   | `int`     | 32           | `0`        | Integral                            |
| `UInt32`  | `uint`    | 32           | `0U`       | Integral                            |
| `Single`  | `float`   | 32           | `0.0F`     | Binary Floating-point (binary32)    |
| `Int64`   | `long`    | 64           | `0L`       | Integral                            |
| `UInt64`  | `ulong`   | 64           | `0UL`      | Integral                            |
| `Double`  | `double`  | 64           | `0.0`      | Binary Floating-point (binary64)    |
| `Decimal` | `decimal` | 128          | `0.0M`     | Decimal Floating-point (decimal128) |
| `String`  | `string`  | Unspecified  | `null`     | Unicode Sequence (UTF-16)           |

Each of the above types has an alias. These aliases are simply other names for the types. These aliases allow us to 
use more common names for these types, so they are preferred. For example, `int` should be preferred over `Int32`.

The zero values for each type are whatever value is considered to be the equivalent of 0 for a given type. For numeric 
types, this is pretty straightforward. For `bool` and `char`, things are a little more interesting. For booleans, 
between `true` and `false`, `false` is the closest to 0. For characters, '\0' is called the *null character*. This is 
simply the character represented by 0.

`string` is the most interesting since its zero value is the only one that doesn't represent a valid value for the 
type. If you tried to do anything with a null string, you would get a `NullReferenceException`. This is because `null` 
is not the same thing as an empty string. We'll learn more about what `null` is and why the `string` type is different 
from the rest later in the course, so for now, just think of it as another data type.

The following table includes newer basic types that extend the existing basic types. While these types are still 
basic types, you won't really use them much. This table is mainly for completion so you know what they are if you 
see code that uses them.

| Type      | Size in Bits | Zero Value     | Classification                   |
|-----------|--------------|----------------|----------------------------------|
| `Half`    | 16           | `(Half)0.0F`   | Binary Floating-point (binary16) |
| `Int128`  | 128          | `(Int128)0L`   | Integral                         |
| `UInt128` | 128          | `(UInt128)0UL` | Integral                         |

The syntax for the zero values for these types is a bit strange because C# doesn't have dedicated literals for these 
types. These types were added after the original types, so the language wasn't originally built for them. We'll learn 
more about this syntax in the next lesson.

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
represent more than 128 unique characters. There are three versions of Unicode: UTF-8, UTF-16, and UTF-32. We won't 
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

### Declaring and Initializing Variables

C# requires us to declare variables before we can use them. The following shows the syntax for declaring a variable in 
C#.

```c#
<type> <name>;
```

If we want to declare an `int` variable called `number`, the following code would do so.

```c#
int number;
```

This tells C# to create a variable called `number` which stores 32-bit integers and reserve memory for it. All 
variables in C# are *zero-initialized*, which means they are automatically assigned the zero value for the type.

Given the following code, what should be printed to the console?

```c#
int number;
Console.WriteLine(number);
```

Unfortunately, the code above won't compile. This is because C# requires us to manually initialize all local variables, 
even though they're zero-initialized. This means you have to make sure to assign your variables values before you can 
read their stored values. The following shows the syntax for assigning a value to a variable. If we are assigning a 
value to a variable for the first time, we call it *initializing* a variable because we are assigning it its initial 
value.

```c#
<name> = <value>;
```

We could update the code above to initialize the `number` variable before attempting to print its value.

```c#
int number;
number = 5;
Console.WriteLine(number);
```

The above code outputs the following to the console.

```text
5
```

The `=` operator is known as the *assignment operator*. Be careful to avoid calling it the "equals operator" or 
anything similar since that actually refers to a different operator.

Since we always need to initialize our variables, it would be a bit silly if we always had to do it on a separate line. 
C# allows us to both declare and initialize variables using the following syntax.

```c#
<type> <name> = <value>;
```

We could update the above code to put the declaration and initialization of `number` on the same line.

```c#
int number = 5;
Console.WriteLine(number);
```

You will mostly declare and initialize variables on the same line, but there will be times where you only want to 
declare a variable, so keep both types of syntax in mind.

### Naming Conventions

C# uses camelCase for naming local variables. C# also prefers using full words over abbreviations. That's why the 
above variable was named `number` instead of `num`. When it comes to acronyms and initialisms, they should only be
used when widely recognized. They should also act like words when it comes to capitalization. The following code
demonstrates proper capitalization of acronyms and initialisms in C#.

```c#
uint idNumber = 1; // all lowercase at beginning
uint studentId = 2; // first letter capitalized when in middle or at end
```

### Using Keywords as Variable Names

There may be times when you wish to use a name for a variable, but you can't because it's reserved by the language. 
This usually isn't a problem, but if you have a really good reason for needing to use a keyword as a variable name, you 
can prepend the *verbatim identifier* (`@`) to the name. The following code demonstrates using the `string` keyword 
as a variable name.

```c#
string @string = "hello";
Console.WriteLine(@string);
```

The above code outputs the following to the console.

```text
hello
```

This is a bad example for why you would want to do this since the name `string` doesn't say anything about the purpose 
of the variable, but it illustrates how you would do it.

### `var` keyword

The `var` keyword can be used in place of a type to have C# deduce the type from the right-hand side. You should use 
the `var` keyword whenever the type is obvious, or when the readability of your code can be enhanced. This means the 
following is preferred.

```c#
var number = 5;
```

This keyword will also allow us to avoid repeating data types later on when we start using other data types.

### Declaring and Initializing Multiple Variables

It's possible to declare multiple variables on the same line. The following code demonstrates declaring two integer 
variables at the same time.

```c#
int x, y;
```

Both `x` and `y` will be declared with the `int` type. This only works if you want the variables to all have the same 
type. While this can shorten your code, it can make it harder to read pretty quickly, so you should only declare 
multiple variables on the same line if they're related in some way. For example, declaring `x` and `y` which presumably 
represent a coordinate together. Unrelated variables of the same type should be declared on different lines.

We can initialize multiple variables on the same line as well. The following code demonstrates this.

```c#
int x = 0, y = 0;
```

When doing multiple declarations and initializations you are required to use concrete types, so `var` wouldn't work 
here.

While this works, the best practice is to *always initialize variables on separate lines* when they're being declared 
and initialized on the same line. There will be a few places where we can't avoid this, so we'll discuss them when they 
come up. You may see this in other people's code, but just know that you shouldn't write code like this just because 
someone else did. You should strive to write the most readable code you can!

### Multiple Assignment

Variables can be assigned to the same value at the same time. The following code demonstrates declaring multiple 
variables and assigning them the value of 0.

```c#
int x, y, z;
x = y = z = 0;
```

`x`, `y`, and `z` will all be assigned the value 0. This is acceptable to do in code, but you must be aware that this 
won't always do what you expect. For primitive values and strings, this will always work as expected, but we'll learn 
what can go wrong when it comes to doing this with other types of values.

#### Assignments Are Expressions

Multiple assignment works in C# because variable assignments are expressions. This means variable assignments are 
evaluated, and their evaluated values are simply the value that was assigned. This means we can do cool things with 
variable assignments when we need to later on, so remember this! We need to learn a bit more about C# before it will 
make sense how to use this information.

## Constants

Constants are variables whose values are known at compile-time and whose values won't change. This essentially means 
you can only assign literal values to constants. Some computation can be done at compile-time as long as the 
arguments are also constants. The following code demonstrates creating a local constant.

```c#
const double g = 9.81;
```

Constants are required to be declared and initialized on the same line. Type deduction is not allowed when declaring a 
constant, so `var` can't be used. When C# compiles your code, it will copy the values in each constant and paste them 
wherever the constants are used. This is why constant values have to be known at compile-time. The following code shows 
how C# processes constants.

```c#
// This is the code as written.
const double g = 9.81;
Console.WriteLine(g);

// This is the code C# will compile.
Console.WriteLine(9.81);
```

Constants should be used whenever possible since they won't actually exist at runtime.

### Using Keywords as Constant Names

The same trick we used to be able to use keywords as variable names can be used with constant names, too. The following 
code demonstrates creating a constant called `int`.

```c#
const int @int = 5;
```

`int` is certainly a bad name for a constant, but it illustrates how you would use a keyword as a constant name.

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

What if we want to write curly brackets inside an interpolated string literal? We can simply double them up to escape 
them!

```c#
const int number = 5;
Console.WriteLine($"The {{number}} is {number}");
```

The above code outputs the following to the console.

```text
The {number} is 5
```

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
