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

It's also possible to convert a string to all uppercase or all lowercase. These methods can be helpful when it's not 
possible to perform case-insensitive comparisons in the traditional way.

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

### Concatenation

*Concatenation* is when we combine multiple strings into one string. To concatenate strings, we use the *addition 
operator* (`+`).

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
different values, or if we want to combine a string literal and a value for outputting, it's better to use an 
interpolated string literal.

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

#### `Contains` and `ContainsAny` Methods

If we want to check if a string contains a particular character or substring, we can use the `Contains` method. We 
can use the method alone to check for a particular character or substring as written, or we can include an 
additional argument to specify that the check should be done *case-insensitively*. This means that we could ask if a 
string contains the letter a by only checking `'a'` case-insensitively. The following code demonstrates both uses of 
the `Contains` method. It also demonstrates searching for a substring both case-sensitively and case-insensitively.

```c#
const string word = "Apple";
Console.WriteLine(word.Contains('a')); // case-sensitive single-character search
Console.WriteLine(word.Contains('a', StringComparison.OrdinalIgnoreCase)); // case-insensitive single-character search
Console.WriteLine(word.Contains("app")); // case-sensitive substring search
Console.WriteLine(word.Contains("app", StringComparison.OrdinalIgnoreCase)); // case-insensitive substring search
```

The above code outputs the following to the console.

```text
False
True
False
True
```

Sometimes we want to search for one of many possible characters in a string. We can do this using the `ContainsAny` 
method. This method is a bit more complicated to use than the plain `Contains` method because C# requires a specialized 
argument when we specify the characters to look for. This is done to increase the efficiency of the search. To use the
`ContainsAny` method, we need to create a `SearchValues` object out of the characters. The following code demonstrates 
searching a string for any vowels.

```c#
const string word = "hello";
Console.WriteLine($"`word` contains vowels: {word.ContainsAny(System.Buffers.SearchValues.Create('a', 'e', 'i', 'o', 'u'))}");
```

The above code outputs the following to the console.

```text
`word` contains vowels: True
```

To create a `SearchValues` object, we use the `Create` method. That much might be straightforward, but what's with the
`System.Buffers` prefix?

##### Namespaces

A *namespace* is like a virtual folder for a particular piece of code. C# code is organized into various namespaces to 
keep different parts of the language organized. This helps make sure data types with similar names are kept separate so 
they won't conflict with each other. Older languages had this problem of names conflicting a lot, so a lot of languages 
these days have something like namespaces to help separate code.

`System` is a namespace for basic C# code. This is where you'll find all of the code we'll be using in this course.
`Buffers` is a namespace within the `System` namespace which holds data types related to storing values and objects. 
We'll learn what buffers are later in the course. The `SearchValues` data type is meant for storing data to be searched 
for, which is why it's in the `Buffers` namespace.

Now that we know about namespaces, does this mean some of the data types we use will require long names all the time?

##### Using-statements

Fear not, because C# has *using-statements*. Using-statements allow us to bring a name from a namespace into the
*global namespace*. You can think of the global namespace as the top namespace, meaning anything in the global 
namespace doesn't require any prefixes to use it. The data types we've been using so far are all part of this global 
namespace! Additionally, new C# projects are set up to automatically put a bunch of commonly used types into the global 
namespace so we don't have to think about it. For any types that aren't already in the global namespace, we can use a 
using-statement to bring the names from a particular namespace into the global namespace. The following code 
demonstrates using a using-statement to bring the `SearchValues` type and other types in the `System.Buffers` namespace 
into the global namespace. It's the same code as before, but now the `SearchValues` type doesn't require a namespace 
prefix!

```c#
using System.Buffers;

const string word = "hello";
Console.WriteLine($"`word` contains vowels: {word.ContainsAny(SearchValues.Create('a', 'e', 'i', 'o', 'u'))}");
```

Using-statements are always used to make sure we don't have to type namespaces in front of the types we use. The only 
time they can't be used is if you need to use different data types from different namespaces that happen to have the 
same name. This is rare, but if it does happen, you can rely on the namespace to help differentiate them!

Using-statements always go at the top of your code, and they should be written in alphabetical order according to the 
namespaces.

For simplicity, the above code can be written with all the characters in one string. Now that you know about 
using-statements, you should assume a using-statement is present in any code snippets where it's not visible. In these 
lessons, using statements will always be included the first time a type is used. They will then be assumed for 
subsequent occurrences.

```c#
const string word = "hello";
Console.WriteLine($"`word` contains vowels: {word.ContainsAny(SearchValues.Create("aeiou"))}");
```

If you want to perform this search case-insensitively, the easiest way is to lowercase the string first before 
searching. There is a way to create a `SearchValues` object that performs case-insensitive searching, but it's much 
more difficult given what you currently know. The following code demonstrates this.

```c#
const string word = "HELLO";
Console.WriteLine($"`word` contains vowels: {word.ContainsAny(SearchValues.Create("aeiou"))}");
Console.WriteLine($"`word` contains vowels: {word.ToLower().ContainsAny(SearchValues.Create("aeiou"))}");
```

The above code outputs the following to the console.

```text
`word` contains vowels: False
`word` contains vowels: True
```

#### `IndexOf`, `LastIndexOf`, `IndexOfAny`, and `LastIndexOfAny` Methods

If we want to get the index value of the first occurrence of a particular character or substring, we can use the 
`IndexOf` method. The following code demonstrates this.

```c#
const string word = "apple";
Console.WriteLine($"Index of 'p': {word.IndexOf('p')}");
Console.WriteLine($"Index of 'z': {word.IndexOf('z')}");
Console.WriteLine($"Index of \"ple\": {word.IndexOf("ple")}");
```

The above code outputs the following to the console.

```text
Index of 'p': 1
Index of 'z': -1
Index of "ple": 2
```

When checking for the index of a substring, the returned value will be the index value of the first character in the 
substring. If there are no occurrences of a character or substring, `-1` is returned.

Sometimes we want to find additional occurrences of characters or substrings after the first occurrence. We can do this 
by providing the `IndexOf` method with a starting index value so it will only find occurrences from that index value to 
the end of the string. The following code demonstrates this.

```c#
const string word = "apple";
int indexOfFirstP = word.IndexOf('p');
int indexOfSecondP = word.IndexOf('p', indexOfFirstP + 1);
Console.WriteLine($"Index values of 'p': {indexOfFirstP}, {indexOfSecondP}");
```

The above code outputs the following to the console.

```text
Index values of 'p': 1, 2
```

Additionally, we can provide a count of how many characters should be searched in total. The following code 
demonstrates finding the index of a substring only in the first half of a string.

```c#
const string phrase = "appleapple";
Console.WriteLine($"Index of \"ea\": {phrase.IndexOf("ea", 0, 5)}"); // starting at index 0 searching 5 characters
Console.WriteLine($"Index of \"ea\": {phrase.IndexOf("ea", 0, 6)}"); // starting at index 0 searching 6 characters
```

The above code outputs the following to the console.

```text
Index of "ea": -1
Index of "ea": 4
```

The first call to `IndexOf` returns -1 since there is no "ea" within the first five characters of the string. When the 
count is set to 6, the "ea" in the string can now be located.

`IndexOf` can be performed case-insensitively the same way `Contains` can.

If you want the last occurrence of a character or substring instead of the first, you can use the `LastIndexOf` method.

Just like the `ContainsAny` method, there is an equivalent `IndexOfAny` method which will get the index value of the 
first occurrence of one of a bunch of characters. The following code demonstrates this.

```c#
const string word = "hello";
Console.WriteLine($"Index of the first vowel: {word.IndexOfAny(SearchValues.Create("aeiou"))}");
```

The above code outputs the following to the console.

```text
Index of the first vowel: 1
```

`IndexOfAny` can be performed case-insensitively the same way `ContainsAny` can.

If you want the last occurrence of one of a bunch of characters instead of the first occurrence, you can use the
`LastIndexOfAny` method.

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

## String Immutability

Strings in C# are *immutable*. This means they can't be changed once created. Even though a lot of string methods in 
C# seem like they modify a string, they actually create a copy with the modified property and return that. This is 
important to know because it can affect the performance of your code. We'll learn a big consequence of this in a later 
module.
