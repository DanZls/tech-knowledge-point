# Entry

## Q1: What are the built-in types available in Python?

Python includes several built-in types for handling different data and operations. The most common numeric types are `int` (integer), `float` (floating-point), and `complex` (complex numbers). For collections, Python has `list`, `tuple`, `set`, `frozenset`, and `dict` (dictionary or map). For text, the main type is `str` (string), while `bytes` and `bytearray` handle binary data. There are also boolean type `bool` (True/False) and the special type `NoneType` for `None`. Additionally, newer Python versions support types like `memoryview` for buffer protocol operations and `range` for sequences of numbers. These types are fundamental to Python programming, enabling everything from basic calculations to complex data structures and flow control.

```python
x = 10            # int
y = 3.14          # float
c = 2 + 3j        # complex
s = "hello"       # str
l = [1, 2, 3]     # list
t = (4, 5, 6)     # tuple
d = {'a': 7}      # dict
st = {1, 2, 3}    # set
b = b"bytes"      # bytes
ba = bytearray(5) # bytearray
fset = frozenset([1, 2])
flag = True       # bool
nothing = None    # NoneType
```
---

## Q2: How do I modify a string?

Strings in Python are immutable, which means you cannot change their contents after creation. When you want to "modify" a string, you instead create a new string based on the original. This can be accomplished using operations such as concatenation, slicing, or string methods (like `replace()`). Trying to assign to an index in a string will cause an error. For frequent modifications, consider using lists of characters and then joining them into a string at the end, as lists are mutable and can be changed in place.

```python
name = "Python"
# Strings are immutable
# name[0] = "J"  # This would raise a TypeError

# Correct way: create a new string
new_name = "J" + name[1:]  # "Jython"

# Using replace
greeting = "Hello World"
new_greeting = greeting.replace("World", "Python")  # "Hello Python"
```
---

## Q3: Name some characteristics of Python.

Python is an interpreted, high-level, and general-purpose programming language. It emphasizes readability with a clean, English-like syntax, enforcing indentation for code blocks. Python is dynamically typed, which means you don’t declare variable types explicitly. It supports multiple programming paradigms, including procedural, object-oriented, and functional programming. Memory management is automatic, handled via reference counting and garbage collection. Python has rich standard libraries and a vast ecosystem of third-party packages. It is platform-independent, meaning Python code runs on various operating systems with little to no modification. Python is open-source and backed by a vibrant community.

```python
# Examples showing Python's features
def func(x):           # Readability and indentation
    return x * 2

val = func(4)          # Dynamic typing
words = ["easy", "to", "read"]  # List (built-in type)
sentence = " ".join(words)      # Standard library use
```
---

# Junior

## Q4: What are the rules for local and global variables in Python?

Python variables are considered local or global based on where they are assigned. If a variable is assigned inside a function, it is local to that function unless explicitly declared as global using the `global` keyword. Variables assigned outside any function are considered global. If a variable is only read inside a function (without assignment), Python looks for it first in the local scope, and then in the global scope. Modifying a global variable inside a function without declaring it using `global` will result in a new local variable of the same name, not affecting the global one.

```python
x = 5  # Global variable

def foo():
    global x
    x = 10  # This modifies the global x

def bar():
    y = 20  # Local variable

foo()
print(x)  # 10
```
---

## Q5: How does the string get converted to a number?

Python provides built-in functions to convert strings to numbers. For integers, use `int()`, and for floating-point numbers, use `float()`. If the string does not represent a valid number, these functions will raise a `ValueError`. It is common to use exception handling (`try-except`) to avoid errors during conversion. For other bases (like binary or hexadecimal), `int()` accepts a second argument specifying the base of the number represented as a string.

```python
num_int = int("42")          # 42
num_float = float("3.14")    # 3.14

# With base
num_bin = int("1010", 2)     # 10

# Error handling
try:
    val = int("not a number")
except ValueError:
    val = 0
```
---

## Q6: What is Lambda Functions in Python?

A lambda function is a small anonymous function defined by the `lambda` keyword. It can take any number of arguments but can only have one expression. The result of this expression is returned automatically. Lambda functions are often used for small, throwaway functions, particularly as arguments to functions like `map()`, `filter()`, or `sorted()`. Despite their convenience, for anything non-trivial or where clarity is needed, named `def` functions should be preferred.

```python
double = lambda x: x * 2
print(double(5))  # 10

numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x**2, numbers))  # [1, 4, 9, 16]
```
---

## Q7: Does Python have a switch-case statement?

Python does not have a traditional switch-case statement as found in some other languages like C or Java. Instead, Python programmers typically use if-elif-else chains to handle multiple conditional branches. For more complex switch-case-like behavior, dictionaries can be used to map keys (cases) to values or functions, essentially simulating switch-case statements. Starting from Python 3.10, there is a new `match-case` statement (structural pattern matching) that brings similar functionality.

```python
# if-elif-else version
value = 2
if value == 1:
    print("One")
elif value == 2:
    print("Two")
else:
    print("Other")

# Dictionary mapping (for functions)
def one(): print("One")
def two(): print("Two")
switch = {1: one, 2: two}
switch.get(value, lambda: print("Other"))()
```
---

## Q8: What are descriptors?

Descriptors are objects that define how attribute access is interpreted by Python’s object system. They are classes that implement any of the descriptor methods: `__get__()`, `__set__()`, and `__delete__()`. Descriptors are the basis for properties, methods, static methods, and class methods in Python. They provide a way to customize how attributes of a class are accessed, set, or deleted, enabling powerful behaviors like computed attributes or managed attributes (e.g., type-checking, validation).

```python
class Descriptor:
    def __get__(self, instance, owner):
        return "value from descriptor"

class MyClass:
    attr = Descriptor()

obj = MyClass()
print(obj.attr)  # "value from descriptor"
```
---

## Q9: What are local variables and global variables in Python?

Local variables are defined within a function and can only be used inside that function. They exist only during the function’s execution. Global variables are defined outside any function and are accessible throughout the module. To modify a global variable inside a function, the `global` keyword must be used. Otherwise, a new local variable with the same name is created inside the function. Using too many globals is discouraged as it can make code harder to read and maintain.

```python
g = "global"

def func():
    l = "local"
    print(l)       # "local"
    print(g)       # "global" (read-only access)

func()
print(g)           # "global"
```
---

## Q10: Name some benefits of Python

Python offers many benefits: it has readable and straightforward syntax, making it easy to learn and use. It’s dynamically typed and supports rapid development. There is a vast standard library and third-party ecosystem, covering diverse tasks from web development to machine learning. Python is cross-platform, running on major operating systems. It supports multiple programming paradigms (procedural, object-oriented, functional). Memory management is automatic, and numerous frameworks exist to speed up project development. Its community is large and helpful, ensuring extensive documentation and resources for learners and professionals alike.

```python
# Example showing readability and rapid prototyping
numbers = [1, 2, 3, 4]
squares = [n**2 for n in numbers]  # List comprehensions
```
---

## Q11: When to use a "tuple" vs "list" vs "dictionary" in Python?

Use a tuple when you need an immutable sequence of items—often for fixed collections like coordinates or RGB values. Tuples are hashable if all items are hashable, so they can be used as keys in dictionaries. Lists are mutable sequences, suitable when you need to change, add, or remove items. Dictionaries store key-value pairs and are great when each value is uniquely identified by a key (such as a name or ID). Choose structures based on mutability (tuple for immutable, list for mutable), and whether you need named key access (dictionary).

```python
coords = (10, 20)  # tuple - fixed coordinates
colors = ["red", "green", "blue"]  # list - mutable sequence
ages = {"Alice": 25, "Bob": 30}    # dict - mapping names to ages
```
---

## Q12: What is Negative Index in Python?

Negative indexing allows access to elements from the end of a sequence (like lists or strings) rather than the beginning. The index `-1` refers to the last element, `-2` to the second last, and so on. This feature provides a convenient way to access items counting backwards, eliminating the need to calculate positions using `len(sequence) - n`. Negative indexing makes operations like retrieving the last or next-to-last item simpler and more intuitive.

```python
lst = [10, 20, 30, 40]
print(lst[-1])  # 40 (last element)
print(lst[-2])  # 30 (second last)

s = "Python"
print(s[-1])    # "n"
```
---

## Q13: Explain what is Linear (Sequential) Search and when may we use one?

Linear Search (Sequential Search) checks each element in a sequence one by one until it finds the target value or reaches the end. Its time complexity is O(n), where n is the number of items. This approach excels when the dataset is small, unordered, or when searching in data structures that don’t support efficient direct access (like linked lists). If the collection is sorted or very large, more efficient searching algorithms like binary search are preferable.

```python
def linear_search(lst, target):
    for index, value in enumerate(lst):
        if value == target:
            return index
    return -1

numbers = [4, 2, 7, 1, 8]
print(linear_search(numbers, 7))  # 2
print(linear_search(numbers, 3))  # -1
```
---

# Mid

## Q14: What is a None value?
None is a special constant in Python that represents the absence of a value or a null value. It is the only value of the NoneType type. None is frequently used to indicate “no result,” “not yet assigned,” or “missing data.” It is often used as a default value for function arguments if nothing is provided, or as a placeholder in data structures. None evaluates as False in Boolean contexts, but is not equal to values like 0 or an empty string. Comparison to None should be done using "is" or "is not", not "==" (since None is a singleton).
```python
x = None
if x is None:
    print("x has no value")
```
---

## Q15: Is it possible to have static methods in Python?
Yes, static methods are supported in Python using the @staticmethod decorator. A static method does not receive an implicit first argument (like self or cls). It behaves like a plain function but belongs to the class's namespace and can be called from instances or directly from the class. Static methods are used when a method logically belongs to a class but neither accesses nor modifies class or instance state. They do not have access to the instance (self) or class (cls).
```python
class Math:
    @staticmethod
    def add(x, y):
        return x + y

print(Math.add(3, 5))
```
---

## Q16: What is the python with statement designed for?
The with statement in Python is designed to simplify the management of resources like files, network connections, or locks. It ensures that setup and cleanup actions are handled automatically, even if exceptions occur. This is achieved via the context management protocol, using __enter__ and __exit__ methods. The most common use is with file handling—ensuring files are properly closed. It can also be used with database connections, threading locks, and other objects requiring “resource management”. The with statement improves code readability and reduces the likelihood of resource leaks.
```python
with open('data.txt', 'r') as f:
    data = f.read()
# file is now automatically closed
```
---

## Q17: Explain the UnboundLocalError exception and how to avoid it?
UnboundLocalError occurs when a variable is referenced before it is assigned within a local scope. This usually happens if a variable is used and also assigned within a function, and Python treats it as local. If you try to use the variable before the assignment, you get UnboundLocalError. To avoid this, assign the variable before referencing it, or use the global or nonlocal statement to explicitly refer to an outer-scope variable.
```python
x = 10
def foo():
    print(x)  # Error!
    x = 5     # Assignment makes x local

# To fix:
def foo_fixed():
    global x
    print(x)   # Works as x refers to global scope
```
---

## Q18: What is Pickling and Unpickling?
Pickling is the process of serializing Python objects into a byte stream, allowing them to be saved to a file or transmitted over a network. Unpickling is the reverse—deserializing the byte stream back into Python objects. This is done using the pickle module. Pickling supports most built-in types and user-defined classes, making it useful for saving program state, caching, or parallel processing. However, not all objects can be pickled (e.g., open files, sockets), and pickle data is not secure against malicious data, so unpickle only data from trusted sources.
```python
import pickle
data = {'a': 1, 'b': 2}
with open('data.pkl', 'wb') as f:
    pickle.dump(data, f)
with open('data.pkl', 'rb') as f:
    restored = pickle.load(f)
```
---

## Q19: What does this stuff mean: "*args", "**kwargs"? Why would we use it?
*args and **kwargs allow flexible function signatures. *args collects additional positional arguments as a tuple, while **kwargs collects additional keyword arguments as a dictionary. They are used when defining functions that need to accept varying numbers or types of arguments, such as wrapper functions, decorators, or APIs. *args and **kwargs are also used for argument unpacking when calling functions. This allows for more generic, reusable, and flexible code.
```python
def fun(*args, **kwargs):
    print(args)
    print(kwargs)

fun(1, 2, 3, a=4, b=5)  # Output: (1,2,3) and {'a':4, 'b':5}
```
---

## Q20: How can you share global variables across modules?
Global variables can be shared across modules by defining them in a separate module and importing that module wherever needed. By importing the module (not the variable), any changes to the variable are reflected across all importing modules. This approach is preferable to using global variables within multiple modules directly, and helps organize shared state or configuration.
```python
# config.py
value = 42

# module_a.py
import config
print(config.value)

# module_b.py
import config
config.value = 100  # change is visible everywhere
```
---

## Q21: What is the function of "self"?
In Python classes, self is the first parameter of instance methods, referring to the specific object (instance) the method is called on. It allows access to the instance’s attributes and other methods. Unlike some other languages, Python explicitly requires self in method definitions. Without self, methods can’t read or modify instance state. Using self also makes the code clear about attribute scope (instance vs. local variable).
```python
class Person:
    def __init__(self, name):
        self.name = name
    def greet(self):
        print(f"Hello, {self.name}")
```
---

## Q22: What is the difference between "range" and "xrange" functions in Python?
In Python 2, range() returns a list of numbers, while xrange() returns an xrange object (like a generator) that computes numbers on demand, saving memory with large ranges. In Python 3, xrange() was removed and range() now behaves like xrange()—it returns a range object that is iterable and lazy (generates numbers as needed), making it memory efficient. Use range() in Python 3 for both small and large loops.
```python
# Python 2
for i in xrange(100): pass

# Python 3
for i in range(100): pass
```
---

## Q23: What is a Callable?
A callable is any object in Python that can be called using parentheses, like a function. This includes functions, methods, classes (calling returns a new instance), and objects that implement the __call__() method. You can check if something is callable using the callable() function. Callables are often used for flexible APIs, function objects, and callbacks.
```python
def f(): pass
class A:
    def __call__(self): pass
a = A()
print(callable(f), callable(a))  # True True
```
---

## Q24: What are virtualenvs?
A virtualenv (virtual environment) is a self-contained directory tree containing a Python installation, packages, and dependencies, isolated from the global Python environment. It enables projects to use their own dependencies and versions, preventing conflicts between projects and with system packages. Virtual environments are managed via venv (standard in Python 3.3+) or virtualenv (third-party tool). They are essential for dependency management and reproducibility in Python projects.
```python
# create and activate a venv (Python 3.3+)
python -m venv myenv
source myenv/bin/activate  # Unix
myenv\Scripts\activate     # Windows
```
---

## Q25: What's the difference between the list methods "append()" and "extend()"?
append() adds its argument as a single element to the end of the list (the argument becomes one new element), whereas extend() iterates over its argument adding each element to the list (merges the argument elements). If you pass a list to append(), the whole list is added as a single element; with extend(), elements are added individually.
```python
lst = [1, 2]
lst.append([3, 4])  # [1, 2, [3, 4]]
lst = [1, 2]
lst.extend([3, 4])  # [1, 2, 3, 4]
```
---

## Q26: What does an "x = y or z" assignment do in Python?
The expression x = y or z assigns x the value of y if y is “truthy”; otherwise, it assigns the value of z. This is a common Python idiom for setting default values or selecting the first valid value in a chain. It works because the or operator returns its first “truthy” operand, or the last operand if none are “truthy.”
```python
x = None
y = x or 5  # y = 5 because x is None (falsy)
```
---

## Q27: How can I create a copy of an object in Python?
Shallow copies of objects can be made using the copy module's copy() function, the list() constructor for lists, slicing ([:]), dict.copy() for dictionaries, etc. Shallow copies duplicate the container but not contained objects. For deep copies (where contained objects are also recursively copied), use copy.deepcopy(). Deep copying is important if mutable objects are nested.
```python
import copy
a = [1, 2, [3, 4]]
b = copy.copy(a)      # shallow copy
c = copy.deepcopy(a)  # deep copy
```
---

## Q28: What are the Wheels and Eggs? What is the difference?
Wheels (.whl) and Eggs (.egg) are packaging formats for distributing Python projects. Wheel is the standard format, replacing Egg. Wheels are easier to install, use a standardized format (PEP 427), and support pure Python and binary builds. Egg was popular with setuptools, but has several limitations—e.g., less compatibility with pip, single version per project, no defined standard, and some install-time issues. Wheels are preferred for modern Python packaging and are supported by pip.
```python
# To create and install wheels:
python setup.py bdist_wheel
pip install mypackage.whl
```
---

## Q29: What are the key differences between Python 2 and 3?
Key differences include: print is a function in Python 3, integer division returns a float by default, Unicode strings are default (str), xrange is replaced by range, exceptions must use as, new syntax for some functions (e.g., input), no implicit tuple parameter unpacking in functions, and many standard library changes. Python 2 is no longer maintained. Porting code from 2 to 3 often involves syntax updates and Unicode handling.
```python
# Python 2
print "hello"
x = range(3)  # returns a list

# Python 3
print("hello")
x = range(3)  # returns a range object (lazy)
```
---

## Q30: What is the difference between "range" and "xrange"? How has this changed over time?
In Python 2, range() produced a list (taking up memory), whereas xrange() produced an iterator that generated values on the fly (more memory efficient). In Python 3, xrange() is removed, and range() behaves like xrange(), returning a range object (an immutable, memory-efficient sequence). This change means code is more memory-efficient and more consistent across platforms, possibly with minor performance differences in some cases.
```python
# Python 2
range(100000)  # large list in memory
xrange(100000) # efficient iterator

# Python 3
range(100000)  # efficient iterator
```
---

## Q31: Explain how to use Slicing in Python?
Slicing extracts a subsequence from sequences (lists, tuples, strings) using [start:stop:step] notation. The start index is inclusive, stop is exclusive, and step is the interval between elements. Omitting start defaults to 0; omitting stop defaults to the end. Negative indices count from the end. Slicing is used for extracting, copying, or reversing sequences and can work with any object implementing __getitem__, __setitem__, and __delitem__ with slice objects.
```python
lst = [0, 1, 2, 3, 4, 5]
print(lst[1:4])     # [1,2,3]
print(lst[::-1])    # [5,4,3,2,1,0] (reverse)
print(lst[:3])      # [0,1,2]
```
---

## Q32: Explain what is Interpolation Search
Interpolation Search is a search algorithm for ordered lists, improving over binary search if values are uniformly distributed. Instead of always checking the middle item, it estimates the position using the formula derived from linear interpolation, expecting to converge faster for uniformly distributed data. Its average time is O(log log n) but worst-case is O(n). Not as commonly used as binary search, but useful for specific data distributions.
```python
def interpolation_search(arr, x):
    lo, hi = 0, len(arr)-1
    while lo <= hi and arr[lo] <= x <= arr[hi]:
        pos = lo + ((x-arr[lo])*(hi-lo)) // (arr[hi]-arr[lo])
        if arr[pos] == x:
            return pos
        elif arr[pos] < x:
            lo = pos + 1
        else:
            hi = pos - 1
    return -1
```
---

## Q33: What is a Jump (or Block) Search?
Jump (or Block) Search is a searching algorithm for sorted arrays that combines features of linear and binary search. The array is divided into blocks of a fixed size (usually √n), and you jump block by block looking for the block containing the target. Then, a linear search is done within that block. Its time complexity is O(√n), making it faster than linear search but slower than binary search. It's simple to implement and works well for specific scenarios, especially with large, sorted data.
```python
import math
def jump_search(arr, x):
    n = len(arr)
    step = int(math.sqrt(n))
    prev = 0
    while prev < n and arr[min(step, n)-1] < x:
        prev = step
        step += int(math.sqrt(n))
    for i in range(prev, min(step, n)):
        if arr[i] == x:
            return i
    return -1
```
---

## Q34: Explain how does Python memory management work?
Python has automatic memory management, which includes private heap space, automatic garbage collection, and dynamic memory allocation. All objects and data structures are allocated their space from a private heap. The Python memory manager handles object allocation internally. Reference counting is used to track the number of references to every object; when this count reaches zero, the object is garbage-collected. For cyclic references, a generational garbage collection algorithm is used (gc module). Memory allocation can also be influenced by using custom allocators in C extensions.
```python
import gc
gc.collect()  # Triggers a manual garbage collection
```
---

## Q35: Why would you use the "pass" statement?
The pass statement is a no-operation (no-op) statement used as a placeholder when a statement is syntactically required but no action is needed. It's common in stub classes and functions, or as a placeholder in loops or conditionals while developing code. It maintains code structure and avoids syntax errors.
```python
def empty():
    pass

if True:
    pass
```
---

## Q36: What is introspection/reflection and does Python support it?
Introspection (also called reflection) is the ability of a program to examine its own type or properties at runtime. Python supports introspection via many built-in functions (type(), dir(), hasattr(), getattr(), isinstance(), vars(), inspect module). This makes Python highly dynamic, enabling generic programming, debugging, dynamic method calls, and frameworks that rely on runtime type or interface checking.
```python
class A: pass
a = A()
print(type(a), dir(a))
```
---

## Q37: What are Decorators in Python?
Decorators are a way to modify or enhance the behavior of functions or classes without changing their source code. A decorator is a higher-order function that takes a function or method and returns a new function with additional behavior. They are applied with the @decorator syntax. Decorators are commonly used for logging, access control, memoization, input validation, and more. They enable clean separation of concerns and reusable code.
```python
def mydecorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper

@mydecorator
def say_hello():
    print("Hello")
```
---

## Q38: What are the Dunder/Magic/Special methods in Python? Name a few.
Dunder (double underscore) methods, also called magic or special methods, are predefined methods with names like __init__, __str__, __repr__, __add__, __call__, __len__, __getitem__, etc. These methods let objects define custom behaviors for operators, built-in functions, and object construction. They are invoked automatically by Python in specific situations, providing key hooks for customizing class behavior.
```python
class MyClass:
    def __init__(self): pass
    def __str__(self): return "MyClass"
    def __len__(self): return 42
```
---

## Q39: Is there a tool to help find bugs or perform static analysis?
Yes, there are multiple tools for static analysis and bug detection in Python. Popular ones include pylint, pyflakes, flake8 (linter and style checker), mypy (for static type checking), and pyright. These tools analyze code without running it and can detect syntax errors, code smells, unused variables, unreachable code, style issues, and (with type hints) type errors, helping improve code quality early in the development process.
```python
# Check a file with flake8:
flake8 myscript.py
```
---

## Q40: What is Monkey Patching and is it ever a good idea?
Monkey patching is the practice of dynamically modifying or extending classes or modules at runtime—e.g., by replacing methods or attributes. It allows altering behavior without changing original source code, but can make the codebase hard to understand, maintain, and test. Monkey patching should be used sparingly, typically only for emergency bug fixes, test stubs/mocks, or integrating with third-party libraries where you can't modify the code. It is generally discouraged in production code unless necessary and used with care.
```python
import math
math.sqrt = lambda x: 42
print(math.sqrt(9))  # Output: 42
```
---

# Senior

## Q41: What's the difference between "lists" and "tuples"?

Lists and tuples are both sequence types in Python, but they have key differences. The most significant difference is that lists are mutable, which means you can change, add, or remove elements after the list is created. Tuples, on the other hand, are immutable; once created, their content cannot be changed. Lists use square brackets `[ ]`, while tuples use parentheses `( )`. Lists are generally used for collections of homogeneous items that may need to change in size or content, such as a list of user inputs. Tuples are often used for fixed collections of heterogeneous data, like the coordinates of a point or multiple return values from a function. Because tuples are immutable, they can be used as dictionary keys, while lists cannot. Also, immutability generally provides tuples with performance advantages in some use-cases and guarantees that the data will not change unexpectedly.
```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)

# Lists are mutable
my_list.append(4)  # [1, 2, 3, 4]

# Tuples are immutable
# my_tuple.append(4)  # AttributeError
```
---

## Q42: What does the Python "nonlocal" statement do (in Python 3.0 and later)?

The `nonlocal` statement in Python is used to refer to variables defined in the nearest enclosing scope (excluding the global scope). This is especially useful when working with nested functions, where you want to assign a value to a variable declared in an outer (but not global) function scope. Without `nonlocal`, assignments inside the nested function create or modify a new local variable, rather than affecting the variable in the enclosing scope. `nonlocal` bridges this gap by allowing you to modify the binding of variables in the outer (enclosing) non-global scope, which is important for maintaining state or closure behavior across function calls.
```python
def outer():
    x = 10
    def inner():
        nonlocal x
        x = 20
    inner()
    return x  # returns 20
```
---

## Q43: What are immutable objects in Python?

Immutable objects in Python are objects whose state or contents cannot be changed after they are created. This means any operation that appears to modify an immutable object actually creates a new object instead. Common immutable types include `int`, `float`, `str`, `tuple`, and `frozenset`. The immutability property makes such objects hashable, so they can be used as keys in dictionaries and elements in sets. Immutability also promotes safer and more predictable code, especially in concurrent or functional programming. Attempting to directly alter an immutable object, such as reassigning a tuple element or modifying a string, will result in errors.
```python
s = "hello"
# s[0] = 'y'  # TypeError

t = (1, 2, 3)
# t[0] = 4    # TypeError
```
---

## Q44: What is the difference between a function decorated with "@staticmethod" and one decorated with "@classmethod"?

A `@staticmethod` is a method that does not receive an implicit first argument (neither `self` nor `cls`). As a result, it cannot access or modify the class state or instance state. It behaves like a plain function but lives in the class namespace for organizational purposes. A `@classmethod`, on the other hand, receives the class (`cls`) as the first argument, and can access or modify class state that applies across all instances. `@classmethod` is commonly used for alternative constructors and methods that need to know which class they are called on, especially in inheritance.
```python
class MyClass:
    @staticmethod
    def static_method():
        return 'static!'

    @classmethod
    def class_method(cls):
        return f'class: {cls.__name__}'
```
---

## Q45: Why are default values shared between objects?

Default parameter values in Python functions are evaluated only once when the function is defined, not each time it is called. If the default value is a mutable object like a list or dictionary, and this object is modified by one call to the function, the modified object will be shared by all subsequent calls that use the default value. This can lead to unexpected behavior, often considered a common source of bugs. To avoid this, it is customary to set the default value to `None` and create a new object within the function if needed.
```python
def foo(val, tmp=[]):
    tmp.append(val)
    return tmp

# Each call shares the same 'tmp' list
foo(1)  # [1]
foo(2)  # [1, 2]

# Safer pattern:
def foo(val, tmp=None):
    if tmp is None:
        tmp = []
    tmp.append(val)
    return tmp
```
---

## Q46: What is Monkey Patching? How to use it in Python?

Monkey patching is the dynamic modification or extension of a module or class at runtime. In Python, thanks to its flexible and dynamic nature, you can alter classes, functions, or modules while the program is running, without modifying the original source code. This technique is often used in testing, prototyping, or to patch bugs in third-party libraries without waiting for an official fix. However, monkey patching can make code harder to understand, debug, and maintain, and should be used judiciously. To monkey patch, simply assign new attributes or override methods.
```python
import datetime

def fake_today():
    return datetime.date(2000, 1, 1)

datetime.date.today = fake_today  # Monkey patching

print(datetime.date.today())  # 2000-01-01
```
---

## Q47: Explain how you reverse a generator?

Generators produce items one at a time and do not store their contents in memory, so they can't be reversed directly since they do not support random access or length querying. To reverse a generator, you need to first exhaust it into a sequence type that supports reversal, like a list, and then iterate in reverse. This, however, can be memory intensive for large generators. For small or finite generators, this approach is practical, but if you only need some reversed results or for infinite generators, it’s not feasible.
```python
def count():
    for i in range(5):
        yield i

gen = count()
reversed_list = list(gen)[::-1]
for item in reversed_list:
    print(item)  # prints 4 3 2 1 0
```
---

## Q48: How is memory managed in Python?

Memory in Python is managed by the Python memory manager which handles allocation, deallocation, and garbage collection automatically. The memory manager uses reference counting as its primary mechanism: each object keeps track of how many references point to it, and when the count drops to zero, the memory is reclaimed. Python also employs a cyclic garbage collector to clean up objects involved in reference cycles (where objects reference each other but become unreachable). The details of memory management vary by Python implementation (e.g., CPython, PyPy) but largely follow this pattern. Most users do not have to manually manage memory, but memory leaks can still occur if cycles reference objects with custom `__del__` methods or if global references are unintentionally retained.
```python
import gc
gc.collect()  # Manually trigger garbage collection
```
---

## Q49: What is Cython?

Cython is a superset of Python that supports compiling Python code (along with optional type annotations) to C, which can lead to significant performance improvements. It allows Python developers to write code that is as readable as Python but compiles down to highly efficient C code, making it particularly useful for computationally intensive tasks. Cython enables seamless calling of C functions and declaring C types in Python code, bridging the gap between Python and C for performance-critical applications, and making it easier to interface with C libraries.
```python
# sample.pyx
def say_hello():
    print("Hello from Cython!")
# Compiled with Cython to a shared object then imported in Python
```
---

## Q50: What is the difference between old style and new style classes in Python?

Old-style classes were present in Python 2, and are those that do not explicitly inherit from `object`. New-style classes inherit from `object` (either directly or indirectly). New-style classes introduced a unified object model, supporting features like descriptors, `super()`, properties, and Method Resolution Order (MRO) via C3 linearization. In Python 3, all classes are new-style classes by default, eliminating the old-style class distinctions. New-style classes provide more consistent and predictable object behavior and allow for advanced object-oriented programming features.
```python
# Python 2
class OldStyle:   # old-style
    pass

class NewStyle(object):  # new-style
    pass

# Python 3: All classes are new-style
class MyClass:
    pass
```
---

## Q51: Why aren't Python nested functions called closures?

A nested function is simply a function defined inside another function. However, for it to be called a closure, it must capture and "close over" variables from its enclosing function's environment, retaining access to those variables even if the outer function has finished execution. Not every nested function does this; some just exist inside another function for code structure and do not reference variables from the outer scope. A true closure occurs only when a nested function references at least one variable from its enclosing scope, ensuring the variable’s state is preserved even after the outer function is gone. Therefore, while all closures are nested functions, not all nested functions are closures. Closures are useful in many patterns, such as creating function factories or decorators that need to "remember" state.

```python
def outer():
    msg = "hello"
    def inner():     # nested, but not yet a closure
        print("I'm inner")
    return inner

def outer_closure():
    msg = "hello"
    def inner():     # this is a closure
        print(msg)
    return inner
```
---

## Q52: What is the difference between deep and shallow copy?

A shallow copy creates a new object but does not recursively copy objects that the original references; instead, it copies references to those objects. Thus, changes to nested objects in the copy will affect the original. A deep copy, on the other hand, recursively copies all objects found in the original, so the new object and the original are completely independent. Shallow copies are usually created with `copy.copy()`, while deep copies use `copy.deepcopy()`. Shallow copy is efficient and works well with simple objects, but can be risky with objects containing mutable nested objects. Deep copy is safer for complex, nested structures, but can be much slower and use more memory, especially for objects containing cycles or large graphs.

```python
import copy
lst1 = [[1,2], [3,4]]
shallow = copy.copy(lst1)
deep = copy.deepcopy(lst1)

shallow[0][0] = 100
# lst1[0][0] == 100, shared reference

deep[0][0] = 200
# lst1[0][0] remains 100, deep is independent
```
---

## Q53: Why Python (CPython and others) uses the GIL?

The Global Interpreter Lock (GIL) is used by CPython (and some other interpreters) to ensure that only one thread executes Python bytecode at a time. This greatly simplifies memory management and object model implementation, especially for reference counting and garbage collection, because only one thread may update Python objects’ internal states at once. The main reason is to protect against race conditions and inconsistent memory caused by concurrent memory modifications. However, the GIL restricts the parallel execution of threads on multi-core processors, making Python threads unsuitable for CPU-bound tasks but still effective for I/O-bound operations. Some Python implementations (like Jython or IronPython) do not use a GIL because they rely on the threading models of their host platforms.

```python
# Simple illustration; only one thread runs Python bytecode at a time.
import threading
def cpu_task():
    for _ in range(1000000):
        pass

t1 = threading.Thread(target=cpu_task)
t2 = threading.Thread(target=cpu_task)
t1.start(); t2.start()
```
---

## Q54: What are metaclasses in Python?

Metaclasses are classes of classes; they define how classes behave, just as classes define the behavior of their instances. In Python, you can customize the creation, initialization, and behavior of classes by defining a metaclass (usually by inheriting from `type`) and specifying it with the `metaclass` keyword. Metaclasses are commonly used for advanced scenarios such as enforcing coding conventions, automatically registering classes, or adding class-level methods. They work by controlling the class construction process (e.g., by customizing `__new__` and `__init__`). Most Python code does not use metaclasses directly, but they’re a powerful tool for framework and library designers.

```python
class MyMeta(type):
    def __new__(cls, name, bases, dct):
        dct['greet'] = lambda self: 'Hello from metaclass'
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=MyMeta):
    pass

obj = MyClass()
print(obj.greet())
```
---

## Q55: Is it a good idea to use multi-thread to speed your Python code?

Using multithreading to speed up Python code only works well for I/O-bound tasks like network requests or file operations. Due to the Global Interpreter Lock (GIL) in CPython, only one thread executes Python bytecodes at a time, so CPU-bound code does not see a performance increase with threading. In fact, it may become slower due to context switching overhead. For speeding up CPU-bound tasks, multiprocessing (which runs separate processes rather than threads) or using C/C++ extensions, or tools like `concurrent.futures.ProcessPoolExecutor`, are generally preferred. However, multithreading is effective for parallelizing tasks that spend a lot of time waiting for external operations (I/O).

```python
import threading
import requests

# Good use: I/O-bound task
def fetch_url(url):
    requests.get(url)

threads = [threading.Thread(target=fetch_url, args=("http://example.com",)) for _ in range(5)]
[t.start() for t in threads]
[t.join() for t in threads]
```
---

## Q56: What are the advantages of NumPy over regular Python lists?

NumPy provides highly efficient, multidimensional arrays that use less memory and allow vast, fast mathematical operations via vectorization. Operations on NumPy arrays are written in optimized C, making them much faster than equivalent Python code using lists, which require slow Python-level iteration. NumPy supports a wide array of mathematical operations, slicing, broadcasting, and advanced features like masking and views. Its arrays are homogeneous (all elements have the same type), which further optimizes memory and computation. This makes NumPy the foundation for thousands of scientific, mathematical, and machine learning libraries in Python.

```python
import numpy as np
arr = np.array([1,2,3,4])
arr2 = arr * 2                 # Fast element-wise multiply
```
---

## Q57: How to work with transitive dependencies?

Transitive dependencies are libraries your direct dependencies require. Managing them typically involves using package managers like pip, poetry, or conda, which automatically find and install the correct versions. You can see transitive dependencies by using `pip freeze`, `pipdeptree`, or similar tools. Sometimes, version conflicts (dependency hell) occur, requiring the use of virtual environments or lock files (like `requirements.txt` or `poetry.lock`) to control installed versions. Keeping dependencies updated and avoiding unpinned requirements helps reduce conflicts and ensure security.

```bash
pip install pipdeptree
pipdeptree                  # Shows dependent and transitive dependencies
```
---

## Q58: What is the purpose of the single underscore "_" variable in Python?

The underscore `_` has several uses in Python. In the interactive shell, it refers to the result of the last executed expression. In coding conventions, it often denotes "don't care" variables (unused values), such as when unpacking tuples. Also, when used as a prefix for variable or method names, it implies internal use. In internationalized applications, `_` can be used as a function for string translations. These are conventions and do not enforce restrictions, but are widely recognized by the community.

```python
a, _, b = (1, 2, 3)          # Ignore middle value during unpacking
print(_)                     # In REPL, prints last result; here, value is 2
```
---

## Q59: Can you explain Closures (as they relate to Python)?

A closure is a function object that retains access to variables from its lexical scope, even after the outer function has finished execution. Closures occur when a nested function references variables from its enclosing function. They are useful for creating function factories, maintaining state in a function, or implementing decorators. This captured environment persists as part of the returned function object, enabling powerful abstractions and concise code.

```python
def make_adder(x):
    def adder(y):
        return x + y
    return adder

add5 = make_adder(5)
print(add5(10))   # 15
```
---

## Q60: Why are Python's private methods not actually private?

Python does not enforce strict access control. Methods or attributes with a single underscore (`_method`) are considered protected (by convention) and a double underscore (`__method`) triggers name-mangling, making it harder but not impossible to access. However, these are conventions; you can still access "private" members by name-mangling or directly. Python emphasizes readability and responsible use over enforced encapsulation, trusting the developer to respect these conventions.

```python
class MyClass:
    def __private(self):
        print("Can't touch this")
      
obj = MyClass()
obj._MyClass__private()  # Accessible despite being intended private
```
---

## Q61: What's the difference between a Python module and a Python package?

A module is a single Python file that can be imported (e.g., `foo.py`). A package is a directory containing a special `__init__.py` file and possibly multiple modules or subpackages. Packages enable hierarchical module organization, while modules are individual files. Both modules and packages can be imported, but packages help structure larger projects across multiple files and directories.

```python
# Directory structure
# mypkg/
#   __init__.py
#   mod1.py

import mypkg.mod1      # import from package
```
---

## Q62: What is an alternative to GIL?

Alternatives include: using Python implementations without a GIL (such as Jython or IronPython), using multiprocessing instead of threading (where each process has a separate interpreter and memory space), or moving performance-critical code to C extensions (thus bypassing the GIL while running native code). Some experimental Python interpreters (like PyPy STM) have tried to remove the GIL with limited success due to increased complexity and overhead.

```python
from multiprocessing import Process

def go():
    print('parallel!')

p1 = Process(target=go)
p2 = Process(target=go)
p1.start(); p2.start()
```
---

## Q63: What is GIL?

The Global Interpreter Lock (GIL) is a mutex in CPython ensuring only one native thread executes Python bytecode at a time. The GIL simplifies memory management and avoids concurrency issues in the interpreter, but inhibits full parallelism on multi-core CPUs for CPU-bound code. It does not affect I/O-bound programs as much, since threads waiting on I/O release the GIL. The GIL is a frequent topic of debate given Python's popularity in concurrent and high-performance programming.

```python
# Only one thread can execute Python code at once, even on multi-core systems.
```
---

## Q64: What is MRO in Python? How does it work?

MRO stands for Method Resolution Order and determines the order in which Python looks up methods and attributes in a hierarchy, especially with multiple inheritance. Python uses the C3 Linearization algorithm to produce a deterministic MRO. You can view a class’s MRO with the `__mro__` attribute or the `mro()` method. MRO ensures consistency, avoids duplicate calls, and is essential when handling complex inheritance graphs.

```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass

print(D.mro())
```
---

## Q65: What is the difference between "@staticmethod" and "@classmethod"?

A `@staticmethod` does not receive an implicit first argument; it behaves like a plain function inside a class's namespace and cannot access or modify class or instance state. `@classmethod` receives the class (`cls`) as its first argument and can access or modify class-level data. Both can be called on class or instance, but `classmethod` is typically used for alternative constructors or methods needing to know which subclass they’re working with.

```python
class Example:
    @staticmethod
    def f1():
        print("static")

    @classmethod
    def f2(cls):
        print("class", cls)
```
---

## Q66: How is "set()" implemented internally?

A `set` in Python is implemented using a hash table, similar to dictionaries but storing only keys (no values). Elements are hashed and stored in a way that allows for fast membership tests, insertion, and deletion, with typical time complexity of O(1). Collisions are handled via open addressing. Since sets depend on hash values, elements must be immutable and hashable. Iteration order is arbitrary and may change with Python version or state of the set.

```python
s = set([1, 2, 3])
print(2 in s)   # Fast O(1) check
```
---

## Q67: Why would you use metaclasses?

Metaclasses allow customization of class creation and behavior. You might use them to automatically register subclasses, enforce coding conventions, inject methods/attributes, or modify inheritance hierarchies. Frameworks such as ORMs or serialization libraries often use metaclasses for declarative APIs. However, they add complexity and are an advanced feature recommended only when regular class mechanisms or decorators can't achieve your goals.

```python
class Registry(type):
    registry = {}
    def __new__(cls, name, bases, attrs):
        new_class = super().__new__(cls, name, bases, attrs)
        cls.registry[name] = new_class
        return new_class

class A(metaclass=Registry): pass
```
---

# Expert

## Q68: Why use "else" in "try/except" construct in Python?

The `else` clause after a `try/except` block executes if no exception was raised in the try block. It keeps code that should only run when there was no error separate from error-handling logic, improving readability and reducing accidental exception masking. The else block is useful when most code can fail, but some follow-up should only run on success. It also avoids catching exceptions from the else block in the except clause.

```python
try:
    val = int('42')
except ValueError:
    print('Bad value')
else:
    print('It worked:', val)
```
---

## Q69: Describe Python's Garbage Collection mechanism in brief

Python primarily uses reference counting to manage memory, immediately freeing objects when their reference count drops to zero. However, reference counting cannot handle cycles, so Python includes a cyclic garbage collector that periodically detects and breaks reference cycles among objects. Objects with a `__del__` method (finalizers) are handled carefully to avoid unexpected consequences. Python’s approach is mostly transparent to the programmer, but features like `gc.collect()` allow manual collection if necessary.

```python
import gc
gc.collect()    # Manually trigger garbage collection
```
---

## Q70: Why isn't all memory freed when Python exits?

When Python exits, memory may not be fully freed due to references held by the interpreter, extensions, or non-Python objects. Some allocations, especially those in C extensions or the Python runtime itself, may persist for performance or technical reasons. The OS will reclaim all memory when the process ends, but tools like Valgrind may still report "leaks" that aren't true leaks in real-world systems.

```python
# OS reclaims memory, but interpreter may keep some until exit
```
---

## Q71: What does Python optimisation ("-O" or "PYTHONOPTIMIZE") do?

Running Python with `-O` or setting the `PYTHONOPTIMIZE` environment variable removes assert statements and sets the `__debug__` variable to False during execution. This results in `.pyo` optimized bytecode files, but does not significantly speed up normal code. The main effect is that runtime assertions are omitted, making it unsuitable for debugging. Further optimization, like dead code elimination, does not occur.

```sh
python -O script.py
```
---

## Q72: Is there any downside to the "-O" flag apart from missing on the built-in debugging information?

Yes, aside from suppressing assert statements and setting `__debug__` to False, using `-O` can lead to unexpected behavior if code relies on asserts for runtime checks or error handling, which is considered bad practice. Additionally, third-party code or frameworks that depend on `__debug__` may behave differently or skip essential checks. It offers essentially no performance benefit in most cases, so should be used with caution.

```python
assert False, "This won't fire with -O"
```
---

## Q73: Is there a simple, elegant way to define singletons?

A common way is using a class that always returns the same instance by overriding `__new__`, or using a module (since modules are imported only once). The decorator pattern or metaclass can also enforce single instantiation. These methods are all simple and Pythonic and avoid global variables.

```python
class Singleton:
    _instance = None
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```
---

## Q74: What is a global interpreter lock (GIL) and why is it an issue?

The Global Interpreter Lock (GIL) is a mutex that prevents multiple threads from executing Python bytecodes simultaneously in CPython. The GIL simplifies memory management but limits concurrency for CPU-bound multithreaded programs: only one thread makes progress at a time, even on multi-core systems. This makes Python's native threading model unsuitable for parallelizing CPU-intensive tasks, though it is fine for I/O-bound tasks or using multiprocessing to distribute work.

```python
# GIL: Only one thread executes Python code at a time, even on multi-core CPUs.
```
---