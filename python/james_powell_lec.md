# Key points from James Powell's talk   

To watch the talk [click here](https://youtu.be/AmHE0kZhLIQ).
   
   
I learned the following things from his talk about python:   

* Python is the language of lazy people. For any given project , do the bare minimum and then add the complexity.

* when printing object in human read-able format such, many object contain "<>" brackets, which means there is addtional data such as buffers
of pointers which cany be converted into human readable format.   

* Memory managment sucks, python garbage collector doesnt really works as efficiently as we think. (i personally use del keyword to delete
objects to free up memory for this reason).   

* Python is build around " do minimal changes" concept, < he mentioned using !r in __repr__ function >.   

*
