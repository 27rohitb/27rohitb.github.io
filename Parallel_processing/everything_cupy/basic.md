# SciPy 2019 - Cupy (by Masayuki Takagi)

It is developed and maintained by Preffered Networks- an AI startup in Japan.
      
## Drop-in replacement with Numpy   

Example: (comments are the lines that can be replaced)
```python

# import cupy as cp
import numpy as np

# x = cp.random.rand(10)
x = np.random.rand(10)

# W = cp.random.rand(10, 5)
W = np.random.rand(10, 5)

# y = cp.dot(x, W)
y = np.dot(x, W)
```

## Supported libraries and function within cupy:
   
* Almost all of the routines and modules of numpy.
* Some of SciPy lib functions are supported such as FFt, Linear Algebra, Interpolation,
 Spare matrix operations and special fucntions like gamma, zeta, erfc ertc.
* All nvidia libs cuDNN , cuBLAS, etc, are accesible through Cupy.

   
## Getting started with CuPy:   
   
### Installation
```
# cuda10.2 ...or whatever the latest version is
pip install cupy-cuda102

# Non usual binary
pip install cupy
```

* Its also available on google collab
   
### Advanced Features:

* Raw kernel from CUDA C in python
* Fusing, combine multiple kernels into one call
* Memery pool (Mem management)
