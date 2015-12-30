---
layout: post
title:  "Revisiting SimCity 2000 - Episode II"
author: keith
date:   2015-12-30 05:00:35
tags: [Machine Learning, Neural Networks, Data Science, Video Games, SimCity, Simulation, Hex Editing]
---
<br>
[Go back to Episode I](/2015/12/29/exploring_simcity_pt1.html)
<br>

## Looking Under the Hood - Continued
In this post I will delve into the details of extracting useful information from our .SC2 file.

Directly referencing David Moew's guide...
{% highlight text %}
Each segment has an 8-byte header:

Bytes 1-4: Type of segment
Byres[sic] 5-8: Number of bytes in this segment, except for this 8-byte header

The remaining bytes in each segment are data.

The data in most SimCity segments is compressed using a form of run-length
encoding.  When this is done, the data in the segment consists of a series
of chunks of two kinds.  The first kind of chunk has first byte from 1 to
127;  in this case the first byte is a count telling how many data bytes
follow.  The second kind of chunk has first byte from 129 to 255.  In this
case, if you subtract 127 from the first byte, you get a count telling how
many times the following single data byte is repeated.  Chunks with first
byte 0 or 128 never seem to occur.
{% endhighlight %}

David also provides a primer for the segment types:
{% highlight text %}
SimCity files consist of the following segment types, in order, with the
following lengths.  Except as noted, segments are compressed as above, and
the length given for them is the length after uncompression; the compressed
length may vary.

Segment type     Length

MISC              4800    
ALTM             32768  (uncompressed)
XTER             16384    
XBLD             16384    
XZON             16384    
XUND             16384    
XTXT             16384    
XLAB              6400    
XMIC              1200    
XTHG               480    
XBIT             16384    
XTRF              4096    
XPLT              4096    
XVAL              4096    
XCRM              4096    
XPLC              1024    
XFIR              1024    
XPOP              1024    
XROG              1024    
XGRP              3328    
CNAM                32  (uncompressed; optional?)
{% endhighlight %}

Below is an explanation of each summary's purpose:
{% highlight text %}
ALTM:  Altitude map
XTER:  Tells whether there is land or water
{% endhighlight %}
