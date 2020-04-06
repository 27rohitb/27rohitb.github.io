# Lecture 2 by Andreas Klockner

PASI: The challenge of Massive Parallelism.

Outline:

* OpenCL runtime.
* Device language.
* OpenCl implementations.
   
## OpenCL Runtime:

### Indepth of OpenCL:

Cl consist of two parts:

* Host-side "runtime": 
```
#include "CL/cl.h"

libOpenCL.so

import pyopencl as cl
```
   
* Devices-side: A dialect of C99
   

### Everything about dataflow:   

<< UML data flow diagram @3:24 >>

* Main part is the **context**, which is obtained from the device, which belongs to a particular platform.   

* For the given context, make a **command queue**.
* The given command queue can be used to make **memory objects** allocate and 
deallocate data and buffer, and also used to make **programs** that will run on GPU.

### CL - Component:

#### Plaforms:
   
* Platform is a collection of devices from **same** vendor.
* Multiple platforms can be used from on program-> ICD (Installable Client Driver)

#### Compute Devices:
   
* Device needs to have processor **with** interface to off-chip memory.
* Anything that fits into the programming model, i.e can follow the grid-block-thread system to process data.,

#### Context:

* For a given device we create a context.

```
context = cl.Context(device=None | [dev1,dev2], dev_type=None)
context = cl.create_some_context( interactive=True )

dev_type = DEFAULT, ALL ,CPU, GPU
````

* Can span **one or more** devices.
* Created from device type or list of devices
   

#### Command Queue:

* Its a mediator between host and device, since both the entities run asynchronously.
* So , Each command/operation gets queued in this command queue and is eventually 
executed.
* We can have more than 1 queue per device.
* By default queue serializes all the operations submitted to it, so if one queue is not 
fully uitlizing the GPU , other queue can be run in parallel.
* There other properties that can be defined for a given queue, such as enabling 
```OUT_OF_ORDER_EXECUTION``` or profiling.
   
* **One device per queue, but multiple queues per devices**    
* **Note: CUDA version of Command queue is called SCREEN**
* CUDA creates context from device automatically.

#### Command queue and Events:

* Everytime we enqueue something, it returns an EVENT.
* An event is an identifier for the time spanned for doing the given operation.
* Hence, for host-device synchronization, EVENT has method ```evt.wait()```.
* We can also for multiple events at the same time.
* All the entites in the command queue can also wait for each other, this can be done 
by keyword argument like :

```python
event = cl.enqueue_XXX(queue, wait_for=[evt1, evt2, ....] )
```

#### Capturing Data dependencies: Avoid deadlock:

The above wait() methods can ensure, that different operations can be run parallely
and a deadlock condition isnt created, becuase one event can wait for the prior event
to complete. Hence "out of order mode" can be enabled for a given queue safely.

Data dependencies are captured by plotting an DAG (directed acyclic graph).
This comes in handy, when different data streams are being run on different GPUs
and data transfer is required between them or other MPIs.


#### Profiling:

* This is done by enabling profiling for a given queue.
* This results in the EVENT object to have:

```python
event.profile = QUEUED, SUBMIT, START, END
````   
There are artifical events: MARKERs
These can be used to pause the timing during profiling to get the the correct time for a 
particular operation.


#### Memory Objects: Buffers

* Its basically a chunck of device memory, with no "type"
* It is NOT tied to a specific device, or doesnt have a fixed address.
* Infact, it **is** is movable between devices.
* **Note** pointers will NOT survive kernel launches.

```python
buf = cl.Buffer(context, flags, size=0, hostbuf=None)
```

* Either hostbuf or size can be specified.
* hostbuf needs a Python buffer interface (eg numpy array, or str)
* passed to device code as POINTERS
* Buffers can also be mapped into host address space.

```python
FLAGS: 
READ_ONLY, WRITE_ONLY/ READ_WRITE
{ ALLOC, COPY, USE}_HOST_PTR
```

##### Flags:

* ```COPY_HOST_PTR``` : uses hostbuf as initial content of buffer.

* ```USE_HOST_PTR```: uses ```hostbuf``` as the buffer, but caching in device memory is allowed.

* ```ALLOC_HOST_PTR```: NEW host memory (independent of hostbuf), visible from device and host.

#### Programs and Kernels

```python
prg = cl.Program(context, src)
```

* ```src``` is OpenCL device code, a derivative of C99.
* functions with ```__kernel``` attribute can be invoked from host!
* ```prg.build(options = "", devices=None)```: can specifiy compiler options and the devices to be used.

Program can also be created from binary: 
   
* ```kernel = prg.kernel_name``` :load program from binary.
* ```kernel(queue, (Gx, Gy, Gz), (Lx, Ly, Lz), arg, ..., wait_for=None): specify global and local size.

Kernel Arguments (Additional, from above):

* ```None```: a NULL pointer.
* Numpy Sized Scalar: ```numpy.int64, numpy.float32``` etc.
* Any object with buffer interface (ndarray, str etc)
* Buffer object
* Also: cl.Image, cl.Sampler, cl.LocalMemory

**Note: Explicit sized scalars are erro-prone:**
   
Solution/Better:

```python
kernel.set_scalar_arg_dtypes([numpy.int32, None, numpy.float32])
# Using None for non-scalars
```

### CL Device Language:

It is C99 with following changes:

+ Index getters (index getting functions: get_local_id() etc).
+ Memory space qualifier
+ Vector data types
+ Many Generic ("overloaded") math functions (sin(), cos() etc)
+ Synchronization
- Recursion
- malloc()

### Cl vector data types:

About:   

* ```floatn vec```, here n =1,2,3....(index of element).
* Elements can be accessed as :```vec.s012``` : will give element 0,1,2 from the vector.
* They can be accessed in ANY order.
* Assigning values: ```vec.s024 = (float3) (1,2,3).

Usage:
   
* Easy elementwise operation
* Loading and storing: ```floatn vloadm/vstoren(offset, float *) (aligned!)
* dot/distance has special functions.

### Concurrency and Synchronization:

Concurrency & Sync between different levels:

Intra-group:   

* barrier(): is like a temporary stop, processes can proceed further untill all other processes arrive to it.
* mem_fence(): order of read/write restriction.
   
CLK_{LOCAL, GLOBAL}_MEM_FENCE
   

Inter-group:
   
* Kernel launch
   
CPU - GPU:

* Command queus
* Events
   
Miscellaneous:
   
There is also Atomic Operations.

## Extension: Future-proof CL:   

2 Mechanism:

### Runtime:

* This can be done with header file change: ```cl_ext.h```.   
* Also using device.extensions
   
### Device Language:

Enable the extension from here using:

```
#pragma OPENCL EXTENSION
name: enable
```

An important extension is : ```cl_khr_fp64``` : The Khronos group extension.
