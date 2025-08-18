
## 9.1

Answer:
1. `__init__` method is called when an object is created
2. `obj.doSomething()` is a method call of an object
3. An object's attributes can be defined outside the `__init__` method

4:
```python
class Address(object):
    def __init__(self, number, streetName):
		self.number = number
		self.streetName = streetName
```

## 9.2

```python
class Clock(object):
    def __init__(self, time):
		self.time = time
    def print_time(self):
		time = '6:30'
		print(self.time)

clock = Clock('5:30')
clock.print_time()
```
- This code prints `5:30`
	- `time = '6:30'` assigns to a variable in the method's scope, not in the object's scope.

```python
class Clock(object):
    def __init__(self, time):
		self.time = time
    def print_time(self, time):
		print(time)

clock = Clock('5:30')
clock.print_time('10:30')
```
- This code prints `10:30`
- The method fails to use `self` pointer.

```python
class Clock(object):
    def __init__(self, time):
        self.time = time
    def print_time(self):
        print(self.time)

boston_clock = Clock('5:30')
paris_clock = boston_clock
paris_clock.time = '10:30'
boston_clock.print_time()
```
- This code prints `10:30`
- paris_clock and boston_clock point to the same object.

## 9.3

Suppose:
```python
class Weird(object):
    def __init__(self, x, y): 
        self.y = y
        self.x = x
    def getX(self):
        return x 
    def getY(self):
        return y

class Wild(object):
    def __init__(self, x, y): 
        self.y = y
        self.x = x
    def getX(self):
        return self.x 
    def getY(self):
        return self.y

X = 7
Y = 8
```

Type and value inside print():
1. `w1 = Weird(X, Y); print(w1.getX())`: error, NameError
2. `print(w1.getY())`: error, NameError
3. `w2 = Wild(X, Y); print(w2.getX())`: int, 7
4. `print(w2.getY())`: int, 8
5. `w3 = Wild(17, 18); print(w3.getX())`: int, 17
6. `print(w3.getY())`: int, 18
7. `w4 = Wild(X, 18); print(w4.getX())`: int, 7
8. `print(w4.getY())`: int, 18
9. `X = w4.getX() + w3.getX() + w2.getX(); print(X)`: int, 31
	- `X -> 7 + 17 + 7 -> 31`
10. `print(w4.getX())`: int, 7
11. `Y = w4.getY() + w3.getY(); Y = Y + w2.getY(); print(Y)`: int, 44
	- `Y -> 18 + 18 -> 36`
	- `Y -> 36 + 8 -> 44`
12. `print(w2.getY())`: int, 8


## coordinate

```python
class Coordinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def get_x(self):
        # Getter method for a Coordinate object's x coordinate.
        # Getter methods are better practice than just accessing an attribute directly
        return self.x

    def get_y(self):
        # Getter method for a Coordinate object's y coordinate
        return self.y

    def __str__(self):
        return '<' + str(self.getX()) + ',' + str(self.getY()) + '>'

	# 1. return if both refer to the same point
	def __eq__(self, other):
		assert type(self) == type(other)
		return self.get_x() == other.get_x() and self.get_y() == other.get_y()

	# 2. return a representation so that eval(repr(c)) == c
	def __repr__(self):
		return f"Coordinate({self.get_x}, {self.get_y})"
```


## int set

```python
class IntSet(object):
    """An intSet is a set of integers
    The value is represented by a list of ints, self.vals.
    Each int in the set occurs in self.vals exactly once."""

    def __init__(self):
        """Create an empty set of integers"""
        self.vals = []

    def insert(self, e):
        """Assumes e is an integer and inserts e into self""" 
        if not e in self.vals:
            self.vals.append(e)

    def member(self, e):
        """Assumes e is an integer
           Returns True if e is in self, and False otherwise"""
        return e in self.vals

    def remove(self, e):
        """Assumes e is an integer and removes e from self
           Raises ValueError if e is not in self"""
        try:
            self.vals.remove(e)
        except:
            raise ValueError(str(e) + ' not found')

    def __str__(self):
        """Returns a string representation of self"""
        self.vals.sort()
        return '{' + ','.join([str(e) for e in self.vals]) + '}'

	# 1.
	def intersect(self, other):
		new_set = IntSet()
		for e in self.vals:
			if other.member(e):
				new_set.insert(e)
		return new_set

	# 2.
	def __len__(self):
		return len(self.vals)
```


## spell

Suppose:
```python
class Spell(object):
    def __init__(self, incantation, name):
        self.name = name
        self.incantation = incantation

    def __str__(self):
        return self.name + ' ' + self.incantation + '\n' + self.getDescription()
              
    def getDescription(self):
        return 'No description'
    
    def execute(self):
        print(self.incantation)


class Accio(Spell):
    def __init__(self):
        Spell.__init__(self, 'Accio', 'Summoning Charm')

class Confundo(Spell):
    def __init__(self):
        Spell.__init__(self, 'Confundo', 'Confundus Charm')

    def getDescription(self):
        return 'Causes the victim to become confused and befuddled.'

def studySpell(spell):
    print(spell)

spell = Accio()
spell.execute()
studySpell(spell)
studySpell(Confundo())
```

Answers:
1. A parent object is Spell
2. Child classes are Accio and Confundo
3. It prints out:
	1. Accio
	2. Summoning Charm Accio
	3. No Description
	4. Confundus Charm Confundo
	5. Causes the victim to become confused and befuddled.
4. The get_description in the Confundo class is called when studySpell(Confundo()) is called.

5.
```python
class Accio(Spell):
    def __init__(self):
        Spell.__init__(self, 'Accio', 'Summoning Charm')
	def getDescription(self):
		return "This charm summons an object to the caster, potentially over a significant distance."
```

## 9.4

```python
class A(object):
    def __init__(self):
        self.a = 1
    def x(self):
        print("A.x")
    def y(self):
        print("A.y")
    def z(self):
        print("A.z")

class B(A):
    def __init__(self):
        A.__init__(self)
        self.a = 2
        self.b = 3
    def y(self):
        print("B.y")
    def z(self):
        print("B.z")

class C(object):
    def __init__(self):
        self.a = 4
        self.c = 5
    def y(self):
        print("C.y")
    def z(self):
        print("C.z")

class D(C, B):
    def __init__(self):
        C.__init__(self)
        B.__init__(self)
        self.d = 6
    def z(self):
        print("D.z")
```

Then:
```
obj = D()
```

```
obj.a -> 4 -> 1 -> 2
obj.b -> 3
obj.c -> 5
obj.d -> 6
```

Answers:
1. `print(obj.a)`: 2
2. `print(obj.b)`: 3 
3. `print(obj.c)`: 5
4. `print(obj.d)`: 6
5. `obj.x()`: A.x
6. `obj.y()`: C.y
7. `obj.z()`: D.z

## hand

```python
def update(self, word):
        """
        Does not assume that self.hand has all the letters in word.

        Updates the hand: if self.hand does have all the letters to make
        the word, modifies self.hand by using up the letters in the given word.

        Returns True if the word was able to be made with the letter in
        the hand; False otherwise.
        
        word: string
        returns: Boolean (if the word was or was not made)
        """

        temp_hand = self.hand.copy()

        for c in word:
            if c not in temp_hand or temp_hand[c] < 1:
                return False
            else:
                temp_hand[c] -= 1
        
        self.hand = temp_hand
        return True
```

## 10.1

There are two ways to write the `Hand.update` method: you could write this method in a way that gets rid of the key letter in the attribute `hand` dictionary when the frequency of the letter falls to 0, or write it in a way that leaves the key letter in the attribute `hand` dictionary even when the frequency of the letter falls to 0.

Will the two different implementations of the `Hand.update` method lead to `Hand` objects having different `hand` internal attributes?
- My implementation leaves the key. But the "in" operator returns True for the key. 
- So, leaving a key might affect other implementations.
- Removing by `del temp_hand[c]` when it reaches 0 changes the situation.

Does the `calculateLen` method, as defined, return different values for the two different implementations of the `update` method?
- No, because adding 0 does not affect the sum.


## gen_primes

```python
def gen_primes():
	primes = [2, 3]
	yield 2
	while True:
		is_prime = True
		for p in primes[:-1]:
			if primes[-1] % p == 0:
				is_prime = False
		if not is_prime:
			primes.append(primes.pop() + 2)
		else:
			yield primes[-1]
			primes.append(primes[-1] + 2)
```


## 10.2

Thinking about the `genPrimes` generator from the last problem, which of the following can be done only by using a generator, instead of defining a function (that uses any type of construct we've learned about, except generators)?
- Everything that can be done with generator can be done with a function.

Every procedure that has a `yield` statement is a generator.
- True

If a procedure has only one `yield` statement, but that statement will never be executed, then the procedure is not a generator.
- Even though the generator has only one yield statement, the statement can be generator.

If we were to use a generator to iterate over a million numbers, how many numbers do we need to store in memory at once?
- The number of variable needed to create a number sequence is one.

For the following tasks, would it be best to use a generator, a standard function, or either?
1. Finding the nth fibonacci number -> either is fine if the implementation depends on the index n.
2. Printing out an unbounded sequence of Fibonacci numbers. -> a generator keeps unnecessary information if nth number does not contribute to other calculations.
3. Printing out a bounded sequence of prime numbers, where the prime numbers are successively computed by division by smaller primes. -> Both a generator and a function can do the same job.
4. Printing out an unbounded sequence of prime numbers, where the prime numbers are successively computed by division by smaller primes. -> A generator is good at producing unbounded sequences.
5. Finding the score of a word from the 6.00x Word Game of Pset 4. -> The score is calculated based on the rule stored in the dictionary. So, it does not have to be a generator at all.

