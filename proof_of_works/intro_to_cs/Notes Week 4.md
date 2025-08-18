
## Programming Challenges

High quality programming:
- Testing: checking if the code works as intended
- Defensive programming: by which prevent bugs to occur
- Debugging: eliminate bugs by careful inspection


Defensive programming:
- Write **specifications** for functions
- **Modularize** programs
- Check conditions on inputs/outputs(assertions)

Testing:
- Compare input/output pairs to the specification

Debugging:
- Study events leading up to errors

## Classes of Tests

Code design for tests:
- Break a program into modules, that can be tested individually
- Document constraints on modules
	- Input and output
- Document assumptions behind code design

Preparations:
- Ensure code runs in some way
	- Remove syntax and static semantic errors
- Have a set of expected results.
	- A input set and expected output for each


Classes of tests:
- Unit testing: validate each piece of program
- Regression testing: add test for bugs as you find them in a function
- Integration testing: check if the overall program runs

Testing approaches:
- Intuition
- Random testing: randomly generate test cases
- Black box testing: explore path through specification
- Glass box testing: explore path through code

Black box testing: designed without looking at the code implementations
- Some one other than the implementer can perform it
	- ...avoiding some implementer biases
- testing can be reused even if the implementation changes
- paths through specification

Test cases example:
```python
def sqrt(x, eps):
	"""Assumes x and eps are floats, x >= 0, eps > 0
```

| case                   | x    | eps             |
| ---------------------- | ---- | --------------- |
| boundary               | 0    | 0.0001          |
| Perfect square         | 25   | 0.0001          |
| Less than 1            | 0.05 | 0.0001          |
| Irrational square root | 2    | 0.0001          |
| extremes               | 2    | 1.0/2.0 ** 64.0 |
| ...                    |      |                 |

Glass box testing: use code directly to guide design of test cases
- **Path-complete** if every potential path through code is tested at least once

Path complete test example:
```python
def abs(x):
	"""Assumes x is int, returns x if x >= 0, otherwise -x"""
	if x < -1:
		return -x
	else
		return x
```
- Path-complete test checks program goes through every path
	- 2 goes to the else block, and -2 goes to the if block. So, ***it is path-complete***.
- However, `abs(-1)` does not follow the specification




## Bugs

Once test is performed:
- Isolate bugs
- Eradicate bugs
- Retest until code runs correctly

Episode on September 9, 1947:
- Mark II Aiken Relay Computer
- Admiral Grace Murray Hopper: found errors on some calculations
	- She found a moth (bug) that was causing the error

![[Pasted image 20250811192631.png]]


Runtime bugs:
- **Overt**: has an obvious manifestation
	- code crashes or runs forever
- **Covert**: has no obvious manifestation
	- code returns incorrect value internally
	- can be dangerous
- Persistent vs intermittent:
	- **Persistent**: occurs every time code is run
		- Easier to fix
	- **Intermittent**: only occurs some times
		- Difficult to fix


## Debugging

Debugging requires experience.

Adding print statements.
- To see values in a variable

Error message:
- IndexError
- TypeError
- NameError
- TypeError
- SyntaxError

Logic errors:
- Hard to find out

Debugging steps:
- Study the code
	- Ask **how** did I get the unexpected result.
- Scientific method:
	- Study available data
	- Form hypothesis
	- Repeatable experiments
	- Pick simplest input to test

Test and debug repeatedly.


## Exceptions

Types of python exceptions:
- IndexError: when try to access outside the range of indices.
- TypeError: when unexpected type is processed
- NameError: referencing a non-existing variable
- SyntaxError: python can't parse program
- AttributeError: attribute reference fails (`int.foo`, no such attribute)
- ValueError: operand type okay, but value is illegal
- IOError: IO system reports malfunction.

Raise an exception:
```python
raise Exception("some message here")
```

Dealing with exceptions using try-except block:
```python
try:
	a = int(input("Tell me one number: "))
	b = int(input("Tell me one number: "))
	print(a/b)
	print("Okay")
except
	print("Bug in user input")

print("Outside")
```
- `try` block sees if an exception occurs
- `except` block is executed if an exception occurs

try-except-else-finally block:
```python
print("--------")
try:
	a = int(input("Tell me a numerator number: "))
	b = int(input("Tell me a denominator number: "))
	print("Okay")
except ZeroDivisionError:
	print("A denominator must be other than 0!!")
else:
	print("The result is:", a/b)
finally:
	print("Thank you !")
print("-------")
```
- `except SomeError` catches only a specific error
- `else` block is executed if the error does not occur at all
- `finally` block runs regardless of whether an exception occurs or not


## Exceptions Examples

```python
while True:
	try:
		n = input("Please enter an integer")
		n = int(n)
		break
	except: ValueError
		print("Input not an integer; try again")

print("Input is indeed an integer!")
```


Control input:
```python
data = []
file_name = input("Provide a name of a file: ")
try:
	fh = open(file_name, 'r')
except IOError:
	print("cannot open", file_name)
else:
	for new in fh:
		if new != '\n':
			addIt = new[:-1].split(',')
			data.append(addIt)
finally:
	fh.close()
```


## Exceptions as Control Flow

Raising an exception
```python
def get_ratios(L1, L2):
	"""Assumes: L1 and L2 are lists of equal length of numbers
		Returns: a list containing L1[i]/L2[i] """
	ratios = []

	for i in range(len(L1)):
		try:
			ratios.append(L1[i] / L2[i])
		except ZeroDivisionError:
			ratios.append(float('nan'))
		except:
			raise ValueError("get_ratios called with bad arg")

	return ratios
			
```

## Assertions

```python
def avg(grades):
	assert not len(grades) == 0, 'no grades data'
	return sum(grades)/len(grades)
```

Syntax:
```
assert <condition>, "some error message"
```
- If `<condition>` is True, it raises `AssertionError`

Assertions...
- ensure that execution halts whenever the code fails to meet the condition
- typically used to check inputs
- can be used to check output of a function






