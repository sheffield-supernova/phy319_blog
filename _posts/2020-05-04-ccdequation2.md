---
layout: post
title:  "CCD photometry 2"
date:   2020-05-03 09:00:00 +0000
categories: photometry
---
{%- include mathjax.html -%}


By now, you should have photometry for sources in your images: the SN and some of the surrounding stars.  The photometry should consist of the counts accumulated in the circular aperture and the counts for the background.  The calculation of the background-corrected source flux has been dealt with in an earlier post.  These can be corrected to instrumental magnitudes, using the standard photometric equation for "Pogson" magnitudes.

Using differential photometry, we can compare the known magnitudes for the surroundings to calculate the *zeropoint* for our observations and calculate the actual magnitude for our SN.  A useful photometric catalogue is the [APASS: The AAVSO Photometric All-Sky Survey](https://www.aavso.org/apass).  This catalogue can be conveniently accessed through the [Aladin Sky Atlas](https://aladin.u-strasbg.fr/).  Below is an image showing a galaxy, with the APASS catalogue loaded (the catalogue can be located by searching for it in the bottom left hand text box - highlighted in the yellow box) and stars, with measured photometry in the APASS catalogue, appear on the image highlighted by red boxes.  Clicking on these boxes yields their photometry (and other things measured by the survey) in the middle panel below the loaded image (as highlighted in the image below).

![image]({{site.baseurl}}/assets/img/aladin_picture.png)
