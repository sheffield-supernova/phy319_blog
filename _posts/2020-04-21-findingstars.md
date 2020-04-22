---
layout: post
title:  "Finding stars"
date:   2020-04-21 09:00:00 +0000
categories: photometry
---

In attempting to conduct aperture photometry, the first stage is to find the stars that
you want to do photometry on.  For this we will use a number of helper functions available through
the `photutils` package.

{% highlight python %}
import numpy as np
import astropy
import photutils
from photutils import datasets, DAOStarFinder, IRAFStarFinder
{% endhighlight %}

The first thing to assess is what constitutes a real signal.  The stars (and galaxies) appear to sit
on top of a relatively smooth background.  To identify a star or supernova, we have to ask how significant is the stellar flux above
any statistical fluctuations in the background. Fortunately, the finder algorithms available through `photutils` can handle this.  If we read in an image called "image_file.fits", into an array called `ximage`, we can run:

{% highlight python %}
hdu = fits.open("image_file.fits")
ximage = hdu[0].data.astype(float) #Read in the actual image and put in the ximage variable
ximage -= np.mean(ximage) #subject off the mean background level
#create a DAOStarFinder object called daofind
daofind = DAOStarFinder(fwhm = 4.0, threshold = 10.0,
                       sharplo = -4.0, sharphi = 4.0,
                       roundlo = -4.0, roundhi = 4.0)
sources = daofind.find_stars(ximage)
{% endhighlight %}
`fwhm` is the Full Width at Half-maximum of the point spread function for the observations (likely to be different for each reduced/combined image).  This can be estimated using `iraf`, but by zooming in on the images using `ds9` you can make a reasonable guess at this value by eye.  The `threshold` keyword specifies how far above the background fluctuations, in units of standard deviations, a source has to be for it to be considered a significant detection.  Because we're interested in bright, well detected sources this can be set to a high number.  The other values used in setting up the DAOStarFinder object are to do with the shape of the Point Spread Function - and using the values shown above should be suitably permissive for the quality of the images you are using.

The coordinates for the sources detected in the image by the `DAOStarFinder` algorithm are stored in the `sources` array (which is a slightly annoying table format that is used by `astropy`).  The positions you will want to use are the Cartesian `centroid` positions, i.e. the `x` and `y` pixel locations.

{% highlight python %}
#this is just a housekeeping step
for col in sources.colnames:
    sources[col].info.format = '%.8g'  # make the precision quoted in the table consistent
#extract the actual x and y centroid positions
positions = (sources['xcentroid'], sources['ycentroid'])
{% endhighlight %}

You should be able to pull the `x, y` positions from this list (of two lists) and plot the positions of the detected sources on top of your fits images in a `matplotlib` plot.  Are you seeing objects you clearly think look like stars?  If there are too many sources, some which look to be marginal detections, you should consider increasing the value of the `threshold` parameter; conversely, if only one or two of the brightest sources are detected you should decrease the value assigned to `threshold`.
