---
layout: post
title:  "Lists, lists of lists and dicts"
date:   2020-02-21 11:00:00 +0000
categories: astropy
---

Python comes with two native data structures that allow you to move beyond dealing with a single variable.

**The list**

A list is a collection of variables ordered sequentially, which means 
you can access individual variables based on *where* they occur in the 
list.

An empty list can be initialised by using:

{% highlight python %}
newlist = [] #note the square brackets
{% endhighlight %} 

and new elements can be added to list (empty or not) by using the `append` command:

{% highlight python %}
newlist.append(newvar) #add newvar to the end of newlist
{% endhighlight %}

To find out how many elements are in the list, use the `len` function:

{% highlight python %}
newlist = [1,2,3,4,5,6]
print(len(newlist)) #prints out 6
{% endhighlight %}

To extract out individual elements from the list, you can invoke the 
position of that element in the list, using an integer referring to the 
*index* of that variable in the list.

So, for example, if we want to extract the second element in the list, 
because python begins counting from 0, we need to refer to `index = 1`, and place it inside *square brackets* after the list name, i.e.

{% highlight python %}
newlist = [1,2,3,4,5,6]
i = 1 #index for the second element
print(newlist[i]) #prints out 2
{% endhighlight %}
The implication of this is that the last element of the list is `len(newlist) - 1`.

If we want to through each element in the list, we can iterate over the 
list, using a `for` loop (with the `range` function - which gives a series of numbers, ranging from `0` to `len(newlist) - 1`):

{% highlight python %}
for i in range(len(newlist)): #invokes for loop
    print(newlist[i])
#prints out 
# 1
# 2
# 3
# 4
# 5
# 6
{% endhighlight %}

Sometimes I may accidentally refer to this as an "array", but I really 
mean "list".


**The dictionary**
A "dictionary" or "dict" is an associative array, where entries are 
grouped into pairs: a "key" and a "value".  This is much like the 
entries found in a FITS header.
An empty dictionary can be invoked as:

{% highlight python %}
newdictionary = {} #note the curly brackets
{% endhighlight %}

Here an element in the dict is defined as `{ "key" : "value"}` and, if 
you want to add a new key/value pair to the dict you use `update()` 
(instead of append).

{% highlight python %}
newdictionary.update({"binning" : 2}) #for example
      #where key = "binning"
      #  and val = 2
{% endhighlight %}

Accessing the elements in a dict is similar to that for a list, except one does not refer to the *index*, but rather the key, such that:

{% highlight python %}
print(newdictionary["binning"]) #prints the value 2
{% endhighlight %}
Note: that "binning" must be enclosed in quotes, because it is not a variable itself - it's phrase.  If you assigned the phrase "binning" to a variable you could instead use:
{% highlight python %}
mykey = "binning"
print(newdictionary[mykey]) #prints the value 2
{% endhighlight %}

Sometimes I may accidentally refer to this as a "hash", but I mean a "dict".


