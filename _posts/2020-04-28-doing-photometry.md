---
layout: post
title:  "Doing photometry"
date:   2020-04-27 09:00:00 +0000
categories: photometry
---
By now you should have a list of the `x` and `y` coordinates of stars in your image (in a list called `positions`).  
Now we wish to measure the number of counts for your target supernova and for the surrounding stars.  To do this we
are going to conduct _aperture photometry_.  A helpful guide for doing aperture photometry (although
  written for the `iraf` environment - but the underlying principles are the same) can be found [here](https://www.mn.uio.no/astro/english/services/it/help/visualization/iraf/daophot2.pdf).

As before, we need to invoke the [`photutils` package](https://photutils.readthedocs.io/en/stable/):
{% highlight python %}
import photutils
from photutils import datasets, aperture_photometry, CircularAperture, CircularAnnulus
from astropy.io import fits, ascii
{% endhighlight %}

Now you have to define some apertures.  A relatively straightforward way to handle this is to define a
variable called (something like) `aprad` which will hold the radius of the aperture, which is usually set to the same as the FWHM.  From here, it is them straightforward to define a _circular_ aperture for measuring the brightness of the source and, at a large distance from the source, an _annulus_ aperture for measuring the sky background contribution.
{% highlight python %}
#aperture for the source
aper = CircularAperture(positions, r = aprad)
#here you need the positions you derived in the previous step

#here define a sky annulus, centred on the source, but to look at the level
#of counts at a large radius from the source (which will be our measure of the
#background contribution).

#set the inner and outer radii of the sky annulus to some large values (here 2 and 3)
skyann = CircularAnnulus(positions, r_in = 2.0 * aprad, r_out = 3.0 * aprad)
#create a combined list of both apertures
apertures = [aper, skyann]
#Do photometry of the image (note this is the actual image data)
phot_table = aperture_photometry(image, apertures, method = 'exact')
{% endhighlight %}

There are some useful attributes for apertures you have defined, but perhaps one of the most important is the `area` (gives the area of the aperture in pixels units).  In the table `phot_table` you can access some useful properties of the photometry for each star - where `aperture_sum_0` is the sum of the counts in circular aperture (i.e. the first aperture in the list `apertures`), while `aperture_sum_1` is the sum of the counts in the annulus (the second aperture in the list `apertures`).

{% highlight python %}
#to get mean background in the annulus per pixel
bkg_mean = phot_table['aperture_sum_1']/skyann.area
#total counts divided by area
#calculate the total number of counts due to the sky in the circular aperture
bkg_sum = bkg_mean * aper.area
#list of background subtracted counts for each source
obj_counts = phot_table['aperture_sum_0'] - bkg_sum
{% endhiglight %}
