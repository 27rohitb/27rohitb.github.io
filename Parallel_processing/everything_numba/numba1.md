# Notes from 20mins lecture (Basics)

## Few key points:   

* Compiling the jit function first time, takes A LOT of time. Subsequent runs are faster.
* If the return type, is a collection of elements with different data types, Numba will be SLOW.
* Generally, use ```njit```, or ```jit(nopython=true)```, mostly, DONT use ```jit```. (njit is basically jit with nopython).
* DONT use python list() , wiht numba, because it will use reflection() to figure out the datatype in the list, which takes a lot of time.
* Use ```vectorized()``` decorator for scalar computation.
* 
