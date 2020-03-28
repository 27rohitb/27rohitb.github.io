# Multiprocessing

[here](https://stackoverflow.com/questions/26520781/multiprocessing-pool-whats-the-difference-between-map-async-and-imap)

## Multiprocessing using pool:

## Using process pool executor:

```python
import concurrent.futures

with oncurrent.futures.ProcessPoolExecutor() as executor:
  res = [executor.submit( function_name, args=[]) for _ in range(10)]
  #
  # no need for below for loop when using map() 
  # or if we would like the result inorder of input, INSTEAD of future objects:
  res = executor.map( function_name , arg_list )
  
  
  for f in concurrent.futures.as_completed(res):
    print(f.result())
```

## Native way:

**Note: Arguments passed to a function being executed by multiprocess, MUST BE pickle-able**

### Serial spawing multiple processes:

Import module for multiprocessing:
```python
import multiprocessing
```

Creating processes:
```python

p1 = multiprocessing.Process(target= function_name, args=[])
```

Executing and syncing processes:
**Note: Join() is reuqired, otherwise it will execute the main script in parallel to these processes**
``` 
python
p1.start()

p1.join()
```

### Spawning processes in a loop:
```python

prcocess_list = []

for _ in range(10);
  p = multiprocessing.Process(target= function_name, args=[])
  p.start()
  process_list.append(p)
  
for p in process_list:
  p.join()
```
