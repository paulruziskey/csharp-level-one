# Strings

## String Literals

### Basic String Literals

Enclosing text in double quotes creates a *string literal*. String literals can then be assigned to variables to 
create `string` objects. The following code demonstrates creating a string from a string literal.

```c#
var sentence = "Hello, world!";
```

#### Escape Sequences

We can also include *escape characters* in string literals. Escape characters are characters formed by escaping 
another character with the *escape character* (`\`). We can use these escape characters to include newlines and tabs in
strings, among other things. The following code demonstrates using escape characters for newline (`\n`) and tab (`\t`).

```c#
Console.WriteLine("\tEach\nword\nwill\nbe\non\nits\nown\nline");
```

The above code outputs the following to the console.

```text
    Each
word
will
be
on
its
own
line
```

We can also use the escape character to help us output characters we would otherwise have trouble with. For example, 
you can't normally output a double quote since C# would treat it as the end of the string literal. A similar problem
exists when trying to write a backslash character in a string literal since backslash is the escape character. The
following code demonstrates how we can output double quotes and backslashes using escape characters.

```c#
Console.WriteLine("Here is a \"backslash\": \\");
```

The above code outputs the following to the console.

```
Here is a "backslash": \
```

### Raw String Literals

Sometimes we want to write strings which would end up spanning multiple lines in the console. This means we would 
need to include a lot of newline characters, which would make it a bit hard to read the string. This is where *raw 
string literals* come in! These string literals will ignore all escape sequences, meaning backslashes will work just 
fine without escaping. Raw strings also let us span multiple lines, and any formatting in a raw string literal 
becomes part of the final string! This means if we indent in the raw string, the indentation will be in the actual 
string! The following code demonstrates creating a string from a raw string literal.

```c#
const string dialog = """
    It was time to write some code.
        "Hello, world!" said the code.
        "Goodbye, code!" said the programmer, fearing his creation had
    become sentient.
    """;
Console.WriteLine(dialog);
```

The above code outputs the following to the console.

```text
It was time to write some code.
    "Hello, world!" said the code.
    "Goodbye, code!" said the programmer, fearing his creation had
become sentient.
```

Notice how the formatting is remembered by the string and now none of the double quotes needed escaping? This is the 
power of raw string literals! Definitely make use of them when you need a string that spans multiple lines.

When declaring a raw string literal, the opening triple double quotes and the closing triple double quotes must be 
on their own lines. You can also include `$` before the opening triple double quotes to make it interpolated!

## String Properties and Methods

### Concatenation

*Concatenation* is when we combine multiple strings into one string. To concatenate strings, we use the *addition operator*
(`+`).

```c#
Console.Write("Enter a word: ");
string word1 = Console.ReadLine()!;
Console.Write("Enter another word: ");
string word2 = Console.ReadLine()!;
Console.WriteLine(word1 + word2);
```

The above code outputs the following to the console.

```text
Enter a word: hello
Enter another word: world
helloworld
```

Concatenation is useful when we want to simply combine two or more strings. If we want to build a string from many
different values, or if we want to combine a string literal and a value for outputting, it's better to use an interpolated
string literal.

### `Length` Property and Indexing

If we want to get the length of a string (i.e., the number of Unicode characters), we can use the `Length` property. 

If we want to get a character at a particular index value, we can use the *element-access operator* (`[]`) to do so.

The following code demonstrates the `Length` property and the element-access operator.

```c#
const string word = "hello";
Console.WriteLine($"{word} has {word.Length} character(s) in it!");
Console.WriteLine($"{word} starts with the letter {word[0]}");
```

What if we wanted to get the last letter in `word`? We would need to use the `Length` property to get the last index 
value. This is demonstrated in the following code.

```c#
Console.WriteLine($"{word} ends with the letter {word[word.Length - 1]}");
```

This is a little annoying since it makes everything longer. Luckily for us, C# has the *index-from-end operator* 
(`^`) which lets us index from the end of the string instead of the beginning! The following code does the same 
thing as the above code.

```c#
Console.WriteLine($"{word} ends with the letter {word[^1]}");
```

`^1` is actually syntactic sugar for `word.Length - 1`. This means that `^n` translates to `word.Length - n`. This 
definitely makes the code nicer to read and write!

### Substrings Using Ranges

We can also get a substring by using a `Range` object. Ranges are created using the *range operator* (`..`). `a..b` 
creates a range starting from `a` and ending at the value *before* `b`. This means the starting value is *inclusive* 
while the ending value is *exclusive*. If we want a range that starts at zero and ends before a particular value, we 
can leave off the zero. `..b` creates a range starting from zero and ending at the value before `b`. Likewise, if we 
want to create a range starting at some value and ending at the end of a string, we can leave off the ending value. 
`a..` creates a range starting from `a` and ending at the end of the string. The following code demonstrates using 
different ranges to get substrings.

```c#
const string word = "hello";
Console.WriteLine(word[1..4]);
Console.WriteLine(word[..3]);
Console.WriteLine(word[2..]);
```

The above code outputs the following to the console.

```text
ell
hel
llo
```

### Inclusion

If we want to check if a string contains a particular character or substring, we can use the `Contains` method. We 
can use the method alone to check for a particular character or substring as written, or we can include an 
additional argument to specify that the check should be done *case-insensitively*. This means that we could ask if a 
string contains the letter a by only checking `'a'` case-insensitively. The following code demonstrates both uses of 
the `Contains` method.

```c#
const string word = "Apple";
Console.WriteLine(word.Contains('a')); // case-sensitive
Console.WriteLine(word.Contains('a', StringComparison.OrdinalIgnoreCase)); // case-insensitive
```

The above code outputs the following to the console.

```text
False
True
```

If we want to get the index value of the first occurrence of a particular character or substring, we can use the 
`IndexOf` method. The following code demonstrates this.

```c#
const string word = "apple";
Console.WriteLine($"Index of 'p': {word.IndexOf('p')}");
```

The above code outputs the following to the console.

```text
Index of 'p': 1
```

`IndexOf` can also be performed case-insensitively the same way `Contains` can.

### Equality

If we want to check if two strings are equal, we simply use the *equals operator* (`==`). This will perform a 
case-sensitive check. If we want to check if two strings are equal without worrying about case, we can use the 
`Equals` method with an additional argument. Without the additional argument, the `Equals` method does the same 
thing as the equals operator. The following code demonstrates using the equals operator and the `Equals` method.

```c#
const string word1 = "apple";
const string word2 = "APPLE";
Console.WriteLine(word1 == word2); // case-sensitive
Console.WriteLine(word1.Equals(word2)); // same as `==`
Console.WriteLine(word1.Equals(word2, StringComparison.OrdinalIgnoreCase)); // case-insensitive
```

The above code outputs the following to the console.

```text
False
False
True
```

### Ordering

If we want to see how one string compares to another, we can use the `CompareTo` method. This method supports both 
case-sensitive and case-insensitive checking.

When comparing strings for ordering, C# will compare them *lexicographically*. This means they will be compared for 
their alphabetical ordering. The `CompareTo` method will return a negative number if the first string comes first in 
the alphabet, a positive number if the first string comes second in the alphabet, and a zero if they're the same 
word. The following code demonstrates using the `CompareTo` method.

```c#
const string word1 = "apple";
const string word2 = "banana";
const string word3 = "APPLE";
Console.WriteLine(word1.CompareTo(word2)); // case-sensitive
Console.WriteLine(word1.CompareTo(word3));
Console.WriteLine(word1.CompareTo(word2, StringComparison.OrdinalIgnoreCase)); // case-insensitive
Console.WriteLine(word1.CompareTo(word3, StringComparison.OrdinalIgnoreCase));
```

The above code outputs the following to the console.

```text
-1
-1
-1
0
```

The first -1 makes sense since "apple" comes before "banana" in the alphabet. The reason for the second -1 is 
because 'A' actually comes before 'a' in Unicode, and the comparison was case-sensitive. The third -1 is because 
"apple" still comes before "banana"; case doesn't affect this answer. We then get 0 for the last answer since 
"apple" and "APPLE" are the same word when compared case-insensitively.

### Parsing Helpers

It's often desirable to get rid of stray whitespace around a string when we need to parse it. C# strings have a 
`Trim` method which strips leading and trailing whitespace characters. You can also use this method to strip other 
things besides whitespace characters, but you'll mostly use it to strip whitespace characters.

```c#
Console.Write("Enter something: ");
string trimmed_input = Console.ReadLine()!.Trim();
Console.WriteLine($"You entered: \"{trimmed_input}\"");
```

The above code outputs the following to the console.

```text
Enter something:         okay      
You entered: "okay"
```

It's also possible to convert a string to all uppercase or all lowercase. We'll learn in the next module that it might be more desirable to convert a string to lowercase to compare it rather than using case-insensitive comparisons, so these methods are useful in those contexts.

```c#
Console.Write("Enter a word: ");
string word = Console.ReadLine()!;
Console.WriteLine(word.ToLower());
Console.WriteLine(word.ToUpper());
```

The above code outputs the following to the console.

```text
Enter a word: Hello
hello
HELLO
```

## String Immutability

Strings in C# are *immutable*. This means they can't be changed once created. Even though a lot of string 
methods in C# seem like they modify a string, they're actually creating a copy with the modified property and 
returning that. This is important to know because it can affect the performance of your code. We'll learn 
a big consequence of this in a later module.
