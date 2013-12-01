---
layout: default
title: LaTeX error with double definition of \iint
---
Suddenly when I was trying to compile an old (not more that a few months old) document, I got the following error:

	! LaTeX Error: Command \iint already defined.
				Or name \end... illegal, see p.192 of the manual.

	See the LaTeX manual or LaTeX Companion for explanation.
	Type  H   for immediate help.
	...                                              
                                                  
	l.506 ...d{\iint}{\DOTSI\protect\MultiIntegral{2}}

This error was possibly caused be an update to my TexLive distribution (2012.28273), but a fellow called YoungFrog on #latex@irc.freenode.net, told me that I could fix it by adding a optional option for the package wasysym, called nointegrals so I did that and it actually fixed the error. So this is how I include the package now:

	\usepackage[nointegrals]{wasysym}


