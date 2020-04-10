# Lecture 4 by Andreas Klockner

Outline:

1. PyCUDA
2. Automatic GPU Programming
3. GPU-DG: Challenge and Solution (skipped this part, not relevant to my research)

## PyCUDA:

Basic code:
```python
import pycuda.driver as cuda  
import pycuda.autoinit, pycuda.compiler
import numpy as nps
a = np.random.randn(4,4).astype(np.float32)
a_gpu = cuda-mem_alloc(a.nbytes)
cuda.memcpy_htod(a_gpu, a)
```
   
Instead of creating context, we just imported ```pycuda.autoinit````
   
```python
mod = pycuda.compiler.SouceModule("""
	__global__ void twice( float *a)
	{
		int idx = theradIdx.x + threadIdx.y*4;
		a[idx] *=2;
	}
	""")

func = mod.get_function("twice")
func(a_gpu, block=(4,4,1))

a_doubled = numpy.empty_like(a)
cuda.memcpy_dtoh( a_doubled, a_gpu)
```

### GPUarray:

Meant to look and feel like numpy array. Similar stuff to pyopencl version of numpy array.

```python
import pycuda.gpuarray as garr

a_gpu = garr.to_gpu(np.radnom.randn(4,4).astype(np.float32))
a_doubled = (2*a_gpu).get()
```

### Sparse Matrix-Vector on the GPU:

This is special in pyCUDA. Can also integrate with scipy.sparse. Conjugate-gradient solver is also included.

### PyCUDA <> PycOpenCL Table:

| PyOpenCL | PyCUDA |
|---------------|-------------|
| Context | Context |
| CommandQueue | Stream |
| Buffer | mem_alloc/DeviceAllocation |
| Program | SourceModule | 
| Kernel | Function |
| Event | Event |
   
**PyCUDA workflow diagram @7:10**
   
Also note: CUDA does NOT come with JIT unlike OpenCL.
   
## Automatic GPU Programming
   
Can be time-consuming, unintuitive and error-prone; Solve using:   
* smart compilers.
* Dumb enumeration.
