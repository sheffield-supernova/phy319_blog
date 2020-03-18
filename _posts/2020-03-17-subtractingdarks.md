---
layout: post
title:  "Subtracting dark images"
date:   2020-03-17 09:00:00 +0000
categories: astropy
---
If you have produced a master dark image, a combination of the individual bias-subtracted
dark exposures (using the `average` method), you are now ready to process images in the
next stage of the calibration chain.  Moving to the flats, taken with the 1x1 binning
configuration, you need to gather the appropriate masterbias and masterdark frames.
As with the individual darks, you will need to subtract the masterbias from the individual flat field images.
You are then ready to subtract the masterdark from the flat field images - but it's important to note the exposure times
of the masterdark image (which should be an average of the exposures times of all the individual dark images) and the exposure time of the individual flat fields.  These will be different.

You then need to employ the task `subtract_dark`, for which more information can be found [here](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.subtract_dark.html).


To subtract the master dark image `masterdark`, with exposure time 60s, from an individual flat field image called `flat` that has an exposure time of 2s (note these are just dummy values for illustration), we will ask `subtract_dark` to scale the counts in `masterdark` to match the exposure time of the flat field.

{% highlight python %}
darksub = ccdproc.subtract_dark(flat, masterdark, dark_exposure = 60.0*u.s, data_exposure = 2.0*u.s, scale = True, exposure_unit='adu')
{% endhighlight %}

In this example we have explicitly defined the exposure times of the dark (`dark_exposure`) and the data to be corrected (`data_exposure`).  The value `scale = True` tells `subtract_dark` to scale the dark counts in each pixel from the exposure time of the dark to the exposure time of the flat.

As the pt5m data have set header keywords for all exposures (irrespective of the type of the exposure - e.g. bias, flat, dark or science) we can instead, leaving out the `dark_exposure` and `data_exposure` variables, just say `exposure_time = "EXPTIME"`, where `EXPTIME` is just the header keyword in all pt5m FITS files for the exposure time.
