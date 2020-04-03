# Lecture 1(PyCUDA crash course):
   
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
* A grid is divided into blocks: described are ```blockIdx.x```.
* A block has some specific number of theads, whoes index is described as ```threadIdx.x```.
* Total number of threads per block is the dimension of the block, described as ```blockDim.x```.
* The global location of thread is calculated and denoted by ```int idx```.   
* The final computation (multiply the number by 2) is performed, using the line ```a[idx] *= 2```.   
* **Grid size = total number of blocks, Block size = total number of threads.**

We can select the number of processing elements by defining the number of threads per block when launching the kernel.
Different elements of the input array are automatically mapped to different thread, giving data parallelism in processing.
   
Getting the Function from the kernel:   
```python
# In string is the function name as mentioned in the Kernel
function = module.get_function("double_array")
```   

Calling / Executing the kernel:   
```python
# func ( (args to the kernel function <gpu mem locations >, block=(x,y,z), grid=(a,b,c) )
function( a_gpu, block=(16, 1, 1), grid=(1, 1, 1))
```
   
Place Holder for result:   
```python
# Empty arrary with dim same as a
final_a = np.empty_list(a)
```   

Copying data back from gpu:   
```python
cuda.memcpy_dtoh( a_final, a_gpu )
```
