---
layout: post
tags: linux
---

If you are looking for a way to change the file encoding on a file in
Linux, you have arrived at the right place. First you should check
what exactly the encoding is on the file that is to be converted.

	file --mime-encoding foo.html

To finally convert the file a little tool called iconv can be used. We
have to specify the original encoding and our desired encoding, and
iconv will print it to stdout, wich we will redirect to a new file,
and then move to the old file.

	iconv --from-code=ISO-8859-1 --to-code=UTF-8 ./foo.html > ./bar.html
	mv ./bar.html ./foo.html

Now the file has been converted.
