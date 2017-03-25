---
layout: post
title: Extra Simple GGPLOT2 Graphs in RStudio
---
### Playing with NASA’s Global Mean Estimates and Simple GGPLOT2 Graphs in RStudio

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

The file contains: years, temperature anomaly for every month, the anomalies' average for the periods January-December, December-November, the anomalies for each quarter of the year. We will only use the first 14 columns, so the year, monthly anomalies and the JanuaryDecember average. To make file ready for use let's get rid of the first row (please edi the file in Excel or Notepad), which is completly useless, the last row, as it is incomplete, save file and then import it to RSTUDIO. We can immediately cut off few columns we won't need.

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
Here's a quick "man" about ggplot (you can have more info about ggplot2 checking docs.ggplot2.org or executing `?ggplot` in RStudio):
```r
Usage
ggplot(data = NULL, mapping = aes(), ...)

Typically
ggplot(dataset, aes(x, y, <other aesthetics>))

Where
data is the  default dataset to use for plot and mapping is the default list of aesthetic mappings (which describe how and which data variables are mapped to aesthetic properties of the layer) to use for plot. If not specified, must be suppled in each layer added to the plot.
```
Let's try it then. We will show the average temperature anomaly for each year, telling ggplot that we will use data from dataset called nasa, specifically columns Year and J.D:
```r
ggplot(nasa, aes(Year,J.D))
```

Did anything happen?  No! That's because we need to add layers to our graph. Let's add layer with points.
```r
ggplot(nasa, aes(Year,J.D)) + geom_point()
```
![graph_points](/images/ggplot_points.png)

Of course we can modify the layout of our points:
```r
ggplot(nasa, aes(Year,J.D)) + geom_point(color="purple",size=5)
```
![graph_points](/images/ggplot_points_purple.png)

We can add additional layer, this time with line graph, playing with line color(color="pink") and width(lwd=3)
```r
ggplot(nasa, aes(Year,J.D)) + geom_point(color="purple",size=5) + geom_line(color="pink",lwd=3)
```
![graph_points](/images/ggplot_line_pink.png)

Ok but let's be serious and check what the graph tells us. We can see that the average temperatures anomalies grows. We can underline it by adding trend line to our graph as the third layer! (pssst, what trend line is? It is a line on a graph showing the general direction that a group of points seem to be heading.)
```r
ggplot(nasa, aes(Year,J.D)) + geom_point() + geom_line() + geom_smooth(color="red")
```
![graph_points](/images/ggplot_trend_line.png)

Great, we have proved that the average temperatures anomalies grows by showing each year's average on the graph. How about we try to illustrate the average anomalies monthly, for one specific year, let's say 1991, the year when Jackson's album Dangerous was released. As you know, ggplot wants us to tell him which columns goes on the graph. As you see, we don't have a column containing average temperature anomaly for one specific year, we only have rows with that information.
```r
> head(nasa)
  Year   Jan   Feb  Mar  Apr   May   Jun  Jul  Aug  Sep  Oct  Nov   Dec  J.D
1 1880 -0.84 -0.41 -.48 -.67  -.37  -.50 -.49  .06 -.51 -.69 -.53  -.55 -.50
2 1881 -0.80 -0.63 -.37 -.28  -.05 -1.15 -.56 -.28 -.34 -.47 -.54  -.13 -.47
3 1882  0.09 -0.14 -.10 -.62  -.40 -1.05 -.74 -.14 -.10 -.35 -.42  -.70 -.39
```
If only we could give our table one clockwise turn ... But we can ;) We can reshape the table. Let's do it. First, we can remove the J.D column, it is no longer useful.
```r
nasa$J.D <- NULL
```

Before we go to the super-complicated table-reshaping function, let's think about what we wanna achieve. 
![graph_points](/images/transposition.png)

We need to provide R a dataframe to operate on (nasa), a list of variable names that define our different metrics (varying = "Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"), the name we wish to give the column containing these values in our dataset (v.names = "Deviation"), the name we wish to give the column describing the different metrics (timevar = "Month"), the values this variable will have (times = "Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"), the fact that table should be vertical (direction = "long").

 Now  some magic:
 ```r
 nasa.reshaped <- reshape(nasa,
                          varying = list( c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul",                                                 "Aug", "Sep", "Oct", "Nov", "Dec")),
                          v.names = "Deviation",
                          timevar="Month",
                          times = c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug",                                          "Sep", "Oct", "Nov", "Dec"),
                          idvar = "Year",
                          direction = "long")
```                          
We received the table with columns: Year, Month, Deviation, and the following values: temperature for January 1880, January 1881, January 1882..... and so on.
```r
> head(nasa.reshaped)
         Year Month Deviation
1880.Jan 1880   Jan     -0.84
1881.Jan 1881   Jan     -0.80
1882.Jan 1882   Jan      0.09
1883.Jan 1883   Jan     -0.71
1884.Jan 1884   Jan     -0.64
1885.Jan 1885   Jan     -0.97
```
To select particular year from the dataset we can use:
```r
> nasa.reshaped.1991 <- nasa.reshaped[nasa.reshaped$Year==1991,]
> nasa.reshaped.1991
         Year Month Deviation
1991.Jan 1991   Jan      0.49
1991.Feb 1991   Feb      0.61
1991.Mar 1991   Mar      0.47
1991.Apr 1991   Apr      0.72
1991.May 1991   May      0.41
1991.Jun 1991   Jun      0.68
1991.Jul 1991   Jul      0.62
1991.Aug 1991   Aug      0.55
1991.Sep 1991   Sep      0.62
1991.Oct 1991   Oct      0.34
1991.Nov 1991   Nov      0.32
1991.Dec 1991   Dec      0.32
```
So now we can ask ggplotly to draw a line graph using subset nasa.reshaped.1991, columns Month and Deviation.
```r
ggplot(nasa.reshaped.1991, aes(x=Month,y=Deviation)) + geom_line()
```
Did you receive the error message? "geom_path: Each group consists of only one observation. Do you need to adjust the group aesthetic?" Good! Why is this happening? As **"Cookbook for R, Chapter: Graphs Bar_and_line_graphs_(ggplot2), Line graphs."** says 

>For line graphs, the data points must be grouped so that it knows which points to connect. In this case, it is simple -- all points should be connected, so group=1. When more variables are used and multiple lines are drawn, the grouping for lines is usually done by variable.

Therefor, we add group = 1 to oue aestethics et voilà:
```r
ggplot(nasa.reshaped.1991, aes(x=Month,y=Deviation,group=1)) + geom_line()
```
![graph_oneyear](/images/oneyear.png)




___
Temperature anomalies indicate how much warmer or colder it is than normal for a particular place and time. For the GISS analysis, normal always means the average over the 30-year period 1951-1980 for that place and time of year. This base period is specific to GISS, not universal. But note that trends do not depend on the choice of the base period: If the absolute temperature at a specific location is 2 degrees higher than a year ago, so is the corresponding temperature anomaly, no matter what base period is selected, since the normal temperature used as base point is the same for both years.
Note that regional mean anomalies (in particular global anomalies) are not computed from the current absolute mean and the 1951-80 mean for that region, but from station temperature anomalies. Finding absolute regional means encounters significant difficulties that create large uncertainties. This is why the GISS analysis deals with anomalies rather than absolute temperatures. For a more detailed discussion of that topic, please see "The Elusive Absolute Temperature". (source  -> https://data.giss.nasa.gov/gistemp/faq/#q101)
___

