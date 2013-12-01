---
layout: default
---

I usually shutsdown my computer with poweroff, whereby I do not have
to wait for stuff to close, wich I like. I will not shutdown unless I
have saved relevant work. Since I use the browser a lot, I have set it
to autostart, but every single time booted my box it started firefox
with the "Well, this is embarrassing." wee all know. Therefore I
wanted Firefox to auto restore the tabs instead of manually clicking
the "Restore" button. The solution I found via the friendly people at
irc.mozilla.org #fx-team suggested I could use a pref parameter
(whatever that is) which is found in the about:config page.

So the solution was to change the
"browser.sessionstore.max_resumed_crashes" to a high number,
preffearbly a number larger that the number of tabs you would have
auto restored.

This could impose a problem if you have many tabs open, that could
make you browser crash, but this can also be solved. You could do;
options -> general -> don't load tabs until selected.
