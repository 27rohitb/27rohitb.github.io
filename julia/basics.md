# Basics

### Datatypes:
   
Quick 4:   
* ```Int/Float/Real/Complex 8/32/64```
* Same as above but **"Big"** with _Arbitrary Precision_
* ```String``` **is different** than ```Char```

### NOTE:

* There are **NO** ":" like python
* Every block (function/if-else/etc) **MUST** have and ```end``` keyword
* **!** after a function, means that fucntions is editing the given variable
* Array are stored in **Column major** aka *fortran style* format; accessing them is same, each row of given column is displayed first.
* Array _index start_ **at 1**
* For **element-wise** operation use ```.``` dot=operator with ```+ - /```.

#### Determine type
```julia
typeof()
```
   
### String functions:
Essentially its a **container** of chars.

#### Concatenate any number of strings
```julia
a * b
```
   
### if-else
```julia
if (x > 0) && (y > 0)
   println("x AND Y is positive")
elseif (x < 0) || (y <0)
   println("x OR y is NEG")
else
   println("x is NOT positive")
end
```
   
* **SHORTCIRCUITING** : If multiple if-else statements are true, it will just execute the first one and _exit the block_.
   
### Ternary Operator:
```
x <conditional operation> ? <TRUE clause> : <FALSE clause>
x > 0 ? println("is POS") : println("not positive")
```
