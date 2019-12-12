CLASSES:
#this is basically a NEW DATA TYPE
#class to be inherited ,must be imported!!!

class <class_name>(<inherited_from_class_name>):
	#data & stuff goes here
	
	def __init__(self, var):
		#Define the constructor
		
		self.var = var
	
	def <other_functions_name>(self):
		#TODO in these function
		#NOTE these function will OVERRIDE function with same name from parent class!!
		
# Usage in other files:
from <file_name> import <class_name> as <some_var>
