# Matrices and Linear Algebra Related stuff:

Following libraries are used:
* LinearAlgebra
* Plots

## Vector functions

#### Norm:
```julia
norm(x)
```

#### Normalize vector:
```julia
normalize(x)
```

#### Dot product:
```julia
dot(x,y)
```

#### Cross product:
```julia
cross(x,y)
```

___
## Multiplication Operations:

#### Multiplication:
```julia
A * B
```

#### Trace, Determinant, Transponse, Inverse:
```julia
tr(A)
det(A)
transpose(A)
inv(A)
```

#### Eigen values & vectors:
```julia
eigvals(A)
eigvecs(A)
```

#### Factorize (LU):
```julia
factorize(A)
```

___
## Special Matrices
These optimization can process things faster.

#### Diagonal:
```julia
D= Diagonal(n) # given n X n dim diagonal matrix with 1
```

## Solve linear system Ax = b:
```julia
# For eg:
A = [1 2; 1 -1]
b = [5, -1]

# check this before going ahead
A = factorize(A)

# Simple answer: 
x0 = A \ b
```
