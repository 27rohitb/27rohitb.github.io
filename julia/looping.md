# Different Functions for looping:
    
### Range:

#### STEP-Range:
```julia
<var name> = range(<start>, <stop>, length=<number of points between start and stop>)
r = range(1, 20, length=10)
```
    
#### UNIT-Range:
```julia
<var name> = <start>:<step size>:<stop>
r = 1:2:20
```

### List comprehension:
```julia
l1 = [x for x in <start>:<stop>]

