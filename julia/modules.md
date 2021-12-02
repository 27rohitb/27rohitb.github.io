# Modules

Similar to python. One files containing everything; function, vars, etc for one type of entity.

## Key points:

```Modules``` and files ```<your file>.jl``` are two SEPERATE things. Modules, is like classes _without_ scopes or security. Here are the key points:
* Modules are a way to clean up ```namespaces```. Key things seperate, to avoid conflicts.
* One file can contain mutliple modules.
* Each module has its stuff (data, functions) which can either be brough into current namespace or used with the help of ```qualified name```.
* 

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
   
