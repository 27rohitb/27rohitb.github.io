# Modules

Similar to python. One files containing everything; function, vars, etc for one type of entity.

### Creating modules:
```julia
module <mod_name>
  #
  # body
  #
end
```

### Including & USING modules:
```julia
include("<mod_FILE_name>.jl")

# 2 different ways to use it
using .<mod_name>
include .<mod2_name>

<var> = <mod_name>.<whatever>
```
   
**Additionally:**   ```using``` includes ```export``` related content of modules into current namespace; i.e no "." required, just use that var or function natively. as if it were present in current file.
   
