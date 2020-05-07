---
layout: post
title:  "CCD photometry 3"
date:   2020-05-03 09:00:00 +0000
categories: photometry
---
{%- include mathjax.html -%}

For a given star $i$, the _instrumental magnitude_ in some filter $X$ is $m^{inst}_{i}(X) = -2.5\log10(n(ADU))$.  This needs to be placed on the proper magnitude scale.  It is important to note that this magnitude does not take into account a number of factors (including the size of the aperture).  Because these are factors, and the magnitude scale is logarithmic, we can find a magnitude offset that will shift our instrumental magnitude onto the proper magnitude scale.  Using Aladin, we can identify stars whose brightness has already been measured and placed on the proper scale; for star $i$ let's call this $m^{cat}_{i}(X)$.  For all stars in the field with instrumental and catalogue magnitudes we wish to determine $ m^{inst}_{i}(X) - m^{cat}_{i}(X)$ - which means we can place our photometry of sources not in the catalogue, i.e. the supernova, on the right magnitude scale.  Using multiple stars in the field around the SN, we can calculate the average "zeropoint correction" from a plot like this:

![image]({{site.baseurl}}/assets/img/magcorr.png)

This is the correction you can apply to your photometry of the SN, in instrumental magnitudes, to determine its brightness on the standard magnitude system.
