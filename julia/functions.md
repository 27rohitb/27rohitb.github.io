# Functions

Key points:

* Scope matters, order does not. Function  written on the bottom can be called by the top part as long as they are in the same scope.
* return last line by default, unless _return_ keyword is used.

___
### Links:

* [Functions Julia Docs](https://docs.julialang.org/en/v1/manual/functions/)
*
   
___
### General Syntax:
```
function <name>(<arguments> ; <keyword args>)
  #
  # function body
  #
  return <var>    #this is OPTIONAL, returns last in by default
end
```

### Calling a function:
```
<function name>(<args>, <keyword>=<arg>)
```
   
___
### Smaller lambda type function:
```
<func_name>(<arguments>) = <function body>
```
   
Example:
```julia
c(r) = 2*pi*r
```

____
### Anonymous function:
```
map(<var> -> <function_body>, <vector to be calculated>)
```

Example:
```julia
map(x -> 2 * pi * r, [1,3,5])
```

___
## Other stuff:

### Type decleration:
Make a filter on the input by explicitly declaring the type.
```julia
function circumference(r::Float64)
```

___
## Arguments:

### Default argument:
```julia
function U(m::real, h=100)
```

### Keyword argument:
```julia
function U(m,h,;g)

#calling it as:
U(1,1,g=1)
```

### Variable argument:
The ```...``` is a variable argument, i.e, it can accept any number of parameters.
```julia
function sum(x, y...)
```
