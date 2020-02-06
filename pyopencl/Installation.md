# Installation

*pyCUDA on windows is a complete mess.*   

It requires:   
* Boost
* CUDA
* Numpy   
___   
### A simple guide:   

PyCUDA wiki has a simple windows installation guide step by step, for windows8, which might work Windows 10, if done correctly: [HERE](https://wiki.tiker.net/PyCuda/Installation/Windows)   
___

## Important points:   

### For Boost (windows)

* Precompiled Boost is available [here](https://sourceforge.net/projects/boost/files/boost/)
* Prebuild python.Boost is available [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#boost.python)
* For compiling *bjam* note that bjam = b2, which is included in the zip.

___
   
### For CUDA toolkit installation

* Download CUDA toolkit from [here](https://developer.nvidia.com/cuda-downloads).
* If CUDA needs to install *newer* geforce experience and driver, then DO IT, otherwise it will break cuda installation.   

___
### For pyCUDA:

* For official websites [Click Here](https://developer.nvidia.com/pycuda)
* For pre-build pycuda [Click Here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pycuda)

___
## Errors:

#### cl not found:
   
Stackoverflow link [here](https://stackoverflow.com/questions/8125826/error-compiling-cuda-from-command-prompt)
CL (x64) path for new Visual Studio 2019 Community edition is:   
```
nvcc fatal   : Cannot find compiler 'cl.exe' in PATH
64-BIT : C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.20.27508\bin\Hostx64\x64
```

#### Cannot find corecrt.h
   
Stackoverflow link [here](https://stackoverflow.com/questions/38290169/cannot-find-corecrt-h-universalcrt-includepath-is-wrong)
This was moved in Windows kit and needs to added to nvcc.profile file (include path)

```
Cannot find corecrt.h

Go to nvcc.profile file  located at: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\bin

Change the include line to: 
INCLUDES += "-I$(TOP)/include" "-I$(TOP)/include/cudart" "-IC:\Program Files (x86)\Windows Kits\10\Include\10.0.18362.0\ucrt" $(_SPACE_)
```

#### Cannot find nvcc compiler
Add it's path to environment variable. It is located at:
```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\bin
```
