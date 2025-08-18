
## 1
Assume `s` is a string of lower case characters.
Write a program that counts up the number of vowels contained in the string `s`. Valid vowels are: '`a`', '`e`', '`i`', '`o`', and '`u`'. For example, if `s = 'azcbobobegghakl'`, your program should print:

```
Number of vowels: 5
```

```python
def num_vowels(s):
	num = 0
	for c in s:
		if c in 'aeiou':
			num += 1
	print(f"Number of vowels: {num}")
```

## 2
Assume `s` is a string of lower case characters.

Write a program that prints the number of times the string `'bob'` occurs in `s`. For example, if `s = 'azcbobobegghakl'`, then your program should print

`Number of times bob occurs is: 2`

```python
def num_bob(s):
	message = "Number of times bob occurs is:"
	if len(s) < 3:
		print(message, '0')
		return
		
	num = 0
	for i in range(len(s) - 2):
		if s[i] == 'b' and s[i + 1] == 'o' and s[i + 2] == 'b':
			num += 1
			i += 1

	print(message, num)
```


## 3

Assume `s` is a string of lower case characters.

Write a program that prints the longest substring of `s` in which the letters occur in alphabetical order. For example, if `s = 'azcbobobegghakl'`, then your program should print

```python
def longest_substring(s):
	message = 'Longest substring in alphabetical order is:'
	
	if len(s) < 2:
		print(message, s)
		return

	start = 0
	end = 1
	result = ''
	for i in range(len(s) - 1):
		if ord(s[i]) <= ord(s[i + 1]):
			end += 1
		else:
			if end - start > len(result):
				result = s[start:end]
			start = i + 1
			end = i + 2

	if (end - start > len(result)):
		result = s[start:end]

	print(message, result)
		
```


