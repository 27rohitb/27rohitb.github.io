# Notes from Scipy2019 Lec by Stan Siebert

## Random points:

* Mentioned about pypy.
* Floating points operations will give different results depending upon the order of in which the numbers are processed. This is
due to rounding off.
* ```Numpy Testing``` module has good fault tolerance functions.
* 

4 step process:

* Honest, self inventory. Then express your final goal, which should be feasible.
- Is it for scalability?
- Is it for faster processing? etc.

< Refer to Maslow's Hierarchy of Software Project Needs. (Its is nice triangle) >

* Measurement
- Unit tests are NOT performance test. Should design and have both.
- Get good with profiling tools like cProfile. This profile can be views through ```pstats``` module (CLI, hard to navigate)
or use ```snakeviz``` or for a function that class a lot of numpy functions: ```line_profiler```.
(Profiling is about finding which thing **actually** has the biggest impact, rather than assuming)

* Refactoring the Code.
- Options for introducing Numba into codebase:
* Replace code with Numba implementation.
* **Compile** functions **only when** Numba is present.
* Pick between different implementation of same function RC. 

## How Numba Works?   

* Numba does JIT compilation of individual or group of functions.
* Compilation: (what the code does) + (on what data type it works upon)
* Backend aka machine level code generation happens in LLVM lib.

* Numba does "unboxing"; remove python object bits from the given data.
* Actively swap the numpy builtin function with its own representation/fucntion for faster translation to machine code.

Basically, numba goes from Python to low level (LLVM) lang directly. NO C/C++ intermediate compilation etc.

## What Numba is NOT doing:

* It's not transalation of Cpython or Numpy...its literally replaces it, with faster machine convertible code.


## Dont use numba if:

* Entire program compilation
* Critical functions are already in C/C++.
* Any interfacting of code generation to C/C++.
