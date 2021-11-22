# Basics

### Datatypes:
   
Quick 4:   
* ```Int/Float/Real/Complex 8/32/64```
* Same as above but **"Big"** with _Arbitrary Precision_
* ```String``` **is different** than ```Char```

### NOTE:

* There are **NO** ":" like python
* Every block (function/if-else/etc) **MUST** have and ```end``` keyword
* **!** after a function, means that fucntions is editing the given variable
* Array are stored in **Column major** aka *fortran style* format; accessing them is same, each row of given column is displayed first.
* Array _index start_ **at 1**

#### determine type
```julia
typeof()
```
   
### String functions:
Essentially its a **container** of chars.

#### Concatenate any number of strings
```julia
a * b
```
   
### if-else
```julia
if (x > 0) && (y > 0)
   println("x AND Y is positive")
elseif (x < 0) || (y <0)
   println("x OR y is NEG")
else
   println("x is NOT positive")
end
```
   
* **SHORTCIRCUITING** : If multiple if-else statements are true, it will just execute the first one and _exit the block_.
   
### Ternary Operator:
```
x <conditional operation> ? <TRUE clause> : <FALSE clause>
x > 0 ? println("is POS") : println("not positive")
```

### Array
Can hold objects of _different_ types.

**NOTE**: _Empty_ arrays are of type _Any_   

### Creating Empty Array of ANY type:
```julia
emty_arr = []
```
   
### Add ONE element to EMPTY array
```julia
push!(empty_arr, 1)
push!(empty_arr, "hello") #possible because of type "ANY"
```

### Concatenate Array(/containers)
```julia
append!(arr, arr2)
```

### Update element:
```julia
arr[1] = 67
```

### Create a SPECIFIC type array:
```julia
<var name> = Array{<Type>}(undef, <lowest dimension>)
x = Array{Int64}(undef, 1) #creates a 1 dimension, 1 element Int64 array
```

**NOTE:**: 

* ```undef``` is undefined is shortcut to ```undefInitializer()``` which creates array whoes memory has NOT been allocated yet.
*  DO NOT use _Float64/nn_. The first element WONT be exact zero. **Use** ```AbstractFloat```.
*  It can upgrade ```INT``` to float for a float type array.
*  A ```Real``` type can contain both ```Float``` AND ```INT```.
*  A ```Numbers`` type can take everything in ```Real``` And ```Complex```.

### Create array of zeros:
```julia
zeros(2,2)
```

### Create array of ones:
```julia
ones(2,2)
```
