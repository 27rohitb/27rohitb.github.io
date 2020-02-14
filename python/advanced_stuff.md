# Advanced Concepts   

This file has some advanced concepts like Generators, Iterators etc.
   
## Generators:

This is memory efficient way to implement a function or a forloop in a function.   
The keywords used are : **yield** and **next**:

**NOTE**:

* Generators can return ONLY 1 item, so they should be used in functions "generating" some kind of data, and NOT in function that are
manipulating it.

Taking example of function that computes the square of numbers in a given list.

```
python

# Normal, less mem-efficient function:

def sq_num(alist):
   my_result = []
   for i in alist:
      my_result.append(i * i)
   return my_result
   
# Usage:    print(sq_num([1,2,3,4]))

# Using Generators (mem-efficient approach):

def sq_num(alist):
   for i in alist:
      yield (i * i)  # yield KEYWORD used HERE
      
            res = sq_num([1,2,3,4])
# Usage:    
print(res)        # will return a generator object
print(next(res))  # NEXT keyword used HERE, will give output for 1st value in list, i.e "1"
```

### Converting list comprenhension to generator:

```
python
list_comp = [x*x for x in my_list]
my_gen = (x*x for x in my_list)
```

### Converting Generator to list :

```
python
my_list = list(my_gen)
```

## NOTE: Almost ALL dunder(__) methods have a normal method which calls them internally.

## if '__name__' == '__main__' :

The above important. When we import a module, everything not under the above line **run** by the python. The function under the above
file **wont** be executed!!.

Also note that, when we run a module directly, the ```__name__``` is directly set as ```__main__``` by default, but when it is being 
imported, it is set to ```<file name of the module>``` by default.

## Iterators & Iterables:

_Iterable_- Something that can be looped over. For anything to be iterable, it needs to have **__iter__** .
So, Iterable returns an "iterator";    

An _iterator_ is an object with a state, which remember where it is, during the iteration. They also know, how to get their next value, 
that is using **__next__** method. Note: Iterators are also iterables (can be looped over).

**NOTE** : 
* Iterators can ONLY go forward or reset it!
* Iterators don't need to end, as long they have next value.

### Difference between Generators & iterators:   

Generators are also iterators, but the ```__iter__ & __next__``` methods are created automatically.

Also, Geneator -> for a function, while Iterator -> for a class.
