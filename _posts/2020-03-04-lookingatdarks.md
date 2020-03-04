---
layout: post
title:  "Processing dark images"
date:   2020-03-04 09:00:00 +0000
categories: astropy
---
With master bias frames constructed for each detector/binning configuration it
is possible to proceed to the next stage of the reduction.  As with the bias
images, which are dependent on the readout properties of the detector, the dark
frames describe how the detector responds to *thermal noise* as a function of
time.  The accrued *dark* signal does not depend on the detector actually being
exposed to light.  In your batch of data you will find there are multiple dark
images for each detector/binning cofiguration.  As with the biases, it will be
important to group these images depending on that configuration.  As with all
the other calibration and the science images, the first thing to do is subtract
the bias level, for which you have already constructed a master bias image.

Following from the recipe for reading in the individual bias images, the first thing
to do is read in a list of the dark images (for a given detector configuration)
using `CCDData.read(filename, unit='adu')`,  and store the data in a list.

You will then need to read in the single *master bias* image for that
configuration.

The set of dark images can then have the bias levels removed using:

{% highlight python %}
dark_biassub = ccdproc.subtract_bias(darklist, master_bias)
#where darklist is the list of dark data and
#master_bias is the master bias frame for that detector
#configuration
{% endhighlight %}

You can then construct a master dark frame using `ccdproc.combine`, just as you did
with the bias images.