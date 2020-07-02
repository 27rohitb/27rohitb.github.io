# Documentation for M4iprocessorGPU (m4idigi) module.    

This python module is used to operate the Spectrum M4i.4450-x8 in conjuction with GPU for data processing. Hence, it uses Spectrum module present at : ```<qcodes-installation path>\Qcodes\qcodes\instrument_drivers\Spectrum``` for controlling the card and ADGprocessorGPU module present at ```<qcodes-installation path>\Qcodes\qcodes\instrument_drivers\sqdlab``` for data processing.   

This class was designed to combined the digitizer card and GPU data processing in one module. Hence it requires 2 key components:

1. The Spectrum M4i driver and card installed.
2. Any OpenCL compatible device, python 3.3< version < 3.7 , other version might cause compatibility issues with pyopencl_.py module present in ```Qcodes/qcodes/instrument_drivers/sqdlab/dsp``` since newer python versions have ```async``` as keyword, the new keyword that replaces this is ```async_```. This fix will **only** be required when upgrading python version in the future.

___

# Index:

The document is divided into 3 parts:
   
A. Software & Driver Installation.   
B. Tutorial on M4iprocessorGPU (+Errors).   
C. Tips on adding acquisition device in Qcodes + UQTools for future.   

   
___
# Part A: Software & Driver Installation
  
## Installation 

**You MUST HAVE admin privilege for the system you would like to install the drivers on.**   

This documentation assumes the following:   

1. Qcodes & UQTools have been downloaded from the [SQDLab Github](http://github.com/sqdlab) and installed in C:/User/Experiment/Qcodes and uqtools respectively.

2. The M4i card has been plugged in the PCI-E slot (x16 (Gen2 or above)) and at least one OpenCL computer device is present in the system.

  
For the rest of the tutorial, it is assumed that the card installed is **Spectrum M4i.4450-x8** and OpenCL device is **Nvidia RTX** graphics card, on **windows 10**.

___
### Part 1: Installing Spectrum M4i 4450-x8 card drivers.

1. Go to <https://spectrum-instrumentation.com/en/m4i4450-x8>
2. Click on _Download_ tab. 
3. Goto _WINDOWS Drivers + Software_ section and download and install the following files:  
* ```spcm_drv_install_x.xx.xxxxx.exe``` ```M2i/M3i/M4i/M4x/M2p/DN2/DN6 driver for Windows 7, 8, 10 (32/64 bit)```
* ```spcmcontrol_install64bit.exe``` ```Spectrum Control Center (64-bit) / Windows 7, 8, 10```
* ```specdigitizer.msi``` ```IVI Driver for IVI Digitizer class (32 bit)```
* ```sbench6_64bit_vx.x.xxxxxxxxx.exe``` ```SBench 6 (64-bit) Installer / Windows 7, 8, 10```

Installing the above setup will install the required driver for the card and also install _Spectrum Control Center_ which can be used to test the card for errors and update its firmware. Along with it, it will also install _SBench_ which is a GUI which can be used to control the card and analyse the data.

___
### Part 2: Installing & configuring PyOpenCL and CUDA.

#### Install CUDA:

1. Download and install from <https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exelocal>

#### Compile and Install PyOpenCL

There are a lot of Visual Studio 14 or 2008 C++ compiler or windows.h or other files which were available natively in Visual studio or windows and were moved when Microsoft decided to "re-organize" its internal libraries. So, **DO NOT do direct install**  from ```pip```.

To give an overview:

1. Download and install Visual Studio & other additional library for compiling pyopencl.
2. Download source
3. Download wheel for pybind11 > Install it.
4. Now build and install pyopencl

Use the method mentioned at wiki tinkere: [here](https://wiki.tiker.net/PyOpenCL/Installation/Windows) to compile pyopencl from source.

If the Wiki Tinkere's ```siteconf.py```does not work use the following include/lib directories:
   
```
CL_INC_DIR = ['C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.2\\include','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\ucrt','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\um','C:\\Program Files (x86)\\Windows Kits\\10\\Include\\10.0.18362.0\\shared']

CL_LIB_DIR = ['C:\\Program Files\\NVIDIA GPU Computing Toolkit\\CUDA\\v10.2\\lib\\x64','C:\\Program Files (x86)\\Windows Kits\\10\\Lib\\10.0.18362.0\\ucrt\\x64','C:\\Program Files (x86)\\Windows Kits\\10\\Lib\\10.0.18362.0\\um\\x64']
```

#### Common Error:

* ```fatal error LNK1158: cannot run 'rc.exe'```. Following stackoverflow answer [HERE](https://stackoverflow.com/questions/14372706/visual-studio-cant-build-due-to-rc-exe) worked at the time of writing this documentation.

___
# Part B: Tutorial on M4iprocessorGPU (+Errors)

## Modes Operations:

The device is currently configured to have 2 modes of operation:  

1. Normal Trigger based acquisition mode.   

Works exactly like fpga. Total samples, averages and segments can be configured. Device has some limit on the maximum number of sample * segments (also known as blocksize) that can be captured in one acquisition, due to card's memory limit of 4GB, and GPU's Memory limit of 8GB.

2. Singleshot acquisition mode.

In this mode, the averaging is not done and data is returned as it is.The data shape is: (iterations, segments, samples, channels).
   
___
## Creating object:   

It can either be directly imported from Qcodes:
```python
from qcodes.instrument_drivers.sqdlab.M4iprocessorGPU import M4iprocessorGPU

m4idigi = M4iprocessorGPU("digi")
```
    
Or it can be loaded from the station:   
**Please make sure it is present in the station yaml with proper name**   
```python
import qcodes 
station = qcodes.Station(config_file=r'C:/code_win/test_files/Spectrum/new_rack.yaml')
qcodes.config.current_config['user']['station'] = station
# m4idigi to acquire and process data
m4idigi = station.load_m4idigi()
```
___
## Information & Parameters:    

There are 2 key component whose parameters can configured:   

* Digitizer (refereed to as 'digi')
* Data-processing (refereed to as 'processor')

Both of the above mentioned component can be created outside of the M4iprocessorGPU object and passed to the object at the time of initialization, the keyword for which are 'digi' and 'processor' respectively. Note that, as of now the digitizer and the processor **must** be object of class ```M4i``` and ```TvModeGPU``` respectively. If no digitizer or processor is passed
,by default the ```check_digi()``` and ```check_processor()``` function will try to initialize and M4i object and a TvModeGPU object with default parameters.   
   
___
## List of User-settable parameters:

### IF-Frequency :   
It can be set in the following range: 0 - 250MHz . Please note that setting IF-Frequency too off from the input signal can lead to unexpected result!!! ' (**revision required**)   
```python
m4idigi.if_freq(25e-6)
```   

### Decimation:
It must be an integer. 1 usually means no decimation.   
```python
m4idigi.decimation(1)
```

### FIR-coefficients:
By default these are set using ```scipy.signal.firwin()```. But it can also be passed by the user. Usually ```np.array([1,])``` means no filtering.   
```python
m4idigi.fir()
```

### Samples:
Number of samples **MUST** be a power of 2, otherwise card _might_ through an error(More info is mentioned in the Errors and Information section).
The number of sample **must** be in range: 2**5 to 2**17 .   
```python
m4idigi.samples(2**10)
```   

### Averages:
These are the number of blocks acquired. Note that more the number of averages, more is the time required to do the given measurement. Increasing averages increases the quality of data captured.  
```python
m4idigi.averages(2**10)
```
   
### Segments:
This can be set in the following range: 1 to 2**17, Setting it to '0' (zero), enabled autosegmentation. 
**Please note** When 1 Channel is enabled, card looks for sequence start marker on digital channel 'X0'. **All other digital channels (X1, X2) must be terminated!!**   
If both Channel are being used to capture, card looks for sequence start markers on digital Channel 'X2'. **X1 must be terminated!!**
```python
m4idigi.segments(1)
```

### Sampling Rate
It must be 500M/2**n, and can range from 500MHz to 976.562KHz. Any other value is set to closest approximation of the previous equation.   
```python
m4idigi.sample_rate(500e-6)
```   

### Channels
Card has two channels, both of them will be sampled at the rate given by the user.
```python
m4idigi.channels(1)
```
___
## Output data:

### Power Spectral Density
It does PSD on the data returned by the processor.
```python
data = m4idigi.psd()
```

### FFT
This will return the data with fft and shift. PLease use this function to get data with FFT. Note that this function behaves similar to context and restores the "enable_fft" parameter value after just before returning.
```python
data = m4idigi.fft()
```

### Raw Data with Averaging (Analog)

This is use to get processed data from the card, in the shape (segments, samples, channel). It is analogous to 'voltages' used in FPGA
```python
data = m4idigi.analog()
```

### Single Shot data
This can **only** be used in single-shot mode. It returns data of shape (iterations, segments, samples, channels). Please Note: since there is no averaging, this data can be huge!.
```python
data = m4idigi.singleshot_analog()
```

### Single Shot with Time Integration (on GPU)
This feature enable time integration of single shot data on gpu. The shape of data returned is: (iterations, segments, channels).
```python
data = m4idigi.time_integrated_singleshot_analog()
```
___
## Sample Code:

### Using the module directly
```python
# Import module
from qcodes.instrument_drivers.sqdlab.M4iprocessorGPU import M4iprocessorGPU

# Create object
new_digi = M4iprocessorGPU("one")

# Set required parameters for measurement
new_digi.segments(1)  
new_digi.averages(2**10)
new_digi.samples(2**10)

data = new_digi.analog()
```

### Using context library
```python

# C object
from qcodes.instrument_drivers.sqdlab.M4iprocessorGPU import M4iprocessorGPU
m4idigi = M4iprocessorGPU("digi")

# Define acquisition length lambda function
if 'fpga' in globals():
    acq_duration_get_cmd = lambda: 10e-9*fpga.tv_samples.get()*fpga.tv_decimation.get() if fpga.app.get() == b'tvmodev02' else None
elif 'm4idigi' in globals():
    acq_duration_get_cmd = lambda: m4idigi.samples.get()/m4idigi._digi.sample_rate.get()
else:
    acq_duration_get_cmd = None

# Create TvMode Measurement:
tv = uq.DigiTvModeMeasurement(m4idigi, data_save=True)

tv_int = uq.Integrate(tv,
                     tv.coordinates['sample'], average=True)

tv_av = uq.Integrate(uq.DigiTvModeMeasurement(m4idigi, data_save=False),
                     tv.coordinates['sample'], average=True)

# Import Contexts:
%run -Gi "Z:/DataAnalysis/Notebooks/Tools/Tools.ipynb"
%run -i -G "Z:/DataAnalysis/Notebooks/qcodes/Setup/000 Setup.ipynb"

# Additional context if required :
def ctx_set_tv_samples(tv_samples):
    return RevertInstrument(m4idigi, 'digi_tv_samples', tv_samples)
def ctx_set_tv_samples_by_time(time):
    return RevertInstrument(m4idigi, 'digi_tv_samples', round(time*m4idigi.sample_rate.get()))

# Single Shot context if required:
# TvMode without averaging. Returns the same as TvMode but with an extra dimension for iterations.
tv_ss = uq.DigiTvModeMeasurement(m4idigi, singleshot=True, data_save=True)
# Time integrated tv_ss (singleshot). Currently uses uqtools and saves both time domain and time integrated files.
tv_ss_int = uq.Integrate(tv_ss, tv_ss.coordinates['sample'], average=True)

``` 
___
## Error & mitigation:

### Error Table 
Due to digitizer and GPU having limited memory , and being linked by PCI-E connection, creates some limitation on the amount of data that can be handled by each component.
Following are the error and the reason for each, along with the possible solution.

No. |Error | Reason | Fix
----|------|---------|-----
1 | ```The length of the fir filter window must be less than or equal to the number of samples per acquisition ``` | The FIR filter length (length of coefficients) **must** be equal to of greater than length of acquisition (number of points in one sample). | Try increasing the number of samples or decreasing the filter length.
2 | ```Number of acquisitions must be greater than or equal to 16.``` | Total number of samples to be captured (number of samples per acquisition * total segments) is less than 16. | Try increasing number of samples of number of segments.
3 | ```The number of segments does not fit in 1 block of GPU processing. Reduce number of segments or samples.``` | Total number of samples to be captured (number of samples per acquisition * total segments) is greater than 2^18. | Try reducing number of samples per acquisition or segments.
4 | ```Check if the sequence start trigger is connected and is arriving after the acquisition trigger``` | Card is unable to capture the sequence start trigger on digital port (X0 for 1 channel and X0 & X2 bot 2 channel) | Try placing the sequence start trigger within the acquisition time using oscilloscope (don't be lazy.)
5 | ```No synchronization marker received``` | Same as error #4 , card is unable to detect sequence start trigger. | Try to put the marker at the start of acquisition.
6 | ```The card raised an exception. It may be locked. Try getting the error``` | Some error had occurred in the card during previous run, which needs to be read. | Run the following line ```m4idigi._digi.get_error_info32bit(verbose=True)``` to get the error and unlock the card.
7 | ```Invalid Blocksize``` | Either the number total number of acquisitions (number of samples per acquisition * number of segments) are too large(2^18) or too small(2^5). | Try increasing or decreasing the number of samples of segments.

### Card Freezing:
   
If the **_Card never capture the data, just keep running until interrupted_**. It can happened due to following reasons :

1. Acquisition Start trigger might not be received by the card. In this case card wait for the trigger, which might not be programmed correctly or wire might not be connected.  

2. Clock signal might not be connected.   

3. The total number of samples might be > 2**17, which can cause the GPU to stall, please reduce the samples or segments.

___      
# Part C: Helpful points for adding future acquisition devices to existing software stack(Qcodes+UqTools):   

* Context Library was modified to make it work with existing Jupyter Notebooks, that is, context such as ```ctx_tv_samples, ctx_tv_segments, ctx_tv_averages```, works out of the box now.
* FPGA module in UQTools has been modified to add ```DigiTvModeMeasurement```, uqtools alternative to fpga class (TvModeMeasurement).
* **Please note** averaging is done by default on the GPU, when digitizer is used.
* TimingConfig was made compatible with digitizer, so it shows the acquisition time correctly, using the following code:

```python
if 'fpga' in globals():
    acq_duration_get_cmd = lambda: 10e-9*fpga.tv_samples.get()*fpga.tv_decimation.get() if fpga.app.get() == b'tvmodev02' else None
elif 'm4idigi' in globals():
    acq_duration_get_cmd = lambda: m4idigi.samples.get()/m4idigi._digi.sample_rate.get()
else:
    acq_duration_get_cmd = None
```   
