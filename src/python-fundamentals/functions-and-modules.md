# Functions and Modules

## Defining a Function

Use `docstring` to describe what the function does.

- When Python generates documentation for the functions in your programs, it looks for a string immediately after the function's definition.
- These strings are usually enclosed in triple quotes, which lets you write multiple lines.

```python
def greet(name):
    """display a simple greeting"""
    print(f"Hello, {name.title()}!")

greet('kevin') # Hello Kevin!
```

### Arguments and Parameters

- The **variable** `name` in the definition of `greet()` is an example of a **parameter**, a piece of information the function needs to do its job.
- The **value** `'kevin'` in `greet('kevin')` is an example of an **argument**.

❗People sometimes speak of arguments and parameters interchangeably.

## Passing Arguments

### Positional Arguments, Keyword Arguments

```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print(f"\nI have a {animal_type}.")
    print(f"My {animal_type}'s name is {pet_name.title()}.")

# positional arguments
describe_pet('hamster', 'harry')

# keyword arguments
describe_pet(animal_type='hamster', pet_name='harry')
```

### Default Arguments

Default arguments need to be placed at the end, because it's not necessary to provide a value for them when calling the function.

```python
def describe_pet(type, name, action='wuff'):
    print(f"{name} is a {type} and it can {action}")
```

## Return Values

```python
def get_name(first_name, last_name):
    """return full name"""
    full_name = f"{first_name} {last_name}"
    return full_name.title()
```

## Passing an Arbitrary Number of Arguments

The asterisk in the parameter name `*toppings` tells Python to make a `tuple` called `toppings`, containing all the values this function receives.

> You’ll often see parameter name `*args`, which collects arbitrary positional arguments.

```python
def make_pizza(*toppings):
    print(toppings)

make_pizza('mushrooms', 'peppers', 'cheese', 'ham') # ('mushrooms', 'peppers', 'cheese', 'ham')
```

### Mixing Positional and Arbitrary Arguments

```python
def make_pizza(vege, *toppings):
    print(toppings)

make_pizza('mushrooms', 'peppers', 'cheese', 'ham') # ('peppers', 'cheese', 'ham')
```

### Using Arbitrary Keyword Arguments

The double asterisks before the parameter `**user_info` tells Python to create a `dictionary` called `user_info` containing all the extra name-value pairs the function receives.

```python
def build_profile(first, last, **user_info):
    user_info['first'] = first
    user_info['last'] = last
    return user_info

build_profile('kevin', 'hsiao', height=178, weight=68)
```

> You’ll often see parameter name `**kwargs` used to collect nonspecific keyword arguments.

## Modules

A module is a file ending in `.py` that contains the code you want to import into your program.

```python
def make_pizza():
    print('How to make a delicious pizze:')
    #...
```

We can then import the file in the **same directory**,

```python
# importing an entire module
import pizze
pizza.make_pizza()

# importing specific functions
from pizza import make_pizza, cut_pizza
make_pizza()
cut_pizza()

# using as to give a function an alias
from pizza import make_pizza as mp
mp()

# using as to give a module an alias
import pizza as p
p.make_pizza()

# importing all functions in a module
from pizza import *
make_pizza()
```
