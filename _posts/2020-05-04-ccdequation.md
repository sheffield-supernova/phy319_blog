---
layout: post
title:  "CCD Equation"
mathjax: true
date:   2020-05-04 09:00:00 +0000
categories: photometry
---

## What is gain?

The `gain` is a conversion factor between the charge in a pixel ($e^{-}$) and converts it to a number that is stored in a file.  The gain is expressed in units of $e^{-}$ per ADU.  The number that you measure using aperture photometry, by counting up the total number of counts inside the aperture, is in units of ADU.
Importantly, to evaluate the uncertainties correctly, in particular the Poisson statistics associated with the number of photons received, this must be done in units of electrons.

For a signal constituted of $n($e^{-})$, the corresponding uncertainty is $\Delta \left( n($e^{-})\right) = \sqrt{n($e^{-})}$.  From aperture photometry, you will have measured the number of counts $n(ADU)$.  This means:

$
\Delta \left( n(ADU) \right) = \frac{\Delta \left(n(e^{-}) \right)}{gain} = \frac{\sqrt{n(e^{-})}}{gain} = \sqrt\frac{{n(ADU)}}{gain}
$



## Photometry
