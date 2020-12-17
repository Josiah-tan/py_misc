# ez_life
The objective of ez_life is to make coding with Python easier by removing repetitive code while still maintaining the same level of functionality

# param2attr
- Here is a little sneak peak of what you can do with this package!
	- First consider this code block:

```python
from ez_life import Param2attr

class Foo:
	def __init__(self, param1 = None, param2 = None, param3 = None):
		# This sux
			self.param1 = param1
			self.param2 = param2
			self.param3 = param3
```

- We can instead create a class that looks like this, using a property decorator to perform the param to attribute assignments 

```python
class Foo:
	@Param2attr(exclude=None) 
	def __init__(self, param1 = None, param2 = None, param3 = None): 
		# this good, allows u to write other code here during initialization 
		pass
```

- If you are interested to learn about the implementation or other features that param2attr supports, feel free to read the [documentation](https://colab.research.google.com/github/Josiah-tan/ez_life/blob/main/ez_life/param2attr.ipynb)

# JTProperty
- Ez_life can also manage variable dependencies, building upon the @property decorator!

- First here's some code with the classic @property decorator:

```python
class SetAndGet:
  def __init__(self, r = 1):
    # initialise the protected variable
    self._radius = None

    # calls the @radius.setter method
    self.radius = r
  @property
  def radius(self):
    if self._radius is None:
      self.radius = 2
    return self._radius
  @radius.setter
  def radius(self, r):
    if r <= 0:
      raise ValueError("radius should be greater than 0")
    self._radius = r
```
- Using the @JTProperty decorator, we can see that we can abstract away the self._radius variable and hence write less code!

```python
class JTSetAndGet:
  def __init__(self, r = 1):
    self.radius = r
  @JTProperty(setter = True)
  def radius(self):
    return 2

  @radius.setter
  def radius(self, r):
    if r <= 0:
      raise ValueError("radius should be greater than 0")
    return r
```

- JTProperty also supports a variety of other features including:
	- Automatic setter creation
	- Graph Dependencies
		- Support for inheritence
- Read the [documentation](https://colab.research.google.com/github/Josiah-tan/ez_life/blob/main/ez_life/jt_property.ipynb) here to learn about these features!


# ez_life directory layout:

- ez_life: the package containing all .ipynb dev files and converted .py files
	- param2attr.ipynb: dev notebook for automation of parameter creation to class object attributes
	- param2attr.py: param2attr.ipynb -> param2attr.py via Makefile
	- jt_property.ipynb: dev notebook for more writing dependency related code
	- jt_property.py: jt_property.ipynb -> jt_property.py via Makefile
- .gitignore: for ignoring files when pushing and pulling
- LICENSE: what u can and can't do with this repo
- MAKEFILE: automated test cases and .ipynb to .py conversion
- README: this file essentially
- test*.py: test files for modules within ez_life

