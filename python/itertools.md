# Itertools module   

This is native in python (that is, available in standard library), and allows working with iterables in fast & **memory efficient** way.   

It contains commonly used iterators, and functions for combining several iterators. 

## Following are the functions with sample python script:   
   
```python
import itertools
```
 
* ```counter = itertools.count(start=1, step=-2)``` : Does counting. (usuful with zip, when indexing is required and size of data is not known. It can count in reverse direction also !

* ``` daily_data = zip( iterator_A, iterator_B )```: Combines two iterator together (linearly) and return an iterator.
   

