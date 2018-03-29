# Level Up With Python

## Learning Objectives

* Customize a development environment
* Discuss the PEP8 rules
* Discuss Sandi Metz's rules for programming
* Use generators in Python
* Look at magic methods in Python

## PEP8

> PEP stands for Python Enhancement Proposal. A PEP is a design document providing information to the Python community, or describing a new feature for Python or its processes or environment. The PEP should provide a concise technical specification of the feature and a rationale for the feature.
[src](https://www.python.org/dev/peps/pep-0001/)

### Why is it important?

> Code is read much more than it is written
Guido Van Rossum

Following code rules leads to more maintainable and debuggable code. It also encourages collaboration when developers follow similar standards across projects.

### The Rules

* 4 **spaces** for each level of indentation
* Lines must be less than 80 characters long
* Use absolute imports, and don't use the wildcard (`*`) operator!
* Separate your imports into three categories: standard library, pip installed, and your own. Split each category with a line break.

```py
# Standard Library
import time
import sys

# Pip Installed
import pandas
import numpy

# Your own
import mymodule.myfile
```

* Write docstrings for all public modules, functions, classes, and methods.
* Naming conventions
  * Private methods and variables (the ones you aren't using outside of a class) should be prefixed with an underscore. `_my_private_variable`
  * Try to not use single character variables
  * Classes should be capitalized like so: `ClassName`
  * Otherwise, use snace_case for variables, methods, and functions
  * Use ALL_CAPS for constants
* Surround functions and classes with two blank lines
* Surround a method with a single bank line
* Use whitespace sparingly elsewhere (within functions, loops, etc.)
* Lambda functions, list comprehensions, and conditional expressions are fine as long as they are simple and fit on one line

### PEP8 Tools

If you are using a text editor, you can install a linter or package to check PEP8 compliance. You can also check from the command line by running the command `$ pip install pep8` and then running `$ pep8 my_file.py` to output whether your code complies with PEP8!

### Exercise: PEP8 Your Code

Take 5 minutes to PEP8-ify any piece of your code from this class. 

### Bonus: Google Style Docstrings

Docstrings are Python comments used for documentation. They start and end with three quotation marks so that they can encompass multiple lines. Normally, they are used for each module, function, class, and method to document what that piece of code is for. They normally also contain information on what the function or method takes as arguments and returns. You can also use Sphynx to generate pretty documentation based on your docstrings!

[Here](http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html) are some examples of Google style docstrings.

### Exercise: Docstring-ify Your Code

Take 5 minute to add Google Docstrings to one piece of your code from this class.

### Bonus: The Zen of Python

PEP 20: The Zen of Python

```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

> `import this` anywhere in your code to get the Zen of Python!


## Sandi Metz's Rules for Developers

Sandi Metz, who is an awesome Ruby developer, speaker, and author has four rules for writing clean code.

1. Classes can be no longer than 100 lines of code
2. Methods and functions can be no longer than 5 lines of code
3. Pass no more than 4 parameters into a method
4. Controllers can instantiate only one object (this one isn't really relevant for you all - yet!)

[Watch](https://www.youtube.com/watch?v=npOGOmkxuio) her full talk on this topic, its awesome!

## Break (10 Minutes)

## Generators

A generator is a function which returns an iterator instead of a collection or ready-to-use value. Sometimes we will want to generate a large amount of data -- so much data that it will be difficult for our computers to deal with at once. 

Generators look very similar to a normal function, except they have yield statements which will produce a series of values that can be retrieved with the `next()` function.

You've probably already used `range` in this class. Range is a generator! Let's write some code that will act like Python's built-in range function!

```py
def range_(start, end, increment=1):
    while start < end:
        yield start
        start += increment

one_to_one_hundred = range_(1, 100)
print(next(one_to_one_hundred))
```

### Exercise: Project Euler Problems with Generators

* [Generate the Multiples of 3 and 5](https://projecteuler.net/problem=1)
* [Generate Even Fibonacci Numbers](https://projecteuler.net/problem=2)

**Bonus**
* [Generate the squer differences of numbers](https://projecteuler.net/problem=6)

## Magic / Dunder / Special Methods

### Review Exercise: Create a BankAccount class.

* Bank accounts should be created with the kind of account (like "savings" or "checking").
* Each account should keep track of it's current balance.
* Each account should have access to a deposit and a withdraw method.
* Each account should start with a balance set to zero.
* return the amount withdrawn, for convenience

### What are Dunder Methods?

You've probably seen one dunder method before, `__init__`, which is called whenever you create an instance of a class. These methods are invoked by Python when you use a built-in method. For example the `__str__` dunder method is called whenever we use the `str()` function on an instance of the class. Let's see what that looks like:

```py
class Dog:
    def __init__(self, name):
        self.name = name
    
    def __str__(self):
        return self.name


maddie = Dog('Maddie')
print(str(maddie))
print(maddie)
```
Some others include:
* `__getattr__` for when you get an attribute (i.e. `maddie.name`)
* `__setattr__` for when you get an attribute (i.e. `maddie.name = 'Madison'`)
* `__len__` for when you call `len` on the class
* `__add__` for when you add instances of the class
* `__getitem__` for using bracket notation on an instance of the class (i.e. `maddie['food']`)

etc. They exist for almost every operator! [Reference on more](http://www.diveintopython3.net/special-method-names.html).

### Exercise: Fancy Bank Accounts

* When you print the bank account, make it so that it prints a well formatted blurb about the kind of account and its balance. (ex. `Savings Account: $50`) 
* Make it so that you can add the balances of two bank accounts by adding two instances of the class.
* Make it so that you can subtract, multiply, and divide the balances of two bank accounts by performing those mathematical operations on two instances of the class.
* Make it so that you can compare the balances of two bank accounts by using the greater than, less than, and equals to operators in Python on two instances of the class.
