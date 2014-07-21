---
layout: post
tags: computing linux
title: Default X cursor
---

Once upon a time I opened `lxappearence` by accident, then suddenly my default X
cursor theme was changed to the only style I had installed, Adwantia,
and this theme is OK as such, but I really like the default X cursors.
But it was impossible to remove an assigned style, since there was only this one style to select in `lxappearence`.

So I was digging around, and eventually found that one has to delete
~/.icons/default/index.theme to remove the settings applied by
`lxappearence`.

The inverse of my problem,
<https://bbs.archlinux.org/viewtopic.php?pid=923253#p923253>
