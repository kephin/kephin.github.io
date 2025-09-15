# Files and Exceptions

## Read from a file and write to a file

```python
from pathlib import Path

path = Path('doc.txt')
contents = path.read_text().rstrip()
path.write_text(contents + '\nI love python!\n')
print(contents)
```

### Relative and Absolute File Paths

A _relative_ file path is relative to the directory where the currently running program file is.

```python
# relative path
path = Path('text_files/filename.txt')
# absolute path
path = Path('/home/eric/data_files/text_files/filename.txt')
```

## Exceptions

`try`-`except`-`else`-`finally` block.

- `try`: put code that might cause an exception
- `except`: what to do when a certain exception arises on trying to run the code in the `try` block
    - `pass`: fail silently
- `else`: additional code that should run only if the `try` block was successful
- `finally`: code that should run no matter what

```python
from pathlib import Path

path = Path('alice.txt')
contents = ''

try:
    contents = path.read_text(encoding='utf-8')
except FileNotFoundError:
    print(f"Sorry, the file {path} does not exist.")
except PermissionError:
    pass
except:
    # catch all other exceptions
    print('An unexpected error occurred')
else:
    print(contents)
    # we don't want to catch the error if it's raised
    doSomethingElse()
finally:
    print('the job is done')
```

## Storing Data

- `json.dumps`: put any data into JSON
- `json.loads`: put JSON back to any data

```python
from pathlib import Path
import json

path = Path('number.json')
numbers = [1,2,3,4,5]

content = json.dumps(numbers)
path.write_text(content)
```

```python
from pathlib import Path
import json

path = Path('number.json')
contents = path.read_text()
numbers = json.loads(contents)
print(numbers)
```
