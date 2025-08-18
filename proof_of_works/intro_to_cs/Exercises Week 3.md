
## 5.1

Suppose
```python
x = (1, 2, (3, 'John', 4), 'Hi')
```

Type and value:
- `x[0]`: int, 0
- `x[2]`: tuple, (3, 'John', 4)
- `x[-1]`: str, 'Hi'
- `x[2][2]`: int, 4
- `x[2][-1]`: int, 4
- `x[-1][-1]`: str, 'i'
- `x[-1][2]`: error, IndexError
- `x[0:1]`: int, 1
- `x[0:-1]`: tuple, `(1, 2, (3, 'John', 4))`
- `len(x)`: int, 4
- `2 in x`: bool, True
- `3 in x`: bool, False
 - `x[0] = 8`: error, TypeError

## odd tuples

```python
def odd_tuples(t):
    '''
    t: a tuple
    returns: tuple, every other element of aTup. 
    '''
	ot = ()
	for i in range(0, len(t), 2):
		ot = ot + (t[i],) # a tuple can be added to a tuple

	return ot
```

## 5.2

Suppose:
```python
x = [1, 2, [3, 'John', 4], 'Hi']
```

Type and value:
- `x[0]`: int, 1
- `x[2]`: list, `[3, 'John', 4]`
- `x[-1]`: str, 'Hi'
- `x[2][2]`: int, 4
- `x[0:1]`: int, 1
- `2 in x`: bool, True
- `3 in x`: bool, False
- `x[0] = 8 x`: list, `[1, 2, [3, 'John', 4], 'Hi']`


## 5.3

Suppose:
```python
listA = [1, 4, 3, 0]
listB = ['x', 'z', 't', 'q']
```

Specify type and value (modification stays):
1. `listA.sort`: function
2. `listA.sort()`: NoneType, None
3. `listA`: list, `[0, 1, 3, 4]`
4. `listA.insert(0, 100)`: NoneType, None
5. `listA.remove(3)`: NoneType, None
6. `listA.append(7)`: NoneType, None
7. `listA`: list, `[100, 0, 1, 4, 7]`
8. `listA + listB`: list, `[100, 0, 1, 4, 7, 'x', 'z', 't', 'q']`
9. `listB.sort(); listB.pop()`: str, 'z'
10. `listB.count('a')`: int, 0
11. `listB.remove('a')`: NoneType, None
12. `listA.extend([4, 1, 6, 3, 4])`: NoneType, None
13. `listA.count(4)`: int, 3
14. `listA.index(1)`: int, 2
15. `listA.pop(4)`: int, 7
16. `listA.reverse()`: NoneType, None
17. `listA`: list, `[4, 3, 6, 1, 4, 4, 1, 0, 100]`

## 5.4

```
>>> aList = [0, 1, 2, 3, 4, 5]
>>> bList = aList
>>> aList[2] = 'hello'
>>> aList == bList
bool, True

>>> aList is bList
bool, True

>>> aList
list, [0, 1, 2, 3, 4, 5]

>>> bList
list, [0, 1, 2, 3, 4, 5]

>>> cList = [6, 5, 4, 3, 2]
>>> dList = []
>>> for num in cList:
        dList.append(num)
>>> cList == dList
bool, True

>>> cList is dList
bool, False # they are different objects

>>> cList[2] = 20
>>> cList
list, [6, 5, 20, 3, 2]

>>> dList
list, [6, 5, 4, 3, 2]
```

## apply to each

Suppose:
```python
def apply_to_each(L, f):
    for i in range(len(L)):
        L[i] = f(L[i])
		
testList = [1, -4, 8, -9]
```

Provide expression to be:
```
>>> print(testList)
[5, -20, 40, -45]
```

```python
def times_five(num):
	return num * 5
	
apply_to_each(testList, times_five)
```

---

```
>>> print(testList)
  [1, 4, 8, 9]
```

```python
def f(x):
	return abs(x // 5)

apply_to_each(testList, f)
```

---

```
 >>> print(testList)
  [2, -3, 9, -8]
```

```python
def inc_one(x):
	return x + 1

apply_to_each(testList, inc_one)
```

---

```
>>> print testList
  [1, 16, 64, 81]
```

```python
def pow_two(x):
	return x * x

apply_to_each(testList, pow_two)
```

## 5.5

Suppose:
```python
def applyEachTo(L, x):
	"""
	L: list of functions, x: number
	L: [f1, f2, ...]
	Returns a new list: [f1(x), f2(x), ...]
	"""
    result = []
    for i in range(len(L)):
        result.append(L[i](x))
    return result

def square(a):
    return a*a

def halve(a):
    return a/2

def inc(a):
    return a+1
```

Evaluate:

```python
applyEachTo([inc, square, halve, abs], -3)
```
- `[-2, 9, -1.5, 3]`

```python
applyEachTo([inc, square, halve, abs], 3.0)
```
- `[4.0, 9.0, 1.5, 3.0]`

```python
applyEachTo([inc, max, int], -3)
```
- `TypeError`
	- max takes an iterable rather than a number `-3`


## 6.1

Suppose:
```python
animals = {'a': 'aardvark', 'b': 'baboon', 'c': 'coati'}

animals['d'] = 'donkey'
```

Evaluate:

```
>>> animals
{'a': 'aardvark', 'b': 'baboon', 'c': 'coati', 'd': 'donkey'}
```

```
>>> animals['c']
'coati'
```

```
>>> animals['donkey']
KeyError
```

```
>>> len(animals)
4
```

```
>>> animals['a'] = 'anteater'
>>> animals['a']
'anteater'
```

```
>>> len(animals['a'])
8
```

```
>>> 'baboon' in animals
False
```

```
>>> 'donkey' in animals.values()
True
```

```
>>> 'b' in animals
True
```

```
>>> animals.keys()
dict_keys(['a', 'b', 'c', 'd'])
```

```
>>> del animals['b']
>>> len(animals)
3
```

```
>>> animals.values()
dict_values(['anteater', 'coati', 'donkey'])
```

## how many

Suppose:
```python
animals = { 'a': ['aardvark'], 'b': ['baboon'], 'c': ['coati']}

animals['d'] = ['donkey']
animals['d'].append('dog')
animals['d'].append('dingo')
```

First, write a procedure, called `how_many`, which returns the sum of the number of values associated with a dictionary.

```python
def how_many(a_dict):
	'''
    a_dict: A dictionary, where all the values are lists.
    returns: int, how many values are in the dictionary.
    '''

	return sum(map(len, a_dict.values()))
```


## biggest

```python
animals = { 'a': ['aardvark'], 'b': ['baboon'], 'c': ['coati']}

animals['d'] = ['donkey']
animals['d'].append('dog')
animals['d'].append('dingo')
```

This time, write a procedure, called `biggest`, which returns the key corresponding to the entry with the largest number of values associated with it. If there is more than one such entry, return any one of the matching keys.

```python
def biggest(a_dict):
	'''
    a_dict:  dict, where all the values are lists
    returns: list, keys with the largest number of values associated with it
    '''
	max_count = max(map(len, a_dict.values))
	
	result = []
	for k in a_dict:
		if len(a_dict[k]) == max_count:
			result.append(k)

	return result
```


## Fibonacci and Dictionaries

Fibonacci number in this recursive function:
```python
def fib(n):
	if n == 1 or n == 2:
		return 1

	return fib(n-1) + fib(n-2)
```

The problem: this recursive function executes same overlapping calculations.
```
fib(10) -> fib(9) + fib(8) -> fib(8) + fib(7) + fib(7) + fib(6) -> ...
```
- Those overlapping fib(7) is calculated independently, creating identical call stacks.

Fibonacci using memoization:
```python
def fib(n, d):
	"""
	n: int
	d: dict, where value of fib(n) is stored as n:fib(n) pairs
	Returns n-th value of Fibonacci sequence
	"""

	if n in d:
		return d[n]
		
	ans = fib(n-1, d) + fib(n-2, d)
	d[n] = ans # memoization
	
	return ans
```


## Global Variables

Global variables...
- can be dangerous to use becuase
	- it can break the scoping of variables
- can be handy if used to keep track of information inside a function

`global` keyword to declare global variable
```python
def fib(n):
	global numFibCalls
	numFibCalls += 1
	if n == 1 or n == 2:
		return 1
	return fib(n-1) + fib(n-2)
```


