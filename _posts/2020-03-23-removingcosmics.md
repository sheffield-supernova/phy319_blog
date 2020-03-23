---
layout: post
title:  "Removing cosmics rays"
date:   2020-03-23 09:00:00 +0000
categories: astropy
---

In order to check the alignment of images, we need to remove any residual signatures
due to cosmic rays or hot pixels.  The alignment algorithm relies on recalibrating the
World Coordinate System (WCS) for the images, and that means it has to be able to
match bonafide stars with the stars that appear in a catalogue - this means removing spurious
signals due to things like cosmic rays (that will appear in the images as obvious
non-stellar sources - quite different to the stars you can see in the image and the
supernova itself) that will prohibit a good alignment solution.

For each science image, you will need to apply the `lacosmic` routine that scans the
images looking for obvious non-stellar sources and removes them from the images.  
You can find more information on `lacosmic` [here](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.cosmicray_lacosmic.html).
If you have a reduced (bias subtracted, dark subtracted and flat-field corrected) science image
called `file.fits`, you can apply `lacosmic` by:

{% highlight python %}
inscifile = CCDData.read("file.fits", unit='adu')
oscifile = ccdproc.cosmicray_lacosmic(inscifile, sigclip=5, gain_apply=False)
{% endhighlight %}
(the parameter `sigclip` dictates most of the behaviour of `lacosmic`, but as you can see
from the [function webpage](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.cosmicray_lacosmic.html)
there are plenty of other parameters that can be tweaked).

If you plot up the image before and after correction for cosmic rays, you will see
that some of the bright, non-stellar sources are removed and the image looks much
smoother.


(* note *: the alignment step itself is not something you will be asked to do yourselves,
but removal of non-stellar cosmic ray sources is an important step to facilitate
a good alignment solution)
