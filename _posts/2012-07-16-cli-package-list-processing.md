---
title: Some commandline package list processing
layout: post
tags: bash arch pacman
---

This seems to come up a lot for me. I'm sure I'm the only person in the world, though.

I have two problems:

1) Every now and then, I get the urge to reinstall (nearly) every package on my system

2) I've got a pile of explicitly installed packages which are not in the package repositories

The solution to problem number one under arch is a simple pacman -S $(pacman -Qq). Easy as.<br>
Of course, all of the packages from problem number two get in the way of this. There's no clear way around the problem, so here's some text processing fun:

{%highlight bash%}
# pacman -Qq > all
# pacman -Qm | cut -d\  -f 1 > bad
# grep -vf bad all > good
# pacman -S - < good
{%endhighlight%}