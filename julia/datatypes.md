# Datatypes

## Arrays

Array is the most general purpose container similar to list in python. 1D arrays is vector, 2D array is matrix. Everything else about array is [here](./array.md).

___
## Tuple

**Note:**

* Immutable; CAN't be modified.
    
```julia
t = (1,2,3)

# access
t[1] 
```
___
## Name Tuple 

```julia
nt = (a=1, b=2, c="hello")

# access
nt[1]
nt.a    # access using keys
```

___
## Dictionary

```julia
dik = Dict('a' => 1, 'b'=>2)
```

**Note:**

* Dictionary **CAN** be altered.
