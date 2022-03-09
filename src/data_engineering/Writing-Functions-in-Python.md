# Writing Functions in Python

## Best Practices
### Docstirng
	- function
	- args
	- return value
	- errors raised
	- notes or usage
- Styles: Google style, Numpydoc

```
# Numpy doc
"""
Description of what the function does.

Parameters
----------
Args:
	arg_1 : expected type of arg_1
		Description of arg_1
	arg_2 : int, optional
		Write optional when an argument has a default value
		Default=42
	
Returns
-------
The type of the return value
	Can include a description of the return value
	Replace "Returns" with "Yields" if this function is a generator
```

### Refactoring
	- Don’t Repeat Yourself
	- Do One Thing: split functions
	- Advantages: flexible code, easy to test/debug

### Pass by assignment
- immutable: int, float, bool, string, bytes, tuple, frozenset, None

> There are only a few immutable data types in Python. Because almost everything is represented as an object. The only way to tell if something is mutable is to see if there is a function or method that will change the object without assigning it to a new variable.

```
>>> a = 'string'
>>> b = a
>>> a
'string'
>>> b
'string'
>>> a[0] = 'e'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```