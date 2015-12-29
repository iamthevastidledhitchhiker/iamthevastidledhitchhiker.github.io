---
layout: post
title:  "Revisiting SimCity 2000 - Episode I"
author: keith
date:   2015-12-29 05:53:35
categories: Offbeat
tags: [Machine Learning, Neural Networks, Data Science, Video Games, SimCity, Simulation, Hex Editing]
---
<br>

####Before we begin, a brief backstory...
On my 7th birthday I received a copy of Simcity 2000 Special Edition for Macintosh. I spent a lot of time playing it until I received a copy of Simcity 4 (for PC). I skipped Simcity 3000, primarily due to the fact that my family's Macintosh LC 550 was incapable of running it. I would estimate that I logged about 1000 hours into both games. The amount of data lost due to the shear number of cities and regions that I abandoned and/or deleted breaks my heart a little. In order to keep my nostalgia in check, I'll end here and move on to the stuff people might actually care about...
<br>  

##Prologue: Getting Under the Hood

<p>SimCity 2000 owes its recognition to the folks at Maxis Emeryville and their dedication to creating simulations that are playable yet realistic enough to derive a sense of accomplishment for successful players
<a href="http://www.rockpapershotgun.com/2014/01/07/john-vs-the-trees-woodcutter-simulator-2013/" target="_blank">an achievement easier said than done</a>.
 With this realism comes a certain amount of data that can be modeled. Because SimCity 2000 (SC2K) is a simulation with known successful and unsuccessful strategies, the data produced should have relatively little noise. Getting access to that data in an interpretable form, on the other hand, is a different matter.<p/>
 Cities from SC2K are saved under the .SC2 file extension and are structured as IFF files - a file format created by Electronic Arts back in 1985. I spent some time researching what exactly is contained within these files, but it seems little work has been done on interpreting SC2K IFF files, spare for the <a href="http://djm.cc/simcity-2000-info.txt/" target="_blank">work done by David Moews back in 1995</a>. I also only managed to find a single project with the intention of reading out the data from SC2 files. The source code for this project <a href="https://github.com/emtiu/sc2000tool" target="_blank">is available on Github</a>.
 <p>The shear amount of information stored in these files is incredibly useful from the perspective of understanding how SimCity 2000 works. <a href="https://www.vice.com/read/the-totalitarian-buddhist-who-beat-sim-city/" target="_blank">While work has already been done to "beat" SC2K's sequel SimCity 3000</a>, this work was achieved through a mixture of trial and error, research, and scratch-pad mathematics. While my approach is similar in that it involves a lot of trial and error, I am far more interested in the implications of extracting the data from the entire SimCity 2000 Special Edition "CITIES" folder and building models that identify successful cities from unsuccessful cities, with the intention of unraveling the inner workings of the SC2K engine.</p> <p>The definition of a "successful" city is subject to enormous interpretation, so it is important to analyze cities from multiple perspectives. Granted, SC2K is not a perfect simulation by any means; extracting any sort of "wisdom" from a simulation, however sophisticated, is dangerous. The purpose of this undertaking is more an exercise in creativity and boredom rather than a means to generate the ideal city, real or fictional. Taking a page out of the book of flaws from the 2013 SimCity reboot...<a href="https://www.youtube.com/watch?v=IHt0kAhXIu4/" target="_blank">just because a simulation says building 100% residential is profitable does not mean that it's a good idea.</a></p>

 <p align="center"> <a href="http://iamthevastidledhitchhiker.github.io/figs/simcity_ep1/SS_01.png"><img src="http://iamthevastidledhitchhiker.github.io/figs/simcity_ep1/SS_01.png"> </a> </p>
