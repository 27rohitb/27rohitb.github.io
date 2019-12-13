String function: 

str.index("str")   
#Tells us where is "str" located in whole of the str.
Note that if "str" is NOT present in str, then it WILL throw and ERROR!!

str.replace("old", "new)      
#Replace "old" with "new" in str if "old" present.


Numbers function:

() 
#prantheses can be used to specify the order of equation. (3* (4+5))

a % b
#remainder of (a/b)

floor(3.7) = 3
#round off to min(given number)

ceil(2.3) = 3
#round off to max(given number)


Input function:

str_var = input("str")
#inputs stuff from user DEFAULT input is takes as STRING

no_var = eval(input("number"))
#eval will check what is the data type (int/float/complex) and convert input data to that


Datatypes:

LIST FUNCTIONS:

list_var[-index]
#start indexing from the end and given the number at "index".

list_var[start_index:end_index]
# gives all the element from "start_index" up till "end_index" (EXCLUDING thing at end_index)
#NOTE that start/end_index = null/nothing, which means from/till start/end

list_var.extend(list2_var)
#append/merge two lists
#its NOT same as append-> which is used to add data "into" the list

list_var.insert( index_no, data )
#ADDS data at the given index_no

list_var.pop()
#Remove the last element and return it

list_var.index( data )
#returns the INDEX of data

list2_var = list_var.copy()
#returns a copy of the list <PLEASE TELL IF ITS A DEEPCOPY OR NOT>


TUPLE FUNCTION:

()
# USE THIS WHEN U DONT WANT THE DATA TO CHANGE.
<similar to list, just without modification functions or fancy indexing>

DICTIONARY STUFF:

{}
#thing with KEY-VAL pair. KEY must be unique.
#can be used to make converter (for eg, expander of "jan" to "january")

dict_var[KEY]
#return value for the given key, if it exists.

dict_var.get(KEY, default_val) 
#retun default_val if key is NOT found, only valid for this.


OTHER STUFF:

"a" in "str":
#return a bool if "a" is present in "str"

CATCHING ERRORS: (Try-Except block)
# best practise: use Specific Errors mostly.
# put specific exceptions at the top.
syntax:

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

raise Exception
# is used to maually raise general exception on demand


FILE IO:

file_var.readable()
#return a BOOL val depending upon the readability of the file.
#NOTE is ALSO depends upon the MODE inwhich file was opened (r/r+/w)

file_var.readlines()
# returns a LIST of lines in the file which was read
#NOTE its readLINES and NOT readLINE.

open("filename","a/w")
# a:  append mode to file
# w: OERWRITE file

file_var.write( data )
# if filemode is append, then it adds "data" to last line
#NOTE: it does NOT adds newline.
