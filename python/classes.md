# CLASSES
This is basically defines a _new!!_ datatype.  

>**NOTE: For a class to be inherited ,it must be imported first!!!**

```python
class <class_name>(<inherited_from_class_name>):
	#data & stuff goes here
	
	def __init__(self, var):
		#Define the constructor
		
		self.var = var
	
	def <other_functions_name>(self):
		#TODO in these function
		#NOTE these function will OVERRIDE function with same name from parent class!!
```

## Usage in other files:
```python
from <file_name> import <class_name> as <some_var>
```
