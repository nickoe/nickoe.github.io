---
style: post
title: Including git hash in C
tag: programming git
---

Sometimes when generating embedded software (written in C), one often
embed version and build date. I have found it usefull to also embed
the VCS revision, here done with the git hash. This is done by making
`make` fetch the HEAD version.

	GITCOMMIT= -D'__GIT_COMMIT__="$(shell git rev-parse HEAD)"'

and add the variable to the `CFLAGS`

	CFLAGS=$(GITCOMMIT)

Then to access this information in your .c-file just construct the
array, which can be used to print the hash.

	char gitcommit[sizeof(__GIT_COMMIT__)] = __GIT_COMMIT__; 

