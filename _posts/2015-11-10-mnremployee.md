---
layout: post
title: "Metro North Employee Demographics"
date: "November 10, 2015"
output: html_document
---

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


{% highlight r %}
libs <- c("class", "plyr", "tm", "data.table", "tidyr", "dplyr", "igraph", "ggplot2")
lapply(libs, require, character.only = TRUE)
{% endhighlight %}



{% highlight text %}
## Loading required package: class
## Loading required package: plyr
## Loading required package: tm
## Loading required package: NLP
## Loading required package: data.table
## data.table 1.9.6  For help type ?data.table or https://github.com/Rdatatable/data.table/wiki
## The fastest way to learn (by data.table authors): https://www.datacamp.com/courses/data-analysis-the-data-table-way
## Loading required package: tidyr
## Loading required package: dplyr
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:data.table':
## 
##     between, last
## 
## The following objects are masked from 'package:plyr':
## 
##     arrange, count, desc, failwith, id, mutate, rename, summarise,
##     summarize
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
## 
## Loading required package: igraph
## 
## Attaching package: 'igraph'
## 
## The following objects are masked from 'package:dplyr':
## 
##     %>%, as_data_frame, groups, union
## 
## The following object is masked from 'package:tidyr':
## 
##     %>%
## 
## The following object is masked from 'package:class':
## 
##     knn
## 
## The following objects are masked from 'package:stats':
## 
##     decompose, spectrum
## 
## The following object is masked from 'package:base':
## 
##     union
## 
## Loading required package: ggplot2
## 
## Attaching package: 'ggplot2'
## 
## The following object is masked from 'package:NLP':
## 
##     annotate
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] TRUE
## 
## [[2]]
## [1] TRUE
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] TRUE
## 
## [[5]]
## [1] TRUE
## 
## [[6]]
## [1] TRUE
## 
## [[7]]
## [1] TRUE
## 
## [[8]]
## [1] TRUE
{% endhighlight %}


{% highlight r %}
#Set Options
options(stringsAsFactors = FALSE)
biodata_vw <- read.csv("~/Documents/Data Science/Projects/MNR - Employee Information/MetroNorthEmployeeApp/biodata_vw.csv", sep="")
### Clean the data ### 
db <- biodata_vw
db <- filter(db, DESCR10 == "Active" | DESCR10 == "Leave" | DESCR10 == "Leave W/Py")
db <- filter(db,  HOURLY_RT != 0)
db <- rename(db, "RACE" = DESCR50, "JOB_CAT_SHORT_01" = DESCRSHORT, "JOB_CAT_SHORT_02" = DESCRSHORT1, 
             "MNR_ID" = ALTER_EMPLID, "EMP_STATUS" = DESCR10, "ACTN_REASON" = DESCR1)
{% endhighlight %}


{% highlight r %}
###Convert date columns 
db <-mutate(db, BIRTHDATE = as.Date(BIRTHDATE), HIRE_DT = as.Date(HIRE_DT), 
                DT_OF_DEATH = as.Date(DT_OF_DEATH), LAST_HIRE_DT = as.Date(LAST_HIRE_DT), ORIG_HIRE_DT = as.Date(ORIG_HIRE_DT))
{% endhighlight %}


{% highlight r %}
###Clean Race column, part I
db$RACE[which(db$RACE == "NHOPI")] <- "American Indian"
db$RACE[which(db$RACE == "Not Specified")] <- "Other"
{% endhighlight %}


{% highlight r %}
db <- mutate(db, AGE = as.numeric(abs(difftime(BIRTHDATE, Sys.time(), units = "days")/365)))
#db <- mutate(db, YEARS_EMPLOYED = (ORIG_HIRE_DT - Sys.time))
#db <- mutate(db, FULL_ADDRESS = trimws(paste(ADDRESS1, CITY, STATE, POSTAL)))
#db <- select(db, -MIDDLE_NAME, -ADDRESS2, -ADDRESS3, -B_SAFETY_SENSTV, -SUPV_LVL_ID)
{% endhighlight %}


{% highlight r %}
m <- ggplot(data = db, aes(x = AGE, y = HOURLY_RT)) + geom_point()
m
{% endhighlight %}

![center](http://iamthevastidledhitchhiker.github.io/figs/mnremployee/unnamed-chunk-6-1.png) 

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
