---
layout: post
tags: computing linux
title: Default X cursor
---

One I opened lxappearence by accident, then suddenly my default X
cursor theme was changed to the onlu style I had instlaled, Adwantia,
and this theme is OK as such, but I really like the default cursors.
But it was impossible to remove an assigned style, it can only be
chagend by lxappearence.

So I was digging around, and eventually found that one has to delete
~/.icons/default/index.theme to remove the settings applied by
lxappearence.

The inverse of my problem,
https://bbs.archlinux.org/viewtopic.php?pid=923253#p923253
