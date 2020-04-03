# PyOpenCL (by Andreas Klochkner PT1)

## Introduction:   

* Talks about arch. changes between CPU and GPU.
* **EU = Execution Unit __replace by__ Execution Context = Data that we operate on.**
   
   
3 Key arch. changes for making parallel execution faster:

* Remove Component that makes Single INST go faster, like branch prediction, out-of-order execution etc.
* Add more ALUs
* More context, that is, different data.
   
   
Basically ,Perfrom a single operation using different ALU in parallel, over different data.

## Mapping data onto Infinitely many ALUs:

*Cores: On compute element on GPU , consisting of Fetch/Decode, ALU & Context.

So the mapping is done by assuming a 2-D grid:

* The grid is divided into small "groups", which are further divided into "work items".
* Each Group is a passed onto one core.
* Further, each work item in the given work group, is passed onto one ALU of the given core.
   

Note: X,Y,Z order _within_ the group **matters**. (but , not amongst the group though.)

## Addressing:

A given function is run on all work items in the given grid. Inorder to determine , which is current work item 
is being dealt with, GPU use : ```local_id, group_id, global_id```   (all these are relative to some axis (1,2,3....which is basically x,y,z....))
   
Note: Grids can be 1,2 or 3 dim.   

## Introduction to OpenCL:

Main advantage of OpenCL, is that it comes with RTCG (runtime code generation) out of the box.

## OpenCl <-> Cuda concept mapping:

| OpenCl | CUDA |
|-----------|----------|
| Grid | Grid |
| Work Group | Block |
| Wirk Item | Thread |
| __kernel  | __global__ |
| __global | __device__ |
| __local | __shared__ |
| __private | __local__ |
| imagend_t | texture<type, n , ....> |
| barrier(LMF) | __syncthreads() |
| get_local_id(012) | threadIdx.xyz |
| get_group_id(012) | blockIdx.xyz |
| get_global_id(012) | -(reimplement) |   
   
Other terminologies: 

* Host (CPU), this where the runtime code lives 
* Compute Devices (device), where the computation is performed, the GPU etc.

## PyOpenCL Coding HERE:   

NOTE:
* For Memory allocation we interact with the context object, i.e ctx.
* For any other operation, including data transfer, computation we use queue object.   
   
Other key points:

* **Unlike** CUDA, global size in openCL is specified as global_size * group_size

### Initializing and performing the computation:
``` python
import pyopencl as cl
import numpy

# Create a 256^3 element numpy array
a = numpy.random.rand(256**3).astype(numpy.float32)

# Create context ->  a living space for all the opencl objects !!!!!
ctx = cl.create_some_context()

# For the given context, create command queue -> Contains details about devices, platform we live on.
queue = cl.CommandQueue(ctx)

# For the given context, create a buffer -> ALLOCATE memory space on DEVICE,
# on which we transfer data, that needs to be processed.
a_dev = cl.Buffer(ctx, cl.mem_flags.READ_WRITE, size=a.nbytes)

# This will TRASNFER data from host to device USING the command Queue (which is literally a queue of commands)
cl.enqueue_write_buffer(queue, a_dev, a)

# Write the program for the computation we want to perform:
prg = cl.Program(ctx, """
	__kernel void twice( __global float *a)
	{ a[ get_global_id(0)] * = 2; }
	""").build()

# Run the program on the data using the Queue
prg.twice(queue, a.shape, (1,), a_dev)
```

* The C-function inside triple quote is called **compute kernel**.
* the input to the ```twice``` function is ```(command queue, grid size = a.shape, workgroup size = (1,), buffer = a_dev)```

### Extracting the Result from the Computation:

```python
# Create an empty array with same dimension as that of a
result = numpy.empty_like(a)

# Wait for the result and the transfer
cl.enqueue_read_buffer(queue, a_dev, result).wait()
```

### After proper index generation:

The indexing and call changes are as follows:
```python
a [ get_local_id(0) + get_local_size(0)*get_group_id(0) ] =* 2;

prg.twice(queue, a.shape, (256,), a_dev)
```
