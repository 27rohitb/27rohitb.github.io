
# Array
Can hold objects of _different_ types.

**NOTE**: 
* _Empty_ arrays are of type _Any_   
* USE ```display``` instead of ```println```

### Display properly:
```julia
display(<array/matrix>)
```

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

### MULIT-Dimensional Access!:
```
# FOR MULTI-DIMENSIONAL
arr[r,c] # YES, r,c, though IN memory, its column majors!!!!!!
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

___
## Pre-allocating array   
Use the bottom ones and the edit these. _Its faster_
   
### Create array of zeros:
```julia
zeros(2,2)
```

### Create array of ones:
```julia
ones(2,2)
```
   
