# Fitting

Using 2 built-in libraries:
* ```Polynomials``` ( Polynomial fitting )
* ```Lsqfit``` ( Least Sqaures fit )

___
### Polynomial fit:
```
fitted_data_var = fit( <xdata>, <ydata>, <n-th degree poly to be fit>  )
```

___
### Generic curve fit:
```julia
# model(x,y,z) = <function you are trying to fit>
# first args (x,y) are indpendent var.
# last are dependent vars.

model(t,p) = p[1] * exp.(-p[2] * t)

# p0; guess somewhere to start
p0 = [0.5, 0.5]

nfit_obj = curve_fit(model, xdata, ydata, p0)
```
