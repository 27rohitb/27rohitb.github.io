# Advanced Concepts   

This file has some advanced concepts like Generators, Iterators etc.
   
## Generators:

This is memory efficient way to implement a function or a forloop in a function.   
The keywords used are : **yield** and **next**.

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
# Usage:    print(res)        # will return a generator object
#           print(next(res))  # NEXT keyword used HERE, will give output for 1st value in list, i.e "1"
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
