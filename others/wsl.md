# WSL stuff

This page contains frequently used command or instructions that might come in handy for using, setting up or in general dealing with WSL in window.   

___
## Installing WSL2:

This has been mostly copied from microsoft's [website](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps), but it's a simplified version:   
   
#### Requirenment:   

* You WILL need to open powershell with admin permissions.
* For x64 systems: Version 1903 or higher, with Build 18362 or higher.
* For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.   
   
#### Check windows build no.

* Start+I
* System
* About \-\> Version \& OS Build

#### Enable WSL:
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
      
#### Enable VM:
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
   
#### Download Linux kernel package:

[Cick Here](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) to download.
   
#### Set WSL2 as default:
```
wsl --set-default-version 2
```
   
#### Install Ubunut

Open Microsoft store , search ```Ubunutu``` and install whatever version you want, 20.04 or 18.04.
   
___
## MOVE WSL Location

This is take from [this answer](https://superuser.com/questions/1550622/move-wsl2-file-system-to-another-drive).   
   
It's a 4 step process:   

#### Export:
```
mkdir D:\backup   
wsl --export Ubuntu D:\backup\ubuntu.tar
```

#### Unregister:
```
wsl --unregister Ubuntu
```
    
#### Import:    
```
 mkdir D:\wsl   
 wsl --import Ubuntu D:\wsl\ D:\backup\ubuntu.tar
 ```
    
 #### Register the old user:
 ```
 cd %userprofile%\AppData\Local\Microsoft\WindowsApps   
 ubuntu config --default-user <username>
 ```
 
