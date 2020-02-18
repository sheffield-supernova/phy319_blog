---
layout: post
title:  "Running astropy"
date:   2020-02-17 12:52:16 +0000
categories: astropy
---

On the astrolab system, you should be able to access python through two mechanisms:
either through a jupyter notebook or through writing a text file (using a simple
text editor like `nano`).  It should be possible to invoke the jupyter notebook using the command 
`jupyter notebook`.   From the command line, you can run a python script (let's
call it `test.py`), by running:
{% highlight bash %}
> python3 test.py
{% endhighlight %}

For both the command line version and using [jupyter
notebook](https://www.dataquest.io/blog/jupyter-notebook-tutorial/) it is
important to invoke python3' (In
the notebook this will appear as an option in the dropdown meny "kernel").  This is the
latest standard and `astropy`, `ccdproc` and `photutils` are designed to work with it.

At the very beginning of your script (or code block in your notebook), start with
invoking the necessary modules.

{% highlight python %}
import astropy
{% endhighlight %}

If you run a test script just containing this line (or a single code block in a
  jupyter notebook) there should be no output if `astropy` is installed and working correctly.
  If it's not working correctly, you will know by the large number of error messages!
