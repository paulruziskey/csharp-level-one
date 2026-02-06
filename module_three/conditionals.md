# Conditional Statements/Expressions

## What Are Conditional Statements?

Conditional statements are statements which make a decision based on a condition. This condition could be a number 
of things, so it depends on what kind of conditional statement you're using.

## Types of Conditional Statements

### If-statements

#### Basic If-statements

If-statements are conditional statements which make a decision based on a boolean value. If the boolean value is 
`true`, the body of the if-statement is executed. If the boolean value is `false`, the body of the if-statement is 
skipped. The following code demonstrates the simplest kind of if-statements.

```c#
if (true) { Console.WriteLine("Hello, world!"); }
if (false) { Console.WriteLine("Goodbye, world!"); }
```

The above code outputs the following to the console.

```text
Hello, world!
```

The syntax for an if-statement starts with the `if` keyword. It is followed by the boolean condition wrapped in 
parentheses. The body of the if-statement is then specified in curly brackets. If there is only one line's worth of 
code in an if-statement, it's common to see it written on one line. If there are multiple lines, they will appear 
after the `if` keyword and the condition as demonstrated by the following code.

```c#
if (true)
{
    Console.WriteLine("This will always run!");
    Console.WriteLine("Hello, world!");
}
```

One important thing to understand about if-statements in C# is that they only actually accept one statement to run 
as their bodies. This seems strange considering the previous if-statement had a two line body! It turns out the 
curly brackets are actually grouping the two statements into one by forming a code block. The if-statement then 
executes this code block. This means the curly brackets are optional for one-line if-statements as far as C#'s 
syntax is concerned.

```c#
if (true) Console.WriteLine("Hello, world!");
if (false)
    Console.WriteLine("Goodbye, world!");
```

Both of the above if-statements are valid in C#. However, there's a bit of a problem when we write if-statements 
without brackets. What do you think the output of the following code is?

```c#
if (true)
    Console.WriteLine("Hello, world!");
    Console.WriteLine("Hello, again, world!");
```

If you guessed the following output, you'd be right!

```text
Hello, world!
Hello, again, world!
```

So what's the issue? Let's play this game again. What do you think the output of the following code is?

```c#
if (false)
    Console.WriteLine("Goodbye, world!");
    Console.WriteLine("Just kidding!");
```

The above code outputs the following to the console.

```text
Just kidding!
```

Remember that if-statements only accept one statement as their body. This means only the next line is part of the 
body of an if-statement if the if-statement doesn't use brackets. Any lines after that, even if they're indented, 
won't be part of the body of the if-statement.

Now it might seem like the solution is to use brackets when there are multiple lines, but omit them when there's 
only one line! It would certainly be this simple if the omission of curly brackets didn't lead to bringing down the 
entire AT&T network on the East Coast! It seems so innocuous, but it can cause real problems. The reason is that 
someone may come along and wish to add code to an if-statement, but they may not realize there aren't any brackets 
if it was previously one line. This means they may write an if-statement like the one above where the indentation 
makes it seem like everything is okay, but it's not. This means you should ***always use brackets when writing 
if-statements***! It's only a few more characters to type, and it results in safer code!

Let's take a look at a non-trivial if-statements. We can use standard relational operators to do comparisons in 
if-statements.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
if (number > 0) 
{
    Console.WriteLine("You entered a positive number!");
}
```

`number > 0` returns a boolean, so the if-statement simply uses the result of the comparison to decide whether to 
run the code.

#### If-blocks

Each if-statement is what's known as an *if-block*. If-blocks are conditional blocks constructed from an if-statement; 
zero or more else-if-clauses; and zero or one else-clauses. Else-if-clauses allow for us to specify additional 
conditions to check if none of the preceding conditions were `true`. Else-clauses allow us to specify a catch-all 
statement which will run if none of the conditions in an if-block were `true`. The following code demonstrates using 
else-if-clauses and an else-clause to check multiple conditions.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
if (number < 0) 
{
    Console.WriteLine("You entered a negative number!");
}
else if (number == 0)
{
    Console.WriteLine("You entered zero!");
}
else if (number < 10)
{
    Console.WriteLine("You entered a single positive digit!");
}
else
{
    Console.WriteLine("You entered something else!");
}
```

It's important to note how this is different from simply using four if-statements in a row. In an if-block, 
conditions are only checked until a `true` condition is found. If a `true` condition is found, the body of the 
associated statement runs, then the if-block is done. No remaining conditions will be checked. With four 
if-statements in a row, each condition will be checked regardless of the outcome of the previous conditions. Whether 
you want a bunch of if-statements or one if-block simply depends on what type of logic you need. Take a look at the 
output of the previous code.

```text
Enter a number: -1
You entered a negative number!
```

Notice how only the if-statement ran? `number < 0` was `true`, so the if-statement ran, then since the other 
statements were part of the same if-block, they were skipped. Let's take a look at the same code, but using four 
if-statements instead of one if-block.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
if (number < 0) 
{
    Console.WriteLine("You entered a negative number!");
}
if (number == 0)
{
    Console.WriteLine("You entered zero!");
}
if (number < 10)
{
    Console.WriteLine("You entered a single positive digit!");
}
if (number >= 10)
{
    Console.WriteLine("You entered something else!");
}
```

Let's see how the output differs for the same input.

```text
Enter a number: -1
You entered a negative number!
You entered a single positive digit!
```

Notice how some extra text printed that doesn't make sense? That's because the previous code was relying on if-block 
logic to prevent later statements from running if a preceding statement was `true`. To make the new code act like the 
old code, we would need to change the third condition `number < 10` to `number > 0 && number < 10`.

### Switch-statements

Switch-statements are another kind of conditional statement in C#. Switch-statements work by taking in a value and 
checking different cases for that value to decide what to do. Switch-statements are useful when we want to do 
different things based on a particular value. The following example shows how to use a switch statement to print 
different things depending on the value of a number.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
switch (number) 
{
case < 0:
    Console.WriteLine("You entered a negative number!");
    break;
case 0:
    Console.WriteLine("You entered zero!");
    break;
case < 10:
    Console.WriteLine("You entered a single positive digit!");
    break;
default:
    Console.WriteLine("You entered something else!");
    break;
}
```

The above code does the same thing as the if-block in a previous example. Each case has a particular pattern 
specified to compare with the value in `number`. If `number` is less than zero, then the `< 0` pattern matches, and 
that case runs. Just like with if-blocks, switch-statements will run until the first case that matches, then they 
will run the code for that case and exit. The default case runs if none of the regular cases match.

So, what's with all the `break`s? C# syntax requires that every switch-case ends with code that causes the logic to 
leave the switch-statement. Most commonly, this is `break`, but it could be something else as long as it causes the 
logic to leave the switch-statement. Switch-statements originally came from The C Programming Language, so C# is 
mimicking how switch-statements would have looked in C. It's definitely strange since C# requires it, so it could 
very well be the default.

In C, the `break`s were optional, and cases without a `break` would fall through to the 
next case. Whenever this behavior wasn't desirable (which was all the time), `break` was used to end a 
switch-statement before a case could fall through to the next case. I don't know why C# opted to require code that 
ends a switch-statement in each switch-case since it would make more sense for it to simply be the default, but this 
is the syntax.

Let's now look at checking multiple patterns in a switch-case.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
switch (number) 
{
default:
    Console.WriteLine("You entered something else!");
    break;
case >= 0 and <= 9:
    Console.WriteLine("You entered a single digit!");
    break;
case < 0 or > 100:
    Console.WriteLine("You entered a negative number or a number greater than 100!");
    break;
}
```

One thing to note is that the default case can actually go anywhere in a switch-statement, and it won't affect the 
logic. This also comes from C because it could change the behavior when fall-through was used, but in C#, it's more of 
party trick, so the default case should always go at the end.

Switch-statements can be used with values of any type. The following code demonstrates switching on a string.

```c#
Console.Write("Enter a word: ");
string word = Console.ReadLine()!;
switch (word.ToLower())
{
case "hello":
    Console.WriteLine("Hey, there!");
    break;
case "goodbye":
    Console.WriteLine("You're already leaving?");
    break;
default:
    Console.WriteLine("That's a nice word!");
    break;
}
```

This can be an alternative to writing an if-block doing a bunch of case-insensitive equality comparisons.

#### Case Ordering Rules

In C#, it's an error for a case that covers the same thing as another case to come before it. Cases must be mutually 
exclusive, or more specific cases must come before more generic cases.

```c#
Console.Write("Enter a number: ");
var number = Convert.ToInt32(Console.ReadLine());
switch (number)
{
case not 5:
    Console.WriteLine("It's not five! How surprising!");
    break;
case < 0:
    Console.WriteLine("It's a negative number!");
    break;
default:
    Console.WriteLine("It's something else!");
    break;
}
```

Trying to run the above code would result in a syntax error since `not 5` covers negative numbers, but `< 0` checks 
negative numbers and comes after `not 5`. To get this code to run, either the second case would have to go before 
the first case, or the first case would have to be rewritten to avoid matching negative numbers.

## Using If-statements to Parse Inputs

Until now, any bad input results in an exception being thrown. This isn't great since it's not unexpected for a user 
to accidentally enter the wrong thing. It's also possible that people may try to abuse a piece of software by 
entering bad inputs. Luckily, C# provides methods to help with parsing basic data types! Each basic built-in type 
has a `TryParse` method which will return a boolean signaling whether valid input was entered. Let's take a look at 
some code using the `TryParse` method for integers.

```c#
Console.Write("Enter an integer: ");
if (int.TryParse(Console.ReadLine(), out int number)) 
{
    Console.WriteLine($"You entered {number} as your number!");
}
else
{
    Console.WriteLine("Your input was invalid");
}
```

The `TryParse` method returns `true` if the input is valid, so in that case, the if-statement will run. If the input 
is invalid, the else-clause will run! So, what's up with the `out int number`? The `TryParse` method uses what's 
known as an *output parameter* to give back the parsed integer on a successful parse. If the parsing is unsuccessful,
this variable will be set to the default value for an integer which is its zero value. This is simply another way 
for methods to send information back when they're done! This allows methods to more easily return multiple values in 
more convenient ways. In the case of the above code, the variable which will get the output parameter's value is 
declared as part of the method call, but it can be done differently. It's possible to declare the variable ahead of 
time and simply use it as part of the method call. In this case, the data type would be omitted, but the `out` 
keyword would remain since that is required when specifying a variable for an output parameter.

The scope of output-parameter variables declared inline is the enclosing scope of the method call. This means that 
`number` is scoped to the surrounding code rather than the if-statement. We will see later on that this affects 
things in ways we may not expect.

## What Are Conditional Expressions?

Conditional expressions are expressions which evaluate to a value based on the result of a condition. Conditional 
expressions can be a compact way to decide between several values.

## Types of Conditional Expressions

### Ternary Expression

Ternary expressions are expressions formed using the *ternary operator* (`?:`). The ternary operator is an 
interesting operator because it's the only operator that accepts three arguments. This is actually where it gets its 
name: *unary* operators accept one argument, *binary* operators accept two arguments, and *ternary* operators accept 
three arguments. Since it's the only operator that accepts three arguments, it became known as the ternary operator.

Ternary expressions are used to decide between one of two values depending on the value of a boolean expression. The 
following code demonstrates using a ternary expression to display the result of an evenness check in a user-friendly 
way.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
string result = int.IsEvenInteger(number) ? "even" : "odd";
Console.WriteLine($"Your number is {result}");
```

The above code outputs the following to the console.

```text
Enter an integer: 3
Your number is odd
```

Ternary expressions are written as `condition ? valueIfTrue : valueIfFalse`. In the above example, the number 3 is 
odd, so `int.IsEvenInteger` returned `false`, meaning the ternary expression evaluated to `"odd"`.

We could have written the above code a bit more compactly by writing the ternary expression inside the interpolated 
string. This is perfectly okay to do, we just have to remember to wrap it in parentheses so the interpolated string 
doesn't get confused.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"Your number is {(int.IsEvenInteger(number) ? "even" : "odd")}");
```

### Switch Expressions

Switch statements have an expression version with a more compact syntax. Switch expressions follow the same logic as 
switch statements, but they're written a little differently. They are also evaluated since they are expressions. The 
following code demonstrates using a switch expression to print one of three possible messages depending on the 
number a user enters.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine(number switch
{
    < 0 => "Negative numbers are pretty cool",
    > 0 => "Positive numbers are a little less cool, but still pretty cool",
    0   => "Zero is an interesting number",
});
```

The above code outputs the following to the console.

```text
Enter an integer: -4
Negative numbers are pretty cool
```

We can see the syntax for switch expressions is more compact than the syntax for switch statements. We don't need 
the `case` keyword, and the objects that come after each `=>` are what the switch expression will evaluate to if the 
corresponding pattern is matched. Each option for a switch expression is known as an *arm*.

One important thing to note is that switch expressions must be *exhaustive*. This means switch expressions will 
raise a syntax error if none of the provided patterns match an object. In the above example, any integer could attempt 
to be matched, and no matter what the integer is, it will always match one pattern.

Another thing to note is that switch expressions only allow a single object to be provided in each arm. Unlike 
switch statements which allow for multiple lines of code in each case, switch expressions only allow single objects.
