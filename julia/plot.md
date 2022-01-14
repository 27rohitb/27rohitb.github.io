# Plotting

#### Links:

* Very nice tut by Purdue here ```https://www.math.purdue.edu/~allen450/Plotting-Tutorial.html```

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
plot(x,y, label="linear", legend=:topleft, xaxis="x", yaxis=("y", :log), dpi=200)

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

### Add anotation:
Anotation = text on the graph:
```julia
anotate!(x, y, Plots.text("This will appear at x,y", 5, :red) )
```

#### Save plot:
```julia
savefig("<filename>.<extension>")
```

### Scatter plot:
```julia
scatter(x, y, yerr=yerr, markersize=2, markershape=:o, alpha0.5, label="data")
```

___
# Subplots:

*  Make plot objects.
*  Pass these all at once into plot command, with ```layout``` kwarg.

Example:
```julia
# Make a plot and modify it to add another plot on the same.
p1 = scatter(x,y)
p1 = plot!(x2,y2)

# Make another plot and modify it as well:
p2 = scatter(x3,y3)
p2 = plot!(x4, y4)

# PLOT THEM ALL
plot(p1, p2, layout=(2,1), dpi=200)
```
   
___
# Pylot from Julia

Much faster !!!!

#### using package:
```julia
using PyPLot
```

#### plot command:
```
julia
plot(x,y, color="red", linewidth=2.0, linestyle="--")
```

#### Add title:
```julia
title("A sin wave")
```
