---
layout: post
title:  "Metro-North Employee Demographics"
author: keith
date:   2015-11-10 22:53:35
categories: Metro-North
---

I recently came across a data set that contains detailed employee information at Metro-North Railroad.
It includes names, addresses, position titles, marital status, military status, and other data that
could be useful in mapping employee demographics.

## Step 1: Setup and Cleaning
I prefer loading all necessary packages at the start to accomodate the inevitable idea fairy. 
Also I hate typing require() or library() more than once.

{% highlight r %}
libs <- c("class", "plyr", "tm", "data.table", "tidyr", "dplyr", "igraph", "ggplot2", "leaflet", "ggmap")
lapply(libs, require, character.only = TRUE)
{% endhighlight %}

For the sake of brevity I have only included a small snippet of the data cleaning code.
During this step I also used the ggmap package and geocoded concatenated employee addresses for further analysis.

{% highlight r %}
#Set Options
options(stringsAsFactors = FALSE)
biodata_vw <- read.csv("~/Documents/Data Science/Projects/MNR - Employee Information/MetroNorthEmployeeApp/biodata_vw.csv", sep="")
### Clean the data ### 
db <- biodata_vw
db <- filter(db, DESCR10 %in% c("Active","Leave","Leave W/Py"), HOURLY_RT != 0)
db <- rename(db, "RACE" = DESCR50, "JOB_CAT_SHORT_01" = DESCRSHORT, "JOB_CAT_SHORT_02" = DESCRSHORT1, 
             "MNR_ID" = ALTER_EMPLID, "EMP_STATUS" = DESCR10, "ACTN_REASON" = DESCR1)
{% endhighlight %}







##Step 2: Exploring the Data

After doing a lot of cleaning and geocoding we can use the ggplot2 package to first create some simple charts

###General demographics
#### Age
We bin employee ages in 5 year intervals to reveal a fairly old company
![center](http://iamthevastidledhitchhiker.github.io/figs/mnremployee/unnamed-chunk-5-1.png) 

#### Ethnic Makeup

{% highlight text %}
## Source: local data frame [6 x 2]
## 
##              RACE     n
##             (chr) (int)
## 1 American Indian    25
## 2           Asian   221
## 3           Black  1358
## 4        Hispanic   657
## 5           Other   153
## 6           White  4151
{% endhighlight %}
Plotting this summary:

{% highlight r %}
ggplot(data = m, aes(x = RACE, y = n, fill = RACE)) + geom_bar(stat = 'identity') + theme(legend.position="none") + geom_text(stat='identity',aes(label=n),vjust=-0.25) + theme_minimal()+ labs(title = "Metro-North Employees by Ethnicity", x = NULL, y = NULL)
{% endhighlight %}

![center](http://iamthevastidledhitchhiker.github.io/figs/mnremployee/unnamed-chunk-7-1.png) 


#### Hourly Wage by Ethnicity 
![center](http://iamthevastidledhitchhiker.github.io/figs/mnremployee/unnamed-chunk-8-1.png) 

![center](http://iamthevastidledhitchhiker.github.io/figs/mnremployee/unnamed-chunk-9-1.png) 


#### Location
