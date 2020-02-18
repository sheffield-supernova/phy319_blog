---
layout: post
title:  "Linux commands"
date:   2020-02-17 12:52:16 +0000
categories: linux commands
---
Most of the work you will need to do can be done in a jupyter notebook, but for
locating and moving data it will be important to interact with the shell through
the command prompt.  There are some common and very useful commands that can
help you navigate the file system, and some examples are given here:

{% highlight bash %}
> ls #list all the files
> ls -ltr #lists all the files (l) in reverse (r) time (t) order
> mv filea.fits fileb.fits #renames filea.fits to fileb.fits
> pwd #find out which directory you're in
> cd dir_a #move down to a sub directory called dir_a
> cd .. #move back up to the original directory
{% endhighlight %}

Sometimes it might be necessary to access a file (such as the .jnl files that
come with your pt5m observations).  You can skim through the contents of the
text file using:

{% highlight bash %}
> more test_file_name.jnl
{% endhighlight %}

and use the space bar to work through the length of the file.

It may even be necessary to directly edit a text file, and there is a
rudimentary text editor called `nano` available:

{% highlight bash %}
> nano test_file_name.jnl
{% endhighlight %}

which can be very powerful (instructions for its use are in a helpful menubar
running along the bottom of the screen after you have invoked the editor).
