---
layout: post
title:  "Reading a fits file"
date:   2020-02-19 11:00:00 +0000
categories: astropy
---

If you are working from a jupyter notebook, you should be able to see in the top
left-hand corner the location the notebook currently thinks it's in *relative to
your home directory*.  
<img src="../img/jupyter_loc.png">
i.e. in this image, the notebook is working in the home directory (confusingly
represented by a single `/`).
If you want to access a specific file, you will need to define it in its current
location relative to where the notebook is currently working from or change the
notebook's working location.
For the sake of this example, I've got the data for SN 2020ue (located in a
directory `2020ue` in my home directory), which means the
science data, taken with the "B"-filter are located in the directory: `2020ue/2020-01-29/SCIENCE/FILT_B/`.
To read in the header information for one of the files (`r0606633.fits`)
{% highlight python %}
  import astropy #loads up astropy
  from astropy.io import fits #makes the fits package available
  hdu = fits.open("2020ue/2020-01-29/SCIENCE/FILT_B/r0606633.fits")
  hdu.info() #prints out basic information about the header (78 entries)
            #and the image (1092 x 736 pixels)                
{% endhighlight %}
For pt5m there is only on set of "header + image", which means it is given the
number 0 (if there were more, they would be numbered 1, 2, and so on).
To get the information that is in the header:

{% highlight python %}
  hdr = hdu[0].header # 0 because this was the first and only data in the file              
{% endhighlight %}
The header is composed of a series of entries that make up a "dictionary", where
 each entry is composed of a "keyword" that maps to a "value".  For example, in
this fits header "OBJECT" maps to "SN2020ue".
These values can be accessed by:
{% highlight python %}
value = hdr["OBJECT"] #i.e. VALUE = hdr[KEYWORD] (note the keyword
                      #needs to be surrounding by speech marks)
print(value)          #yields SN2020ue
{% endhighlight %}

You can see the whole header by running:
{% highlight python %}
print(hdr.keys)
{% endhighlight %}

If you are only interested in the values belonging to a set of keywords, you can
 make a loop and create a corresponding list of the values:
 {% highlight python %}
mykeys = ["NAXIS1", "RA", "CRPIX1", "OBJECT", "TYPE", "TELE"] #just an example
myvals = [] #creates an empty list
for i in range(len(mykeys)): #step through the array mykeys
    myvals.append(hdr[mykeys[i]]) #add the value onto the end of the list myvals
print(myvals) #[1092, '12:42:46.80', 538.9261761, 'SN2020ue', 'SCIENCE', 'pt5m']
{% endhighlight %}
