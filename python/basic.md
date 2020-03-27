# Basic
This module contains snippets of code/info. which are easier to forget and can come in handy later.

## String functions: 
> Tells us where is "str" located in whole of the str.  
**NOTE: that if "str" is NOT present in str, then it WILL throw and ERROR!!**
```
str.index("str")
```
>Replace "old" with "new" in str if "old" present.
```
str.replace("old", "new)      
```
>Return a bool if only "a" sub-string is present in "str"
```
"a" in "str":
```   

## Number functions:
>Remainder of (a/b)
```
a % b
```  
>Round off to min(given number)
```
floor(3.7) = 3
```
>Round off to max(given number)
```
ceil(2.3) = 3
```

## Input functions:
>Inputs stuff from user DEFAULT input is takes as STRING
```
str_var = input("str")
```
>Eval will check what is the data type (int/float/complex) and convert input data to that
```
num_var = eval(input("number"))
```

## List functions:
>Start indexing from the end and given the number at "index".
```
list_var[-index]
```
>Gives all the element from "start_index" up till "end_index" (EXCLUDING thing at end_index)  
**NOTE: that start/end_index = null/nothing, which means from/till start/end**
```
list_var[start_index : end_index]
```
>Appends/merge two lists  
**NOTE: its NOT same as _append_ which is used to add data "into" the list**
```
list_var.extend(list2_var)
```
>_Inserts_ data at the given index_no
```
list_var.insert( index_no, data )
```
>Remove the last element and return it
```
list_var.pop()
```
>Returns the INDEX of data
```
list_var.index( data )
```
>Returns a copy of the list <PLEASE TELL IF ITS A DEEPCOPY OR NOT>
```
list2_var = list_var.copy()
```

## Tuple functions:
```
() -> Tuples
```
These are **used when you dont want the data to change**, say for example coordinates. Similar to list, just without modification functions or fancy indexing.

## Dictionary functions:
```
{} -> Dictonary will be made only if key:value is given, otheriwse it will creates a set.
```
Mostly used to make converter or map something (for eg, expander of "jan" to "january")

>**NOTE: In KEY-VAL pair. KEY must be unique and Value MUST be hasbable.**  

>Return value for the given key, if it exists.
```
dict_var[KEY]
```
>retun default_val if key is NOT found, only valid for this.
```
dict_var.get(KEY, default_val) 
```

## Other stuff:

## CATCHING ERRORS:
Best practise:
* Use Specific Errors mostly.
* Put specific exceptions at the top.

>syntax:

```python
try:
	#code here
except ZeroDivisionError as err:
	#Do something
	#as err-> STORES error into variable "err"
except <any error by default>:
	#TODO for everything else
else:
	#TODO if no exception is found
finally:
	#TODO independent of an error or not
```
>Raise general exception on demand
```
raise Exception
```

## FILE IO:
    
Most common way to open read the file line by line (this automatically closes the file after reading:   
```python
with open(cfile_name,"r") as fin:
	line = fin.readline()
```    

Return a BOOL val depending upon the readability of the file.   
**NOTE is ALSO depends upon the MODE inwhich file was opened (r/r+/w)**
```
file_var.readable()
```   

Returns a LIST of lines in the file which was read
#NOTE its readLINES and NOT readLINE.
```
file_var.readlines()
```   

a:  append mode to file; w: _Overwrites!!_ file
```
open("filename","a/w")
```   

If filemode is append, then it adds "data" to last line.  
**NOTE: it does NOT adds newline.**
```
file_var.write( data )
```
