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
## Errors for pyCUDA:

**Initially try installing pycuda; should work.**

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

___
## Errors for pyOpenCL:

Steps for pyopencl2019:
   
1. Download source
2. Download wheel for pybind11 > Install it.
3. Now build and install pyopencl

___

There are a lot of Visual Studio 14 or 2008 C++ compiler or windows.h or other files which were available natively in Visual studio or windows were moved when Microsoft decided to "re-organize" its internal libraries. So, **DO NOT** do directly installation of pyOpenCL from ```pip install```.
   
Instead use the method mentioned at wiki tinkere: [here](https://wiki.tiker.net/PyOpenCL/Installation/Windows) .
    
For editing siteconf.py, use the following include/lib directories:
```
CL_INC_DIR = ['C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.2\\include','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\ucrt','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\um','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\shared']

CL_LIB_DIR = ['C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.2\\lib\\x64','C:\\Program Files (x86)\\Windows Kits\\10\\Lib\\10.0.18362.0\\ucrt\\x64','C:\\Program Files (x86)\\Windows Kits\\10\\Lib\\10.0.18362.0\\um\\x64']
```

#### fatal error LNK1158: cannot run 'rc.exe' :    

The answer from stackoverflow suggest to copy some files, [Here](https://stackoverflow.com/questions/14372706/visual-studio-cant-build-due-to-rc-exe) , which worked for me.
