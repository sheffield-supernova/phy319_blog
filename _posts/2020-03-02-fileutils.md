---
layout: post
title:  "Moving files around in python"
date:   2020-03-02 09:00:00 +0000
categories: astropy
---

If you are doing a lot of work in python, especially on files that you are
modifying using your script, it may be important to make new versions of files
or backups of older files.  It can be quite tedious doing this by hand in a
terminal window, but it is possible to automate this within your python script
using `shutil`.  More information about this module can be found at [this
page](https://docs.python.org/3/library/shutil.html).  This module can be
invoked using:

{% highlight python %}
import shutil
{% endhighlight %}

Perhaps the most useful function in `shutil` is the `copy` function:

{% highlight python %}
filea = 'firstfile.fits' #name of a pre-existing fits file
fileb = 'secondfile.fits'
shutil.copy(filea, fileb) #create "fileb.fits" which is a copy of filea
{% endhighlight %}

Placed inside a loop, this can be a quick, efficient and powerful way to make backups of
the original data as you process them.
