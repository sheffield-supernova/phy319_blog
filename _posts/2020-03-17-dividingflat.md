---
layout: post
title:  "Dividing by a flat"
date:   2020-03-17 12:00:00 +0000
categories: astropy
---
By now, you should be able to start looking at your science images (which were acquired with 2x2 binning).
In hand you should have:
1. master bias frame for 2x2 configuration
2. master dark frame for 2x2 configuration
3. a master flat frame for each filter (in 1x1 binning)

## Rebinning the flat
The flat-fields were acquired with 1x1 binning, which means you have to rebin the
flat field images to match the 2x2 configuration of the science images. To rebin
you need to employ `ccdproc`'s `rebin` function, for which more information can
be found [here](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.rebin.html).

You can find the dimensions to which you have to rescale the size of the master flat images
by looking at the size of the 2x2 images, taking those dimensions and using them with `rebin`.
If the 2x2 images have dimensions `nx` by `ny`, you can rescale the flat_1x1 to produce a
flat-field of half the size (flat_2x2), in each direction, by running:

{% highlight python %}
flat_2x2 = rebin(flat_1x1, (nx,ny))
{% endhighlight %}

## Dividing by the flat
For each science frame, of a given filter, you should then be able to apply the calibrations
in turn:
1. bias subtraction using `subtract_bias`
2. dark subtraction using `subtract_dark`
3. Division by the flat field using
{% highlight python %}
sci_reduced = ccdproc.flat_correct(sci_biasdarksub, flat_2x2)
{% endhighlight %}

This should leave you with completely reduced science images and the next step will be to combine them.
You may wish to plot them, using matplotlib in your jupyter notebook (don't forget, after running, `import matplotlib as plt` to insert the line `%matplolib inline` to ensure the figures are plotted correctly in the notebook). 
