# Loops

## What Are Loops?

Loops are simple statements that repeat another statement based on a condition. C# has two main types of loops, 
*while-loops* and *for-loops*, which are closely related, but which are used in different situations. These two main 
types of loops also come in different versions.

An important term related to loops is *iteration* which refers to the act of repeating a statement using a loop. 
More generally, the term *iteration* means repeating a process to generate a sequence of outcomes, but when it comes 
to programming, loops facilitate this.

## While-loops

### Basic While-loops

*While-loops* are loops that evaluate a boolean expression and continue repeating a given statement until the 
boolean expression evaluates to `false`. While-loops are used to repeat code when we don't know how many times we 
need to repeat the code, but we know when it needs to stop. The following code demonstrates using a while-loop to 
count to 10.

```c#
var i = 0;
while (i <= 10)
{
    Console.Write(i + " ");
    i = i + 1;
}
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 7 8 9 10 
```

This isn't a great example of when to use a while-loop since we actually know how many times we need the loop to run,
but we don't really have any better ways given what we know. As we move through the course, you'll get a much better 
idea for when to use while-loops.

While-loops share the same syntax as if-statements except for the use of the `while` keyword instead of the `if` 
keyword. Additionally, like if-statements, while-loops only accept a single statement to repeat. This means we have 
to use curly brackets to create a compound statement if we want to repeat more than one line of code. Just like with 
if-statements, it's best practice to always write curly brackets with while-loops.

#### Compound Assignment Operators

The above code updates `i` by reassigning it to its current value plus one. We can simplify this by using the 
*compound assignment-addition operator* (`+=`).

```c#
var i = 0;
while (i <= 10)
{
    Console.Write(i + " ");
    i += 1;
}
Console.WriteLine();
```

`i += 1` is a shorthand for `i = i + 1`. Other compound assignment operators exist for substraction, multiplication, 
division, and modulo. These operators can be used with the primitive numeric types we've learned about so far except 
for `bool`. Additionally, the compound assignment-addition operator can be used with strings to facilitate easier 
string concatenation.

```c#
var phrase = "hello";
phrase += " world";
Console.WriteLine(phrase);
```

The above code outputs the following to the console.

```text
hello world
```

As a reminder, strings in C# are immutable, which means the original string isn't actually being updated even though 
it looks like it is. Rather, a new string is being created from the characters in the original string with the 
characters from the concatenated string appended to the end. This new string is then assigned to the original 
variable.

These compound assignment operators all form expressions, meaning the following code is valid.

```c#
var number = 10;
int number2 = number += 5;
Console.WriteLine($"number: {number}, number2: {number2}");
```

The above code outputs the following to the console.

```text
number: 15, number2: 15
```

In the above example, `number` was incremented by five, increasing its value to 15. The expression `number += 5` 
evaluated to 15 since assignment expressions always evaluate to the assigned value, then the expression result was 
assigned to `number2`. This is why both variables end up with the value 15.

`number += 5` is an example of an expression with a side effect. The side effect is that `number` is increased by 
five. The result of the expression is the increased value, 15. Such expressions can be turned into statements by 
appending a semicolon. That's what was done in the while-loop example. In that case, we only wanted to evaluate the 
expression for its side effect of incrementing `i` by one, and we wanted to discard the evaluated value because we 
didn't need it.

#### Increment and Decrement Operators

Since we're incrementing `i` by one, we can actually make `i += 1` even shorter by using the *prefix increment 
operator* (`++`).

```c#
var i = 0;
while (i <= 10)
{
    Console.Write(i + " ");
    ++i;
}
Console.WriteLine();
```

The above code does the same thing as the code at the start of this section. There is also a *postfix increment 
operator* (`++`) which goes after a variable instead of before it. The following code does the same thing as the 
above code.

```c#
var i = 0;
while (i <= 10)
{
    Console.Write(i + " ");
    i++;
}
Console.WriteLine();
```

So, what's the difference? Both the prefix and postfix versions create expressions, and the difference is in the 
values they return. Let's look at an example using both.

```c#
var number = 10;
int prefixResult = ++number;
int postfixResult = number++;
Console.WriteLine($"number: {number}, prefixResult: {prefixResult}, postfixResult: {postfixResult}");
```

The above code outputs the following to the console.

```text
number: 12, prefixResult: 11, postfixResult: 11
```

Is this what you expected? Let's go through this example.

The first thing to understand is that `++number` and `number++` are both examples of expressions with side effects. 
The side effect is that the value stored in the variable will always be incremented by one no matter which operator 
you use. Now that we know this, let's run through the code.

A variable called `number` is declared and initialized with the value 10. A variable called `prefixResult` is then 
declared and initialized with the result of the evaluated expression `++number`. We know `number` will be 
incremented by one, so `number` now holds 11. Prefix-increment-operator expressions return the result of the 
assignment, so `prefixResult` gets assigned the value 11. A variable called `postfixResult` is now declared and 
initialized with the result of the evaluated expression `number++`. We know `number` will be incremented by one, so 
`number` now holds 12. Postfix-increment-operator expressions return the initial value stored in the variable rather 
than the incremented value, so `postfixResult` gets assigned the value 11.

This difference can be confusing when you first learn about it, so here are some tips to help you.

* Reading prefix and postfix expressions from left to right tells you whether the incrementing happens first or last. 
  `++number` means `number` is incremented first, then the expression evaluates to the new value. `number++` means 
  the expression evaluates to the original value, then `number` is incremented.
* Unless you care about the result of the expression, always use the prefix version. This is because it will either 
  be faster than the postfix version, or it will be the same speed. Modern-day compilers will typically optimize 
  this difference away for primitive types, but that isn't always guaranteed, and the story may be different for 
  other types, so it's better to prefer the operator you know will always be the fastest. This means you won't need 
  to choose between the prefix version and the postfix version in most situations!

In addition to the increment operators, C# has *prefix* and *postfix decrement operators* (`--`) as well. These 
operators have the side effect of decrementing a variable's value by one. These operators follow the same rules for 
what their expressions will evaluate to as the increment operators.

The prefix and postfix increment and decrement operators can be used with the primitive numeric types we've learned 
about so far except for `bool`.

We can now update the while-loop from earlier to take advantage of the expression created by the postfix increment 
operator!

```c#
var i = 0;
while (i <= 10) { Console.Write(i++ + " "); }
Console.WriteLine();
```

This code works the same as before, but now the while-loop body is down to one line!

Before moving on, take a look at the following code.

```c#
var i = 11;
while (i <= 10) { Console.Write(i++ + " "); }
Console.WriteLine();
```

The code is the same as before, but the condition has changed a bit. This code doesn't output anything to the 
console besides a newline since the while-loop never runs. While-loops check their condition *first*, then they 
start repeating their code if they need to. This means basic while-loops won't run if their condition is initially 
`false`. This means basic while-loops should be used if you need to check the condition at the start of the loop.

### Do-while-loops

While basic while-loops check their condition at the start of the loop, *do-while-loops* check their conditions at 
the end of the loop. This ensures that the body of the loop will run at least once no matter what the condition is. 
Do-while-loops are used far less often than basic while-loops, but they're still useful to know about. The following 
code demonstrates using a do-while-loop to count to 10.

```c#
var i = 0;
do
{
    Console.Write(i++ + " ");
} while (i <= 10);
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 7 8 9 10 
```

We can see that this code does the same thing as the basic-while-loop example, so what's the difference? Let's see 
what happens if we initialize `i` to 11 like we did with the basic while-loop.

```c#
var i = 11;
do
{
    Console.Write(i++ + " ");
} while (i <= 10);
Console.WriteLine();
```

The above code outputs the following to the console.

```text
11 
```

We can see that the body of the loop ran once even though the condition was `false` at the start of the loop. Because 
do-while-loops check their condition at the end, they will always run their code at least once before checking if 
they should continue. Do-while-loops are useful if you need to run the loop code to get a value for your condition.

The syntax for do-while-loops is a little different from basic while-loops, but it follows the same principle. You 
start with the `do` keyword followed by a statement to repeat. The above examples use compound statements. As with 
basic while-loops, it's best practice to always use curly brackets, even if you're only repeating a simple statement.
At the end of the compound statement, we use the `while` keyword followed by a boolean expression in parentheses 
serving as the condition. This is the only time in C# when code goes on the same line as a closing curly bracket. We 
do this to make sure the while-clause isn't accidentally treated as the start of a basic while-loop; it makes it 
much clearer what the while-clause belongs to.

### While-true-loops

*While-true-loops*, often called *infinite loops*, will repeat their statements forever. While-true-loops are 
created by simply writing a basic while-loop using `true` as the condition. Since `true` is never false, the loop 
will run forever.

The following code demonstrates using a while-true-loop to count forever.

```c#
var i = 0;
while (true) { Console.WriteLine(i++); }
```

The above code will repeatedly output the current value of `i`. This doesn't seem very useful... On their own, 
while-true-loops are only useful if you need to create a program that does the same thing over and over again until 
the user decides to stop the program. This is certainly useful, but it's not the most user-friendly way to write a 
program like this since the user would need to force the program to quit since the program wouldn't be capable of 
stopping itself. This is where *loop-control-statements* come in!

#### Loop-control-statements

C# provides two loop-control-statements which affect the behavior of a loop.

##### Break-statements

The most important loop-control-statement is the *break-statement*. When C# encounters a break-statement in a loop, 
it ends the loop immediately. The statement is called a break-statement since we use it to break out of a loop. The 
following code demonstrates counting to 10, but stopping early if the number seven is encountered.

```c#
var i = 0;
while (i <= 10)
{
    if (i == 7) { break; }
    Console.Write(i++ + " ");
}
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 
```

We can see the program works as before until `i` holds 7, at which point the condition for the if-statement 
evaluates to `true`, and the break-statement runs. We can see that the loop ends immediately at the break-statement 
since 7 is never printed.

Break-statements are very useful with every kind of loop, but they're especially useful with while-true-loops since 
they allow us to end while-true-loops! The following code demonstrates counting to 10 using a while-true-loop, which 
is now possible with break-statements!

```c#
var i = 0;
while (true)
{
    if (i >= 11) { break; }
    Console.Write(i++ + " ");
}
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 7 8 9 10 
```

Now that we can break out of while-true-loops, we can use them in more contexts! While-true-loops are used whenever 
you need to check a condition in the middle of a while-loop. This is typically the case when getting user input, as 
you'll see in the section on getting safe user input with loops.

##### Continue-statements

*Continue-statements* are used to stop the current iteration of a loop and proceed directly to the next iteration. 
Continue-statements aren't very well named, since they make it sound like the code will proceed unaffected, so do 
your best to remember what they actually do. Continue-statements aren't as important as break-statements because you 
can often rewrite loop code to avoid them. That being said, they're very helpful when it comes to code semantics 
and avoiding indentation. The following code demonstrates counting to 10 skipping the number 5.

```c#
var i = -1;
while (++i <= 10)
{
    if (i == 5) { continue; }
    Console.Write(i + " ");
}
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 6 7 8 9 10 
```

For this code to work, incrementing `i` needed to be moved to the condition, and `i` needed to be initialized to -1 
since the prefix increment operator is being used. If `i` holds the value 5, the if-statement condition evaluates to 
`true`, and the continue-statement runs. This skips the rest of the loop which is why 5 isn't printed. If `i` 
doesn't hold the value 5, the if-statement condition evaluates to `false`, and the code proceeds to the print 
statement where the current value of `i` is printed.

We could have written the above code without the continue-statement.

```c#
var i = -1;
while (++i <= 10)
{
    if (i != 5) { Console.Write(i + " "); }
}
Console.WriteLine();
```

As mentioned above, we can often rewrite code to avoid continue statements. So why isn't this better?

The first issue is that the semantics aren't as clear. When a continue-statement is used, it's clear that you're 
ignoring a particular situation or value. With the above code, you have to do a bit more reading to figure out that 
five is being singled out and ignored. Of course, the above example isn't very complex, but for more complex 
examples, it can take longer to figure these things out.

The second issue is that the main purpose of this loop is to print values from zero to 10 ignoring five, yet that 
code is nested inside an if-statement. It would make more sense for that code to be unconditional, i.e., outside the 
if-statement. Even though we had to write an extra line of code with the continue-statement, it was clearer what the 
main loop code was. In loops with more code, continue-statements can save you a lot of nesting!

Given the above reasons, it's best to use continue-statements to skip particular situations or values rather than 
nesting the main code of a loop.

## For-loops

C# has two kinds of for-loops, but we're only going to learn about basic for-loops for now since we won't be able to 
use the other kind of for-loop until we learn about other concepts.

### Basic For-loops

*For-loops* are a way to rewrite while-loop code to include a counter. The above while-loop examples were only doing 
counting, so we could use for-loops instead to include the counter as part of the loop!

Take the following while-loop code.

```c#
var i = 0; // counter declaration and initialization
while (i <= 10) // loop condition
{
    Console.Write(i + " ");
    ++i; // counter change
}
Console.WriteLine();
```

We can rewrite the above code using a for-loop.

```c#
// (counter declaration and initialization; loop condition; counter change)
for (var i = 0; i <= 10; ++i) { Console.Write(i + " "); }
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 7 8 9 10 
```

#### Rewriting a For-loop Using a While-loop

Both the while-loop version and the for-loop version do the same thing, but the for-loop code is much more concise! 
Notice how the for-loop is declared with the same code we used with the while-loop? Let's examine the syntax of 
for-loops more closely.

For loops are declared using the following syntax.

```c#
for (<initialiation>; <condition>; <change>) 
{
    // loop code
}
```

For-loops are typically used for counting, so we mainly use for-loops when we know how many times we want to repeat 
a statement. Nearly all for-loops can be rewritten using while-loops since they're really just more convenient 
while-loops. For example, the above for-loop syntax could be written as the following using a while-loop.

```c#
<initialization>;
while (<condition>) 
{
    // loop code
    <change>;
}
```

This would probably be correct in 99 percent of cases without worrying about what the loop is actually doing. Where 
things get a bit more complicated is when continue-statements are involved. Take a look at the following example 
which counts to 10 skipping the number five.

```c#
for (var i = 0; i <= 10; ++i)
{
    if (i == 5) { continue; }
    Console.Write(i + " ");
}
Console.WriteLine();
```

The above outputs the following to the console.

```text
0 1 2 3 4 6 7 8 9 10 
```

The above code works as intended. What happens if we translate it to a while-loop using the method we learned about 
above?

```c#
var i = 0;
while (i <= 10)
{
    if (i == 5) { continue; }
    Console.Write(i + " ");
    ++i;
}
Console.WriteLine();
```

The above code outputs the following to the console before stopping and running forever.

```text
0 1 2 3 4 
```

Why is this? It's because continue-statements skip the rest of the current loop iteration, meaning `i` stops being 
incremented once `i` holds the value 5. In the for-loop example, `i` is incremented even if a continue-statement is 
encountered. This is a subtle but important difference to remember.

#### For-loop Syntax

##### What Is Required for a For-loop

For-loops are actually very expressive depending on what you need. The following code demonstrates the simplest 
for-loop you can write in C#.

```c#
for (;;) {}
```

It turns out the only required part of a for-loop declaration is the semicolons! So, what does the above for-loop do?
It's equivalent to a while-true loop! When the condition is omitted, C# will assume `true`. That means the following 
for-loop declaration is the same as the above declaration.

```c#
for (; true;) {}
```

It's worth noting that while-true-loops should always be preferred over the infinite for-loop version for 
readability. Neither of the above two loops should ever be written over a while-true-loop, even though they do the 
same thing.

The initialization and change sections are only necessary if you need them for your loop. Omitting them has no side 
effects. It may seem strange to omit these sections, but it can help in certain situations. For example, if you 
already have a variable you want to use as your for-loop counter, you can omit the initialization section since 
you've already declared and initialized the variable.

```c#
var i = 0;
for(; i <= 10; ++i) { Console.Write(i + " "); }
Console.WriteLine();
```

The above code outputs the following to the console.

```text
0 1 2 3 4 5 6 7 8 9 10 
```

This is certainly a bit of a toy example, but it illustrates the point.

##### Initialization Section

While the initialization section makes it sound like you're required to declare and initialize a variable, you're 
not! You can provide any simple statement for the initialization section, and it will run before the loop starts. 
There's very little reason to use this section for anything other than variable initialization, but the following 
for-loop is possible.

```c#
var i = 0;
for(Console.WriteLine("Loop starting"); i <= 10; ++i) { Console.Write(i + " "); }
Console.WriteLine();
```

The above code outputs the following to the console.

```text
Loop starting
0 1 2 3 4 5 6 7 8 9 10 
```

We can see the print statement gets run once at the start of the loop, then never again.

##### Condition Section

The only requirement for the condition section is that the condition be a boolean expression. Any valid boolean 
expression is allowed in this section.

##### Change Section

Just like with the initialization section, the change section only requires a simple statement. While this is 
typically used to change or update the value of a loop variable, the following for-loop is possible.

```c#
for (var i = 0; i <= 10; Console.WriteLine("Iteration end"))
{
    Console.Write(i++ + " ");
}
```

The above code outputs the following to the console.

```text
0 Iteration end
1 Iteration end
2 Iteration end
3 Iteration end
4 Iteration end
5 Iteration end
6 Iteration end
7 Iteration end
8 Iteration end
9 Iteration end
10 Iteration end
```

We can see "Iteration end" is printed at the end of each iteration. Whatever statement you put in this section will 
be run at the end of each iteration, even if a continue-statement was used to end an iteration.

There are, of course, much better uses for these for-loop features, but the print statements help illustrate what's 
going on.

#### For-loops with Other Types of Counters

Since we can write any simple statement for the initialization and change sections, we can write for-loops using 
different data types for the loop variable. The following code demonstrates printing the alphabet using a for-loop.

```c#
for (var c = 'a'; c <= 'z'; ++c) { Console.Write(c + " "); }
Console.WriteLine();
```

The above code outputs the following to the console.

```text
a b c d e f g h i j k l m n o p q r s t u v w x y z 
```

Since characters are integral types, we can treat them like we do integers to essentially iterate through the alphabet.

#### For-loop Variable Naming Conventions

When it comes to naming for-loop variables, you'll typically see single-letter variable names used. This is one of 
the few acceptable times to use a single-letter variable name. Typically, the name is simply the first letter of the 
data type. For example, `i` for `int` and `c` for `char`. You should do this if there is no significance to your 
loop variable other than being a counter. We do this by convention since it's clear what we're doing. C# also has 
some strict conventions when it comes to loop variables as you'll see later in this lesson, so using single-letter 
variable names helps.

That being said, if there is a significance to your for-loop variable, you should *use a proper variable name*. 
Don't always use a single-letter name just because your variable is a loop variable. Keep this in mind as you 
practice writing loops!

#### For-loops with Multiple Variables

Since we can write any simple statements we want for the initialization and change sections, we can write for-loops 
with multiple variables. The following code demonstrates a for-loop with two counters.

```c#
for (int ones = 1, twos = 2; ones <= 10; ++ones, twos += 2)
{
    Console.WriteLine($"ones: {ones}, twos: {twos}");
}
```

The above code outputs the following to the console.

```text
ones: 1, twos: 2
ones: 2, twos: 4
ones: 3, twos: 6
ones: 4, twos: 8
ones: 5, twos: 10
ones: 6, twos: 12
ones: 7, twos: 14
ones: 8, twos: 16
ones: 9, twos: 18
ones: 10, twos: 20
```

We can see `ones` is counting by ones and `twos` is counting by twos. The condition is only based on one of the 
counters because both variables count at the same time. If we wanted the loop to end on whichever counter reached 10 
first, we could do the following.

```c#
for (int ones = 1, twos = 2; ones <= 10 && twos <= 10; ++ones, twos += 2)
{
    Console.WriteLine($"ones: {ones}, twos: {twos}");
}
```

The above code outputs the following to the console.

```text
ones: 1, twos: 2
ones: 2, twos: 4
ones: 3, twos: 6
ones: 4, twos: 8
ones: 5, twos: 10
```

Since the above loop only runs while `ones` and `twos` are both less than or equal to 10, the loop stops once one of 
them reaches 10.

This is the only time when it's acceptable to declare and initialize multiple variables on the same line; we don't 
have a choice in this situation. The fact that we can declare and initialize multiple variables on the same line is 
what allows us to write for-loops with multiple variables in the first place.

The change section is a bit of a special case since that particular type of syntax is only supported in for-loops. 
The original syntax for C-style for-loops came from C, and C# wanted to preserve as much of the original 
functionality as possible without allowing comma-statements to be used elsewhere. You'll only encounter 
comma-statements when writing for-loops with multiple variables.

##### Limiting the Number of For-loop Variables

For-loops can support any number of variables. That being said, you should only use two variables at most. This is 
the best practice if you're going to use a multivariable for-loop since they can become unreadable very quickly. You 
won't encounter too many situations where you want multiple variables in a for-loop. If you do encounter one such 
situation, you probably won't need more than two, so this isn't a huge restriction, but keep it in mind.

## Scope of Loop Variables

All variables declared as part of a loop declaration belong to the scopes of the loops, not the enclosing scopes. 
This includes for-loop variables declared with the loop as well as output parameters. Note that the scope of output 
parameters in general depends on the context. For loops, the scope is the loop's scope. For everything else, the 
scope is the enclosing scope. The following examples demonstrate the scope of for-loop variables.

```c#
for (var i = 0; i < 10; ++i) // `i` declared as part of loop
{
    // do something
} // `i` valid until here
// Console.WriteLine(i); // doesn't compile since `i` is only part of the loop
```

```c#
int i; // `i` declared outside loop
for (i = 0; i < 10; ++i)
{
    // do something
}
Console.WriteLine(i); // works just fine
// `i` valid until end of program
```

The following examples demonstrate the scope of output parameters declared as part of a loop declaration. This 
behavior is different from what we've seen with conditional statements!

```c#
while (!int.TryParse(Console.ReadLine(), out int result)) // `result` declared as part of loop
{
    // do something
} // `result` only valid until here
// Console.WriteLine(result); // doesn't compile since `result` is only part of the loop
```

```c#
int result; // `result` declared outside loop
while (!int.TryParse(Console.ReadLine(), out result))
{
    // do something
}
Console.WriteLine(result); // works just fine
// `result` valid until the end of the program
```

This affects not only where you declare your variables, but what variables you declare. Take a look at the following 
example.

```c#
for (var i = 0; i < 10; ++i)
{
    // do something
}
var i = 5; // fails to compile because `i` was already used as part of the loop
```

This doesn't make a lot of sense because the `i` variable that was used for the loop should be out of scope when the 
other `i` variable is declared. While it's true that the `i` variable that's part of the loop is out of scope by the 
time the other `i` variable is declared, C# doesn't allow this, so why not? It's because C# wants to make sure that 
variables in the enclosing scope of a loop won't ever affect the validity of loop variables, no matter where they 
are. It's sometimes necessary to move code from below a loop to above a loop. If we move the second declaration of 
`i` to above the loop, we can immediately see a problem.

```c#
var i = 5;
for (var i = 0; i < 10; ++i) // second declaration of `i`
{
    // do something
}
```

It's immediately clear why the above example doesn't work. C# tries to prevent situations like this due to 
rearranging code, so that means loop variables are off limits even after they've gone out of scope. This typically 
won't be a problem when it comes to for-loop variables, but this also applies to output-parameter variables, so 
that's where you'll mainly have to be a bit careful.

## Nested Loops

*Nested loops* are loops inside of loops. You can nest as many loops as you want, and those loops can be all 
for-loops, all while-loops, or a mix of both. One thing to keep in mind when nesting loops is that loop variables 
for outer loops remain in scope for the inner loops. This means you'll need to change the names of the variables for 
your inner loops to get your code to compile. We typically use `j` if we've already used `i` and `k` if we've 
already used `j` and so on.

Nested loops are used to repeat code that is already repeating. For example, take the following code which prints a 
row of five asterisks.

```c#
for (var i = 0; i < 5; ++i) { Console.Write('*' + " "); }
Console.WriteLine();
```

The above code outputs the following to the console.

```text
* * * * * 
```

What if we wanted a square of asterisks? We already have one row, so we just need to repeat this row five times. We 
can do this with another loop!

```c#
for (var i = 0; i < 5; ++i)
{
    for (var j = 0; j < 5; ++j) { Console.Write('*' + " "); }
    Console.WriteLine();
}
```

The above code outputs the following to the console.

```text
* * * * * 
* * * * * 
* * * * * 
* * * * * 
* * * * * 
```

Just like that, we get out square! This is the power of nested loops! Each loop in the above example is performing a 
specific job: the inner loop is responsible for printing a single row of asterisks, and the outer loop is 
responsible for printing the rows on separate lines. Thinking of the job of each loop can help make nested-loop code 
easier to understand and easier to write.

### Breaking Out of Nested-loops

What happens if we try to use continue-statements or break-statements inside a nested loop? These statements only 
apply to the *nearest* loop, meaning it's not possible in C# to use a break-statement to break out of nested loops 
in one go.

#### Traditional Way

The following code demonstrates how we could break out of a nested loop after both loops have reached their third 
iterations.

```c#
for (var i = 0; i < 5; ++i)
{
    var done = false;
    for (var j = 0; j < 5; ++j)
    {
        if (i == 2 && j == 2)
        {
            done = true;
            break;
        }
        Console.Write(j + " ");
    }
    if (done) { break; }
    Console.WriteLine();
}
```

The above code outputs the following to the console.

```text
0 1 2 3 4 
0 1 2 3 4 
0 1 
```

While this certainly works, it would be nice to have a way to completely break out of several loops at once. We can 
do this with a *goto-statement*.

#### Goto-statements

##### Using goto-statements

*Goto-statements* are statements that transfer control from one part of our code to another via a label. We can 
write labels in our code to mark specific starting points, then we can use a goto-statement to move from the 
goto-statement to the first statement after the label. The following code demonstrates the use of a goto-statement.

```c#
Console.Write("Enter an integer: ");
var integer = Convert.ToInt32(Console.ReadLine());
if (integer == 7)
{
    Console.WriteLine("You entered a lucky seven!");
    goto ProgramEnd; // goto-statement
}
Console.WriteLine($"You entered {integer}");
ProgramEnd: // label
Console.WriteLine("Done processing input");
```

The above code outputs the following in different cases.

```text
Enter an integer: 7
You entered a lucky seven!
Done processing input
```

```text
Enter an integer: 5
You entered 5
Done processing input
```

Labels are always defined on their own lines, and they are named using PascalCase. Labels are also followed by a 
*colon*, not a semicolon. This is because labels mark statements; they aren't statements, themselves. Notice how 
printing the inputted number is skipped when the inputted number is 7? This is because the goto-statement transfers 
control to the `ProgramEnd` label, which jumps over the print statement which prints the inputted number. Labels 
have no effect on the regular control flow of a program; they only act as markers for use with goto-statements. This 
means the label was simply skipped over when a 5 was inputted.

If we didn't care about printing anything at the end of the program, we would have a problem. This is because labels 
need a statement to mark, so what can be done if we want to go to the end of the program? We can simply use a null 
statement as shown in the following example.

```c#
Console.Write("Enter an integer: ");
var integer = Convert.ToInt32(Console.ReadLine());
if (integer == 7)
{
    Console.WriteLine("You entered a lucky seven!");
    goto ProgramEnd; // goto-statement
}
Console.WriteLine($"You entered {integer}");
ProgramEnd:; // label marking null statement
```

The above code outputs the following in different cases.

```text
Enter an integer: 7 
You entered a lucky seven!
```

```text
Enter an integer: 5
You entered 5
```

This is also useful if you wish to transfer control to the end of a compound statement without leaving it. The 
following example demonstrates this.

```c#
for (var i = 0; i < 10; ++i)
{
    if (i == 5)
    {
        Console.WriteLine("Found five!");
        goto LoopEnd;
    }
    Console.WriteLine($"Current number: {i}");
    LoopEnd:;
}
```

The above code outputs the following to the console.

```text
Current number: 0
Current number: 1
Current number: 2
Current number: 3
Current number: 4
Found five!
Current number: 6
Current number: 7
Current number: 8
Current number: 9
```

We can see that "Current number: 5" wasn't printed due to the goto-statement skipping over it. We can also see that 
we *remain in the loop* since the goto-statement didn't transfer control outside the loop body.

We've looked at a bunch of examples now, but if you look closely, you'll notice that none of these examples required 
goto-statements to work. In the if-statement examples, simply adding else-clauses would have removed the need for 
the goto-statements. Likewise, in the above loop example, we actually just recreated the behavior of a 
continue-statement! The following code does the same thing as the above code using a continue-statement instead of a 
goto-statement.

```c#
for (var i = 0; i < 10; ++i)
{
    if (i == 5)
    {
        Console.WriteLine("Found five!");
        continue;
    }
    Console.WriteLine($"Current number: {i}");
}
```

This is really what a continue statement becomes when it's compiled! Can we recreate a break-statement using a 
goto-statement? Absolutely!

```c#
for (var i = 0; i < 10; ++i)
{
    if (i == 5)
    {
        Console.WriteLine("Found five! No more work for me!");
        goto LoopExit;
    }
    Console.WriteLine($"Current number: {i}");
}
LoopExit:;
```

The above code outputs the following to the console.

```text
Current number: 0
Current number: 1
Current number: 2
Current number: 3
Current number: 4
Found five! No more work for me!
```

The following is the equivalent code using a break-statement.

```c#
for (var i = 0; i < 10; ++i)
{
    if (i == 5)
    {
        Console.WriteLine("Found five! No more work for me!");
        break;
    }
    Console.WriteLine($"Current number: {i}");
}
```

Simply changing whether the label is inside the loop or outside the loop changes the behavior significantly!

We've been learning about goto-statements, but none of the examples we've seen requires a goto-statement. That's 
because these examples were meant to simply illustrate how goto-statements work, and goto-statements can really make 
the logic of your code confusing. Take a look at the following hyperbolic example.

```c#
var i = 0;
A:
if (i is < -100 or > 100) { goto B; }
Console.WriteLine($"Working on {i}");
i += int.IsEvenInteger(i) ? 10 : -10;
goto A;
B:;
```

Do you know what this code does? It's pretty confusing to look at (mainly because I purposefully used bad label 
names). The above code outputs the following to the console. See if you can try figuring out what the code outputs 
before looking at the answer!

```text
Working on 0
Working on 10
Working on 20
Working on 30
Working on 40
Working on 50
Working on 60
Working on 70
Working on 80
Working on 90
Working on 100
```

Anything surprising? We wrote a for-loop without a for-loop! This is actually what for-loops end up being when your 
code is compiled! While-loops are similar. The above code is equivalent to the following code.

```c#
for (var i = 0; i is >= -100 and <= 100; i += int.IsEvenInteger(i) ? 10 : -10)
{
    Console.WriteLine($"Working on {i}");
}
```

While the loop is still a somewhat confusing loop, the code is much clearer now! The takeaway here is that you 
should *avoid goto-statements at all costs*. They break the normal flow of logic, they make code more confusing, and 
there are usually other statements or clauses that could replace the uses of goto-statements. What was the point of 
learning about them, then? We can use them to break out of nested loops!

##### Breaking Out of Nested Loops with Goto-statements

Remember the following example from earlier?

```c#
for (var i = 0; i < 5; ++i)
{
    var done = false;
    for (var j = 0; j < 5; ++j)
    {
        if (i == 2 && j == 2)
        {
            done = true;
            break;
        }
        Console.Write(j + " ");
    }
    if (done) { break; }
    Console.WriteLine();
}
```

We can use a goto-statement to avoid the extra work and simply break out of both loops at the same time.

```c#
for (var i = 0; i < 5; ++i)
{
    for (var j = 0; j < 5; ++j)
    {
        if (i == 2 && j == 2) { goto OuterLoopEnd; }
        Console.Write(j + " ");
    }
    Console.WriteLine();
}
OuterLoopEnd:;
```

This code outputs the same output as before, but it's definitely written in a cleaner way. Breaking out of nested 
loops is the one acceptable use of goto-statements in C#. Make sure your labels are as readable as possible when you 
do this!
