
## Problem 1

1-1
We are also interested in the design of code besides the correctness.

1-2
When determining asymptotic complexity, the term with the largest growth rate only counts.

1-3
Bisection search is an example of logarithmic time complexity.

1-4
An algorithm with `20000n^2` steps is better than an algorithm with `0.001n^5` steps

## Problem 2

2-1
Indirection means accessing value indirectly rather than directly.

2-2
The time complexity of a binary search algorithm is $O(\log{n})$

2-3
The worst case time complexity of selection sort is $O(n^2)$

2-4
The base case for the recursive version of merge sort may count when the list is either empty or 1, regarding them as sorted.

## Problem 3

Expression -> Big Oh notation
- $0.0000001n + 1000000$ -> $O(n)$
- $0.00001n^{2} + 20000n - 9000$ -> $O(n^{c})$
- $20n + 900 \log{n} + 100000$ -> $O(n)$
- $(\log(n))^{2} + 5n^{7}$ -> $O(n^{c})$
- $n^{200} - 2n^{30}$ -> $O(n^{c})$
- $30n^{2} + n\log{n}$ -> $O(n^{c})$
- $n\log{n} - 3000n$ -> $O(n\log{n})$
- $3$ -> $O(1)$
- $5^{n} + n^{5} + n + 5$ -> $O(c^{n})$
- $n\log{n} + n^{2} + n + \log{n} + 1 + 2^{n}$ -> $O(c^{n})$

## Problem 4

4-1
Suppose:
```python
def modten(n):
    return n%10
```

The order of growth of `midten` is $O(1)$.

4-2
```python
def multlist(m, n):
    '''
    m is the multiplication factor
    n is a list.
    '''
    result = []
    for i in range(len(n)):
        result.append(m*n[i])
    return result
```

The order of growth of `multilist` is `O(len(n))`

4-3

```python
def foo(n):
    if n <= 1:
        return 1
    return foo(n/2) + 1
```

The order of growth of `foo` is $O(\log{n})$

4-4

```python
def recur(n):
    if n <= 0:
        return 1
    else:
        return n*recur(n-1)
```

The order of growth of `recur` is $O(n)$


4-5

```python
def baz(n):
    for i in range(n):
        for j in range(n):
            print( i,j )
```

The order of growth of `baz` is $O(n^2)$

## Problem 5

```python
"""
Suppose L is a list of positive integers in an increasing order.
"""
def search(L, e):
    for i in range(len(L)):
        if L[i] == e:
            return True
        if L[i] > e:
            return False
    return False
 
    
def newsearch(L, e):
    size = len(L)
    for i in range(size):
        if L[size-i-1] == e:
            return True
        if L[i] < e:   # L[size-i-1] < e makes sense
            return False
    return False
```

`search` and `newsearch` return the same answers for lists `L` of length 0, 1, or 2.
- When `len(L)` is 0, both functions return `False`
- When `len(L)` is 1, both functions consider the only element in a same way.
- When `len(L)` is 2:
	- `search` performs a standard linear search.
	- `newsearch` considers:
		- If e is in the last element, `if L[size-i-1]:` block returns True.
		- If e is in the first element, `if L[0] < e` does not return False. Then, the next iteration checks the first element.
		- If e is not in the list, it returns False.


## Problem 6

```python

# SELECTION SORT
def swapSort(L): 
    """ L is a list on integers """
    print("Original L: ", L)
    for i in range(len(L)):
        for j in range(i+1, len(L)):
            if L[j] < L[i]:
                # the next line is a short 
                # form for swap L[i] and L[j]
                L[j], L[i] = L[i], L[j] 
                print(L)
    print("Final L: ", L)
```

6-1
`swapSort` sorts a list in an increasing order.

6-2
The worst case time complexity of `swapSort` is $O(n^{2})$ (because it is selection sort)

6-3
```python
def modSwapSort(L): 
    """ L is a list on integers """
    print("Original L: ", L)
    for i in range(len(L)):
        for j in range(len(L)):
            if L[j] < L[i]:
                # the next line is a short 
                # form for swap L[i] and L[j]
                L[j], L[i] = L[i], L[j] 
                print(L)
    print("Final L: ", L)
```

`modSwapSort` now orders the list in descending order for all lists.
- The inner loop finds the smallest value and stores in `L[i]`
- Each outer loop iteration ensures `L[:i]` is always in descending order.
- After the last iteration of the outer loop, `L[:len(L)] == L`, becomes in a descending order.

Assumption: `L[:i]` is in descending order before each iteration for `i > 0`
The base case: `i=1`, then `L[:1]` has only one element.
Suppose the assumption is true for `i=k`, then `L[:k]` is in descending order. Then `L[k]` is compared with values in `L[:k]`.
Each comparison:
- `L[k]` holds smaller value than `L[j]` after the comparison.
- In the next iteration of the inner loop,:
	- When a swap occurs, then the `L[j]` has smaller value than `L[j-1]`, keeping the descending order.
	- When a swap does not occur, still `L[:k]` is in a descending order.
	- After the last comparison between `L[k-1]` and `L[k]`, `L[:k+1]` is in the descending order.
So, `L[:k+1]` keeps the descending order after comparisons. By mathematical induction, the assumption holds.


6-4
The best and worst cases of `modSwapSort` are $O(n^{2})$, this is the same as the selection sort's $O(n^{2})$


