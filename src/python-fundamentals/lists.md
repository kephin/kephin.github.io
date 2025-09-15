# Lists

It's just like `array` in JavaScript.

```python
names = ['kevin', 'john', 'troy', 'allen']
# recreive
names[-1] # 'allen'
names[0:3] # ['kevin' 'john', 'troy']
'joy' in names # False
len(names) # 4

# edit
names[3] = 'tony'
names.append('zion')
names.insert(3, 'kile')

# delete
del names[2]
names.pop()
names.pop(1)
names.remove('allen') # only delete the first-find element
names.clear()

# sort
names.sort()
names.sort(reverse=True)
names.reverse()
# `sorted` will NOT affect the original data
sorted(names)
sorted(names, reverse=True)
```

## Working with Lists

### Loop through the list

```python
names = ['kevin', 'john', 'troy', 'allen']
for name in names:
    print(name)
```

### Make Numerical Lists

```python
# Numerical list
for value in range(1, 5): # will print 1, 2, 3, 4
for value in range(5): # 0, 1, 2, 3, 4
for value in range(1, 5, 2): # 1, 3

min(numbers) # 0
max(numbers) # 9
sum(numbers) # 45

# use range() to make a list
numbers = list(range(10)) # [0, 1, ..., 9]

# list compreshension
squares = list(number**2 for number in range(1, 10)) # [1, 4,..., 81]
```

### Working with Part of a List

A specific group of items in a list, called a `slice` in Python.

```python
names[1:5]
names[:10] # start at the beginning
names[2:] # end to the last item
name[:] # means to copy the whole list
```

## Tuples

used when create a list of items that cannot change, in another word, tuples is also called _immutable list_.

```python
dimensions = (200, 50)
dimensions[0] # 200
dimenstions[1] = 100 # TypeError: 'tuple' object does not support item assignment

for dimension in dimensions:
    print(dimension)
```

Although you can’t modify a tuple, you can assign a new value to a variable that represents a tuple.

```python
dimensions = (20, 10)
dimensions = (40, 20) # re-assign
```
