# Other additional libraries

___
## QuadGK library ( Integration of function ):
For different integration methods.

#### Simpson's method:
```julia
quadgk(f, a, b, rtol=1e-5)

"""
f = main function (slope)
a = start limit
b = end limit
rtol = err limit
"""
```

___
## DifferentialEquations ( Solving ODEs ):
For solving ODEs.

#### Solving 1 ODE:
```julia
# u = y, t = time span, p = params
df(u,p,t) = <write the equation>

# define bounds (start point, end point)
tspan = (0, 2)

# Create ODEproblem obj, u0 = init condition
prob_obj = ODEProblem(df, u0, tspan)

# solve ODE
sol3 = solve(prob)
```

#### Solving system of ODEs:
start by defining 1 function that contain system of ODEs:
```julia
"""
  du = output solutions
  u = input (x) independent param
  p = params
  t = time
"""
function df(du, u, p, t)
  du[1] = <enter equation here>
  du[2] = <enter eq1 here>
end
```

Now define initial params, and time to solve, and solve it similar to above:
```julia
u0 = [0,0] #its dimensions have CHANGED
tspan = (0, 1.0)
prob = ODEProblem(df, u0, tspan)
sol = solve(prob)
```

#### PLotting solution:
Since for couples equation we have 2 system's solution, and t on 3rd axis, we can select waht to plot, though _by default_ plot obj will plot correctly.

```julia
plot(sol, vars=[1,2])
# 1=x, 2=y ....
```
