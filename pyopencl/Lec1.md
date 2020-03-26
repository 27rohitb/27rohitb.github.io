# Lecture 1:
   
Importing and initiazlizing pyCUDA:   

```python
import pycuda.drive as cuda
import pycuda.autoinit
```
   
Import Cuda Compiler:   
```python
from pycuda.compiler import SouceModule
```
   
Some data, say numpy array:
```python
# Create a numpy array of float32
a = np.random.rand(16)
a = a.astype(np.float32)
```

Memory allocation on GPU:   
```python
a_gpu = cuda.mem_alloc(a.nbytes)
```
   
Copy data to GPU (htod: Host To Device):   
```python
# Copy direction is from LEFT to RIGHT
cuda.memcpy_htod(a_gpu, a)
```
   
Write C++ kernel that would be executed on GPU:   
```python
module = SouceModule("""
   __global__ void double_array(float *a){
      int idx = blockIdx.x * blockDim.x + threadIdx.x;
      a[idx] *= 2;
      }
   """)
```   

Here:   
* ```__global__``` means kernel will launch from the cpu and run onto GPU.   
* ```void``` return type.   
* ```double_array``` is the name.   
* ```float *a``` is the pointer for a (memory address).   

Underlying concept:   

* each thread does some computation in a kernel.
* A given computation is bascially mapped onto a grid.
* A grid is an arrangment of threads.
* A thread is divided into thread blocks.
