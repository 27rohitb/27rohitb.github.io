# Additional Notes:

I made these notes after reading material from the following site: [Click here](https://downloads.ti.com/mctools/esd/docs/opencl/execution/kernels-workgroups-workitems.html)
   
   
## Key points:

* There are two OpenCL APIs for enqueueing a kernel; 
1.```enqueueNDRangeKernel()```
2.```enqueueTask()```.
   
Note: enqueueTask is just a special case of enqueueNDRangeKernel where the offset, global size, and local size are fixed to 0, 1, and 1 respectively in a single dimension.
   
* When an enqueueNDRangeKernel API call is made, the key three arguments to the API are:   
1.the kernel object which has previously been associated with the kernel name,   
2.the number of work-items you wish to execute (called the global size),   
3.the number of work-items you wish to group into a work-group (called the local size).   
