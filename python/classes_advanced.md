# Advanced Stuff about classes  

## Magic Methods   

* These are in built methods in python and can be used for doing stuff on classes.   
* These begin with "dunders" or "__".
  
```__init__``` is called when objected is **CREATED**.   
```__repr__``` is used for debugging/dev, by providing an unambiguous representation of the object.   
```__str__``` is readable representation of the object, for display to the end user.

## Property Decorator (getter method) & Setter Method & Deleter Method:   

Lets us define a method, which can be accessed like an attribute. -> This can be useful in scenarios where class requires modification 
(some attribute must be updates, which is generally done through functions), but maintain the compatibility!.    

This done using property decorator as:   
```python

class someclass():
  
  def __init__(self,var):
    self.var = var
    
  @property
  def var(self):
    # var has already been updates
    return self.var
    
  @var.setter
  def var(self, new_val):
    self.var = new_val
    
   @var.deleter
   def var(self):
      self.var = None
```
   
> Deleter Method are called while deleting the class object, for eg:
```python
someobj = someclass(somevar)

# Below
del someobj
```
