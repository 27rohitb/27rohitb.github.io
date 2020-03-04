# Itertools module   

This is native in python (that is, available in standard library), and allows working with iterables in fast & **memory efficient** way.   

It contains commonly used iterators, and functions for combining several iterators. 

## Following are the functions with sample python script:   
   
```python
import itertools
```
 
* ```counter = itertools.count(start=1, step=-2)``` : Does counting. (usuful with zip, when indexing is required and size of data is not known. It can count in reverse direction also !

* ``` daily_data = zip( iterator_A, iterator_B )```: Combines two iterator together (linearly) and return an iterator. "This ends on the shortest iterable is exhausted"- that is, between the two iterators; A,B , the zip functions stops with first iterable throws "Stop Iteration" exception. The rest of the data for second iterable is NOT mapped to anything.   

* ```itertools.zip_longest( iter_A, iter_B )```: Now it will map the remaning value of longer iterator to "None".   

* ```itertools.cycle( iter_A ):``` Returns an iterator which loops over and can continue forever.
   
* ```itertools.repeat(2, times=3):``` Returns and iterator that repeats given value for given number of time, and then throw Exception.

* ```map( func_A, iter_A, iter_B ):``` Returns an iterator where the values from iter_A and iter_B is being passed as an argument to func_A.   

* ```itertools.starmap( func_A, [(val_1, val_2) ...]):``` Takes a function and a list of tuples, which have values already paried up, and does the same thing as ```map()``` function above.
