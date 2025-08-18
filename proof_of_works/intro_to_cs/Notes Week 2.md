
## Approximate Solutions

To approximate solutions:
1. Start with exhaustive enumeration
2. Guess a value
3. Check the value is close enough. If so, end the loop.
4. Update the value so that the value gets closer to the answer.

End case for calculating cube root of $x$
$$
\vert \text{guess} \vert^{3} - x \le \epsilon
$$
- for small $\epsilon$

Code approximates cube root of a number
```python
def cube_root(n):
	epsilon = 0.01
	guess = 0.0
	increment = 0.001
	while abs(guess ** 3 - n) >= epsilon:
		guess += increment

	if n < 0:
		guess = -guess
		
	print(f"Cube root of {n} is approximately {guess}")
```
- Problem: the number of iterations gets bigger if the input number increases.

## Bisection Search

Bisection search algorithm:
1. Guess using the middle value of the possible range.
2. Compare the middle value with the answer.
3. Update the possible range and repeat the process until the value is close enough to the answer.

```python
x = 25
epsilon = 0.01
low = 1.0
high = x
ans = (high + low) / 2.0

while abs(ans ** 2 - x) >= epsilon:
	if ans ** 2 < x:
		low = ans
	else:
		high = ans

	ans = (high + low) / 2.0

print(f"{ans} is close to square root of {x}")
```

Observations:
- Time complexity: $O(\log{n})$
- Should work on problems with ordering property
	- which means the value of function varies monotonically

## Floats and Fractions

Floats approximate real numbers.
 - Decimal number: digits of 0-9
 - Binary number: digits of 0 or 1

Decimal to binary conversion:
1. Divide a decimal by 2
2. The remainder becomes the left-most digit of the binary number
3. Keep the process for each quotient, until the quotient becomes 0.

The Code:
```python
def dec_to_bin(num):
	isNeg = num < 0
	num = abs(num)
	result = ''
	
	while True:
		result = str(num % 2) + result
		num = num // 2
		if (num == 0):
			break

	if (isNeg):
		result = '-' + result

	return result
```

Fractions to binary:
1. Write as a float number
2. Multiply by 2 until it becomes nearly a whole number
3. Convert the whole number to the binary
4. Divide the binary by how many times multiplied by 2 ($n$ of $2^{n}$), shifting right $n$ times.


## Newton-Raphson

General approximation algorithm to find roots of a polynomial in one variable
$$
p(x) = a_{n}x^{n} + a_{n-1}x^{n-1} + \ldots + a_{1}x + a_{0}
$$
- Find $r$ such that $p(r) = 0$
- E.g., to find $\sqrt{24}$, find the root of $p(x)$ = $x^{2} - 24$

Newton showed that if $g$ is an approximation to the root, then
$$
g - \frac{p(g)}{p'(g)}
$$
is a better approximation.

When, $p(x) = x^{2} - k$,
$$
(x^{2}- k)' = 2x
$$
$$
\frac{p(x)}{p'(x)}= \frac{x^{2} - k}{2x}
$$

So the new approximation $g$ is,
$$
g := g - \frac{g^{2} - k}{2g}
$$


Code:
```python
def nr_sqrt(k):
	epsilon = 0.01
	g = k / 2.0

	while abs(g ** 2 - k) >= epsilon:
		g = g - (g ** 2 - k) / (2 * g)

	return g
```

## Decomposition and Abstraction

Functions introduce a mechanism to achieve decomposition and abstraction.
- Abstraction: Hiding internal details, exposing only necessary parts.
- Decomposition: Breaking a complex thing into simple parts.

Module:
- Self-contained
- Reusable
- Organizes code
- Makes code coherent

## Introducing Functions

Function components:
- Name
- Parameters
- Docstring
- Body (code block)

```python
def function_name(var1, var2, ...):
	"""
	Docstring
	...
	"""
	<code_block>
```
- The code block can have return statement, which indicates the return value of the function

A function that takes integer
```python
def is_even(n):
	"""
	Input: n, positive integer
	Returns True if n is even, otherwise False
	"""
	return n % 2 == 0
```


## Calling Functions and Scope
```python
def f(x):
	x = x + 1
	print(f"in f(x): x = {x}")
	return x

x = 3
z = f(x)
```
- Global scope: x -> 3
- A function creates a new scope.
	- Initially x -> 3
	- Then, x -> 4

Python returns `None` value when a function returns nothing.
- `print('string')` returns None

Scope examples:
```python
def f(y):
	x = 1
	x += 1
	print(x)

x = 5
f(x)
print(x)
```
- Global scope: x -> 5
- Function scope: x -> 1, then x -> 2
- Prints `2`, then `5`

```python
def g(y):
	print(x)
	print(x + 1)

x = 5
g(x)
print(x)
```
- Global scope: x -> 5
- Function scope: x -> global x -> 5
- Prints `5`, `6`, then `5`

```python
def h(y):
	x = x + 1

x = 5
h(x)
print(x)
```
- Global scope: x -> 5
- In `x = x + x`:
	- `x` in the left hand side declares `x` in the function scope, which is unassigned yet.
	- Then, Python tries to read `x` in the right had side.
	- Python refers to the `x` in the function scope, but the value is not assigned. 
	- This raises a static semantic error: `UnboundLocalError`


Nested function
```python
def g(x):
	def h():
		x = 'abc'
	x = x + 1
	print("in g(x): x =", x)
	h()
	return x
x = 3
z = g(x)
```
1. Global scope: x -> 3 and z' (unassigned)
2. g(x) where x -> 3
3. g(x -> 3):
	1. h -> h()
	2. declare x'
	3. x + 1 where x -> 3
	4. x -> 4
	5. print("...", 4)
	6. h()
		1. x -> 'abc'
		2. returns None
	7. return x, where x -> 4
4. z -> 4


## Keyword Arguments

Default value and explicit assignement:
```python
# If reverse is not assigned, then reverse points to False
def print_name(first_name, last_name, reverse=False):
	if reverse:
		print(last_name + ', ' + first_name)
	else:
		print(first_name, last_name)

print_name("John", "Doe")
# > John Doe

print_name("Eric", last_name="Grimson")
# > Eric Grimson

print_name(last_name="Nakamoto", first_name="Satoshi", reverse=True)
# > Nakamoto, Satoshi
```
- When using only keyword assignment, order is 

## Specifications

**Specification**: a contract between the implementer of a function and the clients who will use it.
- **Assumptions**: conditions that must be met by clients of the function.
- **Guarantees**: conditions that must be met by function, providing it has been called in manner consistent with assumptions

Example in docstring
```python
def is_even(i):
	"""
	Input: i, a positive int
	Returns True if i is even, otherwise False
	"""
	return i % 2 == 0
```
- It's important to document each code component

## Iteration vs Recursion

Recursion is a good way to design solution to problems by **divide-and-conquer** or **decrease-and-conquer**

Multiplication by addition and iteration:
```python
def mult_iter(a, b):
	result = 0
	while b > 0:
		result += a
		b -= 1
	return result
```

Factorial by recursion:
```python
def fact(n):

	if n == 0 or n == 1: # base case
		return 1

	return n * fact(n-1) # calls itself
```



## Inductive Reasoning

How our recursive code will work?
- Check if the recursion reaches the base case.

**Mathematical induction**:
To prove a statement indexed on integers is true for all values of n:
- Prove it is true when n is the smallest value.
- Assume n satisfies the statement, then prove it for n + 1.

Example
$$
0 + 1 + \ldots + n = \frac{n(n+1)}{2}
$$
For n = 0, it holds.

n = n + 1, then
$$
\frac{(n + 1)(n + 2)}{2}  = \frac{n^{2} + 3n + 2}{2}
$$
$$
 = \frac{n^{2}+n}{2} + n + 1 = 0 + 1 + \ldots + n + n + 1
$$


## Towers of Hanoi

Recursively thinking,  it is very easy problem.
- It is hard to solve using iterations.

Code to show the instructions of the solution:
```python
"""
Move the towers of hanoi from 'fr' stack to 'to' stack.
The stacks:
  |     |      |
[fr] [spare] [to]
"""
def print_move(fr, to):
	print(f"move from {fr} to {to}")

def towers(n, fr, to, spare):
	"""
	fr, to, spare: str, index or name of each stack
	n: int, 
	"""
	if n == 1:
		print_move(fr, to)

	else:
		# Move all other than the biggest to spare
		towers(n-1, fr, spare, to)
		# Move the biggest to 'to' stack
		towers(1, fr, to, spare)
		# Move the smaller part from spare to 'to' 
		towers(n-1, spare, to, fr)	
```


## Fibonacci

Fibonacci numbers:
- Base cases:
	- Fib(0) = 1
	- Fib(1) = 1
- Recursive case:
	- Fib(n) = Fib(n-1) + Fib(n-2)

```python
def fib(x):
	if x == 0 or x == 1:
		return 1
	return fib(x-1) + fib(x-2)
```

## Recursion on non-numerics

How to check if a string of characters is a palindrome; reads the same forwards and backwards.

The algorithm:
- Base case: if the length of a string is 0 or 1, it is palindrome.
- Recursive case: if the first and the last character is the same, and the remaining part is palindrome, then it's palindrome.

```python
def is_palindrome(s):
	if len(s) <= 1:
		return True
		
	return s[0] == s[-1] and is_palindrome(s[1:-1]) 
```

This is an example of "divide-and-conquer" algorithm.


## Files

**Module**: `.py` file that contains a collection of Python definitions and statements.

Example: `circle.py` file
```python
pi = 3.14159
def area(radius):
	return pi*(radius ** 2)
def circumference(radius):
	return 2*radius*pi
```

Another file in the same directory as `circle.py`:
```python
import circle
print(circle.pi)
print(circle.area(3))
print(circle.circumference(3))
```

Import all from a module:
```python
from circle import *
print(pi)
print(area(3))
print(circumference(3))
```

Open a file in a mode:
```python
f = open('file_name', 'w')
f.close() # once opened, it must be closed
```
- Modes:
	- `w`: write
	- `r`: read
	- `a`: append

