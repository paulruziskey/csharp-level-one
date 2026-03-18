# C# and Programming Syntax Basics

## Statements

*Statements* are code units that express a task to be performed.

### Simple Statements

*Simple statements* are statements which can contain no other statements. Simple statements may contain internal 
components, such as expressions. Calling a method in C# is an example of a simple statement.

```c#
Console.WriteLine("Hello, world!");
```

C# requires semicolons at the end of all simple statements.

The simplest statement in C# is the *null statement*. Null statements are created using a single semicolon.

```c#
;
```

The above code shows a null statement in C#. This statement doesn't look useful at all, and it's not! Why does C# allow 
them, then? They're used to enable certain syntax that otherwise wouldn't be possible. We'll be seeing an example at 
the end of the next module!

### Compound Statements

*Compound statements* are statements which contain sequences of statements. Compound statements in C# are created 
using *curly brackets* `{}`.

```c#
{
    Console.WriteLine("Hello, world!");
    Console.WriteLine("Hello again, world!");
}
```

Compound statements are treated like simple statements when executed. Compound statements are typically called *code 
blocks*.

#### Scope

*Scope* represents the parts of code where declarations are valid. For example, variables are valid from where they 
are declared to the end of the scope in which they were declared. This matters when compound statements (i.e., code 
blocks) are used since compound statements create new scopes. Scopes declared within other scopes inherit the 
existing declarations from the outer scopes, while the outer scopes don't inherit any declarations from the inner 
scopes. The following code demonstrates basic C# scope rules.

```c#
var number = 5;
{ // new scope is created
    var number2 = 7;
    Console.WriteLine(number + number2);
    {
        var number3 = 10;
        Console.WriteLine(number + number2 + number3);
    } // `number3` valid until here
    // Console.WriteLine(number3); // error since `number3` is out of scope
    Console.WriteLine(number + number2);
} // `number2` valid until here
// Console.WriteLine(number3); // error since `number3` is out of scope
// Console.WriteLine(number2); // error since `number2` is out of scope
Console.WriteLine(number);
// `number` valid until end of program
```

Understanding scope can be pretty difficult when you first start, but you'll get the hang of it with practice!

## Expressions

*Expressions* are code units which yield values when evaluated. `3 + 4` is a simple example of an expression which, 
when evaluated, yields the value `7`. It's worth noting that `3` and `4` are themselves expressions since they yield 
the literal values they're written with. Expressions can have *side effects* where the evaluation of an expression 
causes something else to happen. Sometimes we only want to evaluate an expression for its side effects rather than 
its value. In C#, we can turn an expression into a statement by placing a semicolon at the end. Only certain 
expressions can become statements, and you'll learn what these are as we continue through the course.

## Literals

*Literals* are values directly written into the source code. `0`, `3.4`, and `"hello"` are all examples of literals 
since they represent their values literally. A string taken from the user is not a literal since the value of the 
string isn't written directly in the code. If a literal is numeric, it's known as a *numeric literal*. If a literal is 
character-based, it's known as a *character literal* or a *string literal* depending on whether it uses single or 
double quotes.

### Numeric Literal Suffixes and Formatting

Numeric literals may include capital letters at the end to reflect the data type of the literal. For example, `3.99M` 
represents a decimal literal, and `47U` represents an unsigned integer literal. The following table outlines the 
literal suffixes and their meanings.

| Suffix | Data Type | Meaning       |
|--------|-----------|---------------|
| `U`    | `uint`    | Unsigned      |
| `L`    | `long`    | Long          |
| `UL`   | `ulong`   | Unsigned long |
| `F`    | `float`   | Float         |
| `M`    | `decimal` | Money         |

While these suffixes can be either uppercase or lowercase syntactically, you should prefer writing them in uppercase so 
they can't be confused for digits. Lowercase "l"s and ones are similar in a lot of fonts.

Additionally, while you can't include commas in numeric literals like you might want to for larger literals, you can 
use underscores! This means we can write literals for large numbers like 1,000,000 as `1_000_000`. These underscores 
can go anywhere you want, so you don't have to limit yourself to the way commas would be used with regular numbers. 
This is because the underscores are ignored by the compiler. For example, the numeric literal `1___0.57_9` is valid and 
represents the value 10.579. You should never write a literal this confusing, but it's possible. The only syntax 
restriction on underscore placement is there must be at least one digit or underscore on either side of an underscore. 
This means you can't start or end numeric literals with underscores, and underscores can't go around a decimal point if 
it appears.
