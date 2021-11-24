# Unit checking!

Following packages are used:
* Unitful

#### Attaching units to any quantity:
```julia
# METHOD 1: use '*u"<units>"'
a = 9.18*u"m/s^2"

# METHOD 2:
v0 = 5u"m/s"
```

#### Displaying unit
Normal ```print``` function will display them

#### Converting unit
```julia
uconvert(u"yr", t1)
# unconvert(<convert to>, <given param>)
```

#### Expanding constants to normal units:
```julia
h = 10*u"\hbar"
println(h)
```

#### Look at Dimensions:
```julia
print(typeof(h))
```

#### View in SI units:
```julia
print(upreferred(h))
```
   
**NOTE** _Default_ value of ```upreferred``` function is SI units, but it can changed to CGS as follows:
```julia
using Unitful
Unitful.preferunits(u"cm,g,s"...)
```
