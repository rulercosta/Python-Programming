# Advanced topics in Python
## (to be updated in the future)

### Topics covered here, in no particular order, are the ones which are either too speific to Python or I am too stupid to remember their use cases and syntax quite.

## File Handling

File handling is the process of reading and writing data to and from files. Python provides various functions and methods for working with files, such as ``open()``, ``read()``, ``write()``, ``close()``, etc.

To open a file, use the ``open()`` function, which takes the file name and the mode as arguments and returns a file object. The mode specifies how you want to open the file, such as:

- ``'r'`` : Read mode, the default mode. Opens the file for reading only.
- ``'w'`` : Write mode. Opens the file for writing only. If the file exists, it will be overwritten. If the file does not exist, it will be created.
- ``'a'`` : Append mode. Opens the file for writing only. If the file exists, the data will be appended to the end of the file. If the file does not exist, it will be created.
- ``'r+'`` : Read and write mode. Opens the file for both reading and writing.
- ``'w+'`` : Write and read mode. Opens the file for both writing and reading. If the file exists, it will be overwritten. If the file does not exist, it will be created.
- ``'a+'`` : Append and read mode. Opens the file for both writing and reading. If the file exists, the data will be appended to the end of the file. If the file does not exist, it will be created.

One can also specify the encoding of the file, such as ``'utf-8'``, ``'ascii'``, etc.

An example of opening a file in write mode and writing some data to it:

```python
file = open('test.txt', 'w', encoding='utf-8')
file.write('Hello, world!')
file.close()
```
This will create a file named ``test.txt`` in the current directory and write the string ``'Hello, world!'`` to it.

To read data from a file, there are various methods, such as:

- ``read()`` : Reads the entire file and returns a string.
- ``readline()`` : Reads one line from the file and returns a string.
- ``readlines()`` : Reads all the lines from the file and returns a list of strings.

An example of opening a file in read mode and reading its contents:
```python
file = open('test.txt', 'r', encoding='utf-8')
data = file.read()
print(data)
file.close()
```
Output:
```python
Hello, world!
```
It is important to close the file after it is done with it, as it frees up the resources and avoids any potential errors. Use the ``close()`` method to close the file, or use the ``with`` statement, which automatically closes the file for you. For example:
```python
with open('test.txt', 'r', encoding='utf-8') as file:
    data = file.read()
    print(data)
```
Output:
```python
Hello, world!
```
## Exception Handling

Exception handling is the process of dealing with errors and unexpected situations that may occur during the execution of a program. Python provides various mechanisms for handling exceptions, such as:

- ``try`` : A block of code that may raise an exception.
- ``except`` : A block of code that handles a specific type of exception.
- ``else`` : A block of code that executes if no exception is raised in the try block.
- ``finally`` : A block of code that always executes, regardless of whether an exception is raised or not.

An example of exception handling in Python:

```python
try:
    x = int(input('Enter a number: '))
    y = 10 / x
    print(y)
except ZeroDivisionError:
    print('Cannot divide by zero')
except ValueError:
    print('Invalid input')
else:
    print('No exception occurred')
finally:
    print('This is always executed')
```
This program asks the user to enter a number and prints the result of dividing 10 by that number. However, it may raise two types of exceptions:

- ``ZeroDivisionError`` : If the user enters 0, the program will try to divide 10 by 0, which is not allowed in Python and will raise a ``ZeroDivisionError``.
- ``ValueError`` : If the user enters something that is not a valid integer, such as a letter or a symbol, the program will try to convert it to an integer using the  ``int()`` function, which will raise a ``ValueError``.

The program uses the ``try`` block to enclose the code that may raise an exception, and the ``except`` blocks to handle each type of exception separately. If an exception is raised, the corresponding ``except`` block will execute and the rest of the try block will be skipped. If no exception is raised, the ``else`` block will execute. The ``finally`` block will always execute, regardless of whether an exception is raised or not.

Some possible outputs of the program:

```
Enter a number: 5
2.0
No exception occurred
This is always executed
```
```
Enter a number: 0
Cannot divide by zero
This is always executed
```
```
Enter a number: a
Invalid input
This is always executed
```

## Closure function

A closure is a function that can access and modify the variables of the enclosing scope, even after the scope is exited. A closure is created when a nested function is returned by the outer function. The nested function can access the variables of the outer function, and those variables are said to be closed over by the nested function.

Closures are useful for creating function factories, which are functions that can generate specialized functions based on some parameters. Closures can be used to implement decorators, which are functions that modify the behavior of other functions.

An example of a closure in Python:

```python
def make_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

times3 = make_multiplier(3)
times5 = make_multiplier(5)

print(times3(4)) # 12
print(times5(4)) # 20
```
Function named ``make_multiplier`` takes a parameter ``n`` and returns a nested function named ``multiplier`` that takes another parameter ``x`` and returns the product of ``x`` and ``n``. The nested function multiplier is a closure that can access and modify the variable n of the outer function ``make_multiplier``, even after the outer function is exited.

The code then creates two closures, ``times3`` and ``times5``, by calling the ``make_multiplier`` function with different values of ``n``. The closures ``times3`` and ``times5`` are specialized functions that can multiply any number by 3 and 5, respectively.

## Operator Overloading

Operator overloading is the process of defining how operators, such as ``+``, ``-``, ``*``, ``/``, etc., behave when applied to objects of a custom class. Operator overloading allows to customize the behavior of classes and make them more intuitive and expressive.

To overload an operator, implement a special method in your class that corresponds to the operator. The special method name follows the format ``op``, where ``op`` is the operator symbol. For example, the special method for the ``+`` operator is ``add``, the special method for the ``*`` operator is ``mul``, etc.

An example of overloading the ``+`` and ``*`` operators for a custom class named ``Vector`` that represents a two-dimensional vector:

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __mul__(self, other):
        return Vector(self.x * other, self.y * other)

    def __str__(self):
        return f'({self.x}, {self.y})'

v1 = Vector(2, 3)
v2 = Vector(4, 5)

print(v1 + v2) # (6, 8)
print(v1 * 2) # (4, 6)
```
This code defines a class named ``Vector`` that has two attributes, ``x`` and ``y``, that store the coordinates of the vector. The code t and s m methods, which define how the + and * operators work when applied to Vector objects. The code alsostrents the sostrents the __str__ method, which defines how the Vector objects are converted to strings when printed.

The code then creates two Vector objects, v1 and v2, and performs some operations on them using the overloaded operators. The code prints the results of the operations, which are also Vector objects.

## Lambda Functions

Lambda functions are anonymous functions that can be defined inline using the ``lambda`` keyword. Lambda functions are useful for creating simple functions that can be passed as arguments to other functions, such as ``map()``, ``filter()``, ``sorted()``, etc.

The syntax of a ``lambda`` function is:

```python
lambda parameters: expression
```
The parameters are optional and can be one or more variables separated by commas. The expression is a single statement that returns a value. The lambda function can access the variables of the enclosing scope, but cannot modify them.

Some examples of lambda functions and how to use them:

```python
# A lambda function that adds two numbers
add = lambda x, y: x + y
print(add(2, 3)) # 5

# A lambda function that returns the square of a number
square = lambda x: x ** 2
print(square(4)) # 16

# A lambda function that checks if a number is even
is_even = lambda x: x % 2 == 0
print(is_even(5)) # False

# A lambda function that reverses a string
reverse = lambda s: s[::-1]
print(reverse('hello')) # olleh

# Using lambda functions with map()
numbers = [1, 2, 3, 4, 5]
squares = map(lambda x: x ** 2, numbers)
print(list(squares)) # [1, 4, 9, 16, 25]

# Using lambda functions with filter()
numbers = [1, 2, 3, 4, 5]
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens)) # [2, 4]

# Using lambda functions with sorted()
words = ['apple', 'banana', 'cherry', 'date']
words_sorted_by_length = sorted(words, key=lambda x: len(x))
print(words_sorted_by_length) # ['date', 'apple', 'banana', 'cherry']
```
## Assert

The ``assert`` statement is a debugging tool that allows you to check if a condition is ``true`` and raise an ``AssertionError`` exception if it is ``false``. The ``assert`` statement has the following syntax:

```python
assert condition, message
```
The condition is an expression that evaluates to a boolean value. The message is an optional string that provides additional information about the error. The ``assert`` statement does nothing if the condition is ``true``, but raises an ``AssertionError`` with the message if the condition is ``false``.

The ``assert`` statement is useful for testing your assumptions and finding bugs in your code. You can use it to check the validity of your inputs, outputs, and intermediate results. However, you should not use it for handling runtime errors, such as invalid user input, network failures, etc. For those cases, you should use proper exception handling techniques.

Some examples of using the ``assert`` statement:

```python
# A function that calculates the factorial of a number
def factorial(n):
    assert n >= 0, 'n must be non-negative'
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

# Testing the function
print(factorial(5)) # 120
print(factorial(-1)) # AssertionError: n must be non-negative

# A function that checks if a string is a palindrome
def is_palindrome(s):
    assert isinstance(s, str), 's must be a string'
    return s == s[::-1]

# Testing the function
print(is_palindrome('racecar')) # True
print(is_palindrome(123)) # AssertionError: s must be a string
```
## @property
The ``@property`` decorator is a built-in decorator that allows you to define properties in a class, which are attributes that have getter and setter methods. Properties are useful for controlling the access and modification of the attributes, as well as adding some logic or validation to them.

To define a property, you need to use the ``@property`` decorator on a method that returns the value of the attribute. This method is called the getter method, and it defines the name of the property. To define a setter method, which allows you to assign a value to the property, you need to use the ``@property_name.setter`` decorator on another method that takes the value as an argument. You can also define a deleter method, which allows you to delete the property, by using the ``@property_name.deleter`` decorator on another method.

An example of defining a property in a class:

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @property
    def area(self):
        return 3.14 * self.radius ** 2

    @area.setter
    def area(self, value):
        self.radius = (value / 3.14) ** 0.5

    @area.deleter
    def area(self):
        self.radius = 0
```
This code defines a class named ``Circle`` that has an attribute named ``radius`` and a property named ``area``. The ``area`` property has a getter method that returns the area of the circle, a setter method that sets the radius based on the given area, and a deleter method that sets the radius to zero.

One can use the property as if it was a regular attribute, but behind the scenes, the getter, setter, and deleter methods will be invoked. For example:

```python
c = Circle(2)
print(c.radius) # 2
print(c.area) # 12.56
c.area = 50
print(c.radius) # 3.99
print(c.area) # 50.0
del c.area
print(c.radius) # 0
print(c.area) # 0.0
```

## Decorators

Decorators are a powerful feature of Python that allow you to modify the behavior of functions, classes, and methods at runtime without making permanent changes to their original structure. Decorators are useful for adding extra functionality, such as logging, caching, debugging, timing, etc.

A decorator is a function that takes another function as an argument and returns a modified function. The modified function typically wraps the original function and executes some code before and/or after calling the original function.

To apply a decorator to a function, you can use the ``@`` syntax, which is equivalent to passing the function to the decorator and assigning the result back to the function. For example:

```python
def hello():
    print('Hello, world!')

def uppercase(func):
    def wrapper():
        original_result = func()
        modified_result = original_result.upper()
        return modified_result
    return wrapper

@uppercase
def hello():
    print('Hello, world!')
```
This code defines a decorator named ``uppercase`` that converts the output of the original function to uppercase. The ``@uppercase`` line applies the decorator to the ``hello`` function, which is equivalent to:

```python
hello = uppercase(hello)
```
Calling the ``hello`` function, output gets modified:

```python
hello()
```
Output:

```
HELLO, WORLD!
```
Applying multiple decorators to a function, will result in them executing in the order they are stacked. For example:

```python
@decorator1
@decorator2
@decorator3
def func():
    pass
```
This is equivalent to:

```python
func = decorator1(decorator2(decorator3(func)))
```
One can also define decorators that accept arguments, which allow to customize the behavior of the decorator. To do this, define another function that takes the arguments and returns the actual decorator function. For example:

```python
def repeat(n):
    def decorator(func):
        def wrapper():
            for i in range(n):
                func()
        return wrapper
    return decorator

@repeat(3)
def hello():
    print('Hello, world!')
```
This code defines a decorator named ``repeat`` that takes an argument ``n`` and returns a decorator that repeats the original function ``n`` times. The ``@repeat(3)`` line applies the decorator to the ``hello`` function, which is equivalent to:

```python
hello = repeat(3)(hello)
```
Calling the hello function, will result in the output repeating three times:

```python
hello()
```
Output:

```
Hello, world!
Hello, world!
Hello, world!
```

## Shallow Copy and Deep Copy

Shallow copy and deep copy are two ways of copying objects in Python. Shallow copy creates a new object that references the same elements as the original object, while deep copy creates a new object that contains copies of the elements of the original object.

Shallow copy and deep copy are useful for working with mutable objects, such as lists, dictionaries, sets, etc., that can be modified after they are created. Shallow copy and deep copy can affect how the changes made to the original object or the copied object are reflected in the other object.

To create a shallow copy of an object, use the ``copy()`` method of the ``copy`` module, or the slicing operator ``[:]`` for sequences. To create a deep copy of an object, use the ``deepcopy()`` method of the ``copy`` module.

An example of shallow copy and deep copy in Python:

```python
import copy

lst1 = [1, 2, [3, 4]]
lst2 = copy.copy(lst1) # shallow copy
lst3 = copy.deepcopy(lst1) # deep copy

lst1[0] = 10 # change the first element of lst1
lst1[2][0] = 30 # change the first element of the sublist of lst1

print(lst1) # [10, 2, [30, 4]]
print(lst2) # [1, 2, [30, 4]]
print(lst3) # [1, 2, [3, 4]]
```
This code creates a list named ``lst1`` that contains two integers and a sublist. The code then creates two copies of ``lst1``, one using the ``copy()`` method and one using the ``deepcopy()`` method. The code then modifies the first element of ``lst1`` and the first element of the sublist of ``lst1``.

The code prints the three lists and shows the differences between shallow copy and deep copy. The shallow copy ``lst2`` references the same elements as ``lst1``, so the changes made to the sublist of ``lst1`` are also reflected in ``lst2``. However, the changes made to the first element of ``lst1`` are not reflected in ``lst2``, because the shallow copy created a new object for the top-level list. The deep copy ``lst3`` contains copies of the elements of lst1, so the changes made to ``lst1`` are not reflected in ``lst3`` at all.

## Regex

Regex, short for regular expressions, are a powerful tool for matching patterns in strings. Regex can be used for various tasks, such as:

- Validating user input, such as email addresses, phone numbers, passwords, etc.
- Searching and replacing text, such as removing whitespace, correcting spelling errors, etc.
- Extracting information from text, such as names, dates, numbers, etc.
- Parsing and analyzing text, such as HTML, XML, JSON, etc.

To use regex in Python, you need to import the ``re`` module, which provides various functions and methods for working with regex. For example:

- ``re.search(pattern, string)`` : Returns a match object if the pattern is found in the string, or None otherwise. The match object contains information about the location and content of the match.
- ``re.match(pattern, string)`` : Returns a match object if the pattern matches the beginning of the string, or None otherwise. Similar to ``re.search()``, but only checks the start of the string.
- ``re.findall(pattern, string)`` : Returns a list of all non-overlapping matches of the pattern in the string, or an empty list if no matches are found.
- ``re.sub(pattern, repl, string)`` : Returns a new string where all occurrences of the pattern in the string are replaced by the repl argument, which can be a string or a function.
- ``re.compile(pattern)`` : Returns a regex object that can be used for faster and more efficient matching. The regex object has the same methods as the ``re`` module, such as ``search()``, ``match()``, ``findall()``, etc.

A regex pattern is a string that defines the rules for matching. A regex pattern can consist of various characters and symbols, each with a special meaning. Some of the most common ones are:

- ``.`` : Matches any single character, except a newline.
- ``^`` : Matches the start of the string.
- ``$`` : Matches the end of the string.
- ``*`` : Matches zero or more occurrences of the preceding character or group.
- ``+`` : Matches one or more occurrences of the preceding character or group.
- ``?`` : Matches zero or one occurrence of the preceding character or group.
- ``{n}`` : Matches exactly n occurrences of the preceding character or group.
- ``{n,m}`` : Matches at least n and at most m occurrences of the preceding character or group.
- ``[...]`` : Matches any one of the characters inside the brackets.
- ``[^...]`` : Matches any one of the characters not inside the brackets.
- ``|`` : Matches either the expression before or after the symbol.
- ``(...)`` : Groups a subexpression and captures its match.
- ``\`` : Escapes a special character or introduces a special sequence.

Here are some examples of regex patterns and what they match:

- ``\d`` : Matches any digit (0-9).
- ``\w`` : Matches any word character (a-z, A-Z, 0-9, _).
- ``\s`` : Matches any whitespace character (space, tab, newline, etc.).
- ``\D`` : Matches any non-digit character.
- ``\W`` : Matches any non-word character.
- ``\S`` : Matches any non-whitespace character.
- ``\b`` : Matches a word boundary (the position between a word and a non-word character).
- ``\A`` : Matches the start of the string.
- ``\Z`` : Matches the end of the string.
- ``\n`` : Matches a newline character.
- ``\t`` : Matches a tab character.

For example, the regex pattern ``r'\w+\s\w+'`` matches any two words separated by a space, such as ``'Hello world'`` or ``'Python regex'``. The ``r`` prefix indicates that the string is a raw string, which means that the backslashes are not treated as escape characters.

## Iterators

An iterator is an object that can be iterated over, meaning that you can traverse through all the values it contains. Iterators are useful for working with large or infinite sequences of data, as they only produce one value at a time, saving memory and improving performance.

To create an iterator, you need to implement two methods in your class:

- ``iter()`` : This method returns the iterator object itself and is required for your object to be iterable (i.e., usable in a for loop or with the ``next()`` function).
- ``next()`` : This method returns the next value from the iterator. If there are no more values, it should raise a ``StopIteration`` exception.

An example of a simple iterator that generates the Fibonacci sequence:

```python
class Fibonacci:
    def __init__(self):
        self.a = 0
        self.b = 1

    def __iter__(self):
        return self

    def __next__(self):
        result = self.a
        self.a, self.b = self.b, self.a + self.b
        return result
```
This iterator can be used like this:

```python
fib = Fibonacci()
for i in range(10):
    print(next(fib))
```
Output:

```
0
1
1
2
3
5
8
13
21
34
```
## Generators

A generator is a special type of iterator that is created using a function. A generator function uses the ``yield`` keyword to return a value and suspend its execution. The next time the function is called, it resumes from where it left off.

Generators are convenient for creating iterators, as they allow you to write the logic in a sequential way, without having to manage the state of the iterator object.

An example of a generator function that produces the same Fibonacci sequence as the iterator class above:

```python
def fibonacci():
    a = 0
    b = 1
    while True:
        yield a
        a, b = b, a + b
```
This generator can be used like this:

```python
fib = fibonacci()
for i in range(10):
    print(next(fib))
```
Output:

```
0
1
1
2
3
5
8
13
21
34
```
## Maps and Filters

The ``map()`` and ``filter()`` functions are built-in functions that allow you to apply a function to each element of an iterable and return a new iterable with the results.

The ``map()`` function takes a function and an iterable as arguments and returns a map object that is an iterator over the results of applying the function to each element of the iterable. For example:

```python
def square(x):
    return x ** 2

numbers = [1, 2, 3, 4, 5]
squares = map(square, numbers)
print(list(squares))
```
Output:

```
[1, 4, 9, 16, 25]
```

The ``filter()`` function takes a function and an iterable as arguments and returns a filter object that is an iterator over the elements of the iterable that satisfy the function. The function should return a boolean value, indicating whether the element should be included or not. For example:

```python
def is_even(x):
    return x % 2 == 0

numbers = [1, 2, 3, 4, 5]
evens = filter(is_even, numbers)
print(list(evens))
```
Output:

```
[2, 4]
```
Lambda functions can be used as arguments for ``map()`` and ``filter()``, which are anonymous functions that can be defined inline. For example:

```python
numbers = [1, 2, 3, 4, 5]
squares = map(lambda x: x ** 2, numbers)
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(squares))
print(list(evens))
```
Output:

```
[1, 4, 9, 16, 25]
[2, 4]
```

## Functional Programming

Functional programming is a programming paradigm that focuses on using pure functions, which are functions that do not have any side effects and always return the same output for the same input. Functional programming also emphasizes the use of higher-order functions, which are functions that can take other functions as arguments or return other functions as results. Functional programming can make your code more concise, readable, and testable.

Python supports some features of functional programming, such as:

- Lambda functions, which are anonymous functions that can be defined inline using the ``lambda`` keyword.
- Built-in functions, such as ``map()``, ``filter()``, ``reduce()``, etc., that can apply a function to an iterable and return a new iterable or a single value.
- The ``functools`` module, which provides various tools for working with functions, such as ``partial()``, ``lru_cache()``, ``singledispatch()``, etc.

Some examples of functional programming in Python:

```python
# Using lambda functions with map() and filter()
numbers = [1, 2, 3, 4, 5]
squares = map(lambda x: x ** 2, numbers)
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(squares)) # [1, 4, 9, 16, 25]
print(list(evens)) # [2, 4]

# Using reduce() to calculate the product of a list of numbers
from functools import reduce
numbers = [1, 2, 3, 4, 5]
product = reduce(lambda x, y: x * y, numbers)
print(product) # 120

# Using partial() to create a function that adds a fixed number to another number
from functools import partial
add5 = partial(lambda x, y: x + y, 5)
print(add5(10)) # 15

# Using lru_cache() to memoize a recursive function that calculates the nth Fibonacci number
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10)) # 55
```