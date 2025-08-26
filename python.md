# Python

https://learnxinyminutes.com/docs/python/
https://docs.python.org/3/tutorial/index.html

- Still a work in progress

## Python 2 vs Python 3
- Python 3 is the current recommended version
- Python 2 may still used as Python 2 to Python 3 migration had breaking changes so https://docs.python.org/3/howto/pyporting.html

## Version check
```
python -V
python2 -V
python3 -V
```

## Running code

### REPL / Interactive
- Run `python` / `python3` / `python2`
- Type commands interactively and press enter
- Exit: `exit` / `Ctrl`+`D` 

### Via file
```
python python_code_file.py
```

### Version Management
- virtualenv
- pyenv

## Dependency Management
- pip
- pip3
- poetry


## Spacing / Scope / Identation
- Spacing: Spaces / Tabs
- Scoping / Identation:
    - Use Spaces / Tabs
    - No brackets used for scoping `{` `}`
- End of line does not need `;`


## Basic Variables and Syntax
```
# A comment

a_string = "String"
another_string = 'String'
an_integer = 123
a_float = 1.23
a_boolean = True
another_boolean = False
multi_line = """\
start of paragrapah
- line 1
   - line 2
"""
multiwords = "manual " + "concat"
multiwords = "auto " " concat"
multiwords = ("auto "
 " concat")
```
## String functions / index

```
a_string[0]    # first character
a_string[-1]   # last character
a_string[1:3]  # characters from index 1 to index less than 3
a_string[1:]   # characters from index 1 onwards
a_string[:3]   # from beginning until index less than 3
len(a_string)  # number of characters

a_string * 10  # repeat string 10 times

```

## Sequences

- Data types
    - list
    - tuple
    - range
- Indexed by a range of numbers e.g. `sequence[0]`

### Sequence Functions

- `x in s`: True if an item of s is equal to x, else False
- `x not in s`: False if an item of s is equal to x, else True
- `s + t`: the concatenation of s and t
- `s * n` or `n * s`: equivalent to adding s to itself n times
- `s[i]`: ith item of s, origin 0
- `s[i:j]`: slice of s from i to j
- `s[i:j:k]`: slice of s from i to j with step k
- `len(s)`: length of s
- `min(s)`: smallest item of s
- `max(s)`: largest item of s
- `s.index(x[, i[, j]])`: index of the first occurrence of x in s (at or after index i and before index j)
- `s.count(x)`:  total number of occurrences of x in s

## Lists

- Equivalent in other languages: array

```
list = [1, 4, 9, 16, 25]
list[0]    # first element
list[-1]   # last element
list[1:3]  # elements from index 1 to less than 3
list[1:]   # from index 1 onwards
list[:3]   # from beginning until index less than 3
len(list)  # number of elements
list * 2   # repeat 2 times
```

```
list.append(x)            # add item to end. Can alos use a[len(a):] = [x].
list.extend(iterable)     # add all the items from the iterable to end. Equivalent to a[len(a):] = iterable.
list.insert(i, x)         # insert item at position i (moves items to the right)
list.remove(x)            # removes item whose value matches x. Raises ValueError if none exist 
del(list[i])              # remove element at position i
del(list[i:j])            # remove elements from position i to j (inclusive)
del(list[:])              # remove all elements
list.pop(i)               # returns item from position i and removes it from list. if none supplied returns last item
list.clear()              # clears lists. del list[:]
list.index(x, start, end) # find x from in list starting from index start to index less than end and returns index in relation to original list. start and end are optional. Raises ValueError if does not exist
list.count(x)            # Return the number of times x appears in the list.
Return zero-based index in the list of the first item whose value is equal to 
    list.sort(*, key=None, reverse=False)
list.reverse()           # Reverse the elements of the list in place.
list.copy()              # Return a shallow copy of the list. Equivalent to a[:].
```

```
for i in ['tic', 'tac', 'toe']:
  print(i)

for i, v in enumerate(['tic', 'tac', 'toe']):
  print(i, v)
```

### List Comprehensions

- Make new lists where each element is the result of some operations applied to each member of another sequence or iterable

```
squares = []
for x in range(10):
  squares.append(x**2)

squares = list(map(lambda x: x**2, range(10)))
squares = [x**2 for x in range(10)]
```

```
combs = []
for x in [1,2,3]:
  for y in [3,1,4]:
    if x != y:
      combs.append((x, y))

[(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
```

## Tuple

Tuples are immutable

```
empty = ()
singleton = 'hello', # <-- note trailing comma
len(empty)           # 0
len(singleton)       # 1
singleton            # ('hello',)
tuple = ( 1, 4, 9, 16, 25 )
tuple = 1, 2, 3      # tuple packing
v1,v2,v3 = tuple     # unpack tuple into individual values, must match in length


tuple[0]        # first element
tuple[-1]       # last element
tuple[1:3]      # elements from index 1 to less than 3
tuple[1:]       # from index 1 onwards
tuple[:3]       # from beginning until index less than 3
len(tuple)      # number of elements
tuple * 2       # repeat 2 times
tuple1 + tuple2 # concatenate tuples into a new tuple
```

## Dictionaries
- Equivalent name other languages: hash / associative memories / associative arrays
- think of them as key-value pairs
- indexed by keys (e.g. `dictitonary[key]`), which can be any immutable type;
   - strings and numbers can always be keys 
   - tuples can be used as keys if they contain only strings, numbers, or tuples; if a tuple contains a mutable object either directly or indirectly, it cannot be used as a key
   - can’t use lists as keys, since lists can be modified in place

- `list(d)` on a dictionary returns a list of all the keys used in the dictionary

```
users = {'Hans': 'active', 'Éléonore': 'inactive', '景太郎': 'active'}

print (users['Hans'] == 'active') # True
print ('Hans' in users) # True
print ('Hans' not in users) # False

for key, value in users.items():
  name = key
  status = value
  if status == 'active':
    print(name)

for item_data in users.items():
  name = item_data[0] # key
  status = item_data[1] # value
  if status == 'active':
    print(item_data[0])
```

```
dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
dict(sape=4139, guido=4127, jack=4098)
# {'sape': 4139, 'guido': 4127, 'jack': 4098}

{x: x**2 for x in (2, 4, 6)}
# {2: 4, 4: 16, 6: 36}
```

## Sets

- unordered collection with no duplicate elements

```
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'} 
emptyset = set()   #  not {}
print(basket)                      # 
# {'orange', 'banana', 'pear', 'apple'}
```

## Math

- `+`, `-`: addition, subtraction
- `*`, `/`, `%`: multiplication, division, modulus/remainder
- `**`, `pow(x, y)`: exponentiation,  x to the power y
- `//` floor division
- `<=`` >=`, `<`, `>`: comparison
- `==`, `!=`: equality and inequality
- `abs(x)`: absolute value or magnitude of x
- `int(x)`: x converted to integer
- `float(x)`:  x converted to floating point
- `complex(re, im)`: a complex number with real part re, imaginary part im. im defaults to zero.
- `c.conjugate()`: conjugate of the complex number c
- `divmod(x, y)`: the pair (x // y, x % y)
- `round(x[, n])`: x rounded to n digits, rounding half to even. If n is omitted, it defaults to 0.
- requires `import math`
    - `math.trunc(x)`: x truncated to Integral
    - `math.floor(x)`: the greatest Integral <= x
    - `math.ceil(x)`: the least Integral >= x

## Bitwise Operators
- `x | y`: bitwise or of x and y
- `x ^ y`: bitwise exclusive or of x and y
- `x & y`: bitwise and of x and y
- `x << n`: x shifted left by n bits
- `x >> n`: x shifted right by n bits
- `~x`: the bits of x inverted


## Conditionals

### Operators
- `in`
- `is None` / `is not None`
- `True` / `False`
- `Not`
- `and` / `or` / `(...)`
- `==`, `!=`, `>`, `>=`, `<`, `<=`, 

### Examples

```
variable is None
variable is not None
1 in list
0 not in list
True and False
True or False
boolean0 or (boolean1 and boolean2)
1 == 1
1 >= 1
1 > 1
1 != 2
```

### Notes
- Sequence objects typically may be compared to other objects with the same sequence type
- Comparison uses lexicographical ordering
   - first the first two items are compared, and if they differ this determines the outcome of the comparison; if they are equal, the next two items are compared, and so on, until either sequence is exhausted. 
   - If one sequence is an initial sub-sequence of the other, the shorter sequence is the smaller (lesser) one
   - Lexicographical ordering for strings uses the Unicode code point number to order individual characters
   - Comparing objects of different types with < or > is legal provided that the objects have appropriate comparison method



### If

```
if x < 0:
    x = 0
    print('Negative changed to zero')
elif x == 0:
    print('Zero')
elif x == 1:
    print('Single')
else:
    print('More')

```


### Match / Case / Switch

**Requires Python 3.10 and higher**

```
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case 401 | 403 | 404:  # multiple 
            return "Not allowed"
        case _:
            return "Something's wrong with the internet"
```    

### Loops

- Loop specific syntax
  - `break`: exit the loop
  - `continue`: goes to the next iteration of the loop

#### For

```
words = ['cat', 'window', 'defenestrate']
for w in words:
  print(w, len(w))
```

```
for i in range(5):
  print(i) # 0 1 2 3 4

for i in range(5,10,2):
  print(i) # 5 7 9
```

```
for n in range(2, 10):
  for x in range(2, n):
    if n % x == 0:
      print(n, 'equals', x, '*', n//x)
      break
  else:
    # loop fell through without finding a factor
    print(n, 'is a prime number')
```

```
for num in range(2, 10):
  if num % 2 == 0:
    print("Found an even number", num)
    continue
  print("Found an odd number", num)
```


The `pass` statement does nothing. It can be used when a statement is required syntactically but the program requires no action. For example:


#### While

```
while True:
  pass  # Busy-wait for keyboard interrupt (Ctrl+C)
```


# Functions

```
def fib(n):    # write Fibonacci series up to n
  """Print a Fibonacci series up to n."""
  a, b = 0, 1
  while a < n:
    print(a, end=' ')
    a, b = b, a+b
  print()
```

```
def cheeseshop(kind, *arguments, **keywords):
  print("-- Do you have any", kind, "?")
  print("-- I'm sorry, we're all out of", kind)
  for arg in arguments:
    print(arg)
  print("-" * 40)
  for kw in keywords:
    print(kw, ":", keywords[kw])

cheeseshop("Limburger", "It's very runny, sir.",
    "It's really very, VERY runny, sir.",
    shopkeeper="Michael Palin",
    client="John Cleese",
    sketch="Cheese Shop Sketch")

# Output: 
# -- Do you have any Limburger ?
# -- I'm sorry, we're all out of Limburger
# It's very runny, sir.
# It's really very, VERY runny, sir.
# ----------------------------------------
# shopkeeper : Michael Palin
# client : John Cleese
# sketch : Cheese Shop Sketch
```

TODO: More position / keyword
file:///Users/thewheat/Downloads/python-3.10.5-docs-html/tutorial/controlflow.html#positional-or-keyword-arguments


## Modules

- Including reusable code in other files

`fibo.py`
```
def fib(n):    # write Fibonacci series up to n
  a, b = 0, 1
  while a < n:
    print(a, end=' ')
    a, b = b, a+b
  print()

def fib2(n):   # return Fibonacci series up to n
  result = []
  a, b = 0, 1
  while a < n:
    result.append(a)
    a, b = b, a+b
  return result
```
- `dir()`
  - The built-in function dir() is used to find out which names a module defines. It returns a sorted list of strings:

```
>>> import fibo
>>> dir(fibo)
['__name__', 'fib', 'fib2']
```

### Import Variations

#### Import Module

```
import fibo      # imports from fibo.py

fibo.fib(1000)
fibo.fib2(100)
fibo.__name__    # module name 'fibo'
```

#### Import Specific Functions
```
from fibo import fib, fib2
fib(500)
```

#### Import All Functions

- Imports all names except those beginning with an underscore (`_`)
- Should not typically be used as it introduces an unknown set of names, possibly hiding some already defined

```
from fibo import *
fib(500)
```

#### Import Module witth a different Namespace

```
import fibo as fib
fib.fib(500)
print(fib.__name__) # fibo
```

#### Import Function a different name
```
from fibo import fib as fibonacci
fibonacci(500)
```

### Executing modules as scripts

```
python fibo.py <arguments>
```

Runs with `__name__` as `__main__` so to support direct execution add the following to module
```
# fibo.py
if __name__ == "__main__":
  import sys
  fib(int(sys.argv[1]))
```

### Standard modules

- Modules that come automatically with Python that provide some common lower level functions e.g. `sys`, `io`, `os`


### Packages

- structure module namespace using “dotted module names”
- `sound.formats`, `sound.effects`

```
package
    __init__.py               Initialize the sound package
    formats/                  Subpackage for file format conversions
        __init__.py
        wavread.py
        wavwrite.py
        ...
    effects/                  Subpackage for sound effects
      __init__.py
      echo.py
      surround.py
```

```
import sound.effects.echo
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)

from sound.effects import echo
echo.echofilter(input, output, delay=0.7, atten=4)

from sound.effects.echo import echofilter
echofilter(input, output, delay=0.7, atten=4)
```

#### Importing * From a Package

- Based on `__all__` in `__init__.py`

```
# sound/effects/__init__.py
__all__ = ["echo", "surround"]
...

# test.py
sound.effects import *       # imports the 2 named submodules
```


```
# sound/effects/__init__.py
# no `__all__` defined
...

# test.py
import sound.effects.echo
from sound.effects import *   # only imports `echo` since it was included above
```

### "Compiled" Python files

- `.pyc` files
- only speed up loading and not actual execution
- Python caches the compiled version of each module in the __pycache__ directory under the name module.version.pyc,


## String formatting

- Use `f'{...}'` / `F'{...}'`
 
```
# Print based on order
print('We are the {} who say "{}!"'.format('knights', 'Ni'))

# Print based on order and name
print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred', other='Georg'))

# Print based on reusing index and key names
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
...       'Dcab: {0[Dcab]:d}'.format(table))
```

```
f'{22/7:.4f}'   # 4 decimal places
f'{"abc":5}'    # min width string (pad on right) 'abc  '   
f'{123:5d}'     # min width number (pad on left)  '  123'
```

```
f'{object!a}'   # ascii(object)
f'{object!r}'   # repr(object)
f'{object!s}'   # str(object)
```

### Old formatting

- Using `%x` to 
- Followed by `% (tuple)`

```
print('float %5.3f integer: %d' % (22/7, 5))
float 3.143 integer: 5
```

## Read / Writing Files

```
# Read
with open('workfile', encoding="utf-8") as f:
  read_data = f.read() # read entire file
  f.readline()         # read single line
  for line in f:       # read line by line
    print(line, end='')

# Write
with open('test.txt', "w") as f:
  f.write('test')

# Append   
with open('test.txt', "a") as f:
  f.write('test')
```

## Read / Deleting Paths

```
import os

for f in os.listdir(path):
  full_path = os.path.join(path, f)
  print(full_path)


# delete folder recursively
import os

def delete_folder(path):
  if os.path.exists(path):
    for f in os.listdir(path):
      full_path = os.path.join(path, f)
      if os.path.isdir(full_path):
        delete_folder(full_path)
        os.rmdir(full_path)
      else:
        os.remove(full_path)
  os.rmdir(path)

# delete folder recursively
import shutil
shutil.rmtree(OUT)
```
### `open()` modes
```
open(file, mode='r', buffering=- 1, encoding=None, errors=None, newline=None, closefd=True, opener=None)¶
```

- `r` open for reading (default)
- `w` open for writing, truncating the file first
- `x` open for exclusive creation, failing if the file already exists
- `a` open for writing, appending to the end of file if it exists
- `b` binary mode
- `t` text mode (default)
- `+` open for updating (reading and writing)

## JSON

```
import json
x = [1, 'simple', 'list', {'a': 'babc'}]
json.dumps(x)

with open('test.json', "w") as f:
  json.dump(x, f)

with open('test.json', "r") as f:
  y = json.load(f)
  print(y)
```

## YAML

- Using `PyYAML==6.0.2`
```
import yaml

## test.yaml
# sites:
#   a:
#     name: "a site"
#     aliases
#       - sitea.com
#       - asite.com
#   b:
#     name: "site b"
#     aliases
#       - beesite.com
#       - siteofabee.com

with open("test.yaml", "r") as stream:
    try:
        yaml_data = yaml.safe_load(stream)

        print(yaml_data)
        print(yaml.dump(yaml_data))

        for site_data in yaml_data['sites'].values():
          print(site_data)
          print(site_data['name'])
          if 'aliases' in site_data:
            print(site_data['aliases'])


        for site_key, site_data in yaml_data['sites'].items():
          print("%s" % (site_key))
          print(site_data['name'])
          if 'aliases' in site_data:
            print(site_data['aliases'])


    except yaml.YAMLError as exc:
        print(exc)
```

## Exceptions / Errors

```
     try:
         x = int(input("Please enter a number: "))
         break
     except ValueError:
         print("Oops!  That was no valid number.  Try again")

```

- Can have multiple errors
```
except (RuntimeError, TypeError, NameError):
     pass
```


* * * 

args
**table
dump


## Sorting

```
list = [111, 4, 9, 16, 25]
list.sort()
list_str = ["1", "4", "9", "16", "25"]

[111, 4, 9, 16, 25]
[4, 9, 16, 25, 111]
['1', '4', '9', '16', '25']
['1', '16', '25', '4', '9']
[111, 4, 9, 16, 25]
[4, 9, 16, 25, 111]
['1', '4', '9', '16', '25']
['1', '16', '25', '4', '9']
```

## Regex

- Requires `re` module (`import re`)
- 2 ways to call regex
  - use `re.FUNCTION(REGULAR_EXPRESSION, STRING)`
  - compile re pattern `p = re.compile(REGULAR_EXPRESS)` then call function on patter `p.FUNCTION(STRING)`


### Matching / Searching

- `.match()` / `.search()`
  - `.match()` will only report a successful match which will start at 0; if the match wouldn’t start at zero, match() will not report it.
  - `.search()` will scan forward through the string, reporting the first match it finds.
- Resulting object
  - `group()`: Return the string matched by the RE
  - `start()`: Return the starting position of the match
  - `end()`: Return the ending position of the match
  - `span()`: Return a tuple containing the (start, end) positions of the match

```
import re

p = re.compile('[a-z]+', re.MULTILINE | re.IGNORECASE)
m = p.search("abcd\ndef")
m = p.match("abcd\ndef")
m.group() # 'abcd'
m.start() # 0
m.end()   # 4
m.span()  # (0, 4)

# match / search
print(re.match('super', 'insuperable')) # None
print(re.search('super', 'insuperable').span()) # (2, 7)


p.findall("abcd\ndef") # ['abcd', 'def']

iterator = p.finditer("abcd\ndef")
for match in iterator:
  print(match.group())
```

### Grouping

```
p = re.compile('(a(b)c)d')
m = p.match('abcd')
m.groups()     # ('abc', 'b')
m.group(0)     # 'abcd'
m.group(1)     # 'abc'
m.group(2)     # 'b'
m.group(0,1,2) # ('abcd', 'abc', 'b')
```

### Split

```
p = re.compile(r'\W+')
p.split('This is a test')           # ['This', 'is', 'a', 'test']
p.split('This is a test', 2)        # ['This', 'is', 'a test']

re.split(r'\W+', 'This is a test')  # ['This', 'is', 'a', 'test']
```

### Substitution / Search and Replace

```
p = re.compile('(blue|white|red)')
p.sub('colour', 'blue socks and red shoes')           # 'colour socks and colour shoes'
p.sub('colour', 'blue socks and red shoes', count=1)  # 'colour socks and red shoes'
p.sub(r'colour: \1', 'blue socks and red shoes').     # 'colour: blue socks and colour: red shoes'
```

## HTTP requests

```
import json
import requests

def getRequest(url)
    headers = {'Header1': "header value"}
    return requests.get(url, headers=headers)

response = getRequest(url)
text = response.text
if(response.status_code > 302):
    print(response.status_code)
    print(text)
else:
    json_data = json.loads(text)
    return json_data
```

## Call external commands via subprocess

```
# recommended way with full outputs
result = subprocess.run(" ".join(cmd), shell=True, capture_output=True)
print(result.returncode)
if(result.stderr):
    print(result.stderr.decode("utf-8"))
if(result.stdout):
    json_data = json.loads(result.stdout.decode("utf-8"))


# only outputs value. raises CalledProcessError if non-zero exit code
cmd = ['curl', '-sSLD', '-', '-o', '/dev/null', 'https://' + domain]
returned_value = subprocess.check_output(cmd)
print(returned_value.decode("utf-8"))
```

