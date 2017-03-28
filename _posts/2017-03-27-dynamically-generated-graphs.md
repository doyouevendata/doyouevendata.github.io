---
layout: post
title:Graphs generated dynamically on hover (using R and plotly)
---
<p align="justify">
Hello! Recently I was asked to create an R program showing one graph and dynamically generating another using the information about mouse position over the first graph. It is not as difficult as I thought, so here's the tutorial.
</p>
#### What we wanna achieve?
<p align="justify">
We're gonna create a simple R application showing annual and monthly average temperature anomalies. On one static graph we will illustrate the annual  average temperature anomalies, showing that they are constantly growing. While moving the mouse over this graph, we will dynamically generate another graph, which will illustrate monthly average temperature anomalies for the specific year our mouse is pointing to. Let me show this idea on a picture.
</p>
<p align="center">
  <img src="/images/dynamic_histogram/sketch.png">
</p>


#### What we need?
- shiny library, which is "A web application framework for R" and "turns your analyses into interactive web applications"
- plotly library, to draw plots
- 2 R files, one called server.R (script that contains the instructions that your computer needs to build your app) and one called ui.R (script that controls the layout and appearance of your app)
- data

To install shiny and plotly execute:
```r
install.packages("shiny")
install.packages("plotly")
library("plotly")
library("shiny")
```
<p align="justify">
You can download data files from <a href="">here</a> and <a href="">here</a>. These are excel sheets prepared from the data availaible on NASA page (<a href="">link</a>). Nasa's data looks like that:
</p>
![image_sketch](/images/dynamic_histogram/all_table.png)
It contains the year, average temperature anomaly for each month (January to December), than the average values for periods January-December, December-November and each quarter. What we've created from it:
![image_sketch](/images/dynamic_histogram/tables.png)

Let's load data into R tables:
```r
> monthly <- read.csv(file="path_to_monthly_file.csv",sep=",",header=TRUE)
> head(monthly)
         Year Month Deviation
1880.Jan 1880   Jan     -0.84
1881.Jan 1881   Jan     -0.80
1882.Jan 1882   Jan      0.09
1883.Jan 1883   Jan     -0.71
1884.Jan 1884   Jan     -0.64
1885.Jan 1885   Jan     -0.97
> annual <- read.csv(file="path_to_annual_file.csv",sep=",",header=TRUE)
> head(annual)
  Year   J.D
1 1880 -0.50
2 1881 -0.47
3 1882 -0.39
4 1883 -0.41
5 1884 -0.70
6 1885 -0.57
```
Now, our program has 2 components and their schema is imposed by Shiny. You can learn more about Shiny by visiting their website www.shiny.rstudio.com 

We will start with ui.R, adding few lines:





   Expression that generates a histogram. The expression is
  wrapped in a call to renderPlot to indicate that:
  
    1) It is "reactive" and therefore should re-execute automatically
       when inputs change
    2) Its output type is a plot
