# python's GIL (by Larry Hastings):

C global var is equivalent to a python module's attribute.
   
## Reference Counting:

* Used to calculate the lifetime of a var.
   
Every python object has the following structure at the top of each object:

```c
typedef struct_object{
	unsigned int ob_refcnt;
	struct _typeobject *ob_type;
} object;
```
   
Here 1st on is the object reference count of the object. (number of entities holding on to that object)
Second is the reference to another class, which has a lot of info about the object.
   
### Managing Reference Count:

```c
#define INCREF(op) ((op)->ob_refcnt++)
#define DECREF(op) \
	if (!--(op)->ob_refcnt >0) \
		DELREF(op)
```   

Decref: Subtracts one from the reference count, and it the final value is zero, delete the reference.
   
### Checking the ref count:

```python
a=[]
b=a
sys.getrefcount(a)
# answer is 3 because another ref is created when 'a' is passed to the function
```
   
## Problem with ref counting and threading:
   
<< Explained in lecture @7:00 >>
 Example is of two threads, simulateously decrementing reference count. While checking the ref count value **parallely** both 
thread will get , say 3, then decrement it by 1, and store the final value 2, back to object. Which is incorrect. Since both the thread
have dropped the object, the final value of ref count should be 1 instead of 2.
   
To overcome this problem, _locks_ were introduced. But this lead to _deadlock_ , which is happening due to **Race condition**.
<< Explaine @9:20 >>
   
To overcome deadlock due to race condition, GIL was introduced: Global Interpreter Lock.
   
## GIL: Global interpreter Lock
   
### The original version:
```c
static type_lock;
interpreter_lock;
```
   
### Py2.7 Version:
```c
static PyThread_type_lock
interpreter_lock = 0;
/* This is the GIL */
```
   
There is **only one** lock,  which needs to be acquired **for interaction 
with C-python interperter** for any operation like mem allocation, runnning bytecode etc. 
Note: that does not include IO operations like socket connection or fileIO, so these can be carried out with other entity has the GIL.

This means, for IO bound task, GIL is fantastic, since it protects from deadlocks etc.
But for CPU bound task, like parallel processing, it is bad, because GIL can only be acquired by 1 entity, therefore 
python interpreter can only be acquired by one thread.
   
## Sharing GIL in IO-Bound:

There are macros used for acquiring and releasing locks:
```c
Py_BEGIN_ALLOW_THREADS
/* Lock released */
/* Other threads can now run */

<< In the middle>>

Py_END_ALLOW_THREADS
/* Lock Acquired */
```
   
## General Sharing of GIL:

This happens, natively in the C-python using the _check interval_, which takes a number 
which is the amount of bytecode executed and then the GIL MUST be passed on to some other entity.
The default number in python 2.7 is 100.
   
### Scheduling: Making IO bound threads happy:

<< See lec @17:50 >>

Becuase CPU bound threads are never happy :P.
   
### Failure of py2.7 GIL:

<< See lec @19:00 >>
   
## Fixing GIL in python 3.2:

<< See lec @19.20 >>

Added a GIL request var (flag), which tell if someone else wanted to acquire the GIL.

```c
static volitile int gil_drop_request = 0;
```

Further fixing requires better Scheduling (very hard to do).

   
## History of Multi-core system:

<< See lec @20:50 >>
    
## Attempt tp get rid of GIL:

<< See lec @22:45 >>

* Free-threading patch
* Atomic incr/decr


## Different python interpreters:

<< See lec @24:52 >>

* cpython
* jpython
* ironpython
* pypy

Note: There are two ways of memory mangement: Pure GC vs  Refcounting with GIL.

Pure GC require heavy C api changes. It would be like starting all over again. 
    
## Software Transactional Memory:

<< See lec @30:50 >>

Its like Databases, but the data is being commited to memory, and if some commits from different thread collide, well, rollback and start over.
It is not slower, its just very hard conceptually to get it right.
   
## Writing new languages:

<< See lec @36:10 >>
