# Boolean Expressions

*Boolean expressions* are expressions that return booleans. Boolean expressions can be as simple as a single boolean 
variable, or they can involve *equality operators*, *relational operators*, *logical operators*, or even *patterns*.

## Equality Operators

Equality operators are operators that compare objects for equality. We will discuss comparing objects for equality 
in more detail later since there's more than initially meets the eye, but for now, we'll focus on simple value 
equality which is very straightforward. The following table shows the equality operators in C#.

| Name                | Operator |
|---------------------|----------|
| Equality Operator   | `==`     |
| Inequality Operator | `!=`     |

The above operators all return booleans to reflect the result of the comparison. The following code demonstrates
using the equality operator.

```c#
Console.WriteLine($"3 == 4: {3 == 4}");
```

The above code outputs the following to the console.

```text
3 == 4: False
```

## Relational Operators

Relational operators are operators used for comparing objects. The following table shows the relational operators in C#.

| Name                           | Operator |
|--------------------------------|----------|
| Less-than Operator             | `<`      |
| Less-than-or-equal Operator    | `<=`     |
| Greater-than Operator          | `>`      |
| Greater-than-or-equal Operator | `>=`     |

The above operators all return booleans to reflect the result of the comparison. The following code demonstrates 
using the less-than operator.

```c#
Console.WriteLine($"3 < 4: {3 < 4}");
```

The above code outputs the following to the console.

```text
3 < 4: True
```

## Logical Operators

Logical operators are operators for combining or manipulating booleans. Each of these operators represents a 
fundamental operation for any computer. We will look at each operator one by one along with its *truth table* to 
understand how they work. When reading truth tables, *A* and *B* are arguments to the operator.

### Logical-and Operator

The logical-and operator (`&&`) evaluates to `true` if both arguments are `true`. Below is the truth table for the 
logical-and operator. *AB* is read as *A and B*.

| A | B | AB |
|---|---|----|
| F | F | F  |
| F | T | F  |
| T | F | F  |
| T | T | T  |

We can see that *A* and *B* must both be `true` for the logical-and operator to evaluate to `true`. The following code 
demonstrates using the logical-and operator.

```c#
Console.WriteLine($"3 is between 1 and 5: {1 <= 3 && 3 <= 5}");
```

The above code outputs the following to the console.

```text
3 is between 1 and 5: True
```

### Logical-or Operator

The logical-or operator (`||`) evaluates to `true` if at least one argument is `true`. Below is the truth table for the 
logical-or operator. *A + B* is read as *A or B*.

| A | B | A + B |
|---|---|-------|
| F | F | F     |
| F | T | T     |
| T | F | T     |
| T | T | T     |

We can see that as long as one argument is `true`, the logical-or operator will evaluate to `true`. The following 
code demonstrates using the logical-or operator.

```c#
Console.WriteLine($"3 is greater than 10 or less than zero: {3 > 10 || 3 < 0}");
```

The above code outputs the following to the console.

```text
3 is greater than 10 or less than zero: False
```

### Logical-not Operator

The logical-not operator (`!`) evaluates to `true` if its argument is `false`, and vice versa. Below is the truth 
table for the logical-not operator. *~A* is read as *Not A*.

| A | ~A |
|---|----|
| F | T  |
| T | F  |

The logical-not operator inverts the value of its argument. The following code demonstrates using the logical-not 
operator.

```c#
Console.WriteLine($"3 is not even: {!int.IsEvenInteger(3)}");
```

The above code outputs the following to the console.

```text
3 is not even: True
```

Of course, it would make more sense to use the `int.IsOddInteger` method, but the above code showcases the 
logical-not operator.

## Pattern Basics

Patterns are a way to match an object against a particular "shape" of object. This is a fairly abstract way of 
putting it, but think of it like we're trying to match an object against particular qualities it might have. We can 
create boolean expressions matching against patterns using the `is` operator, providing an object to match, and 
providing a pattern to match against. There is a bit of a catch with patterns, however: patterns must only use
constants, but in a lot of cases, this isn't a problem. The following code demonstrates matching a user-provided 
value against a pattern to see if it's negative.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"Your number is negative: {number is < 0}");
```

The above code outputs the following to the console.

```text
Enter an integer: 7
Your number is negative: False
```

In the above example, `number` is the object to match, and `< 0` is the pattern to match against. There is little 
reason to use a pattern in the above example since we could have just asked `number < 0`, but where patterns really 
shine is when we combine them using the *pattern-matching operators*.

Patterns have their own equivalent operators to the logical operators above. Patterns use `and`, `or`, and `not` to 
combine and manipulate patterns according to the rules of the equivalent logical operators. The following code 
demonstrates using patterns to check if a value is between two other values.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"Your number is a single digit: {number is >= 0 and <= 9}");
```

The above code outputs the following to the console.

```text
Enter an integer: 7
Your number is a single digit: True
```

In the above example, patterns allowed us to avoid duplicating the `number` variable. Patterns let us to a lot of 
cool things that we'll investigate later, but for now, this is how we'll use them.

Since patterns involve matching an object against something, if we want to check if an object is equal to another 
object, we can simply use that object as the pattern. The following code demonstrates this.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"You entered the number 3 or the number 5: {number is 3 or 5}");
```

The above code outputs the following to the console.

```text
Enter an integer: 5
Your entered the number 3 or the number 5: True
```
