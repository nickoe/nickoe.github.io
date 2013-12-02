---
layout: default
tags: linux xorg
---

It seems that it is problematic on linux (here tested with Ubuntu) to
be able to use the brightness control keys on a laptop with the nvidia
drivers and nvidia/intel setups.

Only Nvidia
-----------
First of all, to enable brightness contol with a nvidia only graphics
card, it is possible to add the following option to
`/etc/X11/xorg.conf.d` somewhere. For example if there already is one file
named `/etc/X11/xorg.conf.d/15-nvidia.conf`. Then all you need to do
is to append the option:

	Option "RegistryDwords" "EnableBrightnessControl=1"

Nvidia and Intel
----------------
In the case of combined graphics where you have an Intel and an
Nvidia card (using bumblebee), there is has been observed that it is
required to inform grub2 about it, and not nessesary to add the above
option to xorg.

This is taken from [askubuntu]. Run the following command in terminal:

	gksu gedit /etc/default/grub

then change

	GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
	GRUB_CMDLINE_LINUX=""

to

	GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_backlight=vendor"
	GRUB_CMDLINE_LINUX="acpi_osi=Linux"

then save and run:

	sudo update-grub 

and then restart the system for changes to take effect.

It might not be nessesary to add the i`acpi_osi` option though. (Not
tested.)


[askubuntu]: http://askubuntu.com/questions/128463/how-to-control-brightness
