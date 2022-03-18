# Troubleshooting_on_lab
The most common problems and their solutions on UBUNTU


**PROBLEM 1: NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver**

Solution 1:

	1. sudo apt install --reinstall gcc
	2. sudo apt-get --purge -y remove 'nvidia*'
	3. sudo apt install nvidia-driver-450 
	4. sudo reboot

Solution 2 (Automatic Install using PPA repository to install Nvidia Beta drivers):

	#add the ppa:graphics-drivers/ppa repository into your system
	1. sudo add-apt-repository ppa:graphics-drivers/ppa
	#identify your graphic card model and recommended driver: 
	2. ubuntu-drivers devices
	#install Nvidia DriverSame as with the above standard Ubuntu repository example, either #install all recommended drivers automatically: 
	3. sudo ubuntu-drivers autoinstall
	#or selectively using the apt command. Example: 
	4. sudo apt install nvidia-driver-470
	5. sudo reboot

**PROBLEM 2: HOW TO HIDE MOUNTED DRIVES ON THE UBUNTU DOCK**

Solution:

	- open a terminal and type "gsettings set org.gnome.shell.extensions.dash-to-dock show-mounts false" for hide
	- open a terminal and type "gsettings set org.gnome.shell.extensions.dash-to-dock show-mounts true" for show
	
**PROBLEM 3: RECOVERING JOURNAL UBUNTU**

Solution:
	Lets first check your file system for errors.

	To check the file system on your Ubuntu partition...

	    - boot to the GRUB menu
	    - choose Advanced Options
	    - choose Recovery mode
	    - choose Root access
	    - at the # prompt, type sudo fsck -f /
	    - repeat the fsck command if there were errors
	    - type reboot

	If for some reason you can't do the above...

	    - boot to a Ubuntu Live DVD/USB
	    - start gparted and determine which /dev/sdaX is your Ubuntu EXT4 partition
	    - quit gparted
	    - open a terminal window
	    - type sudo fsck -f /dev/sdaX # replacing X with the number you found earlier
	    - repeat the fsck command if there were errors
	    - type reboot
	
**PROBLEM 4: UBUNTU LIMPISH ANYDESK INSTALLING BUT NOT OPENING**

Solution:

	- sudo apt install libpangox-1.0-0

**PROBLEM 5: UBUNTU (>18 versions) ANYDESK SMALL BLACK SCREEN PROBLEM**

Solution:
	
	Basically install a dummy driverfor creating a virtual dummy monitor as described here:

	- sudo apt-get install xserver-xorg-video-dummy

	Then write it in the /usr/share/X11/xorg.conf.d/xorg.conf (or possibly /etc/X11/xorg.conf) file (create one, if it does not exist):

	```shell
	Section "Device"
	    Identifier  "Configured Video Device"
	    Driver      "dummy"
	EndSection

	Section "Monitor"
	    Identifier  "Configured Monitor"
	    HorizSync 31.5-48.5
	    VertRefresh 50-70
	EndSection

	Section "Screen"
	    Identifier  "Default Screen"
	    Monitor     "Configured Monitor"
	    Device      "Configured Video Device"
	    DefaultDepth 24
	    SubSection "Display"
	    Depth 24
	    Modes "1024x800"
	    EndSubSection
	EndSection
	```
	- Then restart the computer.
	