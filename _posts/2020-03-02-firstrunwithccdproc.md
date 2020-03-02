---
layout: post
title:  "First look at ccdproc"
date:   2020-03-02 11:00:00 +0000
categories: astropy
---

Having sorted your data, based on criteria of the type of observation and the
instrumental configuration, one can start by looking at the lowest rung of the
data reduction ladder: bias subtraction.

For each detector configuration (primarily binning), pt5m should acquired a set
of bias frames (usually 5 for each binning).  Each one of these will be subject
to uncertainty due to the readout noise, which means to create an accurate
template for the bias levels that affects all the images (later calibration and
the science observations) we need to create a *master bias* image, using the bias
frames acquired.  This is simply an average of all the bias frames.  This can be
made using `ccdproc`.  Let us suppose you have a list of all the fits files
corresponding to the bias frames for a given detector configuration (i.e.
binning), called `filelist`.  This can be ingested into `ccdproc` as:

{% highlight python %}
import numpy as np #make sure have loaded the necessary modules
import ccdproc
from astropy.nddata import CCDData
from astropy.stats import mad_std
from astropy.io import fits

biasfiles = [] #empty list to contain data readin by CCDData
with open('filelist') as f: #open file containing list of bias files
  for line in f: #read through the file
    filename = line.rstrip('\n') #temporary variable to hold filename
    biasfiles.append(CCDData.read(filename, unit='adu'))#units of images are adu
    #read in data from bias image and add to a list containing all the data
    #added so far
f.close() #close filelist

combined_bias = ccdproc.combine(biasfiles,
                             method='average',
                             sigma_clip=True, sigma_clip_low_thresh=5, sigma_clip_high_thresh=5,
                             sigma_clip_func=np.ma.median, sigma_clip_dev_func=mad_std,
                             mem_limit=350e6
                            )

combined_bias.meta['combined'] = True
combined_bias.write('combined_bias.fits')

{% endhighlight%}

If you compare the master bias image with the individual images (e.g. using
`ds9`), you should notice that the master frame should look a bit smoother than
the individual frames, but the overall count levels (at any given location)
should be approximately similar for the two images.
