# Key points from James Powell's talk   

To watch the talk [click here](https://youtu.be/AmHE0kZhLIQ).
   
   
I learned the following things from his talk about python:   

* Python is the language of lazy people. For any given project , do the bare minimum and then add the complexity.

* when printing object in human read-able format such, many object contain "<>" brackets, which means there is addtional data such as buffers
of pointers which cany be converted into human readable format.   

* Memory managment sucks, python garbage collector doesnt really works as efficiently as we think. (i personally use del keyword to delete
objects to free up memory for this reason).   

* Python is build around " do minimal changes" concept, < he mentioned using !r in \__repr\__ function >.   

* Using "Slot" system for memory saving at the cost of reduced dynamic behavior.
   
* Its not a good idea to create new functions/classes etc which leads to new rules on top of existing python object model rules *if* 
it can be done by simple copy past operation (not too redundant), unless you are builidng a library or something very large and 
complicated which required some rules.   

* Python 3.7 has ```dataclass``` to automatically generate boilerplates (init method)

* The existing grammer offered by the python (the dunder methods, etc) might not mean what we think it means. He gave the example of 
\__hash\__ method. (REF@40:00-ish)   

* For the above reason we also need to make sure if the given implemenetation defines the behavior between objects or if its used to 
hook with python interpreter.   

* Re arranging complexity of different operations in a particular way can lead to ease of different actions such as refactoring ,
reasy readability etc. He takes the example of converting a range checking function into a dictionary.   

* Talks something about ChainMapping? Its generally modified the post lookup stuff?   

* What an \__init\__ should look like: (REF@1:00:00-ish) It should **always** be a boiler plate, and let it be that.    

* Python vocab provide dunder method and rules **assuming** there is a unique meaning for things defined in it. For eg, length in
circuit network.

* Using restricted stuff in data model, is sometimes used to convery, that a particular code is designed to do the given task ONLY.   

* Python is not fundamentally dynamic , its operationally dynamic.   

* Classmethods, normals function etc work using something called as _Descriptor protocol_ .   

* There is also _Object Construction protocol_, can be hooked using \__build\_class\__ function in builtins module. This basically 
gives a **hook into class construction mechanics** for the runtime its present in!! It generally used for debugging, memory contraint, 
class construction logs etc.

* Metaclass is a **hook into object construction process** 

* _dis_ module in python can be used to dis-intergrate python code (sort of display its pythonized assembly)

**ALL the above stuff concludes that while all the python projects start simple, as the complexity grows python provides hooks into
each detail such as object construction , class contruction which can customized with the growing complexity**
