
## Exercises 1

1: What is the difference between an Algorithm and a Program?
- Answer: An algorithm is a conceptual idea, a program is a concrete instantiation of an algorithm. (An algorithm does not depend on specific implementations. A program is the implementation of an algorithm.)

2: True or False? A computational mode of thinking means that everything can be viewed as a math problem involving numbers and formulas.
- Answer: False (even though the answer says true.)
- **Computational thinking** is a problem-solving process that involves breaking down a problem and formulating a solution in a way that a computer could execute.
- So, it does not limited to numbers and formulas. For example, imperative knowledge written in English can lead to a computer program.
- C.f. *BBC BITESIZE* https://www.bbc.co.uk/bitesize/guides/zp92mp3/revision/1

3: True or False? Computer Science is the study of how to build efficient machines that run programs.
- Answer: False
- It includes the study of mathematics, algorithms, and programming.

4: The two things every computer can do are...
- Answer: to perform calculations and remember the results.
- Turing machine has a calculator and memory.


## Exercises 2

(True or false)

1: Declarative knowledge refers to statements of fact.
- Answer: True

2: Imperative knowledge refers to 'how-to' methods.
- Answer: True

3: A recipe for deducing the square root involves guessing a starting value for y. Without another recipe to be told how to pick a starting number, the computer cannot generate one on its own.
- Answer: True
- A computer needs every specific instruction to calculate the result.

## Exercises 3

1: True or False? A stored program computer is designed to compute precisely one computation, such as a square root, or the trajectory of a missile.
- Answer: False

2: True or False? A fixed program computer is designed to run any computation, by interpreting a sequence of program instructions that are read into it.
- Answer: False

3: A program counter...
- Answer: points the computer to the next instruction to execute in the program.

4: What does it mean when we say that "the computer walks through the sequence executing some computation"?
- Answer: The computer executes the instructions mostly in a linear sequence, except sometimes it jumps to a different place in the sequence.

5: True or False? In order to compute everything that is computable, every computer must be able to handle the sixteen most primitive operations.
- Answer: False
- Alan Turing proved that all problems can be computed with only 6 primitives.

## Exercise 4

Choose definitions:
1. Determines whether a string is legal
	- Answer: syntax.
	- Syntax defines the legal format of a string
2. Determines whether a string has meaning
	- Answer: static semantics
	- A string does not have static semantics, which means the string cannot be comprehended by a reader even though it follows the syntax.
3. Assigns a meaning to a legal sentence
	- Answer: semantics

## Exercise 5

Indicate type:
- `3.14`: float
- `-34`: int
- `True`: bool
- `None`: NoneType
- `3.0`: float

## Exercise 6

Compute Python expressions:
- `6 + 12 - 3` == 15
- `2 * 3.0` == 6.0
- `- - 4`: 4
	- Python does not have increment or decrement operators as C does.
- `10 / 3` ~ 3.3333
- `10.0 / 3.0` ~ 3.3333
- `(2 + 3) * 4` == 20
- `2 + 3 * 4` == 14
- `2 ** 3 + 1` == 9
- `2.1 ** 2.0` == (2.0 + 0.1) ** 2.0 == 4.0 + 0.4 + 0.01 == 4.41
- `2.2 * 3.0` == 6.6


## Exercise 7


1. `5.0`
2. `4.0`
3. error

## Exercise 8

Evaluate:
- `3 > 4` -> False
- `4.0 > 3.99` -> True
- `4 > 4` -> False
- `4 > + 4` -> False
- `2 + 2 == 4` -> True
- `True or False` -> True
- `False or False` -> False
- `not False` -> True
- `3.0 - 1.0 != 5.0 - 3.0` -> False
- `3 > 4 or (2 < 3 and 9 > 10)` -> False
- `4 > 5 or 3 < 4 and 9 > 8` -> True
- `not(4 > 3 and 100 > 6)` -> False

## Exercise 9

Evaluate (Python REPL):
```
>> a = 3
>> a == 5.0
>> a
3 -- (1)
>> b = 10
>> c = b > 9
>> c
True -- (2)
```

## Exercise 10

Indicate type and result:
```
>> 3 + 5.0
float, 8.0

>> 5/2
float, 2.5

>> 5/2 == 5/2.0
bool, True

>> 5/2.0
float, 2.5

>> round(2.6)
int, 3

>> int(2.6)
int, 2

>> 2.0 + 5.0
float, 7.0

>> 5*2 == 5.0 * 2.0
bool, True
```
- `round()`: rounds a number to the nearest integer.


## Exercise 2.1

- `"a" + "bc"` -> "abc"
- `3 * "bc"` -> "bcbcbc"
- `"3" * "bc"` -> TypeError
- `"abcd"[2]` -> "c"
- `"abcd"[0:2]` -> "ab"
- `"abcd"[:2]` -> "ab"
- `"abcd"[2:]` -> "cd"


## 2.2

```python
str1 = 'hello'
str2 = ','
str3 = 'world'
```

Indicate type and value
```
>> str1
str, 'hello'

>> str1[0]
str, 'h'

>> str1[1]
str, 'e'

>> str1[-1]
str, 'o'

>> len(str1)
int, 5
```

```
>> str1[len(str1)]
type, IndexError

>> str1 + str2 + str3
str, "hello,world"

>> str1 + str2 + ' ' + str3
str, "hello, world"

>> str3 * 3
str, "worldworldworld"

>> 'hello' == str1
bool, True
```

```
>> 'HELLO' == str1
bool, False

>> 'a' in str3
bool, False

>> str4 = str1 + str3 # str4: "helloworld"
>> 'low' in str4
bool, True

>> str3[1:3] # str3: "world"
str, "or"

>> str3[:3]
str, "wor"
```

```
>> str3[:-1]
str, "worl"

>> str1[1:]
str, "ello"

>> str4[1:9]
str, "elloworl"

>> str4[1:9:2]
str, "elwr"

>> str4[::-1]
str, "dlrowolleh"
```
- Substring with a step always includes the first letter indicated, then the step is applied.

## 2.3

Evaluate:

```
if 6 > 7:
	print("Yep")
> (nothing)

if 6 > 7:
   print("Yep")
else:
   print("Nope")
> Nope

var = 'Panda'
if var == "panda":
   print("Cute!")
elif var == "Panda":
   print("Regal!")
else:
   print("Ugly...")
> Regal!

temp = 120
if temp > 85:
   print("Hot")
elif temp > 100:
   print("REALLY HOT!")
elif temp > 60:
   print("Comfortable") 
else:
   print("Cold")
> Hot

temp = 50
if temp > 85:
   print("Hot")
elif temp > 100:
   print("REALLY HOT!")
elif temp > 60:
   print("Comfortable")
else:
   print("Cold")
> Cold
```


## happy

Write a piece of Python code that prints out the string '`hello world`' if the value of an integer variable, `happy`, is strictly greater than 2.

```python
def happy_f(happy):
	if happy > 2:
		print("hello world")
```


## vara varb

Assume that two variables, `varA` and `varB`, are assigned values, either numbers or strings.

Write a piece of Python code that evaluates `varA` and `varB`, and then prints out one of the following messages:
- `"string involved"` if either `varA` or `varB` are strings
- `"bigger"` if `varA` is larger than `varB`
- `"equal"` if `varA` is equal to `varB`
- `"smaller"` if `varA` is smaller than `varB`

```python
def f(varA, varB):
	if type(varA) is str or type(varB) is str:
		print("string involved")
	elif varA > varB:
		print("bigger")
	elif varA == varB:
		print("equal")
	else:
		print("smaller")
```

## 2.4

Indicate what will be printed out

```python
num = 0
while num <= 5:
    print(num)
    num += 1

print("Outside of loop")
print(num)

# 0 1 2 3 4 5 Outside of loop 6
```


```python
numberOfLoops = 0
numberOfApples = 2
while numberOfLoops < 10: # numberOfLoops: 0 to - infinity
    numberOfApples *= 2 
    numberOfApples += numberOfLoops
    numberOfLoops -= 1
print("Number of apples: " + str(numberOfApples))
# (infinite loop)
```

```python
num = 10
while num > 3: # num: 10 to 4
    num -= 1
    print(num)

# 9 8 7 6 5 4 3
```

```python
num = 10
while True: # num: 10, 9, 8, 7, 6
    if num < 7:
        print('Breaking out of loop')
        break
    print(num)
    num -= 1
print('Outside of loop')

# 10 9 8 7 Breaking out of loop Outside of loop
```

```python
num = 100
while not False: # num: stays 100
    if num < 0:
        break
print('num is: ' + str(num))

# (infinite loop)
```

## while

```python
n = 2
while n <= 10:
	print(n)
	n += 2
print("Goodbye!")
```

```python
print("Hello!")
n = 10
while n >= 2:
	print(n)
	n -= 2
```

```python
def f(end):
	"""
	end: positive integer
	"""
	s = 0
	while end > 0:
		s += end
		end -= 1
	print(s)
```

## for

```python
for n in range(2, 11, 2):
	print(n)
print("Goodbye!")
```

```python
print("Hello!")
for n in range(10, 1, -2):
	print(n)
```

```python
def f(end):
	s = 0
	for n in range(end, 0, -1):
		s += n
	print(s)
```


## 2.5

Indicate what is printed out

```python
num = 10
for num in range(5):
    print(num)
print(num)

# 0 1 2 3 4 4
```

```python
divisor = 2
for num in range(0, 10, 2): # num: 0, 2, 4, 6, 8
    print(num/divisor)

# 0.0 1.0 2.0 3.0 4.0
```

```python
for variable in range(20): # 0 to 19
    if variable % 4 == 0:
        print(variable)
    if variable % 16 == 0:
        print('Foo!')
# 0 Foo! 4 8 12 16 Foo!
```

```python
for letter in 'hola':
    print(letter)
# h o l a
```

```python
count = 0
for letter in 'Snow!': # count: only 0
    print('Letter # ' + str(count) + ' is ' + str(letter))
    count += 1
    break
print(count)

# Letter # 0 is S
# 1
```

## 2.6

```python
myStr = '6.00x'

for char in myStr:
    print(char)

print('done')
```
- '6' is printed out once
- '.' is printed out once
- '0' is printed out twice
- 'x' is printed out once
- 'done' is printed out once


```python
greeting = 'Hello!'
count = 0

for letter in greeting:
    count += 1
    if count % 2 == 0:
        print(letter)
    print(letter)

print('done')

# H e e l l l o ! ! done
```
- 'H' prints out once
- 'e' prints out twice
- 'l' prints out three times
- 'o' prints out once
- '!' prints out twice
- 'done' prints out once

```python
school = 'Massachusetts Institute of Technology'
numVowels = 0
numCons = 0

for char in school:
    if char == 'a' or char == 'e' or char == 'i' \
       or char == 'o' or char == 'u':
        numVowels += 1
    elif char == 'o' or char == 'M':
        print(char)
    else:
        numCons -= 1

print('numVowels is: ' + str(numVowels))
print('numCons is: ' + str(numCons))

# M
# numVowels is: 11
# numCons is: -25
```
- 'o' does not print out except for the last two lines
- 'M' prints out once
- 'numVowels' == 11
- 'numCons' == -25

## 2.7

Original code
```python
iteration = 0
count = 0
while iteration < 5: # iteration: 0, 1, 2, 3, 4
    for letter in "hello, world":
        count += 1 # count: len("hello, world") -> 12, 24, 36, 48, 60
    print("Iteration " + str(iteration) + "; count is: " + str(count))
    iteration += 1
```


| Variable                     |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | --- | --- |
| iteration (before increment) | 0   | 1   | 2   | 3   | 4   |
| count (after each for loop)  | 12  | 24  | 36  | 48  | 60  |
^ Variables `iteration` and `count` when the print statement is called

Change the code to the one where a while loop is nested inside a for loop.

Test 1:
```python
for iteration in range(5):
    count = 0
    while True:
        for letter in "hello, world":
            count += 1
        print("Iteration " + str(iteration) + "; count is: " + str(count))
```
- This code is not equivalent to the original code as the while loop is an infinite loop.

Test 2:
```python
for iteration in range(5):
    count = 0
    while True:
        for letter in "hello, world":
            count += 1
        print("Iteration " + str(iteration) + "; count is: " + str(count))
        break
```
- This code is not equivalent to the original code as `count` variable is initialized at the first statement of each iteration.
	- `count` always prints out as `12`

Test 3
```python
count = 0
phrase = "hello, world"
for iteration in range(5):
    index = 0
    while index < len(phrase):
        count += 1
        index += 1
    print("Iteration " + str(iteration) + "; count is: " + str(count))a
```
- Test 3 is equivalent to the original code

Test 4
```python
count = 0
phrase = "hello, world"
for iteration in range(5):
    while True:
        count += len(phrase)
        break
    print("Iteration " + str(iteration) + "; count is: " + str(count))
```
- Test 4 has the same output as the original

Test 5
```python
count = 0
phrase = "hello, world"
for iteration in range(5):
    count += len(phrase)
    print("Iteration " + str(iteration) + "; count is: " + str(count))
```
- Test 5 has the same output as the original

