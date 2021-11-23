# Functions

Key points:

* Scope matters, order does not. Function  written on the bottom can be called by the top part as long as they are in the same scope.
* return last line by default, unless _return_ keyword is used.

### General Syntax:
```
function <name>(<arguments>)
  #
  # function body
  #
  return <var>    #this is OPTIONAL, returns last in by default
end
```

### Smaller lambda type function:
```
<func_name>(<arguments>) = <function body>
```
   
Example:
```julia
c(r) = 2*pi*r
```

### Anonymous function:
```
map(<var> -> <function_body>, <vector to be calculated>)
```

Example:
```julia
map(x -> 2 * pi * r, [1,3,5])
```
