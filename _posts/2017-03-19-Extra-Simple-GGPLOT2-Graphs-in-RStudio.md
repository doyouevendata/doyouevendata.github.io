---
layout: post
title: Extra Simple GGPLOT2 Graphs in RStudio
---


Hi there! Here we have an Extra Simple, Super Easy tutorial about how to draw graphs in RStudio using ggplot2 package

We will need ggplot2 package, so if you don’t have it just do this:

Install.packages(“ggplot2”)
Library(“ggplot2”)

We will use the NASA’s Global Mean Estimates Based on Land-Surface Air Temperature Anomalies from https://data.giss.nasa.gov/gistemp/. More about this dataset: 
What are temperature anomalies (and why prefer them to absolute temperatures)? *

•	Temperature anomalies indicate how much warmer or colder it is than normal for a particular place and time. For the GISS analysis, normal always means the average over the 30-year period 1951-1980 for that place and time of year. This base period is specific to GISS, not universal. But note that trends do not depend on the choice of the base period: If the absolute temperature at a specific location is 2 degrees higher than a year ago, so is the corresponding temperature anomaly, no matter what base period is selected, since the normal temperature used as base point is the same for both years.
•	Note that regional mean anomalies (in particular global anomalies) are not computed from the current absolute mean and the 1951-80 mean for that region, but from station temperature anomalies. Finding absolute regional means encounters significant difficulties that create large uncertainties. This is why the GISS analysis deals with anomalies rather than absolute temperatures. For a more detailed discussion of that topic, please see "The Elusive Absolute Temperature". (source  -> https://data.giss.nasa.gov/gistemp/faq/#q101)
direct link -> https://data.giss.nasa.gov/gistemp/tabledata_v3/GLB.Ts.csv

Quick look at the content of file:

Station: Global Means					
Year,Jan,Feb,Mar,Apr,May,Jun,Jul,Aug,Sep,Oct,Nov,Dec,J-D,D-N,DJF,MAM,JJA,SON
1880,-.84,-.41,-.48,-.67,-.37,-.50,-.49,.06,-.51,-.69,-.53,-.55,-.50,***,***,-.51,-.31,-.58
1881,-.80,-.63,-.37,-.28,-.05,-1.15,-.56,-.28,-.34,-.47,-.54,-.13,-.47,-.50,-.66,-.23,-.66,-.45
1882,.09,-.14,-.10,-.62,-.40,-1.05,-.74,-.14,-.10,-.35,-.42,-.70,-.39,-.34,-.06,-.37,-.64,-.29
1883,-.71,-.97,-.48,-.34,-.38,.41,-.05,-.20,-.49,-.60,-.71,-.43,-.41,-.43,-.79,-.40,.05,-.60
1884,-.64,-.37,-.42,-.96,-1.22,-.86,-.88,.11,-.41,-.81,-.85,-1.03,-.70,-.65,-.48,-.87,-.54,-.69
1885,-.97,-.83,-.95,-.91,-.54,-.98,-.66,-.21,-.20,-.08,-.43,-.03,-.57,-.65,-.94,-.80,-.62,-.24


Now let’s go and draw some graphs!
