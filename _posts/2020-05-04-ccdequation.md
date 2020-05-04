---
layout: post
title:  "CCD Equation"
date:   2020-05-03 09:00:00 +0000
categories: photometry
---
{%- include mathjax.html -%}


## What is gain?

The `gain` is a conversion factor between the charge in a pixel and converts it to a number that is stored in a file.  The gain is expressed in units of $e^{-}$ per ADU.  The number that you measure using aperture photometry, by counting up the total number of counts inside the aperture, is in units of "Analog-to-Digital Units" (ADU). Importantly, to evaluate the uncertainties correctly, in particular the Poisson statistics associated with the number of photons received, this must be done in units of electrons.

If the numnber of "counts" measured for a source, with a given aperture, is $n(ADU)$, this corresponds to $n(e^{-}) = n(ADU) \times gain$ electrons.  The uncertainty, due to shot noise (or Poisson noise), is **not** the same in ADU and electrons.

The standard uncertainty in electrons is:

$
\Delta \left(n(e^{-})\right) = \sqrt{\left(n(e^{-})\right)}
$

such that, in ADU:

$
\Delta \left(n(ADU) \right) = \frac{\Delta \left(n(e^{-})\right)}{gain} = \sqrt{\frac{n(ADU)}{gain}}
$



## Photometry
