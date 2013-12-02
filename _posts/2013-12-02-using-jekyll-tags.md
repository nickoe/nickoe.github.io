---
layout: post
tags: jekyll computing
---

This is a description of my adventure in using tagging in [Jekyll].

I had a need or want to use the tags on my posts, and present them on
my site. This was a hard maneouvere if you search google for ways of
doing it. Most of what can be found is plugins that needs to be run,
which is not run on i.e. github pages. So I wanted something built in
in Jekyll. 

On my endeavour on searching on google, I found [Sjösten] which did
kind of what I needed to do. It motivated me, while I had almost given
up. The problem with his approach was that he only listed the tag
(which I was also able to at the time), but not the seperate URLs for
each posting in the tag/catagory.

I started playing around, with theese [Liquid] format thingies, but it
was hard to get anything usefull out of that and filters. I tried
several approaches to get the paths, nothing really worked out well. 

Then I jumped on to #jekyll@irc.freenode.net, where two guys was
gentle enough to help me out. Theese was `gregkare` and `jaybe`. They
tried to make and example for me both of them at the same time. They
basically ended out with the same. Below is my version of that, merely
with some more HTML added to render it like I wanted.

{% raw %}
	{% for tag in site.tags %}
	<p><a id="{{ tag[0] }}"><h3>{{ tag[0] }}</h3></a></p>
	<ul>
	  {% for post in site.posts %}
			{% if post.tags contains tag[0] %}
			<li>
				<a href="{{ post.url }}">{{ post.title }}</a>
			</li>
			{% endif %}
		{% endfor %}
	</ul>
	{% endfor %}
{% endraw %}

##### End Note
When messing about with `jekyll serve --watch`, Jekyll seems to not
auto refresh, if it has failed in parsing Liquid code. So here one
have to ctrl+c jekyll and start it again.

[Jekyll]: http://jekyllrb.com/
[Sjösten]: http://vvv.tobiassjosten.net/jekyll/jekyll-tag-cloud/
[Liquid]: http://liquidmarkup.org/
