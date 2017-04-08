---
layout: post
title: DataWorks Summit 2017 - Munich
---
April 4th, 5th and 6th 2017, Munich, Germany was good place to be. DataWorks Summit (or as previously called Hadoop Summit) is a conference organized by Hortonworks and Yahoo. It is about Hadoop, Big Data and Open Source community.

This year I've had a chance to be there for the first time and figured I will share my thoughts about the event and things around it.

I have arrived on Tuesday, 4th April, one day before the conference starts but there were some unoficial events that day too. You could have taken one of the trainings or came to several meetups organized by speakers of the event. 

Anyway, for all of you traveling to Munich for the first time. If you happen to get out of your plane and instead of walking into baggage claiming area you are entering the shopping and restaurant zone, don't be worried, that's how it is there ... Your bagge is there somewhere, it's just that somewhere happens to be at the other end of the airport. You have to take a train to get it. I may have not visited a lot of big airports in my life yet, but I have seen few and this was first time I've seen it :) But it could be true (and most probably is) only for the terminal I used, so your expeirence may vary.

![DWS2017 Registration](../images/DWS2017/dws2017_1.jpg)

But let's focus on the main topic. Tuesday was meetups day as I mentioned. There were few of them:

- Accelerating Apache Big Data and Machine Learning Workloads on OpenPOWER
- Big Data in Automotive
- Tensorflow and Hadoop, Accelerating HBase & Using BigBench to compare Hive and Spark
- Cloud – Running and Securing Hadoop in the Cloud
- **SAS and Spark on HDP**
- Solving Cybercrime at Scale and in Realtime

I went to the SAS and Spark on HDP which happend to be Spark on HDP as the SAS speaker couldn't make it. Meetup was hosted by Bernhard Walter and Aengus Rooney of Hortonworks. We went through history and how all that data science in a distributed way started. For all of you not that much into hadoop and Spark in particular. The whole fuss about it is not because spark has some extra powerfull algorithms that are not seen in different libraries, it's because Spark works in a distributed way. That means you are not limited to your PC or Server computing power or amount of RAM you have there.

In fact while Spark is definitelly good at selection of Machine Learning algorithms (MLib), there are betters. But for large scale computations where your training set is large, having possibility to train the model on a cluster of machines is what made it so popular. Of course Spark is not only about ML, but the reasoning still holds. If you have large dataset it is better to compute it having more RAM and CPU at your disposal.

Anyway, Bernhard and Aengus went through the example of building recommendation model based on last.fm dataset that was released sometime in 2015 with arround 1.8 million of artits. Really interresting panel with quick introduction how you can build that in Spark and what are best practices in setting hyperparamethers for instance. How should we use existing data for training and cross validation.

BTW, did you know most people listen to 160 artists only?

![DWS2017 Spark on HDP Summit](../images/DWS2017/dws2017_2.jpg)

I mentioned where Spark wins and why, but if the dataset is small, then often it is better to switch to something else like numpy. Like when guys showed how they checked how many false hits their model produces. We know the exact list of artists each user listens to, we have created a model that predicts what would they like to listen to. We can check the model by running it on a subset of users and look for recommendations of artists they never listen to. Dataset for that one had only 1500 rows, and it was easier to run it locally using numpy.