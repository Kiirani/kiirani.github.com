---
title: bad comments are bad
layout: post
---

My local apache install has some issues. For one thing, it's completely ignoring everything I put in .htaccess.

My first mistake was going into my main configuration to try and track this down.<br>
My second mistake was reading the comments I've left in this file.

I think it might be time to consider reconfiguring apache.

{%highlight bash%}
# Wtf? This is redundant..

# This is going to get in the way in later life :)

# For compatibility with my old setup
# Needs to be changed lol

# Icons for apache generated pages. Should be replaced soon

# For the love of god, turn this down after use

# Rewrite rules SHOULD go into .htaccess files, but nvm for now

# Commented until I can migrate script to modern python

# Should php ever break...

# More magic?

# Indexes are globally disabled, but oh well, need to configure somewhere.
{%endhighlight%}