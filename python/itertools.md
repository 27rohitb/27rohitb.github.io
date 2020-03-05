# Itertools module   

This is native in python (that is, available in standard library), and allows working with iterables in fast & **memory efficient** way.   
**NOTE: File objects are also iterables!, hence they can be used with these itertools!!**

It contains commonly used iterators, and functions for combining several iterators. 

## Following are the functions with sample python script:   
   
```python
import itertools
```

### Functions that can run indefinitely:   
 
* ```counter = itertools.count(start=1, step=-2)``` : Does counting. (usuful with zip, when indexing is required and size of data is not known. It can count in reverse direction also !

* ``` daily_data = zip( iterator_A, iterator_B )```: Combines two iterator together (linearly) and return an iterator. "This ends on the shortest iterable is exhausted"- that is, between the two iterators; A,B , the zip functions stops with first iterable throws "Stop Iteration" exception. The rest of the data for second iterable is NOT mapped to anything.   

* ```itertools.zip_longest( iter_A, iter_B )```: Now it will map the remaning value of longer iterator to "None".   

* ```itertools.cycle( iter_A ):``` Returns an iterator which loops over and can continue forever.
   
* ```itertools.repeat(2, times=3):``` Returns and iterator that repeats given value for given number of time, and then throw Exception.

* ```map( func_A, iter_A, iter_B ):``` Returns an iterator where the values from iter_A and iter_B is being passed as an argument to func_A.   

* ```itertools.starmap( func_A, [(val_1, val_2) ...]):``` Takes a function and a list of tuples, which have values already paried up, and does the same thing as ```map()``` function above.

### Functions that run only for finite number of times:   

**ALL the functions return an iterator**   

#### Combiantion():   
```python

iter_a = ['a','b','c','d']
# number of vals to be considered while making a combination:

num_of_val = 2 
#only a ,b at the given time

# num_of_val = 3 
# a,b,c at the same time

combinations( iter_a, num_of_vals )
```
Produce all possible combintation of element where the order **does not** matter.

#### Permutation():   

Same as combination, except order of element in the output, now matters.

#### Product():   
Give **Catersian Product** of the iterables, something like permutation with repeats.   

```python
itertools.product( iter_a, repeat=4 )
```

#### Combination with repeat:

```itertools.combintations_with_replacement( iter_a, 4)```   

### Iterable manipulation functions:   

#### Combine different iterables into one:   

``` itertools.chain( iter_a, iter_b , iter_c )```

#### Slicing iterators:   

**Slicing function can be used to read file efficiently, since file objects are iterators**   

``` itertools.islice( iter_a, , starting_val*, stopping_val*, steps* ) # *-> optional argument```   

#### Selecting certain elements:   

```Compress()```:     
```python
itertools.compress( iter_a, corresponding_list_of_bools )

# Input example:
iter_a = ['a', 'b', 'c']
list_of_bool = [ True, False, True ] #or
list_of_bool = [1,0,1]
```

```Filter( filter_func, iter_a)```:   
Returns an iterator with values True or False, depending upon which element satisfies filter function.   

```itertools.filterfalse( filter_func, iter_a ):``` Complement of builtin filter function.   

```itertools.dropwhile( filter_func, iter_a ):``` Returns iterable elements (without filtering) after hitting the first "True", (including the true value).   

```itertools.takewhile( filter_func, iter_a ):``` Comlpement of dropwhile function.   
    
Does the given operation ( add, multiply etc) on the iterator elements and return that after each element.
```python
import operator

itertools.accumulate( iter_a, operator.mul ):
```

