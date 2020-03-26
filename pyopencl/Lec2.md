# Lecture 2 (Cuda in an afternoon):   

By uni of edinburgh (Alan Gray)

**I did not complete this video, since it is for C++ and is outdated**

# Intro to CUDA:   

Key points:  

* There are snippets of code "kernels" which are accelerated on GPU.
* Each device, CPU (host) and GPU (device) has its own memory space, and the data transfer between each should be handled by the programmer.
* CUDA is an extension to c/c++ that allows the following advantages:   
**Language Extension for defining kernels and perform parallel decomposition of GPU**   
**API functions for memory management**    

## Stream model of computation:  

* Decompose data in smaller elements.
* "Thread" is basically processing of the data. So use on thread to do one part of the computation (a.k.a execution of kernel) on each element of the data parallely.

## Nvidia GPU structure:    

* 2 level hierarchy:
1. SM cores (streaming multiprocessors) + GPU-specific memory shared by smaller cores.
2. Each Sm has multiples cores.

## Abstraction of data processing:   

This is majorly done to maintain compatibility for data processing across different generation of GPUs.   
As in [LEC1](./lec1.md):   

* Mutliple block in a grid map onto multiple SMs.
* Each block contain multiple threads, which are mapped to cores **within** SM.

## Oversubscribing:   

Instead of knowing the exact number of cores and SMs for each GPU, **we use more blocks than SMs, and more threads than cores**.
They system will automatically schedule and map it to the architecture of the given GPU. Hence, the same code becomes portable accross different GPU.

## dim3 data type:   

A new data type in CUDA, contains 3 integers corresponding to x,y,z directions.
```c
dim3 my_xyz( xval, yval, zval);
```

## Accessing value for dim3 data type:   

This done using dot operator:
```c
x_component = my_xyz.x
```
