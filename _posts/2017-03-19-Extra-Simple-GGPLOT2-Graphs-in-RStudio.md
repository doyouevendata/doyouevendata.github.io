---
layout: post
title: Extra Simple GGPLOT2 Graphs in RStudio
---
### Extra Simple GGPLOT2 Graphs in RStudio

Hi there! Here we have an Extra Simple, Super Easy tutorial about how to draw graphs in RStudio using ggplot2 package. We will visualize the **temperature anomalies for the past 130 years.**


We will be using the **NASA’s Global Mean Estimates Based on Land-Surface Air Temperature Anomalies** from  https://data.giss.nasa.gov/gistemp/ (pssst, what are temperature anomalies,and why prefer them to absolute temperatures? Check the last section of this post to find the answers!). You can download the file with data using this link -> https://data.giss.nasa.gov/gistemp/tabledata_v3/GLB.Ts.csv

Let's have a quick look at the content of file:
```
Station: Global Means					
Year,Jan,Feb,Mar,Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec,J-D,D-N,DJF,MAM,JJA,SON
1880,-.84,-.41,-.48,-.67,-.37,-.50,-.49,.06,-.51,-.69,-.53,-.55,-.50,***,***,-.51,-.31,-.58
1881,-.80,-.63,-.37,-.28,-.05,-1.15,-.56,-.28,-.34,-.47,-.54,-.13,-.47,-.50,-.66,-.23,-.66,-.45
(...)
```

The file contains: years, temperature anomaly for every month, the anomalies' average for the periods January-December, December-November, the anomalies for each quarter of the year. We will only use the first 14 columns, so the year, monthly anomalies and the JanuaryDecember average. To make file ready for use let's get rid of the first row, which is completly useless, save file and then import it to RSTUDIO. We can immediately cut off few columns we won't need.

```r
> nasa <- read.csv(file="path_to_your_file/GLB.Ts.csv", header=TRUE,sep=",")
> nasa <- subset(nasa, select=(1:14))
> class(nasa)
[1] "data.frame"
> head(nasa)
  Year   Jan   Feb  Mar  Apr   May   Jun  Jul  Aug  Sep  Oct  Nov   Dec  J.D
1 1880 -0.84 -0.41 -.48 -.67  -.37  -.50 -.49  .06 -.51 -.69 -.53  -.55 -.50
2 1881 -0.80 -0.63 -.37 -.28  -.05 -1.15 -.56 -.28 -.34 -.47 -.54  -.13 -.47
3 1882  0.09 -0.14 -.10 -.62  -.40 -1.05 -.74 -.14 -.10 -.35 -.42  -.70 -.39
```

#### Now let’s go and draw some graphs!

We will need ggplot2 package, so if you don’t have it just do this:
```r
> install.packages("ggplot2")
> library(ggplot2)
```
Here's a quick "man" about ggplot (you can have more info about ggplot2 checking docs.ggplot2.org or executing ?ggplot in RStudio):

>Usage
>ggplot(data = NULL, mapping = aes(), ...)

>where
> data is the  default dataset to use for plot and mapping is the default list of aesthetic mappings to use for plot. If not specified, must be suppled in each layer added to the plot.

Let's try then:









___
Temperature anomalies indicate how much warmer or colder it is than normal for a particular place and time. For the GISS analysis, normal always means the average over the 30-year period 1951-1980 for that place and time of year. This base period is specific to GISS, not universal. But note that trends do not depend on the choice of the base period: If the absolute temperature at a specific location is 2 degrees higher than a year ago, so is the corresponding temperature anomaly, no matter what base period is selected, since the normal temperature used as base point is the same for both years.
Note that regional mean anomalies (in particular global anomalies) are not computed from the current absolute mean and the 1951-80 mean for that region, but from station temperature anomalies. Finding absolute regional means encounters significant difficulties that create large uncertainties. This is why the GISS analysis deals with anomalies rather than absolute temperatures. For a more detailed discussion of that topic, please see "The Elusive Absolute Temperature". (source  -> https://data.giss.nasa.gov/gistemp/faq/#q101)
___
