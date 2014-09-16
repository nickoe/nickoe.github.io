---
layout: post
tags: computing linux IRC
title: Running Quassel core in chroot under android
---

This post describes how to get Archlinux ARM into a chroot on an
android smartphone device (or really any device), tested on a HTC
Wildfore S (running Marvellous CM10), with an ARMv6. This approach
uses the ARMv5TE image from arhlinuxarm.org. The apporach on chrooting
described in [this forum post][1] is the basis for this post. There
was some smaller errors in the original post that was not corrected.
Hence i write my own version of this, with the addition on how to get
a Quassel core running. Initial testing with just one channel, it
seems to work pretty well.

## Setting up the Archlinux chroot
First thing you need to do is to make sure your phone is rooted, then
install [BusyBox] from google play, and optionally grab some app to
get a sshd running, I used [SSH Server].

	su # Allow it on the screen
	cd /sdcard
	mkdir arch
	dd if=/dev/zero of=alarm.img seek=1549999999 bs=1 count=1 #1550MB	image file
	mke2fs -F alarm.img
	mknod /dev/loop1 b 7 0
	losetup /dev/loop1 alarm.img
	mount -t ext2 /dev/loop1 arch/
	cd arch
	wget http://archlinuxarm.org/os/ArchLinuxARM-armv5te-latest.tar.gz
	tar xzf ArchLinuxARM-armv5te-*.tar.gz
	rm ArchLinuxARM-armv5te-*.tar.gz
	mount -o bind /dev/ /sdcard/arm/dev
	chroot . /bin/bash
	rm /etc/resolv.conf
	echo "nameserver 8.8.8.8" > /etc/resolv.conf
	mount -t proc proc /proc
	mount -t sysfs sysfs /sys
	pacman -Syu # upgrades...

Subsequently it should be enough to run theese commands.

	su
	cd /sdcard
	mknod /dev/loop1 b 7 0
	losetup /dev/loop1 alarm.img
	mount -t ext2 /dev/loop1 arch/
	cd arch
	mount -o bind /dev/ /sdcard/arch/dev
	chroot . /bin/bash
	mount -t proc proc /proc
	mount -t sysfs sysfs /sys

Noting that I also set the CPU govenor to performance and a max
frequency of 787 MHz, anything above that seemed to freeze the device
suddenly.

## Setting up Quassel core
Install Quassel core with `pacman -S quassel-core`. The we need to
generate a SSL certificate.

	openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout	~/.config/quassel-irc.org/quasselCert.pem -out ~/.config/quassel-irc.org/quasselCert.pem

Now we can run the quassel core.

	quassel-core

Then you sould connect with a quassel client, this will allow you to
setup your user on the core.

To be able to run the core when you are not connected to the device
for persistence, you need to run it ins a screen session or similar.
That is a bit difficult. TODO describe a working method for this.

## End notes and trouble shooting tips
Leaving the chroot

	exit
	losetup -d /dev/loop1

If there are problems with using the loopback device, try creating
another, e.g. `mknod /dev/loop7 b 7 7` and use `/dev/loop7` instead.

[1]: http://archlinuxarm.org/forum/viewtopic.php?f=27&t=1361
[Busybox]: https://play.google.com/store/apps/details?id=stericson.busybox
[SSH Server]: https://play.google.com/store/apps/details?id=com.icecoldapps.sshserver
