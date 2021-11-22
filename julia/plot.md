# Plotting

**NOTE:** 

* ```Plots``` package required!.
* It is very slow (like 20 seconds) for **first** time, since it compiles plots.jl. This is why we use pyplot!
   
#### Import plots:
```julia
using Plots  #import package
```

#### Specify backend:
```julia
gr()  #faster backend
```

#### Plot command:
```julia
plot(x,y, label="linear", legend=:topleft)

# FOR MUTIPLE PLOT:
plot!(x2, y2, dpi=200)
```

#### Insert axis:
```julia
xaxis!("x [-]")
yaxis!("f(x) [-]")
```

#### Add title:
```julia
title!("polynomial")
```

#### Save plot:
```julia
savefig("<filename>.<extension>")
```

___
# Pylot from Julia

Much faster !!!!

