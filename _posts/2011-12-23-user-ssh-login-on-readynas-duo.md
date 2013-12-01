---
layout: post
title: User SSH login on Readynas Duo
---

The ReadyNAS Duo i a two bay NAS machine from Netgear. To gain SSH
login access you have to install the `EnableRootSSH_1.0-x86.bin` from
Netgear. Now it should be possible to login with the root user.

Now to make a regular user login you have to either edit
`/etc/passwd` manually for the user or simply use usermod.

When using usermod:

	usermod -s /bin/bash john

Or manually edit the `/etc/passwd` file, you have to change
`/bin/false` to `/bin/bash` on the line with the desired username.

