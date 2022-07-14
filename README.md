# Slackware build-install scripts for Gnome from Bob Funk`s work (https://github.com/0xBOBF/gnome-slackware-15.0)
These scripts are only for the Slackware64 15 (stable) version. 
Scripts using slpkg tool to build and install Gnome from Slackbuilds.org

Requires: slpkg 

## How to:

# STEP 0 
 Download zip file, unzip it and run these 2 scripts as root. 
 
 ```
./Gnome1-slpkg
./Gnome2-slpkg
```
 
 
 It will take some time to build packages...
 
# STEP 1
EDIT /etc/rc.d/rc.local 
and add these lines: 
```
 # Start avahidaemon
if [ -x /etc/rc.d/rc.avahidaemon ]; then
 /etc/rc.d/rc.avahidaemon start
fi
# Start avahidnsconfd
if [ -x /etc/rc.d/rc.avahidnsconfd ]; then
  /etc/rc.d/rc.avahidnsconfd start
fi
```
# STEP 2
EDIT /etc/rc.d/rc.local_shutdown (if not exist then create one)

Add these lines in this file if exist:

```
# Stop avahidnsconfd
if [ -x /etc/rc.d/rc.avahidnsconfd ]; then
  /etc/rc.d/rc.avahidnsconfd stop
fi
# Stop avahidaemon
if [ -x /etc/rc.d/rc.avahidaemon ]; then
  /etc/rc.d/rc.avahidaemon stop
fi
```

if not exist, then create it and add these lines to the empty file:

```
#!/bin/bash
#


# Stop avahidnsconfd
if [ -x /etc/rc.d/rc.avahidnsconfd ]; then
  /etc/rc.d/rc.avahidnsconfd stop
fi
# Stop avahidaemon
if [ -x /etc/rc.d/rc.avahidaemon ]; then
  /etc/rc.d/rc.avahidaemon stop
fi

```
then save it and command 

```
chmod +x /etc/rc.d/rc.local_shutdown
```

# STEP 3
EDIT /etc/rc.d/rc.4
and remove that -nodaemon option from gdm
your file should be like this:
```
if [ -x /usr/sbin/gdm ]; then
  exec /usr/sbin/gdm
fi
```

REBOOT and enjoy! 
