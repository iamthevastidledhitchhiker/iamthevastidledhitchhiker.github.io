---
layout: post
title:  The Hitchhiker's Guide to TensorFlow Ep. 2
subtitle: Char-RNN in TensorFlow
author: keith
date:   2016-03-13 20:00:00
tags: [Machine Learning, Neural Networks, Data Science, Video Games, SimCity, Simulation, Hex Editing]
---
## What are Self-Organizing Maps?
Self-Organizing Maps have been around for a while (I prefer to call them 'Kohonen Maps' but I guess 'SOM' rolls off the tongue better).
[There is no shortage](http://www.ai-junkie.com/ann/som/som1.html) of [articles](http://www.cis.hut.fi/research/reports/biennial02-03/cis-biennial-report-2002-2003-8.pdf) and [papers](http://sci2s.ugr.es/keel/pdf/algorithm/articulo/1990-Kohonen-PIEEE.pdf) available online that cover SOMs in depth, so I'll keep this short.
![center](/figs/mnremployee/unnamed-chunk-5-1.png)

A self-organizing map is an artificial neural network that does not follow the patterns typically associated with a neural network. Yes, SOMs require training, and yes trained SOMs automatically map input vectors. However, the structure of a trained SOM has more in common with a trained k-means model than say, an RNN. Rather than training an SOM using an error-correction model, we use a vector quantization and a neighborhood function to build our SOM.

To oversimplify SOMs, they are a means to reduce high-dimensional data in a 2-D or 3-D space so that observations similar to each other are represented closer together.

There is currently no native SOM implementation available in TensorFlow. PyMVPA,
py-kohonen, sevamoo/SOMPY and JustGlowing/minisom work well enough, but as my interests in TensorFlow have grown over the past six months, I figured this would be a good time to talk about creating new implementations. [Sachin Joglekar's implementation](https://codesachin.wordpress.com/2015/11/28/self-organizing-maps-with-googles-tensorflow/), published back in November 2015, is a great start, but a lot more could be done with it.
