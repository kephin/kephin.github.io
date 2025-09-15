# If Statements

Python does not require an else block at the end of an if-elif chain.

```python
if car == 'bmw':
    print(car.upper())
elif car == 'benz':
    print(car.title())
elif car == 'tesla':
    print(car.lower())
else:
    print(car.lower())
```

## Check Equality

```python
car = 'tesla'
car == 'bmw' # False
car != 'benz' # True

age = 38
age < 20 # False
age >= 38 # True
age > 8 and age < 20
age < 18 or age > 65
```

### Check Whether the Value Is in a List

```python
1 in [1, 2, 3] # True
'a' in ['b', 'c'] # False
'a' not in ['b', 'c'] # True
```

### Check That a List Is Not Empty

```python
messages = []
if messages:
    for message in messages:
        print(f"Message: {message}")
else:
    print("No messages!")
```
