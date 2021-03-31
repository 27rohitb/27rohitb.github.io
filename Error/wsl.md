# Error Related to WSl

## Error in name resolution:

https://github.com/microsoft/WSL/issues/5256

```
Incredibly unhelpful.

It is the issue for many people, it is the same in issue trackers/forums/etc across the internet.

The WSL instance cannot resolve domain names. Editing resolv.conf to point to a functioning nameserver "works" for the duration of the session, but as soon as the distro is rebooted resolv.conf is regenerated using WSL's original template. Because etc/resolv.conf is actually a symlink to run/resolvconf/resolv.conf

Steps that have worked for me:

Boot your distro.
cd ~/../../etc
Create wsl.conf, however you see fit. sudo vim wsl.conf, sudo touch wsl.conf and edit it later, whatever.
Add these lines to wsl.conf:
[network]
generateResolvConf=false
exit or in Windows cmd wsl --terminate [YourDistroName]
Boot your distro.
At this point, thanks to wsl.conf, run/resolvconf should no longer exist and will never be created again.

cd ~/../../etc
sudo rm resolv.conf - this deletes the existing symlink file.
Create a new resolv.conf, however you see fit. sudo vim resolv.conf, sudo touch resolv.conf and edit it later, whatever.
Add this line to resolv.conf:
nameserver 8.8.8.8
replace 8.8.8.8 with your preferred functional nameserver.
exit or in Windows cmd wsl --terminate [YourDistroName]
wsl --shutdown just to be sure that you've definitely killed everything.
Boot your distro.
Confirm that your resolv.conf changes are still in effect, or just ping a domain name and cry tears of joy after struggling to get this working for far too fucking long.
```
