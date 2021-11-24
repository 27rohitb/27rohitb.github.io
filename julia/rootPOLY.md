# Other Stuff 2

We have used 2 libraries here:
* Polynomials
* Plots

## Creating polynomials

#### Generating by coefficients:
```julia
# [] in the below function is x^(n)'s coeffs for n=0 ... N
p = Polynomial( [1,3,5] )
```

#### Generating by roots:
```julia
#
q = fromroots( [1,-4,4] )
```

#### Evaluating polynomials created using above method:
```julia
p(x) # evaluate for x
```

**NOTE:** Basic maths operation work _without_ ".":
```julia
p + q # works
2*p - q # workds
```

___
## Derivative & Integrals:

```julia
derivative(p)
integrate(p)
```

___
## Root finding

```julia
root(q) # find root of poly_type var
```
