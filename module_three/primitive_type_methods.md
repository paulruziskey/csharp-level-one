# Working with Primitive Types

Primitive types are considered basic values in C#. This means we can't call most methods directly on primitive types.
They were designed to be basic, so there's very little we can do with primitive values. We can, however, call 
methods from the data types themselves! These types of methods are known as *utility methods* since they provide 
utilities that don't normally exist for instances of particular data types. The following sections will outline a 
few useful utility methods for primitive types!

## Checking Properties of Numeric Values

We can check different properties of numeric values using utility methods. The most useful to us right now are 
methods for checking the parity of numeric values.

We will explore other numeric-property utility methods as we need them.

### Checking Parity of Numeric Values

We can check whether an integral value is even using the `IsEvenInteger` and `IsOddInteger` methods. These exist for 
all integral types except `char` as well as all floating-point types.

#### Checking Parity for Integral Values

The following code demonstrates checking parity of integral values.

```c#
const int number1 = 7;
const short number2 = 5;
const sbyte number3 = 2;
Console.WriteLine($"{number1} is odd: {int.IsOddInteger(number1)}");
Console.WriteLine($"{number2} is even: {short.IsEvenInteger(number2)}");
Console.WriteLine($"{number3} is even: {sbyte.IsEvenInteger(number3)}");
```

The above code outputs the following to the console.

```text
7 is odd: True
5 is even: False
2 is even: True
```

Make sure to match the data type you call the method from with the data type of the value!

#### Checking Parity for Non-integral Values

We can also check parity for floating-point values. Any floating-point values that aren't whole numbers are 
automatically neither even nor odd. Floating-point whole numbers are then checked for parity like their integral 
counterparts. The following code demonstrates this with doubles, but it applies to all floating-point types.

```c#
const double nonIntegralNumber = 3.3;
const double evenIntegralNumber = 2.0;
const double oddIntegralNumber = 3.0;
Console.WriteLine(
    $"{nonIntegralNumber} - even: {double.IsEvenInteger(nonIntegralNumber)}, odd: {double.IsOddInteger(nonIntegralNumber)}"
);
Console.WriteLine(
    $"{evenIntegralNumber} - even: {double.IsEvenInteger(evenIntegralNumber)}, odd: {double.IsOddInteger(evenIntegralNumber)}"
);
Console.WriteLine(
    $"{oddIntegralNumber} - even: {double.IsEvenInteger(oddIntegralNumber)}, odd: {double.IsOddInteger(oddIntegralNumber)}"
);
```

The above code outputs the following to the console.

```text
3.3 - even: False, odd: False
2 - even: True, odd: False
3 - even: False, odd: True
```

## Properties of Characters

### Checking Properties of Characters

We can check whether characters have certain properties. The following code demonstrates a few useful utility 
methods, but this is far from an exhaustive example.

```c#
const char letter = 'c';
Console.WriteLine($"{letter} is lowercase: {char.IsLower(letter)}");
Console.WriteLine($"{letter} is uppercase: {char.IsUpper(letter)}");
Console.WriteLine($"{letter} is whitespace: {char.IsWhiteSpace(letter)}");
Console.WriteLine($"{letter} is alphabetic: {char.IsLetter(letter)}");
// Determines if character is decimal digit (0 – 9).
Console.WriteLine($"{letter} is digit: {char.IsDigit(letter)}");
// Determines if character is any kind of numeric character (digit, fraction, superscript, subscript, etc.)
Console.WriteLine($"{letter} is numeric: {char.IsNumber(letter)}");
Console.WriteLine($"{letter} is alphabetic or digit: {char.IsLetterOrDigit(letter)}");
Console.WriteLine($"{letter} is punctuation: {char.IsPunctuation(letter)}");
Console.WriteLine($"{letter} is in the alphabet: {char.IsBetween(letter, 'a', 'z')}");
```

The above code outputs the following to the console.

```text
c is lowercase: True
c is uppercase: False
c is whitespace: False
c is alphabetic: True
c is digit: False
c is numeric: False
c is alphabetic or digit: True
c is punctuation: False
c is in the alphabet: True
```

### Modifying Properties of Characters

We can use utility methods to get modified versions of characters. The main two that we're interested in are the 
utility methods for getting uppercase and lowercase versions of characters.

```c#
const char letter = 'a';
Console.WriteLine($"{letter} as uppercase char: {char.ToUpper(letter)}");
Console.WriteLine($"{letter} as lowercase char: {char.ToLower(letter)}");
```

The above code outputs the following to the console.

```text
a as uppercase char: A
a as lowercase char: a
```

For characters that don't have uppercase and lowercase variants the original character is returned by both methods.

## Parsing Values from Strings

We can also use utility methods to help us parse primitive values from strings.

### `Parse` Method

Previously, we used the methods in the `Convert` utility class to parse primitive values from strings. There are 
similar methods in each of the primitive types which work much in the same way. Each primitive type has its own 
version of the `Parse` method. The following code demonstrates using the `int.Parse` method to parse an integer from 
a string.

```c#
Console.Write("Enter an integer: ");
var number = int.Parse(Console.ReadLine()!);
Console.WriteLine($"You entered {number}");
```

The above code outputs the following to the console with the following input.

```text
Enter an integer: 5
You entered 5
```

The same code could be written using the `Convert.ToInt32` method.

```c#
Console.Write("Enter an integer: ");
var number = Convert.ToInt32(Console.ReadLine());
Console.WriteLine($"You entered {number}");
```

For the most part, the methods in the `Convert` utility class and the various `Parse` methods do the same thing. 
However, there is a subtle difference, which you can tell if you notice that we need `!` when using the `int.Parse` 
method, but not when using the `Convert.ToInt32` method. That's because the `Convert.ToInt32` method returns 0 when 
it gets `null`, whereas the `int.Parse` method throws an exception. We haven't discussed `null` yet, but it's 
important to mention it here since it's the only difference. We use the methods in the `Convert` utility class since 
they don't throw exceptions when they encounter `null`. Once we learn about `null` and nullable types, this will 
make more sense.

### `TryParse` Method

Now that we know about conditional statements, we can use the `TryParse` methods to parse user input without crashing!

Until now, any bad input resulted in an exception being thrown. This isn't great since it's not unexpected for a user
to accidentally enter the wrong thing. It's also possible that people may try to abuse a piece of software by
entering bad inputs. Luckily, C# provides the `TryParse` methods! Each basic built-in type has a `TryParse` method 
which will return a boolean signaling whether valid input was entered. Let's take a look at some code using the 
`TryParse` method for integers.

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
