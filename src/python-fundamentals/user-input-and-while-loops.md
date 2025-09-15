# User Input and While Loops

## Receiving Inputs

```python
name = input('what is your name?')
print('hello! ' + name)
```

When you use the `input()` function, Python interprets everything the user
enters as a `string`.

## Type Conversion

- int()
- float()
- str()
- bool()

```python
birth_year = input('what is your birth year?')
age = 2024 - int(birth_year)
print('your age is ', str(age))
```

## Introducing While Loops

```python
i = 1
while i <= 5:
    print(i * '*')
    i += 1
```

### Using break to Exit the Loop

This program will keep asking util user inputs 'quit'.

```python
while True:
    prompt = input('Please enter your name.')
    if prompt == 'quit':
        break
    else:
        print(f"Your name is {prompt}")
```

### Using continue to Skip Part of the Loop

The `continue` statement allows you to skip over the part of a loop where an external condition is triggered, but to go on to complete the rest of the loop.

```python
number = 0
while number < 10:
    number += 1
    if number % 2 == 0:
        continue
    print(number)
```
