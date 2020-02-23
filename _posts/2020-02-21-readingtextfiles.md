---
layout: post
title:  "Reading text files w/ python"
date:   2020-02-21 10:30:00 +0000
categories: astropy
---


Importing information into a python script can be as straight forward as reading in a
list of file names and then conducting an operation of each of those files in turn.
This is a bed rock of automating processes: taking the frame work for running a single
operation on one set of data, but running it multiple times.

At the command prompt, we can get a list of the required files and in this case let's say we're interested in
all the flat images, by using:

{% highlight bash %}
> ls 2020ue/2020-01-29/SKY/FILT*/*fits > flatfile
{% endhighlight %}

In our python script or jupyter notebook, we can then read this into a list (which we can then
pass to the necessary functions):

{% highlight python %}
files = [] #empty list, ready for filenames
with open('flatfile') as f: #open flatfile
  for line in f: #read through the file
    files.append(line) #add each line to the files lists
f.close() #close flatfile
print(files)
{% endhighlight %}
If you examine the output from `print(files)`, you will see all of the files in the textfile
are now present as elements in a list format. Unfortunately, there is a pesky `\n` character
associated with each filename (corresponding to the *invisible* new line character present
at the end of each line in the original text file).  This character will have to be removed, but it
always occurs at the rightmost extreme of each filename, which means we can strip it using `rstrip()`.
{% highlight python %}
files = [] #empty list, ready for filenames
with open('flatfile') as f: #open flatfile
  for line in f: #read through the file, and put each line into the line variable
    files.append(line.rstrip('\n')) #add each line to the files lists
                                    #and remove trailing new line character
f.close() #close flatfile
print(files)
{% endhighlight %}
As you can see, this is just adding in an additional operation on the line variable to
remove that trailing character.

[Here is just one of many web pages, that appear in a Google search, that deal
with this
issue](https://www.guru99.com/reading-and-writing-files-in-python.html), but there may be other resources available that you may find more helpful.
