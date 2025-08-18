## 3.1
```python
iteration = 0
count = 0
while iteration < 5:
    # the variable 'letter' in the loop stands for every 
    # character, including spaces and commas!
    for letter in "hello, world": 
        count += 1
    print("Iteration " + str(iteration) + "; count is: " + str(count))
    iteration += 1 
```


| Variable (at print statement) |     |     |     |     |     |
| ----------------------------- | --- | --- | --- | --- | --- |
| iteration                     | 0   | 1   | 2   | 3   | 4   |
| count                         | 12  | 24  | 36  | 48  | 60  |

```python
iteration = 0
while iteration < 5:
    count = 0
    for letter in "hello, world":
        count += 1
    print("Iteration " + str(iteration) + "; count is: " + str(count))
    iteration += 1
```


| Variable (at print statement) |     |     |     |     |     |
| ----------------------------- | --- | --- | --- | --- | --- |
| iteration                     | 0   | 1   | 2   | 3   | 4   |
| count                         | 12  | 12  | 12  | 12  | 12  |

```python
iteration = 0
while iteration < 5:
    count = 0
    for letter in "hello, world":
        count += 1
        if iteration % 2 == 0:
            break
    print("Iteration " + str(iteration) + "; count is: " + str(count))
    iteration += 1
```

1. The print statement is executed 5 times.
2. The largest value in `iteration` printed out is 4
3. The largest value in `count` printed out is 12
4. The smallest value in `count` printed out is 1


## 3.2
```python
x = 25
epsilon = 0.01
step = 0.1
guess = 0.0

while guess <= x:
    if abs(guess**2 -x) >= epsilon:
        guess += step

if abs(guess**2 - x) >= epsilon:
    print('failed')
else:
    print('succeeded: ' + str(guess))
```
- It is probable that `guess` would be slightly less than 5 after 50th iteration. Then, the while loop would be an infinite loop.

```python
x = 25
epsilon = 0.01
step = 0.1
guess = 0.0

while abs(guess**2-x) >= epsilon:
    if guess <= x:
        guess += step
    else:
        break

if abs(guess**2 - x) >= epsilon:
    print('failed')
else:
    print('succeeded: ' + str(guess))
```
- When `guess` becomes slightly less or more than 5, then the program breaks out of the while loop, and `abs(guess**2 - x) < epsilon` becomes True. So, the success message will be printed.
- Suppose `x = 23` in the first line. When `guess` becomes slightly less or more than 4.8, `guess ** 2` becomes approximately 23.04, and `guess ** 2 - x` becomes around 0.04, which is greater than the epsilon. So the `'failed'` message will be printed out.


## guess my number

Requirements:

Print once at first
```
Please think of a number between 0 and 100!
```

Asking and accepting user input
```
Is your secret number <guessed_number>?
Enter 'h' to indicate the guess is too high. Enter 'l' to indicate the guess is too low. Enter 'c' to indicate I guessed correctly. <user_input>
```

If a user input is 'c':
```
Game over. Your secret number was: <correct_guess>
```

Code:
```python
def guess_game():
	# the rule
	print("Please think of a number between 0 and 100!")

	guess = 50
	high = 100
	low = 0

	while True:
		print(f"Is your secret number {guess}?")
		option = input("Enter 'h' to indicate the guess is too high. Enter 'l' to indicate the guess is too low. Enter 'c' to indicate I guessed correctly. ")

		if(option == 'c'): # correct guess
			print(f"Game over. Your secret number was: {guess}")
			break
		elif(option == 'h'):
			high = guess
			guess = (high + low) // 2
		elif(option == 'l'):
			low = guess
			guess = (low + high) // 2
		else:
			print("Sorry, I did not understand your input.")
		
```



## 3.3

True or False? The internal computer representation of any number is always an approximation.
- False: For example, date number must always be handled in a precise way.

True or False? The internal representation of the decimal number 1/10 = 0.1 requires an infinite number of digits.
- True: A computer must hold the number in binary. The binary representation of 0.1 becomes a repeating fraction.
	- $0.1 \cdot 2^{n}$ can not be a whole number as $0.1 \cdot 2 = 2$ ,  $0.2 \cdot 2 = 0.4$, $0.4 \cdot 2 = 0.8$,  $0.8 \cdot 2 = 1.6$,  $1.6 \cdot 2 = 3.2$, ...


## 4.1

Indicate return type:

```python
def a(x):
   '''
   x: int or float.
   '''
   return x + 1
```
- int or float

```python
def b(x):
   '''
   x: int or float.
   '''
   return x + 1.0
```
- float

```python
def c(x, y):
   '''
   x: int or float. 
   y: int or float.
   '''
   return x + y
```
- int or float
	- int + int becomes int, otherwise float

```python
def d(x, y):
   '''
   x: Can be int or float.
   y: Can be int or float.
   '''
   return x > y
```
- bool

```python
def e(x, y, z):
   '''
   x: Can be int or float.
   y: Can be int or float.
   z: Can be int or float.
   '''
   return x >= y and x <= z
```
- bool

```python
def f(x, y):
   '''
   x: int or float.
   y: int or float
   '''
   x + y - 2
```
- NoneType

## square
Write a Python function, `square`, that takes in one number and returns the square of that number.

```python
def square(n):
	"""
	n: int or float.
	"""
	return n ** 2
```


## eval quadratic

Write a Python function, `evalQuadratic(a, b, c, x)`, that returns the value of the quadratic $a\cdot x^{2} + b\cdot x + c$.

```python
def evalQuadratic(a, b, c, x):
	'''
    a, b, c: numerical values for the coefficients of a quadratic equation
    x: numerical value at which to evaluate the quadratic.
    '''
    return a * x ** 2 + b * x + c
```

## 4.2

```python
def a(x):
   '''
   x: int or float.
   '''
   return x + 1

def b(x):
   '''
   x: int or float.
   '''
   return x + 1.0
  
def c(x, y):
   '''
   x: int or float. 
   y: int or float.
   '''
   return x + y

def d(x, y):
   '''
   x: Can be of any type.
   y: Can be of any type.
   '''
   return x > y

def e(x, y, z):
   '''
   x: Can be of any type.
   y: Can be of any type.
   z: Can be of any type.
   '''
   return x >= y and x <= z

def f(x, y):
   '''
   x: int or float.
   y: int or float
   '''
   x + y - 2
```

Evaluate type and value:
- `a(6)`: int, 7
- `a(-5.3)`: float, -4.3
- `a(a(a(6)))`: int, 9
- `c(a(1), b(1))`: float, 4.0
	- a(1) -> 2
	- b(1) -> 2.0
	- c(2, 2.0) -> 4.0
- `d('apple', 11.1)`: TypeError
- `e(a(3), b(4), c(3, 4))`: bool, False
	- a(3) -> 4
	- b(4) -> 5.0
	- c(3, 4) -> 7
	- e(4, 5.0, 7) -> False
- `f`: function

## 4.3

```python
def a(x, y, z):
     if x:
         return y
     else:
         return z

def b(q, r):
    return a(q>r, q, r)
```

Evaluate type and value:
1. a(False, 2, 3): int, 3
2. b(3, 2): int, 3
	1. a(3>2, 3, 2)
3. a(3>2, a, b): function, a
4. b(a, b): TypeError
	1. a(a > b, a, b)

## 4.4

Evaluate type and value:

```
>>> a = 10
>>> def f(x):
      return x + a
>>> a = 3
>>> f(1)
```
- int, 4


```
>>> x = 12
>>> def g(x):
      x = x + 1
      def h(y):
          return x + y
      return h(6)
>>> g(x)
```
- int, 19
	- x -> 12
	- g -> function
	- g(12)
		- x -> 13
		- h -> function
		- h(6) -> 13 + 6 -> 19
		- return 19

## 4.5

Evaluate value:
```python
def foo(x, y = 5):
   def bar(x):
      return x + 1
   return bar(y * 2)
          
foo(3)
```
- foo(3) -> foo(3, 5) -> bar(5 * 2) -> 11
- Answer: 11

```python
def foo(x, y = 5):
   def bar(x):
      return x + 1
   return bar(y * 2)
          
foo(3, 0)
```
- foo(3, 0) -> bar(0 * 2) -> 1
- Answer: 1

```python
def foo (x):
   def bar (z, x = 0):
      return z + x
   return bar(3, x)

foo(2)
```
- foo(2) -> bar(3, 2) -> 5
- Answer: 5

```python
def foo (x):
   def bar (z, x = 0):
      return z + x
   return bar(3)

foo(5)
```
- foo(5) -> bar(3) -> bar(3, 0) -> 3
- Answer: 3


## 4.6

Suppose:
```
> str1 = 'exterminate!' 
> str2 = 'number one - the larch'
```

1. `str1.upper`: function
2. `str1.upper()`: str, "EXTERMINATE!"
3. `str1`: str, 'exterminate!'
4. `str1.isupper()`: bool, False
5. `str1.islower()`: bool, True (the method only sees alphabet characters)
6. `str2 = str2.capitalize \ str2`: str, 'Number one - the larch'
7. `str2.swapcase()`: str, 'nUMBER ONE - THE LARCH'
8. `str1.index('e')`: int, 0 (the first occurrence, return)
9. `str2.index('n')`: int, 8
10. `str2.find('n')`: int, 8
11. `str2.index('!')`: ValueError
12. `str2.find('!')`: int, -1 (the difference str.index vs str.find)
13. `str1.count('e')`: int, 3
14. `str1 = str1.replace('e', '*') \ str1`: str, `'*xt*rminat*!'`
15. `str2.replace('one', 'seven')`: str, 'Number seven - the larch'

## fourth power

```python
def square(n):
	return n * n

def fourth_power(n):
	'''
	x: int or float.
	Returns n to the forth power 
	'''
	return square(n) ** 2
```


## odd

```python
def odd(x):
    '''
    x: int
    returns: True if x is odd, False otherwise
    '''
	return x % 2 == 1
```


## iter power
```python
def iter_power(base, exp):
	'''
    base: int or float.
    exp: int >= 0
    returns: int or float, base^exp
	'''
	result = 1
	while exp > 0:
		result *= base
		exp -= 1
	return result
```

## recur power
```python
def recur_power(base, exp):
    '''
    base: int or float.
    exp: int >= 0
    returns: int or float, base^exp
	'''
	
	if exp == 0: # base case
		return 1
	
	return base * recur_power(base, exp - 1)
```


## gcd iter

```python
def gcd_iter(a, b):
    '''
    a, b: positive integers
    returns: a positive integer, the greatest common divisor of a & b.
    '''
	
	# Assume a is smaller
	if a > b:
		a, b = b, a

	divisor = a

	while not (a % divisor == 0 and b % divisor == 0):
		divisor -= 1

	return divisor
```

## gcd recur

Euclid's algorithm: suppose `gcd(a, b)` where `a <= b`
- If `a = 0` then the answer is `b`
- Otherwise, `gcd(a, b)` is the same as `gcd(a, b % a)`

```python
def gcd_recur(a, b):
	if a > b:
		a, b = b, a
	if a == 0:
		return b
	return gcd_recur(a, b % a)
```


## is in

```python
def is_in(char, a_str):
    '''
    char: a single character
    a_str: an alphabetized string
    
    returns: True if char is in aStr; False otherwise
    '''
    # Your code here

	if len(a_str) == 0:
		return False

	if len(a_str) == 1:
		return a_str == char

	mid = len(a_str) // 2

	if a_str[mid] == char:
		return True

	return is_in(char, a_str[:mid]) if char < a_str[mid] else is_in(char, a_str[mid:])

```

## 4.7



```python
# inventory.py
aa = "aa"
tripleA = "aaa"
print(aa)
```
- When this runs, it prints `aa`

```python
# inventory.py
aa = "aa"
tripleA = "aaa"
print(batteries.aa)
```
- When this runs, it causes an error.
	- NameError occurs.
	- Because the module `batteries` has not been imported yet.
	

```python
# batteries.py
aa = "AA"
aaa = "AAA"
c = "C"
d = "D"
```

```python
# inventory.py
import batteries
aa = "aa"
tripleA = "aaa"
print(batteries.aa)
```
- When this runs, it prints `AA`

```python
# inventory.py
from batteries import *
aa = "aa"
print(aa, aaa, c, d)
```
- When this runs, it prints `aa AAA C D`
	- Because `aa = "aa"` overrides the name `aa`

## Grader

A regular polygon has `n` number of sides. Each side has length `s`.

The area of regular polygon is:
$$
\frac{0.25 \cdot n \cdot s^{2}}{\tan{(\pi/n)}}
$$
The perimeter of a regular polygon: $n \cdot s$

```python
from math import tan, pi
def polysum(n, s):
	"""
	n: number of sides of a regular polygon
	s: size of each side
	Returns the sum of:
		- the area of the regular polygon
		- the square of the perimeter
	rounded to 4 decimal places.
	"""

	area = (0.25 * n * s ** 2) / (tan(pi/n))

	sq_peri = (n * s) ** 2

	return round(area + sq_peri, 4)
	
```

