
## Tuples

Tuple: an ordered and immutable list of mixed element types.
```python
# empty tuple
t0 = ()
t = (2, "one", False)
t[1] # -> "one"
(1, 2, 3) + (4, 5) # -> (1, 2, 3, 4, 5)
t1 = (1,) # one element tuple
t[0] = 1 # ERROR, immutable
```

Tuples do not need parentheses sometimes:
```python
x = 1, 2
type(x) # tuple
```

Swap variables using tuples:
```python
x, y = y, x
```
- **Tuple packing**: comma-separated values are converted into a tuple when evaluated.
- **Tuple unpacking**: a tuple is assigned to comma-separated variables separately.

Returning a tuple and unpack it.
```python
def qr(x,y):
	return x//y, x%y # tuple packing
```


## Lists

List: ordered and mutable sequence with mixed types.
```python
ls = [] # empty list
ls1 = [2, 'a', True, 1.2]
```

Iteration using `in` operator:
```python
ls = [1, 2, 3, 4, 5]
for num in ls:
	print(num)
```


## List Operations

Appending an element:
```python
ls = [1, 2]
ls.append(3) # ls is now [1, 2, 3]
```

Add lists (without mutations):
```python
x = [1, 2]
y = [3]
x + y # [1, 2, 3]
```

Extend list (with mutations):
```python
x = [1, 2]
y = [3, 4]
x.extend(y)
x # [1, 2, 3, 4]
```

Delete an element:
```python
x = [1, 2, 3]
del x[0]
x # [2, 3]
```

Pop an element:
```python
x = [1, 2, 3]
y = x.pop()
x, y # ([1, 2], 3)
```

Remove a specific element of the first occurrence:
```python
l = [1, 2, 3, 2]
l.remove(2)
l # [1, 3, 2]
```

Split and join:
```python
"apple,banana,orange,lemon".split(",") # default separator is " "
# > ["apple", "banana", "oragne", "lemon"]
','.join([1, 2, 3, 4])
# > '1,2,3,4'
```

Sort:
```python
x = [9, 0, 1, 5, 2]
sorted(x) # returns sorted list without mutating x
x.sort() # sort x, mutating it
x.reverse() # reverse the order of the list
# > [9, 5, 2, 1, 0]
```


## Mutation, Aliasing, Cloning

Aliasing: giving a name to an object.

Cloning a list:
```python
x = [1, 2, 3]
y = x[:]
```

Sorting list:
- `list.sort()` mutates the list
- `sorted(list)` does not mutate the list

Nested list:
```python
x = [1, 2, [3, 4]]
```


Avoid mutation of a list that is used with an iteration.

## Function as Objects

Function is a **first-class object**:
- assigned to a variable
- passed as an argument
- returned as an object

Example, function as an argument:
```python
def apply_to_each(L, f):
	"""
	L: list, f: function
	Suppose L = [e1, e2, ...]
	Mutate a list so that L = [f(e1), f(e2,) ...]
	"""
	for i in rage(len(L)):
		L[i] = f(L[i])
```

Built-in `map()` function returns iterator:
```python
list(map(abs, [-1, -2, 3, -4.5]))
# returns [1, 2, 3, 4.5]
```


## Quick Review

Sequence: an ordered set
- string
- list
- tuple
- range object

Operations on sequence `seq`:
- `seq[i]`
- `len(seq)`
- `seq1 + seq2`
- `n * seq`  (not for range)
- `seq[start:end]` (not for range)
- `e in seq`
- `e not in seq`
- `for i in seq`

## Dictionaries

Dictionary: a mutable set that holds key-value pairs.
- Key: unique in the dictionary and hashable
- Value: any object in any type
- Unordered

Example:
```python
grades = {'Ana': 'B', 'Denise': 'A', 'John': 'A+', 'Katy': 'A'}

grades['John'] # access value of key='John'

grades['Sylvan'] # KeyError, no such key

grades['Sylvan'] = 'A' # Creates a new entry

grades['Ana'] = 'C' # Update an entry

'Denise' in grades # True, returns if key exists

del grades['Ana'] # delete an entry

grades.keys() # returns keys as an iterable (dict_keys object)

grades.values() # returns values as an iterable
```


## Examples with a Dictionary

Word counter:
```python
def word_counter(ls):
	data = {}
	for word in ls:
		if word in data:
			data[word] += 1
		else:
			data[word] = 1
	return data
```

Finding most common words:
```python
def most_common_words(freqs):
	"""
	freqs: dict, contains word:frequency pairs
		- word: str
		- frequency: int
	Returns tuple, (words, best)
		- words: list, most frequent words
		- best: the number the most frequent word appeared
	"""
	for k in freqs:
		if freqs[k] == best:
			words.append(k)
	return words, best
```














