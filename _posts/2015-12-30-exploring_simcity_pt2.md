---
layout: post
title:  "Revisiting SimCity 2000 - Episode II"
author: keith
date:   2015-12-30 05:00:35
categories: Offbeat
tags: [Machine Learning, Neural Networks, Data Science, Video Games, SimCity, Simulation, Hex Editing]
---
<br>
[Go back to Episode I](/offbeat/2015/12/29/exploring_simcity_pt1.html)
<br>

## Looking Under the Hood - Continued
In this post I will delve into the details of extracting useful information from our .SC2 file.

Directly referencing David Moew's guide...
{% highlight text %}
Each segment has an 8-byte header:

Bytes 1-4: Type of segment
Byres 5-8: Number of bytes in this segment, except for this 8-byte header

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
