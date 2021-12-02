# Modules

Similar to python. One files containing everything; function, vars, etc for one type of entity.

## Key points:

```Modules``` and files ```<your file>.jl``` are two SEPERATE things. Modules, is like classes _without_ scopes or security. Here are the key points:
* Modules are a way to clean up ```namespaces```. Key things seperate, to avoid conflicts.
* One file can contain mutliple modules.
* Each module has its stuff (data, functions) which can either be brough into current namespace or used with the help of ```qualified name```.
* There are two ways to "use" a modules: ```using``` and ```import```.
* ```using``` imports everything (data + functions) everything into current namespace and make the modules name as "qualified name" (something that can be used with "." to access modules stuff.
* ```import``` only imports whatever is mentioned in ```export``` statement of module you are importing.
* both ```using``` and ```import``` can be used with "as xyz", which will make "xyz" as a qualified alias.

### Help sources:

From [Here](https://discourse.julialang.org/t/difference-between-include-use-and-import/65918/2)
```
include is used for including the content of a file into your current program. It has per se nothing to do with modules or namespaces. using and import on the other hand have nothing to do with files, and deal exclusively with modules/namespaces.

```
   
**Julia Docs links:**
* [Modules, namepsace and using](https://docs.julialang.org/en/v1/manual/modules/)
* [Code loading](https://docs.julialang.org/en/v1/manual/code-loading/)
   
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
   
