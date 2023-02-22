# Alienware x14 Keyboard Backlight

This is my attempt to contribute [AlienFX](https://github.com/trackmastersteve/alienfx/blob/master/CONTRIBUTING.md).   

* I ran `lsusb` to get the following:
* ```bash Bus 004 Device 002: ID 0bda:0328 Realtek Semiconductor Corp. USB3.0-CRW
  Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
  Bus 003 Device 009: ID 2148:7022  USB2.0 HUB
  Bus 003 Device 004: ID 0c45:673b Microdia Integrated_Webcam_HD
  Bus 003 Device 003: ID 187c:0550 Alienware Corporation LED controller
  Bus 003 Device 002: ID 0d62:3740 Darfon Electronics Corp. 
  Bus 003 Device 006: ID 8087:0033 Intel Corp. 
  Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
  Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
  Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub```

* This showed the PID:VID (product ID: Vendor ID) for the my alienware keyboard controller which, in my case is:
* `Bus 003 Device 003: ID 187c:0550 Alienware Corporation LED controller`

* I came accross a windows alternative for Alienware Command Center, which mentions a controller for [Alienware x17 R5 with same controller](https://github.com/rsm-gh/akbl/blob/stable/usr/share/doc/AKBL/BusData/Data/Alienware17%20R5). This was to confirm and understand that this device could be interfaced using some kinda of python wrapper over USB library in linux, conincidentally which is what AlienFX project seems to do. Now I just need to understand how the device operaters, so i can modify the following: 
  * [cmdpacket](https://github.com/trackmastersteve/alienfx/blob/master/alienfx/core/cmdpacket.py) 
  * [USBdriver](https://github.com/trackmastersteve/alienfx/blob/master/alienfx/core/usbdriver.py)
  * Potentially change other files if required.

* AInspired from Alienware x15 R5 post from earlier, i realised i should read more about USB descriptors and found the following resources:
  *   https://www.slashdev.ca/2010/05/08/get-usb-report-descriptor-with-linux/
  *   Interfacing with HID device: https://raspberrypi.stackexchange.com/questions/3465/usb-hid-device-only-firing-1-event
  *   _Report Descrriptor was missing, but after a bit of googling i found that we need to unbind and then report descriptor shows up._

* Ultimately i decided to dig deeper and properly learn about USB interfacing, from following sources:
  *   https://www.beyondlogic.org/usbnutshell/usb5.shtml
  *   

