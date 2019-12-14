**REMEMBER: putting brackets will EXECUTE the function.**

# Decorators
It is a function that takes in some_func as an argument, adds some functionality to it and returns it, all this, WITHOUT making any change to the original source of the some_func.

## Simplest form:
```
Definition:

def decorator_func(some_func):
	def wrapper_function():
        #TODO something with some_func
        return some_func(*args, **kwargs )
    return wrapper_func

Usage:
decorated_some_func = decorator_func(some_func)
```

## Complicated form:
This will automatically decorate some_func
```
@decorator_func
def  some_func(some_params):
	#TODO
```

_Note:_
* *args -> lets us pass any number of arguments.
* **kwargas -> lets us pass any number of keyword arguments.

## Classes as decorators
```
class dec_class(object):
	
	def __init__(self, some_func):
		self.some_func = some_func
		//to initalize function
	
	def __call__(self, *args, **kwargs):
		//code of wrapper_function goes here
        return self.some_func(*args , **kwargs)
```

## Multiple Decorators
Multiple decorators can be used , by stacking them up on a single function,but **using multiple decorators at once can have unintended consequence**, hence use:
```
from functools import wraps

@warps(some_func)
before every wrapper_func for all decorators
```

## DECORATORS WITH ARGS
Arguments can be passed to decorator, but this requires another level of sopohstication.

```
def prefix_dec(some_var):
	def actual_dec(some_func):
		def wrapper_func(*args, **kwargs):
			#TODO
		    return some_func()
	    return wrapper_func
    return actual_dec
```

Usage example:
```
@actual_dec(some_var)
def some_func:
	#TODO
```
