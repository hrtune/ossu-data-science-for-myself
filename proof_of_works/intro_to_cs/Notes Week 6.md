
## Program Efficiency

How to evaluate efficiency of programs?
- Measure a **timer**.
- **Count** operations
- Abstract notion of **order of growth**.

Timing a program:
```python
import time

def c_to_f(c):
	return c * 9/5 + 32

t0 = time.time()
c_to_f(100000)
t1 = time.time() - t0
print(t1)
```
- `time.time()` returns the current time since the Epoch.

To evaluate an algorithm, rather than an implementation, the measure should:
- depend on algorithm
- not depend on implementations
- be independent of hardware specifications
- not rely on actual operations

Using running time is not favorable because it varies among implementations.

Constant time operations:
- Mathematical operations
- Comparisons
- Assignments
- Accessing objects in memory

```python
def c_to_f(c):
	return c * 9/5 + 32 # 3 ops
```

```python
def mysum(x):
	total = 0 # 1 op
	# x times loops
	for i in range(1, x+1): # 1 op
		total += i # 2 op
	return total
```
- $3x + 1$ operations.


Example:
```python
def search_for_element(L, e): # L: list, e: element
	for i in L:
		if i == e:
			return True
	return False
```
- Best case: `e` is the first element of `L`
- Worst case: `e` is not in `L`
- Average case: `e` is in the middle of `L`

## Big Oh Notation

Big Oh measures an upper bound on the asymptotic growth, often called order of growth.
- Big Oh is used to describe the worst case scenario.

Forming Big Oh:
- Focus on dominant terms

Examples:
- $n^{2} + 2n + 2$ -> $O(n^{2})$
- $n^{2} + 100000n + 3^{10000}$ -> $O(n^{2})$
- $\log{n} + n + 4$ -> $O(n)
- $0.00001 \cdot n \cdot \log{n} + 300n$ -> $O(n \log{n})$
- $2 \cdot n^{30} + 3^{n}$ -> $O(2^{n})$

Types of orders of growth:
- Constant: $O(1)$
- Linear: $O(n)$
- Quadratic: $O(n^{2})$
- Logarithmic: $O(\log{n})$
- $O(n \log{n})$
- Exponential: $O(2^{n})$

**Law of Addition** for $O()$
$$
O(f(n)) + O(g(n)) = O(f(n)+g(n))
$$
Example:
```python
for i in range(n):
	print('a')
for j in range(n*n):
	print('B')
```
is $O(n) + O(n^{2}) = O(n^{2})$ (takes dominant term)

**Law of Multiplication** for $O()$
$$
O(f(n)) \cdot O(g(n)) = O(f(n) \cdot g(n))
$$


## Analyzing Complexity

Quadratic complexity: when it has nested loops.

```python
def is_subset(L1, L2):
	for e1 in L1:
		matched = False
		for e2 in L2:
			if e1 == e2:
				matched = True
				break
		if not matched:
			return False
	return True

# Time complexity: O(n^2) where n is the size of a list.
```


## More Analyzing Complexity

Exponential complexity: when a recursive function creates multiple recursive calls.
```python
def gen_subsets(L):
	res = []
	if len(L) == 0:
		return [[]]
	smaller = gen_subsets(L[:-1])
	extra = L[-1:]
	new = []
	for small in smaller:
		new.append(small+extra)
	return smaller + new

# Time complexity: O(2^n) where n is the size of the list
```

## Tricky Complexity

```python
def h(n):
	"""assume n as int >= 0"""
	answer = 0
	s = str(n)
	for c in s:
		answer += int(c)
	return answer
```

$O(\log{n})$ time complexity because $n$ is divided by $10$ each iteration.


```python
def fib_recur(n):
	"""assumes n an int >= 0"""
	if n == 0:
		return 0
	elif n == 1
		return 1
	else:
		return fib_recur(n-1) + fib_recur(n-2)
			
```

$O(2^{n})$ time complexity because each recursive statement doubles the call stack.

Time complexities of list and dictionary operations
- List:
	- $O(1)$: `access, store, len(list), append()`
	- $O(n)$: `remove, copy, reverse, iteration, in list`
- Dict:
	- Average $O(1)$: `access, store, delete`
	- Average $O(n)$: `iteration`



## Search Algorithms

Linear search: brute force search.
- Suitable for unsorted list
- $O(n)$

Bisection search: for sorted list
- $O(\log{n})$

## Bogo Sort
A.k.a monkey sort, stupid sort, slowsort, permutation sort, shotgun sort.

```python
import random

def bogo_sort(L):
	while not is_sorted(L):
		random.shuffle(L)
```
- Best case: $O(n)$, to check if sorted
- Worst case: unbounded.

## Bubble Sort
1. Iterate through all elements.
2. Compare adjacent elements and swap if not in order.
3. Repeat until no swap is occur.

```python
def bubble_sort(L):
	swap = False
	while not swap:
		swap = True
		for j in range(1, len(L))
			if L[j-1] > L[j]:
				swap = False
				temp = L[j]
				L[j] = L[j-1]
				L[j-1] = temp
```
- Best case: $O(n)$
- Worst case: $O(n^{2})$


## Selection Sort

1. Search the minimum value in the unsorted part. (initially all is unsorted)
2. Swap with the first element of unsorted part.
3. Repeat until unsorted part depletes.

```python
def selection_sort(L):
	unsorted_first = 0
	while unsorted_first != len(L):
		for i in range(unsorted_first, len(L)):
			if L[i] < L[unsorted_first]:
				L[unsorted_first], L[i] = L[i], L[unsorted_first]
```

- $O(n^{2})$ for best and worst cases.

## Merge Sort

Merge sort uses a divide-and-conquer approach.
1. If the size of the list is 0 or 1, it is sorted.
2. If the list is more than one element, split into two lists, and apply merge sort to both.
3. Merge the both sorted lists by which:
	1. Iterate through both sorted lists at the same time one by one.
	2. Arrange smaller value iteratively.

```
# DIVIDE
[2, 6, 3, 4, 1, 5]
[2, 6, 3] [4, 1, 5]
[2] [6, 3] [4] [1, 5]
	 [6] [3]   [1] [5]

# MERGE
	 [6] [3]   [1] [5]
	 [3, 6]     [1, 5]
[2] [3, 6] [4] [1, 5]
[2, 3, 6] [1, 4, 5]
[1, 2, 3, 4, 5, 6]
```

Implementation
```python
def merge_sort(L):
	if len(L) < 2:
		return L[:]
	else:
		middle = len(L) // 2
		left = merge_sort(L[:middle])
		right = merge_sort(L[middle:])
		return merge(left, right)
```

Time complexity:
1. For each level, merge takes $O(n)$ steps.
2. There are $O(\log{n})$ levels created by dividing lists.
3. So, the time complexity is $O(n\log{n})$

## 12.7

Application A: only does linear search
Application B: mergeSort -> binary search

Answers:
1. Worst case of A for one search: $O(n)$
2. Worst case of B for one search: $O(n\log{n})$
3. Worst case of A for k-times search: $O(kn)$
4. Worst case of B for k-times search: $O((n + k)\log{n})$
5. When $k = 1$ A is superior.
6. When $k = \log{n}$, A and B have same performance.
7. For $n^{3}$ requests, I would choose Application B. ( $n^{4}$ vs $n^{3}\log{n}$)

