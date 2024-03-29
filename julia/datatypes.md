# Datatypes

## Pre-defined datatypes:

### Arrays
Array is the most general purpose container similar to list in python. 1D arrays is vector, 2D array is matrix. Everything else about array is [here](./array.md).

### Tuple
**Note:** Immutable; CAN't be modified.   
```julia
t = (1,2,3)

# access
t[1] 
```

### Name Tuple 
```julia
nt = (a=1, b=2, c="hello")

# access
nt[1]
nt.a    # access using keys
```

### Dictionary
```julia
dik = Dict('a' => 1, 'b'=>2)
```

**Note:**

* Dictionary **CAN** be altered.

### Constants:
Some constants that dont exist or we know better : P
```julia
const pie=3.1415
```

___
## User defined:

### Struct:
Everything about struct is [here](./struct.md)

### Abstract type ( Parametric ):
Its basically an alternative to Abstract classes *BUT* it is for **structs**. Its also an example of **parametric**, since its not a parameter to the function, _but_ it can allow the user to define the datatype on the fly. **Similar to templates in C++**.

Example:
```julia
abstract type Shape{T} end

struct Rectangle{T1, T2} <: Shape{T1}
    len::T1
    wid:T2
end
```
  
Usage Example:
```julia
r = Rectangle{Float64, Float64}(5.0,4.0)
```
