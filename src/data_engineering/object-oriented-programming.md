# Object Oriented Programming

- Code as a sequence of steps -> code as interactions of objects
- Object: state + behavior
    - State: attributes
    - Behavior: methods
    - Encapsulation: bundiling attributes with methods that operates on data
- `Everything in Python is an object`
- Classs: blueprint for object outlining states and behaviors
    - self: stand-in for a particular object used in class definition
- Attributes are created by assignment(=) in methods
    - `self.name = 'junu'`
- `__init__`: constructor method is called every time an object is created

## Inheritance

- class attributes: attributes that are shared by all instances of a class
    - use for commonly used values and constants, e.g. `pi` or `min_salary`
- class methods: methods that are shared by all instances of a class
    - main use: alternative constructor, e.g. create instance from file

```python
    @classmethod
    def class_method(cls, args...):
        return

    @classmethod
    def from_file(cls, file):
        with open(file) as f:
            return cls(f.read())
```

- Inheritance: New class functionality + Old class functionality + extra
- `super()`: call parent class method
    - `ParentClass(self).__init__(args)`
    - `super(ParentClass, self).__init__(args...)`

## Integrating with Standard Python

- When an object is created, Python allocates a chunk of memory to that object, and the variable that the object is assigned to actually contains just the reference to the memory chunk
     - call by object reference
- `__eq__()`: is called when 2 objects of a class are compared with `==`
- `__ne__()`: `!=`
- `__lt__()`: `<`
- `__gt__()`: `>`
- `__hash__()`: to use object as dictionary keys and in sets

### Exercise

Which `__eq__()` method will be called when the following code is run?

```python
class Parent:
    def __eq__(self, other):
        print("Parent's __eq__() called")
        return True

class Child(Parent):
    def __eq__(self, other):
        print("Child's __eq__() called")
        return True

p = Parent()
c = Child()

p == c 
>>> Child's __eq__() called
c == p
>>> Child's __eq__() called
```

Why?


### Hash

### Operator overloading

- `__str__()`: for end user
- `__repr__()`: for developers
    - callbacks for `print`

### Exceptions

- Exceptions are classess
- It's better to include an except block for a child exception before the block for a parent exception, otherwise the child exceptions will be always be caught in the parent block, and the except block for the child will never be executed.

## Class Design

### Inheritance and polymorphism

> Liskov substitution principle: Base class should be substitutable for its subclasses without altering the behavior/properties of the subclasses

- Whenever `BankAccount` works, `CheckingAccount` should work too
- Syntactically, function signatures should be the same
    - Same arguments, same return type
- Semantically, the state of the object should be the same
    - Subclass method doesn't strengthen input condition
    - Subclass method doesn't weaken output conditions
    - No additional exceptions

```python
class Parent:
    def talk(self):
        print("Parent talking!")     

class Child(Parent):
    def talk(self):
        print("Child talking!")          

class TalkativeChild(Parent):
    def talk(self):
        print("TalkativeChild talking!")
        Parent.talk(self)  # super().talk()

p, c, tc = Parent(), Child(), TalkativeChild()

for obj in (p, c, tc):
    obj.talk()
```

### Private attributes

- Private attribute starts with a single `_`: internal
- Private attribute starts with two `__`: private
    - Not inherited

### @property

- User-facing: behave like attributes
- Developer-facing: give control of access
- without `@attr.setter`: read-only

```python
class Employer:
    
    def __init__(self, name, salary):
        self._name = name
        self._salary = salary

    @property
    def salary(self):
        return self._salary

    @salary.setter
    def salary(self, new_salary):
        if new_salary < 0:
            raise ValueError("Can't set salary lower than 0")
        self._salary = new_salary
```

### SOLID principles


