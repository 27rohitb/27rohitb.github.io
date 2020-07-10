# Qcodes Writing Instrument Driver CheatSheet

This guide by was written by Rohit B.@SQDLab (27rohitb@gmail.com), in July 2020.   

I am writing this while trying to make driver for Rigol DS5072, which is a AWG.

## There are 3 type of instruments in qcodes:

1. DLL based instruments [here](https://qcodes.github.io/Qcodes/examples/writing_drivers/Creating-Instrument-Drivers.html#DLL-based-instruments).
2. VISA instruments [here](https://qcodes.github.io/Qcodes/examples/writing_drivers/Creating-Instrument-Drivers.html#VisaInstrument:-Simple-example).
3. Manual instruments [here](https://qcodes.github.io/Qcodes/examples/writing_drivers/Creating-Instrument-Drivers.html#Manual-instruments).

I will be writing more in detail for VISA instruments, since the AWG programming is a VISA instruments.   

## Initialize VISA:

```python
from qcodes import VisaInstrument

class DG5072(VisaInstrument):

    def __init__(self, name, address, **kwargs):
        super().__init__(name, address, **kwargs)
```

## Additional essential components for a [Instrument](http://qcodes.github.io/Qcodes/api/instrument/index.html):

There are mainly 3 additional components in qcodes [here](http://qcodes.github.io/Qcodes/api/instrument/base.html#qcodes.instrument.base.InstrumentBase.add_parameter):

1. Parameters [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#module-qcodes.instrument.parameter)- these are values that you would like to set/get and **save**.
2. Functions - these are commands that perform some task, but we **dont** need to save their value.
3. Submodule - these kind of "mini"-instrument within a given instrument. (Could be virtual stuff for post processing)
4. Etc - E.g.: Instrument Channel

### For AWG: [Instrument Channel](http://qcodes.github.io/Qcodes/_modules/qcodes/instrument/channel.html#InstrumentChannel)

For instruments that have output channels like AWGs, qcodes has special module: ```qcodes.instrument.channel```, which contains all the info (parameters) etc for the given channel.
   
#### Writing a Instrument Channel Class:

```python
from qcodes.instrument.channel import InstrumentChannel, ChannelList

class RigolDS5072(InstrumentChannel):

    def __init__(self, parent, name, channel):
        super().__init__(parent, name)
```

Usually these Channels are added into main instrument using channellist in the init of the instrument. Like this:

```python
channels = ChannelList(self, "Channels", RigolDS5072)

for i in channel_number in range(1,3):
    channel = RigolDS5072Channel(self, "ch{}".format(channel_number), channel_number)
    channels.append(channel)

channel.lock()
self.add_submodule('channels',channels)
```

## Adding [parameters](http://qcodes.github.io/Qcodes/api/parameters/index.html):

By default Qcodes includes 3 type of parameters:

1. Default parameter (we get from ```self.add_parameter()```) which has the following input parameters:

Input parameter name | Detail
---------------------|--------
name                | Name of the parameter
instrument          | (optional) The instrument it is associated with
label               | (optional) axis label, when graphed
unit                | (optional) unit for this param
snapshot_get        | (optional) permission for update during snapshot
snapshot_value      | (optional) permission to store value in snapshot
snapshot_exclude    | (optional) permission to include it in snapshot
step                | (optional) max increment that can be done
scale               | (optional) scale to multiply by, before setting this
inter_delay         | (optional) min. time btw successive set
post_delay          | (optional) time to wait after setting 
val_mapping         | (optional) dict of type ```{data_val: inst_code}```
get_parser          | (optional) transform the data from get to final output
set_parser          | (optional) Transform the input value to some input code
vals                | (optional) set Validators from ```qcodes.utils.validators```
max_val_age         | (optional) max time after which the value is invalidated
initial_value       | (optional) set the default value for this param
docstring           | (optional) doc string for this param (not same as label)
metadata            | (optional) extra info to be included in JSON snapshot

2. Parameter With Setpoints [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#qcodes.instrument.parameter.ParameterWithSetpoints)   

This parameters has associated setpoints (a list of other parneters that describe values, name and units of the setpoint axis)   

3. Delegate parameter
4. Array Parameter [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#qcodes.instrument.parameter.ArrayParameter)
5. Multi Parameter [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#qcodes.instrument.parameter.MultiParameter)
6. Manual Parameter (No set/get function)
7. Scaled Parameter (to be used when scaling using different devices is required) (**NOT same as scale**) [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#qcodes.instrument.parameter.ScaledParameter)

**Note: Parameters can also be combined [here](http://qcodes.github.io/Qcodes/api/parameters/parameter.html#qcodes.instrument.parameter.combine) and [here](http://qcodes.github.io/Qcodes/api/parameters/group_parameter.html#module-qcodes.instrument.group_parameter)**   

Apart from the above parameter, user can make their own custom parameter by inheriting the ```python from qcodes import Parameter``` and **override** the ```get_raw()``` and ```set_raw()``` functions. 


## Adding Function:

It's documentation is not in the source code, but at ```<qcodes-installation>/qcodes/instruments/functions.py```
```python
self.add_function()
```

It has the following input parameters:

Input Parameter Name | Detail
---------------------|---------
name                | name of the function
instrument          | (optional) instrument it belongs to
call_cmd            | (optional) command to execute on the instrument
args                | (optional) list of ```Validators```
arg_parser          | (optional) function that transforms input to instrument input. **ONLY works if call_cmd is a string**
return_parser       | (optional) function to transform data to output
docstring           | (optional) docstring

## Adding Submodule

This equivalent of python functions but for the device.

```python
self.add_submodule(name, function)
```
