# Dictionaries

Distionary is a collection of key-value pairs. It's just like `object` in JavaScript.

```python
alien = {
    'color': 'green',
    'age': 3,
}
print(alien['color'])

# modification
alien['age'] = 4
del alien['height']
```

## Using get() to Access Values

Using keys in square brackets to retrieve the value you’re interested in from a dictionary might cause one potential problem: if the key you ask for doesn’t exist, you’ll get an error.

```python
alien['weight'] # KeyError: 'weight'
alien.get('weight', 0) # 0
alien.get('weight') # None
```

## Looping Through a Dictionary

```python
user = {
    'name': 'Kevin',
    'age': 38
}
for key, value in user.items():
    print(key, value)

for key in user.keys():
for key in user.values():

friends_age = {
    'allen': 35,
    'mary': 38,
    'zion': 22,
}
if 'erin' not in friends_age.keys():
    print('eric is not my friend!')
```

### Looping Through a Dictionary’s Keys in a Particular Order

Looping through a dictionary returns the items in the same order they
were inserted. However we can use the `sorted()` function to get the copy of the keys in order.

```python
for name in sorted(friends_age.keys()):
    print(name)
```

### Looping Through a Dictionary Without Repetitive Values

A `set` is a collection in which eash item must be unique.

```python
for name in set(friends_age.values()):
    print(name)
```

By the way, we can declare a `set` by,

```python
languages = { 'python', 'rust', 'python', 'golang' } # { 'rust', 'python', 'golang' }
```
