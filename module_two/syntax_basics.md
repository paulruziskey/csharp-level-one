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
