# Variable Scope

This tells us about what vars can be accessed from different places in the code.

Simple abreviation for scoping rules in python. **Note** that this is also the **_order_** in which python checks the variable in its scope.

So basically, python has list/table for each scope, which contains the name of the variable and its corresponding value. During run-time, the evaluation of given variable takes place in the order given below.    

```
L,E,G,B (or LEG-B)
Local, Enclosing, Global, Built-in
```

___
## Local Scope

Vars defined within a function.

___
## Enclosing Scope
Vars in local scope of _"enclosing"_ functions, that function within a function scenario.
>Use _nonlocal_ keyword to manipulate enforcing scopr variables.
```python
def outer():
    outer_x = "something"
    
    def inner():
        # Can still manipulate outer_x here, since it comes under 
        # enforcing scope, but it can also be done using:
        nonlocal x
```

___
## Global Scope
Vars defined at the top of the doc or defined global using the _"global"_ keywords.

### Modification of global variable
>This is done using _"global"_ keyword:   
```python
x = "something"

def some_func():
    global x
    x = "some_new_thing" #this will now overwrite global x
```
___
## Built-in
Pre-assigned scopes in python. Python searches here, when it cannot find stuff in global scope.
