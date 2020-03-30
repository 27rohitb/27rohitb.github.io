# Multiprocessing

* [Maps vs imap](https://stackoverflow.com/questions/26520781/multiprocessing-pool-whats-the-difference-between-map-async-and-imap)   
* [Map_async vs apply_async](https://stackoverflow.com/questions/27479218/map-async-vs-apply-asyncwhat-should-i-use-in-this-case)
* [Multiprocessing module](https://docs.python.org/3/library/multiprocessing.html)
* [imap_hangs in venv](https://stackoverflow.com/questions/54732436/pool-imap-hangs-in-venv-but-works-if-not-using-venv)
   
# My implementation:

```python
from multiprocessing import Pool

with Pool() as pool:
  res = pool.imap(func=self.calc_vec, iterable=input_str_list, chunksize=4)
  pool.close()
  pool.join()
  pool.terminate()
  del pool
  for i in res:
    yield i
```
  
* ```imap``` will give data inorder, but the function should ONLY take 1 argument.   
* ```starmap``` same as imap, but function can take MUltiple argurment inform: [ (arg1 ,...argm), (tuple2 with different  arg ) ...]
  

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
