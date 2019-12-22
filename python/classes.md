# Classes and Instance

This includes the following topics:
* Creating and instantiating.
* Class vs Instance variables
* Inhertiance
* Static methods and Class methods

Allows for logical grouping and reusing of data and functions . And overall its can be easier to built upon this.   
>Terminology note: Data = attribute and Function = methods.   

> `pass` statment tell python; nothing to do here.

___
## Class & its instance
A class is a blueprint for its instances.

```python
class some_name:
    pass

inst_one = some_name()
```

___
## Init Method
Its the first method that is used to intialize class variables. It is the constructor.

>_Please read the comments carefully_
```python
class some_class:

    def __init__(self, some_argument):
        # self = instance of the class
        # assign specific value to instance
        # good practice is to name the class var as arguments.
        self.some_argument = some_argument

    def some_func(self):
        # TODO something with class vars.

inst_one = some_class(some_argument)
```

>_Running some function of class for given instance._
```python
# METHOD 1
inst_one.some_func() #here inst_one = self variable.

# METHOD 2
some_class.some_func(inst_one) # passing instance as argument.
```

___

## Instance Variables vs Class variable
**Instance variables** contain data _**uniquely**_ associated with the given instance of some class, whereas **Class variables** are common amongst all the instances and generally defined _**outside**_ of "init" method!!.    

> Instance Variable example:   

```python
inst_one = some_class()
inst_one.uniq_var = "some val" #this is uniq to this instance.
```
> Class variable example:   

```python
class some_class:

    random_var = "some Val" # THis is a CLASS Variable

    # <init method goes here>
```   

> There are **two** methods to access class variable within a class:  
> Method 1: accessing through instance variable   

```python
    def some_func(self):
        self.random_var
```
>Method 2: accessing through class variable    

```python
    def some_func(self):
        some_class.random_var
```

NOTE: Some key points to keep in mind are:  
* When an attirbute value is required, it first checked in Instance, the Class, and lastly inherited class.  

* An instance variable does **NOT** contain class variable, thus accessing class variable through them, will require them accesing class namespace themselves.

* If we try to modify class variable throught instance, it will lead to that variable's modified version being added to instance's namespace.

> A namespace is a dict maintain by python to keep the name assigned uniquely to each variable. It can be accessed using:   

```python
# Accessing namespace of an entity: a class or instance.
some_entity.__dict__
```

___
## Class methods & Static methods

### Class methods:   
These are generally used to manipulate class variables.

To _convert_ regular method to class method; 
use decorator **@classmethod** and pass the first argument as class: **cls** keyword being used, since "class" is already a keyword. 

Example:
```python
@classmethod
def somefunc(cls,*args):
```
