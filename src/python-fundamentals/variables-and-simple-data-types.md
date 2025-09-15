# Variables and Simple Data Types

## Variables

Variables are mutable.

```python
age = 20
first_name = 'kevin'
is_online = True
is_online = False
```

## Strings

Can use single quote or double quotes.

```python
# change cases
name = ' kevin '
name.upper()
name.lower()
name.title() # Kevin

# strip white spaces
input = ' i have a pen. '
input.lstrip() # trim on the left side
input.rstrip() # trim on the right side
input.strip() # trim on both sides

# remove prefix/suffix
url = 'https://google.com'
url.removeprefix('https://') # google.com
file = 'file_name.txt'
file.removesuffix('.txt') # file_name

# The find() method should be used only if you need to know the position of sub.
# To check if sub is a substring or not, use the `in` operator
name.find('v') # 2
'ke' in name # True

# f-strings: string interpolation
first_name = 'kevin'
last_name = 'hsiao'
full_name = f"{first_name} {last_name}" # kevin hsiao
```

## Number

- int
- float: in computer science we store data in binary system,

```python
age = 38
monthly_wage = 1_000_000
price_coffee = 3.3
MAX_CONNECTIONS = 1000 # constants - python convention
4/2 # 2.0, the result of the division will always be float
```

### Floats Are Not Always Exact

Be careful when we comparing float numbers, in computer science, we use binary system to store data.

For some float numbers, we are not able to use the binary system to represent the exact value of the number.

`Decimal` can handle exact representation of decimal numbers but it is much slower

```python
format(0.1, '.25f') # '0.1000000000000000055511151'
format(0.125, '.25f') # '0.1250000000000000000000000'

0.1 + 0.1 + 0.1 == 0.3 # False
# When dealing with float numbers, we should not use ==
# instead we should use some measure of closeness (within 0.00001 for example)
abs(0.1 + 0.1 + 0.1 - 0.3) < 0.00001 # True
```
