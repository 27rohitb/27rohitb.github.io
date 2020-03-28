# MultiThreading   

It is NOT same as multiprocessing. It does NOT executes the task in parallel, but rather, it does something conceptually similar.
The basic idea is, if a process (function) is waiting for some input/output operation, the processor can be utilized to execute other
process (function) in the mean time, giving it the illusion of parallel processing.   

## Threading using pool workers:

NOTE: 

* while execution, no exceptions are processes, rather they are shown at runtime.
* It performs AUTO-join().

Importing and creating pool workers:
```python
import concurrent.futures
```

For serial execution of threads:
This is done using Submit(), which return a <future> object.
```python
with concurrent.futures.ThreadPoolExecutor() as executor:
    f1 = executor.submit(function_name, arg=[])
    res = f1.result()    
```

For parallel execution using loop:
```python
# This will give us a list of future object from which we need to GET RESULT
with concurrent.futures.ThreadPoolExecutor() as executor:
  results = [executor.submit(function_name, arg=[]) for _ in range(10)]
  
  for f in concurrent.futures.as_completed(results):
      print(f.result())
```


    
## Native way of threading:

### Serial Threading:   
Import threading lib:
```python
import threading
```

Create thread of function:   
```python
# Remember function_NAME , DO NOT put ()
t1 = threading.Thread(target=function_name, args=[])
```

Running Threads:
```python
t1.start()
t2.start()
```

Note: while these threads are being executed, if they encounter any pause (read or write delay), the main scripted will be executed in the
free cpu time.   

To avoid above situation of main program being executed, we use join():
```python
t1.join()
t2.join()
```

### Parallel Threading:   

```python
thread_list = []

# Creating and Starting the thread
for _ in range(10):
  t = threading.Thread(target=function_name, args=[])
  t.start()
  thread_list.append(t)
  
# Joining the Thread:
for t in thread_list:
  t.join()
 ```
  
