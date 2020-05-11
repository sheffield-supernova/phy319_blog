---
layout: post
title:  "CCD photometry 4"
date:   2020-05-03 09:00:00 +0000
categories: photometry
---
{%- include mathjax.html -%}

# Deriving the luminosity

If you have photometry of your supernova for each filter, calibrated against the APASS catalogue, you should be able to calculate absolute magnitudes (i.e. corrected for the distance and extinction).  This corresponds to the brightness of the supernova if it were located at 10pc.   For each filter, you can calculate the corresponding **flux density** of the supernova, at the _effective wavelength_ of the filter by looking up the properties of the filters [here](http://svo2.cab.inta-csic.es/theory/fps/index.php?mode=browse&gname=Misc&gname2=APASS).  Note the zeropoint is defined relative to Vega, in units called _Janskys_, but the website provides a handy conversion formula:

$
F_{0,\nu}(Jy) = (2.9979246)^{-1} \times 10^{5} \lambda_{eff}^{2} F_{0,\lambda}(\mathrm{ergs\,s^{-1}\,cm^{-2}\AA^{-1}})
$

You will need to derive $F_{0,\lambda}(\mathrm{ergs\,s^{-1}\,cm^{-2}\AA^{-1}})$ for your filters (for Vega, defined as magnitude zero), and then calculate the corresponding flux densities for your SN from the absolute magnitudes that you have derived.

To calculate the apparent luminosity, you will then need to integrate (think of the Trapezium rule) over the spectral energy distribution (for which you have photometry at four discrete wavelengths).  This will allow you to derive the _flux_ in units of $\mathrm{ergs\,s^{-1}\,cm^{-2}}$.

![image]({{site.baseurl}}/assets/img/sed_int.png)

To get the luminosity you will then need to remember that this is luminosity of the SN as measured per $\mathrm{cm^{2}}$ at a distance of 10pc - i.e. smeared out over a total area of $4\pi \times (10pc)$.  What is 10pc in units of $cm$?
