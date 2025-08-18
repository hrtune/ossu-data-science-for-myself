
## 11.1
Suppose:
```python
def linearSearch(L, x):
    for e in L:
        if e == x:
            return True
    return False
```

Answer:
- Best Case Run Time: `linearSearch([20, ...], 20)`
- Worst Case Run Time: `linearSearch([13, 9, 22, 3, 10, 17, 11, 2, 12], 26)`
	- 26 is not in the list.
- Average Case Run Time: `linearSearch([9, 3, 12, 24, 7, 8, 23, 11, 19], 8)`
	- 8 is in the middle.
- Best case time complexity: $O(1)$
- Worst case time complexity: $O(n)$

## 11.2

Program 1
```python
def program1(x):
    total = 0     # 1 op
	
	# 1000 times iterations
    for i in range(1000): # 1 op
        total += i # 2 op

	# x times loop if x > 0, 1 additional comparison
    while x > 0: # 1 op
        x -= 1  # 2 op
        total += x # 2 op

    return total # 1 op
```

The best case is when `x =< 0`, so:
- Assignment takes `1` operation
- The for loop takes `3 * 1000 = 3000` operations.
- The while loop takes `1` operation.
- The return statement takes `1` operation
- **Total**: `3003` operations.

The worst case is when `x > 0`
- The part other than while loop takes `3002` operations.
- The while loop takes `5*n + 1`  operations.
- **Total**: `5*n + 3003` operations.

Program 2
```python
def program2(x):
    total = 0 # 1 op

	# 1000 times iterations
    for i in range(1000): # 1 op
        total = i # 1 op

	# 1 + log(n) times iterations
    while x > 0: # 1 op
        x = x//2 # 2 op
        total += x # 2 op

    return total # 1 op
```

The best case is when `x =< 0`:
- The for loop take `2 * 1000 = 2000` times operations.
- The other lines takes `3` operations.
- **Total**: `2003` times operations.

The worst case is when `x > 0`:
- The part other than the while loop: `2002` operations.
- The while loop takes `5 * (log(n) + 1) + 1 = 5*log(n) + 6` operations.
- **Total**: `5*log(n) + 2008` operations.

Program 3:
```python
def program3(L):
    totalSum = 0 # 1 op
    highestFound = None # 1 op

    # len(L) times iterations
    for x in L: # 1 op
        totalSum += x # 2 op

	# len(L) times iterations
    for x in L: # 1 op
        if highestFound == None: # 1 op
            highestFound = x # 1 op
        elif x > highestFound: # 1 op
            highestFound = x # 1 op

    return (totalSum, highestFound) # 1 op
```

The best case is when `len(L) is 0`
- `0` iterations for both loops.
- `3` constant operations.
- **Total**: `3` operations.

The worst case is when `len(L)` is `n` and the list is in an increasing order:
- `3` trivial operations.
- `3 * n` operations for the first loop.
- The second loop:
	- `3` operations for the first iteration. (`highestFound == None`)
	- `4 * (n - 1)` operations for the remaining iterations.
		-  Program executes `for ...` line, `if ...` line and `elif..` clause, so `1 + 1 + 2 = 4` operations for each iteration.
	- So, the second loop takes `4*(n-1) + 3 = 4*n - 1` operations.
- **Total**: `3 + 3*n + 4*n - 1 = 7*n + 2` operations.


## 11.3

```python
def program1(L):
    multiples = [] # op 1
	
	# len(L) times loop
    for x in L:
	
		# len(L) times loop
        for y in L:
            multiples.append(x*y) # op 2
			
    return multiples # op 1
```

The best case is when `len(L)` is 0:
- Total: `2` operations

The worst case operations:
- The nested loops cost `n * n * 2 = 2 * n^2` steps.
- Remaining parts cost `2` steps.
- Total: `2*n^2 + 2` steps.

The time complexity of the code is $O(n^{2})$

```python
def program2(L):
    squares = [] # op 1
	
	# len(L) times
    for x in L: 

		# len(L) times
        for y in L:
            if x == y: # op1
                squares.append(x*y) # op2
                
    return squares # op 1
```

The best case is when `len(L)` is 0
- Total: 2 operations

The worst case is when the list has elements with the same value.
- The nested loop costs `n * n * 3 = 3 * n^2`
- Remaining: `2`
- Total: `3*n^2 + 2` steps

The time complexity of the code is: $O(n^{2})$

```python
def program3(L1, L2):
    intersection = [] # op1

	# len(L1) times
    for elt in L1: 
        if elt in L2: # op n
            intersection.append(elt) # op1
    return intersection # op 1
```

The best case is when `len(L1)` is 0:
- Total: 2 steps

The worst case is when `L1 == L2` (Both have the same elements.)
- The for loop costs `n * (n + 2)` steps.
- Remaining: 2 steps.
- Total: `n^2 + 2*n + 2` steps.

The time complexity of the code is: $O(n^{2})$

## 10.4

(1)
A tournament where there are `n` contenders creates games of:
$$
\frac{n}{2} + \frac{n}{4} + \frac{n}{8} + \ldots \frac{2n}{n} + 1
$$
$$
= n(1 - \frac{1}{n})
$$
$$
=n - 1
$$
So, the Big Oh for the number of games in a tournament when n contenders is $O(n)$

(2)
To write $n$ pages of a paper, when each page takes 30 minutes, a research paper is completed in:
$$
30 \cdot n \text{  (min)}
$$
So, the time complexity is $O(n)$

(3)
The amount of time needed to write an essay is:
$$
2 \text{ (hrs)}
$$
So, the time complexity is $O(1)$

(4)
The process to match $n$ pieces is:
```
<loop>
	<picking a random piece>
	<Trying to match pieces>
</loop>
```
- The loop takes $n/2$ iterations. - Picking random piece is 1 operation.

Trying to match pieces takes `(n-1), (n-3), ... , 1` operations for each iteration.
- Average is $n/2$ iteration.

Therefore, the whole process takes:
$$
\frac{n}{2} \cdot \left(1 + \frac{n}{2}\right) = \frac{n}{2} + \frac{n^{2}}{4} \text{ (steps)}
$$
So the time complexity of this process is $O(n^{2})$

## 11.5

For each of the following expressions, select the order of growth class.
- $5n$ -> $O(n)$
- $3n^{2}+2n -100$ -> $O(n^{c})$
- $10\log{n} + 5n$ -> $O(n)$
- $10\log{n} + 5n^{2}$ -> $O(n^{c})$
- $3n^{3} - 2000n^{2}$ -> $O(n^{c})$
- $2n^{3}$ -> $O(n^{c})$
- $50n + n\log{n}$ -> $O(n\log{n})$
- $1000 + 2000000$ -> $O(1)$
- $2^{n} + n^{2}$ -> $O(c^{n})$
- $\log{n} + 1000$ -> $O(\log{n})$

## 11.6

```python
# Assume n has been previously bound to some value
i = 0
while i < 5:
   n *= 2
   i += 1

print(n)
```
- $O(1)$, it loops always 5 times.

```python
def iterPower(a, b):
   result = 1
   while b > 0:
      result *= a
      b -= 1
   return result
```
- $O(b)$

```python
def recurPower(a, b):
   print(a, b)
   if b == 0:
      return 1
   else:
      return a * recurPower(a, b-1)
```
- $O(b)$

```python
def recurPowerNew(a, b):
   print(a, b)
   if b == 0:
      return 1
   elif b%2 == 0:
      return recurPowerNew(a*a, b/2)
   else:
      return a * recurPowerNew(a, b-1)
```
- $O(\log{b})$

## 11.7


```python
def lenRecur(s):
   if s == '':
      return 0
   else:
      return 1 + lenRecur(s[1:])
```
- `O(len(s)^2)` since:
	- `s[1:]` is takes `O(len(s))` as slicing string copies the portion of of the original string, which takes `len(s-1)` times.

```python
def isIn(a, s):
   '''
   a is a character, or, singleton string.
   s is a string, sorted in alphabetical order.
   '''
   if len(s) == 0:
      return False
   elif len(s) == 1:
      return a == s
   else:
      test = s[len(s)//2]
      if test == a:
         return True
      elif a < test:
         return isIn(a, s[:len(s)//2])
      else:
         return isIn(a, s[len(s)//2+1:])
```
- `O(log(len(s))` because it utilizes binary search.

```python
def union(L1, L2):
   '''
   L1 & L2 are lists of the same length, n
   '''
   temp = L1[:] # O(n)
   for e2 in L2:
      flag = False
      for check in temp:
         if e2 == check:
            flag = True
            break
      if not flag:
         temp.append(e2)
   return temp
```
-  $O(n^{2})$ time complexity (nested loop)

```python
def unionNew(L1, L2):
   '''
   L1 & L2 are lists of the same length, n
   '''
   temp = []
   for e1 in L1:
      flag = False
      for e2 in L2:
         if e1 == e2:
            flag = True
            break
      if not flag:
         temp.append(e1)
   return temp + L2
```
- $O(n^2)$ time complexity

## 11.8
Time complexities, in ascending order.

1. $500,000$
2. $\log{(\log{n})}$ 
3. $\log{n}$
4. $n$
5. $n\log{n}$
6. $n^{2}$
7. $n^3$
8. $3^{n}$
9. $n^{n}$
10. $2^{n^{2}}$ 

## 12.1

Suppose:
```
a = [1, 2, 3, 4, 0]
b = [3, 0, 2, 4, 1]
c = [3, 2, 4, 1, 5]
```

Values of:
1. `a[0]`: 1
2. `b[1]`: 0
3. `a[a[1]]`: 3
4. `b[b[2]]`: 2
5. `a[b[2]]`: 3
6. `c[a[b[3]]]`: 3
7. `a[c[a[b[0]]]]`: IndexError
8. `a[c[a[b[3]]]]`: 4

```python
def foo(L):
    val = L[0]
    while (True):
        val = L[val]
```
- `foo(a)` and `foo(b)` leads to an infinite loop 
- `foo(c)` leads to IndexError

```python
num = ???
L = [5, 0, 2, 4, 6, 3, 1]
val = 0
for i in range(0, num):
    val = L[L[val]]

print(val)
```

Printed number:
- `num=0`: 0
- `num=1`: 3 <- answer

```python
num = ???
L = [2, 0, 1, 5, 3, 4]
val = 0
for i in range(0, num):
    val = L[L[val]]

print(val)
```

Printed number:
- `num=0`: 0
- `num=1`: 1
- `num=2`: 2
- `num=3`: 0
- ... (impossible to print 3)

## 12.2

Suppose:
```python
"""
L is sorted list in ascending order
	, of positive integers
"""
def search(L, e):
    for i in range(len(L)):
        if L[i] == e:
            return True
        if L[i] > e:
            return False
    return False


def search1(L, e):
    for i in L:
        if i == e:
            return True
        if i > e:
            return False
    return False
```

Correct statement: `search` and `search1` return the same answers.
- Since they are doing the same thing in each line.

## 12.3

Suppose:
```python
"""
L: list, integers in ascending order
"""
def search(L, e):
    for i in range(len(L)):
        if L[i] == e:
            return True
        if L[i] > e:
            return False
    return False

def search2(L, e):
    for i in L:
        if i == e:
            return True
        elif i > e:
            return False
    return False
```

Correct statement: `search` and `search2` return the same answers.
- Since they are doing the same thing in each line.

## 12.4

```python
"""
L: list, integers in increasing order
"""
def search(L, e):
    for i in range(len(L)):
        if L[i] == e:
            return True
        if L[i] > e:
            return False
    return False

def search3(L, e):
    if L[0] == e:
        return True
    elif L[0] > e:
        return False
    else:
        return search3(L[1:], e)
```

Correct statement: `search` and `search3` return the same answers provided L is non-empty and e is in L.
- If e is not in L and `L[-1] < e`, `search3` produces IndexError


## 12.5
Suppose:
```python
# selection sort
def selSort(L): 
    for i in range(len(L) - 1):
        minIndx = i
        minVal = L[i]
        j = i+1
        while j < len(L):
            if minVal > L[j]:
                minIndx = j
                minVal = L[j]
            j += 1
        if minIndx != i:
            temp = L[i]
            L[i] = L[minIndx]
            L[minIndx] = temp

# selection sort
def newSort(L):
    for i in range(len(L) - 1):
        j=i+1
        while j < len(L):
            if L[i] > L[j]:
                temp = L[i]
                L[i] = L[j]
                L[j] = temp
            j += 1
```

Answers:
1. Both results are the same sorted list.
2. `newSort` uses more assignments (or swap) of the list's elements
3. The worst case time complexity is the same $O(n^{2})$

## 12.6

```python

# Bubble sort
def mySort(L):
    """ L, list with unique elements """
    clear = False
    while not clear:
        clear = True
        for j in range(1, len(L)):
            if L[j-1] > L[j]:
                clear = False
                temp = L[j]
                L[j] = L[j-1]
                L[j-1] = temp


# Selection Sort
def newSort(L):
    """ L, list with unique elements """
    for i in range(len(L) - 1):
        j=i+1
        while j < len(L):
            if L[i] > L[j]:
                temp = L[i]
                L[i] = L[j]
                L[j] = temp
            j += 1
```

Answers:
1. Both algorithms creates the same sorted list, as both are valid sorting algorithms.
2. They use the same amount of assignments.
3. The worst case complexity of both algorithms is the same $O(n^{2})$
4. `mySort` and `newSort` examine different numbers of entries.


