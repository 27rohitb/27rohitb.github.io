# Concepts
This module contains definitions of concepts required for decoratos.

## First class citizens:
An entity that supports all general operations, including being passed as an argument, being return from a function and being assigned to a variable.

## First class functions:
A programming language has these if it treats its functions as first class citizens.

## Example for pasing function as an argument:
**Note that no brackets are used, that shows that the function is being "assigned" to the variable (something like a pointer for function)**
```
some_var = some_function_name
```

## Higher-Order Function:
A function that accepts / returns an function as args/return value.

Example of returning function as a value:
```
def outer_func(some_arg):
	
	def inner_func():
	//Do_something with "some_arg"
	//TODO ,notice hoew returned function does NOT have brackets
    return someother_func
``` 

## Closure:
The ability of inner function to access vars inside of outer function , which could be outside the inner fucntion's scope normally.
