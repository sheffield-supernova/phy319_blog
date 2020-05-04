---
layout: post
title:  "CCD Equation I"
date:   2020-05-03 09:00:00 +0000
categories: photometry
---
{%- include mathjax.html -%}


## What is the `gain`?

The `gain` is a conversion factor between the charge in a pixel and the number that is stored in a file to represent the data.  The gain is expressed in units of $e^{-}$ per ADU.  The number that you measure using aperture photometry, by counting up the total number of counts inside the aperture, is in units of "Analog-Digital Units" (ADU). Importantly, to evaluate the uncertainties correctly, in particular the Poisson statistics associated with the number of photons received, this must be done in units of electrons.

If the number of "counts" measured for a source, with a given aperture, is $n(ADU)$, this corresponds to $n(e^{-}) = n(ADU) \times gain$ electrons.  The uncertainty, due to shot noise (or Poisson noise), is **not** the same in ADU and electrons.

The standard uncertainty in electrons is:

$
\Delta \left(n(e^{-})\right) = \sqrt{\left(n(e^{-})\right)}
$

such that, in ADU:

$
\Delta \left(n(ADU) \right) = \frac{\Delta \left(n(e^{-})\right)}{gain} = \sqrt{\frac{n(ADU)}{gain}}
$

Do not forget that the readnoise is, generally, quoted in terms of $e^{-}$.


## Image combination

If you have multiple images that you have combined in some way, the method by which you have combined them will affect the statistics of images and how you can calculate uncertainties:

### Summations

Adding the images together, increases the number of counts (or electrons) from the source, in effect giving a total exposure time $ t_{TOT} = \sum^{N}_{i} t_{i} $

(if there are $ N $ images, of duration $ t_{i} $).  If the images are taken with an identical readout, then the effective gain of the combined image is the _same_ as for the individual images.  There is, however, a price to pay for having multiple readouts: the total readnoise per pixel is increased $R_{TOT} = \sqrt{N}R_{i}$.

### Averages
If we take an average, then for each pixel in the input images, with counts in ADU of $n_{i}(ADU)$, we are calculating the mean:

$
\overline{n(ADU)} = \frac{\sum^{N}_{i}n_{i}(ADU)}{N}
$

$
= \frac{\sum^{N}_{i}n_{i}(e^{-})}{N \times gain}
$

So the effective gain of the averaged image is $N \times gain$.  The final read noise for an averaged frame becomes $R_{TOT} = \frac{R_{i}}{\sqrt{N}}$.
