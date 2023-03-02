What does `if __name__ == '__main__'` do?

A Python **module** is a file containing Python definitions and statements.  When a module is imported, `__name__` is set to the module name:

```py
>>> import os
>>> os.__name__
'os'
```

If the module is executed in the top-level code environment, then `__name__` is set to `__main__`.   The top-level code (aka *entry point*) is the first user-specified Python module to run.

Consider a file `helloworld.py`:

```py
def greet():
	print("hello")

if __name__ == '__main__':
	greet()
```

The `helloworld` module is executed in the top-level environment when:

1. It is passed to the Python interpreter as a file:
	```sh
	$ python helloworld.py
	hello
	```
1. It is passed to the Python interpreter with `-m` argument:
	```sh
	$ python -m helloworld
	hello
	```
In the wild, `if __name__ == '__main__'` can be found in a module that is intended to be run as a script.  When such a module is imported from another module (say to unit test it), the script code won't accidentally run.

For example, a unit test for `helloworld` would look like:

```py
from helloworld import greet

def test_greet():
	...
	greet()
	...
```