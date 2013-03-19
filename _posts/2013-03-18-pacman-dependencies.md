---
title: (pacman) resolving missing dependencies
layout: post
tags: bash arch pacman 
---

I was in dependency hell on my last system update. I'm impatient, so I resolve dependency hell by bypassing dependency checks altogether.

Having successfully run `pacman -Sudd`, I'm now stuck with some missing dependencies and a major headache every time I try to run things... Yay!

The official way to search your Arch system for missing dependencies is the `testdb` command. 

`testdb` is useless for piping into pacman: it doesn't have any special piped output, nor does it have a linear option like pactree (&hearts; pactree -l). 

The resulting output is a mess of human readableness

	missing dependency for blender : openshadinglanguage
	missing dependency for gnome-settings-daemon : ibus
	missing dependency for lib32-mesa : lib32-libdrm
	missing dependency for lib32-mesa : lib32-systemd
	missing dependency for libpurple : farstream-0.1
	missing dependency for mga-dri : mesa-libgl
	missing dependency for openimageio : intel-tbb
	missing dependency for workrave : gtkmm3
	missing dependency for workrave : python2-cheetah


Fortunately this is pretty easily cleaned up with a little bit of commandline magic 
We can cut this at ":", grab the second half, and then trim off the leading whitespace.

{% highlight bash %}
# testdb | cut -d: -f2 | sed s"/ //g"  
openshadinglanguage
ibus
lib32-libdrm
lib32-systemd
farstream-0.1
mesa-libgl
intel-tbb
gtkmm3
python2-cheetah
{% endhighlight %}

This list can then be piped into pacman :
{% highlight bash %}
# testdb | cut -d: -f2 | sed s"/ //g" | pacman -S -
{% endhighlight %}
<br><br>
But for me, this doesn't end here.

The reason I ran an -Sdd in the first place was I have some weird dependency conflicts between mesa-libgl and my nvidia drivers, and I can't be bothered fixing those right now. 

I could do a basic `| grep -v "mesa-libgl"`, but I thought it would be nice to go through each package and check that it and its dependencies won't cause me any problems

{% highlight bash %}
for line in `testdb | cut -d: -f2 | sed s"/ //g"`; do 
    pacman -S $line
done;
{% endhighlight %}
<br><br>
Okay, so, I'm still left in dependency hell with libgl, but most of my system functions and my bash-fu is stronger.
