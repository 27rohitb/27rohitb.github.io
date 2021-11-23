# Struct

Collection of values. **Immutable**.

### Genral declaration syntax:
```
struct <name>
  <var1>
  <var2>
  <varN>
  
  #empty constructor
  function <struct_name>()
      new(1,1,1) #assigns 1, 1, 1 to above
  end
  
  # accepts args, and does condition check
  function <struct_name>(<varX>,<varY>,...<varZ>)
      #do condition check
      error("wahtever")
      #now create and assign 
      new(<varX>,<varY>,....<varZ>)
  end
end
```

**Default constructor** will initialize the variable when creating the object as follows:

```julia
p = Prism(2,3,4)
```

This automatically assigns values inorder to ```<var1>, <var2> ... <varN>```.
   
### Accessing vars inside:
```
<struct obj>.<varN_name>
```

___
## Mutable Struct

CAN make the constructor OUTSIDE of struct:

```julia
mutable struct Circle
  r
end

function Circle_const(r::Real)
  Circle(r)
end
  
