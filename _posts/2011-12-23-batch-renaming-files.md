---
layout: post
tags: notes bash
---

It could be desired to rename files that does not contain a suffix,
while the front of the filename i to be removed. This can be done in
	bash. To rename files like: file.php?id=123 to 123.jpg

	for f in *; do mv $f ${f#file.php?id=}.jpg ; done
