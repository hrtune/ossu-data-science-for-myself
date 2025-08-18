
## Object Oriented Programming

Every object has:
- Type
- Internal data representation
- Methods

Advantages of OOP:
- Bundling data into packages together with procedures
- Divide-and-conquer development
- Classes make it easy to reuse code
	- Inheritances

## Class Instances

Define class:
```python
class SomeClass:
	# attributes and methods
```
- `class SomeClass:` is equivalent to `class SomeClass(object):` in Python 3

Constructor:
```python
def __init__(self, x, y):
	self.x = x
	self.y = y
```

## Methods

```python
class Coordinate:
	def __init__(self, x, y):
		# ...
	def distance(self, other):
		x_diff_sq = (self.x - other.x) ** 2
		x_diff_sq = (self.y - other.y) ** 2
		return (x_diff_sq + y_diff_sq) ** 0.5
```

Representations of object:
- `__repr__` defines representation of object like `<Coordinate: (-1, 2)>`
	- Accessed by `repr(obj)`
- `__str__` defines user-friendly representations like `(-1, 2)`
	- Used by `str(obj)`, `print(obj)`, and so on.

## Classes Examples

Fraction class:
```python
class Fraction:
	def __init__(self, numer, denom):
		self.numer = numer
		self.denom = denom

	def __str__(self):
		return f"{self.numer} / {self.denom}"

	# getters
	def get_numer(self):
		return self.numer
	def get_denom(self):
		return self.denom

	def __add__(self, other):
		numer_new = other.get_denom() * self.get_numer() + self.get_denom() * other.get_numer()
		denom_new = other.get_denom() * self.get_denom
		return Fraction(numer_new, denom_new)

	def __sub__(self, other):
		# ...
```


## Why OOP

Characteristics:
- **Class is the type**.
- A class defines data and methods common across all instances.

Attributes:
- Data attributes: how can you represent your object with data
- Procedural attributes: what kinds of things can you do with the object?

## Hierarchies

Class hierarchies:
- Parent class (superclass)
- Child class (subclass)
	- Inherits all attributes and methods of its parent class

Inheritance:
```python
class SomeClass(SomeParentClass):
	def __init__(self):
		super().__init__()
		self.data = []
```
- `super()` is used to call method of the parent class

## Class Variables

Instance variables: variables that belong to an instance
Class variables: belong to the class, shared among all its instances

```python
class Rabbit(Animal):
	tag = 1 # class variable

	def __init__(self, ...):
		super().__init__(age)
		# ...
		self.rid = Rabbit.tag
		Rabbit.tag += 1 # incremented every time a Rabbit object is created.
		
```

## Building a Class

A class organizing info about people:
```python
import datetime

class Person:
	def __init__(self, name):
		self.name = name
		self.birthday = None
		self.last_name = name.split(' ')[-1]

	def get_last_name(self):
		return self.last_name

	def set_birthday(self, month, day, year):
		self.birthday = datetime.date(year,month,day)

	def get_age(self):
		if self.birthday == None:
			raise ValueError
		return (datetime.date.today() - self.birthday).days

	def __lt__(self, other):
		if self.last_name == other.last_name:
			return self.name < other.name
		return self.last_name < other.last_name

	def __str__(self):
		return self.name
```


Child class of Person:
```python
class MITPerson(Person):
	next_id_num = 0

	def __init__(self, name):
		super().__init__(name)
		self.id_num = MITPerson.next_id_num
		MITPerson.next_id_num += 1


	def __lt__(self, other):
		return self.id_num < other.id_num

	def get_id_num(self):
		return self.id_num
		
```

Case study:
```
p1 = MITPerson('Eric')
p2 = MITPerson('John')
p3 = MITPerson('John')
p4 = Person('John')
```


```
p1 < p2 # True
p1 < p4 # AttributeError!
p4 < p1 # False
```

- `p1 < p2` is equivalent to `p1.__lt__(p2)`
- So, `p4.__lt__(p1)` is valid and returns `False`


## Adding another class

Undergraduate people
```python
class UG(MITPerson):
	MITPerson.__init__(self, name)
	self.year = class_year

	def get_class(self):
		return self.year
	def speak(self, uttername):
		return MITPerson.speak(self, "Dude, " + utterance)

class Grad(MITPerson):
	pass

def isStudent():
	return isinstance(obj, UG) or isinstance(obj, Grad)
```
- `isinstance(obj, class)` checks if the object is an instance of the class.

## Using Inherited Methods

```python
class Professor(MITPerson):
	...
	def speak(self, utterrance):
		new = f"In course {self.department} we say "
		return super().speak(new+utterance)
```

The syntax:
```
super().method_name(arg1, arg2, ...)
```


## Gradebook Example

```python
class Grades:
	def __init__(self):
		self.students = []
		self.grades = {}
		self.is_sorted = True

	def add_student(self, student):
		if student in self.students:
			raise ValueError("...")

		self.students.append(student)
		self.grades[student.get_id_num()] = []
		self.is_sorted = False


	def add_grade(self, student, grade):
		try:
			self.grades[student.get_id_num()].append(grade)
		except KeyError:
			raise ValueError("...")

	def get_grades(self, student):
		try:
			# give a copy not to be mutated
			return self.grades[student.get_id_num][:]
		except KeyError:
			# ...

	def all_students(self):
		if not self.is_sorted:
			self.students.sort()
			self.is_sorted = True
		return self.students[:]


def grade_report(course):
	""" type(course) -> Grade"""
	report = []
	for s in course.all_students()
		tot = 0.0
		num_grades = 0
		for g in course.get_grades(s)
			# ...
	# ...

	return '\n'.join(report)

```
- all_students() includes a sorting process. The best practice is to use a getter method rather than a direct access to the attribute so that the method can be modified later without affecting other code.
- Inefficiency: to get the grades of all students, it creates a copy.


## Generators

Any procedure with `yield` statement is called a generator

```python
def gen():
	yield 1 # first next call returns this
	yield 2 # second next call returns this

type(gen()) # -> generator
```
- A generator object has `__next__()` method.
- `next(generator)` returns the next value of the generator

Example:
```python
def gen_fib():
	fib1 = 1
	fib2 = 0
	while True:
		next = fib1 + fib2
		yield next
		fib2 = fib1
		fib1 = next
```

Generator is iterable
```python
for n in gen():
	print(n)
```

Why generators:
- A generator executes processes and produces results as needed.
	- Lazy implementation.
		- Memory efficient rather than holding entire sequence.


