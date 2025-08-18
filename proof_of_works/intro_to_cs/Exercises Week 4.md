
## 7.1

```python
def size(aSet):
   """
   aSet is a collection of objects, which might be empty.
   Objects are assumed to be of the same type.
   """
```

Good input of test cases:
- Empty set: boundary case
- Set of size 1: boundary case
- Set of size greater than 1: middle value

## 7.2

```python
def union(set1, set2):
   """
   set1 and set2 are collections of objects, each of which might be empty.
   Each set has no duplicates within itself, but there may be objects that
   are in both sets. Objects are assumed to be of the same type.

   This function returns one set containing all elements from
   both input sets, but with no duplicates.
   """
```

Good test cases input:
- Both empty sets: boundary case
- Empty and non-empty set: boundary case
- Both non-empty sets, which do not contain any objects in common: boundary case
- Both non-empty sets, which contain some objects in common: boundary case
- Both non-empty sets, which contain the same objects.: boundary case
	- This does not appear in the choices

## 7.3

```python
def maxOfThree(a,b,c) :
    """
    a, b, and c are numbers

    returns: the maximum of a, b, and c        
    """
    if a > b: # 1
        bigger = a

    else: # 2
        bigger = b

    if c > bigger: # 3
        bigger = c

    return bigger # 4
```

Possible paths are:
- 1, 4  (a)
- 2, 4 (b)
- 1, 3, 4 (c)
- 2, 3, 4 (d)

So, the test suite:
- `maxOfThree(2, -10, 100)` travels (c)
- `maxOfThree(7, 9, 10)` travels (d)
- `maxOfThree(6, 1, 5)` travels (a)
- `maxOfThree(0, 40, 20)` travels (b)

## 7.4

```python
def union(set1, set2):
   """
   set1 and set2 are collections of objects, each of which might be empty.
   Each set has no duplicates within itself, but there may be objects that
   are in both sets. Objects are assumed to be of the same type.

   This function returns one set containing all elements from
   both input sets, but with no duplicates.
   """
   if len(set1) == 0: # 1
      return set2
   elif set1[0] in set2: # 2
      return union(set1[1:], set2)
   else: # 3
      return set1[0] + union(set1[1:], set2)
```

Possible paths:
- 1 (a)
- 2, 1 (b)
- 3, 1 (c)
- Twice recursive calls (d)
	- 2, 2, 1
	- 3, 3, 1
	- 2, 3, 1
	- 3, 2, 1

So, the test cases for glass box testing are:
- `union('', 'abc')`: (a)
- `union('a', 'abc')`: (b)
- `union('ab', 'abc')`: (d)
- `union('d', 'abc')`: (c)


## 7.5

```python
def foo(x, a):
   """
   x: a positive integer argument
   a: a positive integer argument

   returns an integer
   """
   count = 0
   while x >= a: # 1
      count += 1
      x = x - a
   return count # 2
```

Possible paths:
- 2 (a)
- 1, 2 (b)
- 1, 1, 2 (c)

The best glass box test suite for the function `foo`:
- `foo(10, 3)` covers (c)
- `foo(1, 4)` covers (a)
- `foo(10, 6)` covers (b)

## integer division

Suppose
```python
def integerDivision(x, a):
    """
    x: a non-negative integer argument
    a: a positive integer argument

    returns: integer, the integer division of x divided by a.
    """
    while x >= a:
        count += 1
        x = x - a
    return count
```

When this runs:
```
print(integerDivision(5, 3))
```

We get:
```
File "temp.py", line 9, in integerDivision
    count += 1
UnboundLocalError: local variable 'count' referenced before assignment
```

What is the bug?:
- `count += 1` means `count = count + 1`
- So, `count` is referenced although it is not assigned a value.
- Fix: add a line `count = 0` before the line `while x >= a:`
	- so that it satisfies the specification.


## 7.6

```python
def rem(x, a):
    """
    x: a non-negative integer argument
    a: a positive integer argument

    returns: integer, the remainder when x is divided by a.
    """
    if x == a:
        return 0
    elif x < a:
        return x
    else:
        rem(x-a, a)
```

Test cases:
- `rem(2, 5)` returns 2
- `rem(5, 5)` returns 0
- `rem(7, 5)` returns None

When `rem(7, 5)`:
- It calls `rem(2, 5)`
- However, the function just calls it and the function returns nothing eventually.

So the fix is:
- Change the code so that the function returns the value returned from the recursive call.
	- `rem(x-a, a)` -> `return rem(x-a, a)`


## 7.7

```python
def f(n):
   """
   n: integer, n >= 0.
   """
   if n == 0:
      return n
   else:
      return n * f(n-1)
```


Test cases:
- When we call `f(3)` we expect the result 6, but we get 0.
- When we call `f(1)` we expect the result 1, but we get 0.
- When we call `f(0)` we expect the result 1, but we get 0.

The function always returns 0 because, eventually, the code reaches the base case that returns 0.
- The function returns `f(n) * f(n-1) * f(n-2) * ... * f(1) * f(0)`, and f(0) is 0

The meaningful code would contain a base case where:
```python
if n == 0:
	return 1
```


## 8.1

What error?

```
'1' / '2'
```
- TypeError

```
'1' / 2
```
- TypeError

```
int('1') / 2.0
```
- No error

```
mylist = [10, 20, 30]
mylist.index(11)
```
- ValueError: index() only takes a valid index

```
A=2
3*a
```
- NameError


## 8.2

Suppose:
```python
def fancy_divide(numbers,index):
    try:
        denom = numbers[index]
        for i in range(len(numbers)):
            numbers[i] /= denom
    except IndexError:
        print("-1")
    else:
        print("1")
    finally:
        print("0")
```

Answers:
- `fancy_divide([0,2,4], 1)` prints 1 and 0
- `fancy_divide([0, 2, 4], 4)` prints -1 and 0
- `fancy_divide([0, 2, 4], 0)` prints 0 and *ZeroDivisionError*

```python
def fancy_divide(numbers, index):
    try:
        denom = numbers[index]
        for i in range(len(numbers)):
            numbers[i] /= denom
    except IndexError:
        fancy_divide(numbers, len(numbers) - 1)
    except ZeroDivisionError:
        print("-2")
    else:
        print("1")
    finally:
        print("0")
```

Answers:
- `fancy_divide([0, 2, 4], 1)` prints 1 and 0
- `fancy_divide([0, 2, 4], 4)` prints 1,  0
- `fancy_divide([0, 2, 4], 0)` prints -2, and 0

```python
def fancy_divide(numbers, index):
    try:
        try:
            denom = numbers[index]
            for i in range(len(numbers)):
                numbers[i] /= denom
        except IndexError:
            fancy_divide(numbers, len(numbers) - 1)
        else:
            print("1")
        finally:
            print("0")
    except ZeroDivisionError:
        print("-2")
```

Answers:
- `fancy_divide([0, 2, 4], 1)` prints 1 and 0
- `fancy_divide([0, 2, 4], 4)` prints 1, 0, and 0
- `fancy_divide([0, 2, 4], 0)` prints 0 and -2

```python
def fancy_divide(list_of_numbers, index):
    try:
        try:
            raise Exception("0")
        finally:
            denom = list_of_numbers[index]
            for i in range(len(list_of_numbers)):
                list_of_numbers[i] /= denom
    except Exception as ex:
        print(ex)
```

Answer:
- When `fancy_divide([0, 2, 4], 0)` is called, it ***does not*** prints 0
- Exception precedence: the newer exception takes precedence, replacing the original exception.
- So, in this case, `raise Exception("0")` is replaced by `ZeroDivisionError` in the finally block.



```python
def fancy_divide(list_of_numbers, index):
    try:
        try:
            denom = list_of_numbers[index]
            for i in range(len(list_of_numbers)):
                list_of_numbers[i] /= denom
        finally:
            raise Exception("0")
    except Exception as ex:
        print(ex)
```

Answer:
- When `fancy_divide([0, 2, 4], 0)` is called, it prints 0

## simple divide

simple_divide returns 0 if zero division occurs.
```python
def fancy_divide(list_of_numbers, index):
   denom = list_of_numbers[index]
   return [simple_divide(item, denom) for item in list_of_numbers]


def simple_divide(item, denom):
	try:
		return item / denom
	except ZeroDivisionError:
		return 0
```


## 8.3

Suppose
```python
def normalize(numbers):
	"""
	numbers: list, positive numbers
	Returns list, modified numbers where each element is divided by the largest number in the numbers
	"""
    max_number = max(numbers)
    for i in range(len(numbers)):
        numbers[i] /= float(max_number)
    return numbers
```

Then:
```python
try:
      normalize([0, 0, 0])
except ZeroDivisionError:
      print('Invalid maximum element')
```

Answers:
1. The try block throws an exception.
2. It is ZeroDivisionError
3. It prints `Invalid maximum element`
4. Post-condition is that it returns a list, where each number is between 0 and 1
5. Pre-condition should state an input list does not contain all 0s

Suppose:
```python
def normalize(numbers):
    max_number = max(numbers)
    assert(max_number != 0), "Cannot divide by 0"
    for i in range(len(numbers)):
        numbers[i]  /= float(max_number)
        assert(0.0 <= numbers[i] <= 1.0), "output not between 0 and 1"
    return numbers
```

Answers:
1. `assert(max_number != 0)` corresponds to the pre-condition.
2. `assert(0.0 <= numbers[i] <= 1.0)` corresponds to the post-condition
3. `normalize([0, 0, 0])` prints `AssertionError: Cannot divide by 0`


