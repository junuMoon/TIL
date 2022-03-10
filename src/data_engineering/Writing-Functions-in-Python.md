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

## Context Manager
```python
with <context-manager>(<args>):
	# Run code "inside the context"

# This code runs after the context is removed.
```

### Function based context manager
```python
@contextlib.contextmanager
def my_context():
	# Setup
	yield
	# Teardown
```

- yield: return value and finish the rest of the function at some future
- context manager function is technically a generator that yields a single value
- allows hiding things like connecting database
- Nested contexts(with)
- Handling errors: use `try`, `except` and `finally` so that regardless of any error, rest of code will be ran.

### Context manager pattern	
- Open/Close
- Lock/Release
- Change/Reset
- Enter/Exit
- Start/Stop
- Setup/Teardown
- Connect/Disconnect

## Decorators
- Functions as object
	- Functions are just another type of object
	- So you can pass a function as an argument to another function
- Nested Function
- Scope: Builtin ⊃ Global ⊃ Nonlocal ⊃ Local
- Closure
	- python’s way of attaching nonlocal variables to a returned function
	- so the function can operate even when it’s called outside of its parent’s scope
	- `func.__closure__[0].cell_contents`
	- Albeit x doesn’t exist anymore, the value persists in its closure
- Decorator: A wrapper that you can place around a function that changes that function’s behavior

```python
def mul(a, b): return a * b

def double_args(func):
	def wrapper(a, b):
		return func(a * 2, b * 2)
	return wrapper

new_mul = double_args(mul)

@double_args
def mul(a, b): return a * b

```

### Decorator factory
- A function that returns a decorator, that is not a decorator itself

```python

def run_n_times(n):
	"""Define and return a decorator"""
	def decorator(func):
		def wrapper(*args, **kwags):
			for i in range(n):
				func(*args, **kwargs)
		return wrapper
	return decorator

@run_n_times(3)
def print_sum(a, b):
	print(a+b)

run_three_times = run_n_times(3)

@run_three_times
def print_sum(a, b):
	print(a+b)
```
