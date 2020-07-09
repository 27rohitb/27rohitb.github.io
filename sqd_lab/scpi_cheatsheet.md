# SCPI CheatSheet

This cheatsheet was written by Rohit B.@SQDLab, July 2020.
   
## Language help
The following points were taken from DG5000 programming guide for this language:  

* Has **hirerachial tree structure**
* root word + multiple sub-keywords
* Either write **complete** keyword or **only** capital part.

## Convention used for DS5072 prograaming guide:

Symbols | Meaning | Example
--------|---------|---------
```:``` | command start/seperator | ```:DISPlay:SAVer```
```?``` | given command is query | ```:DISPlay:SAVer:STATe?```
```,``` | seprator for multiple paramteres in single command | ```:MMEMory:COPY <dir_name>,<file_name>```
|
--------- |**Following symbols are NOT of SCPI but used by RIGOL** |---------
|
```{}``` | Optional Parameter, executed **iff** it is set | ```:DATA VOLATILE <val>{,<val>}```
```|``` | Seperate different choices(parameters) for given command | ```:DISPlay:BRIGHtness <brightness>|MINimum|MAXimum```
```<>``` | Given parameter **MUST** be replaced by an effective value | ```:DISPlay:BRIGHtness 10```
```[]``` | Given **keyword** is optional and **will** be executed regardless of its mention | ```[:SOURce<n>]:MOD[STATe]?```
   
## Input Parameters types:

Parameter Name | Example
---------------|--------
Bool | ```ON|OFF```
Keyword | ```MAXimum|MINimum```
Consecutive real numbers (default accuracy is upto 6 digits) | ```:MOD:AM:DEPTh<depth>|MIN|MAX``` depth = any real number between 0-120
Dicrete | ```:SOURce<n>``` n = 1 or 2
ASCII Char String | ```:MDIRrectory <dir_name>```

# DS5072 Specific Subsystems:

Following (root)command system(subsystem) are present:

* ```COUPling```
* ```DIGItal```
* ```DISPlay```
* ```MMEMory```
* ```OUTPut```
* ```SOURce```
* ```SYSTem```
* ```TRACe```
