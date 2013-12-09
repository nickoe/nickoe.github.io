---
layout: post
title: FTP Keep-alive
tags: linux workaround
---

An annoyance when using FTP some times is that the server terminates
the connection after some timeout. This happens even if you have a
remote file open in an editor (like `gedit`), and then you try to
save, and the save fails because of the connections is not up.

To workaround this problem, the following script can be run to keep
the connection alive. No more timeout problems, yay.

{% include pathorcmd.html param="ftp-keepalive.sh" %}
	#!/bin/bash
	while true 
	  do
	    ls /run/user/`id -u`/gvfs/* &> /dev/null
	  sleep 42
	done

I just had this script laying around, but don't remember my source,
but there are numerous of this, more or less the same on the web. I
likely got it from one of them using 45 as the sleep timer -- though I
like 42 better.
