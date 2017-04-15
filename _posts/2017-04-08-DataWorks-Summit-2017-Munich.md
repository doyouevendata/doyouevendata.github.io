---
layout: post
title: DataWorks Summit 2017 - Munich
---
<p align="justify">April 4th, 5th and 6th 2017, Munich, Germany hosted DataWorks Summit (or as previously called Hadoop Summit). This is a conference organized by Hortonworks and Yahoo. It's about Hadoop, Big Data and Open Source community.</p>

<p align="justify">This year I've had a chance to be there for the first time and figured I will share my thoughts about the event and things around it.</p>

<p align="justify">I have arrived on Tuesday, 4th April, one day before the conference starts but there were some unoficial events that day too. You could have taken one of the trainings or came to several meetups organized by speakers of the event.</p>

<p align="justify">Anyway, for all of you traveling to Munich for the first time. If you happen to get out of your plane and instead of walking into baggage claiming area you are entering the shopping and restaurant zone, don't be worried, that's how it is there ... Your bagge is there somewhere, it's just that somewhere happens to be at the other end of the airport. You have to take a train to get it. I may have not visited a lot of big airports in my life yet, but I have seen few and this was first time I've seen it :) But it could be true (and most probably is) only for the terminal I used, so your expeirence may vary.</p>

<p align="center">
  <img src="../images/DWS2017/luggage.jpg">
</p>

<p align="justify">But let's focus on the main topic. Tuesday was meetups day as I mentioned. There were few of them:</p>

<ul align="justify">
<li>Accelerating Apache Big Data and Machine Learning Workloads on OpenPOWER</li>
<li>Big Data in Automotive</li>
<li>Tensorflow and Hadoop, Accelerating HBase & Using BigBench to compare Hive and Spark</li>
<li>Cloud – Running and Securing Hadoop in the Cloud</li>
<li><b>SAS and Spark on HDP</b></li>
<li>Solving Cybercrime at Scale and in Realtime</li>
</ul>

<p align="center">
  <img src="../images/DWS2017/dws2017_1.jpg">
</p>

<p align="justify">I went to the SAS and Spark on HDP which happend to be Spark on HDP as the SAS speaker couldn't make it. Meetup was hosted by Bernhard Walter and Aengus Rooney of Hortonworks. We went through history and how all that data science in a distributed way started. For all of you not that much into hadoop and Spark in particular. The whole fuss about it is not because spark has some extra powerfull algorithms that are not seen in different libraries, it's because Spark works in a distributed way. That means you are not limited to your PC or Server computing power or amount of RAM you have there.</p>

<p align="justify">In fact while Spark is definitelly good at selection of Machine Learning algorithms (MLib), there are betters. But for large scale computations where your training set is large, having possibility to train the model on a cluster of machines is what made it so popular. Of course Spark is not only about ML, but the reasoning still holds. If you have large dataset it is better to compute it having more RAM and CPU at your disposal.</p>

<p align="justify">Anyway, Bernhard and Aengus went through the example of building recommendation model based on last.fm dataset that was released sometime in 2015 with arround 1.8 million of artits. Really interresting panel with quick introduction how you can build that in Spark and what are best practices in setting hyperparamethers for instance. How should we use existing data for training and cross validation.</p>

<p align="justify">BTW, did you know most people listen to 160 artists only?</P>

<p align="center">
  <img src="../images/DWS2017/dws2017_2.jpg">
</p>

<p align="justify">I mentioned where Spark wins and why, but if the dataset is small, then often it is better to switch to something else like numpy. Like when guys showed how they checked how many false hits their model produces. We know the exact list of artists each user listens to, we have created a model that predicts what would they like to listen to. We can check the model by running it on a subset of users and look for recommendations of artists they never listen to. Dataset for that one had only 1500 rows, and it was easier to run it locally using numpy.</p>

<p align="justify">We haven't discussed what next if truth be told, I mean once you have your perfect model what are best scenarios to deploy them in production. We may want to have dedicated post about it sometime in future though.</p>

<p align="justify">OK. So that was first day. The summit official start date was Wednesday though at 8AM with breakfast.</p>

<p align="justify">At 9AM it really kicked off with a Keynote and pretty amazing laser show :). This kind of fireworks are common for EMC from my experience, apparently Hortonworks is into it a little too ;) Well, there were no dancers so EMC wins there. But most important was the content of course.</p>

<p align="justify">As one can expect, keynote is for highlevel panels, it's also time for sponsors so nothing very exiting, but one speaker got my full attention and I must say I really liked his panel. It seems that organizers wanted to make sure not everything panels are technical / business. They invited few speakers who focus on ethical side of Data Driven society. The particular panel was held by Dr Barry Devlin.</p>

<p align="justify">In times when AI gets so much better ar interacting, reading context and running processes, we should expect more and more problems due to the fact manual labour but also high profile labour will no longer be needed. Dr Devlin says new approach to handling this kind of issues is needed and guaranted income for everyone is one of them. If you have a chance to watch his speach - definitelly do.</p>

<p align="center">
  <img src="../images/DWS2017/dws2017_3.jpg">
</p>

<p align="justify">During keynote a panel with experts took place too. Most interresting thing I remember from it is what Daljit Rehal of Centrica said about how the work culture changed in his company. Data driven projects are very demanding in terms of skilled engineers. At Centrica some cultural changes had to take place so that employees can focus on actuall work instead of figuring out how they should do that work. Motivation for self development is also a key factor. So the approach changed from centrally managed environment to more people centric approach. For instance if you work at Centrica and already has preffered language you code in, if only it can be used - you are free to do it. I am aware this is not always possible but in project so much oriented on Open Source solutions, this is very much possible and most probably the only way to go. As for motivating people for self development. Engineers at centrica are encourages to give lectures at local Universities which gives them strong motivation factor to be prepared I suppose ;)</p>

<p align="justify">Technical and business sessions were held in 6 different rooms simultaneously. This was the toughest part of the summit, how on earth are you suppose to choose if most of them are equally interesting?</p>

<p align="justify">Good thing about DWS is that most if not all session will be available on YouTube, so you can catch up with those you missed. I strongly encourage you to do so.</p>

<p align="justify">I will sunmmarize some of the sessions I have watched and think were most interesting ones. I think some of them will lead to separate posts related to what was shown on that sessions. So stay tuned for more!</p>

<p align="justify">And go and check DataWorks Summit videos that will be posted on Youtube. I will edit the post when they are published and add links to some I will describe below.</p>

<hr>

<h3>Interactive Analytics at Scale in Apache Hive using Druid</h3>

<p align="justify">If you need to create and then publish dashboards that are built on large amount fo data, then Druid is something you may want to check on. One use case would be for data that you prepare in Spark and then publish in Druid. The advantage of Druid compared to SparkSQL is latency. Druid indexes all its data. So if you need to create visualization layer in your company with large amount of people using it, have a look.</p>

<p align="justify">For more information and a benchmark that compares Druid to Spark, have a look at <a href="https://www.linkedin.com/pulse/combining-druid-spark-interactive-flexible-analytics-scale-butani">this</a> post of Harish Butani.</p>

<hr>

<h3>Streaming Analytics Manager</h3>

<p align="justify">This is something that I'd like to play around definitelly. You should expect dedicated article some time on the future.</p>

<p align="justify">SAM - among others - is a graphical tool that lets you build whole streaming process without need to write a code. Most importantly if at any moment in time schema changes at any place in your process, adjusting it is honestly really easy. Normally you'd have to change code, here you have everything accessible from nice GUI.</p>

<p align="center">
  <img src="../images/DWS2017/streaming-analytics-manager.png">
  Source: <a href="https://hortonworks.com/info/streaming-analytics-manager/">https://hortonworks.com/info/streaming-analytics-manager/</a>
</p>

<p align="justify">On top of that, you have access to all your streaming data and even some metrics in one single graphical tool. If you are into streaming, watch the session recording as soon as it is up on Youtube (I'll add the link then).</p>

<p align="justify">This is not yet production ready mind you.</p>

<hr>

<h3>Machine Learning in Healthcare</h3>

<p align="justify">Some of the session were not about particular tools, new releases, new functionalities. They were about real life examples how Big Data Technologies helped or allowed for businesses to grow or helped scientists or doctors be more precise and much faster in their work.</p>

<p align="justify">One of that session was held by Wade Schulz, Physician Scientist and Clinical Pathology Resident at Yale School of Medicine. Wade is also lead architect of Big Data platform at mentioned School that also operates one of the largest hospitals in US, Yale-New Haven Hospital.</p>

<p align="justify">He gave an example of how they learned to use that possibilities of new technologies. One of the most often laboratory test made in hospitals around the world is <a href="http://www.healthline.com/health/blood-smear#overview1">peripheral blood smear</a>. Blood sample is put on a glass and checked using microscope. Depending on anomalies found a diagnose could be made. Normally tests are subject to human eye perceptivity and its owner experience. In a hospital such as this there are hundreds of those tests made daily. Due to its nature it requires a lot of personel and time to be involved.</p>

<p align="center">
  <img src="../images/DWS2017/dws2017_4.jpg">
</p>

<p align="justify">Dr Schulz and his team work on a Machine Learning model that will analyse images of monolayer containing the tests data. It is now during acceptance tests of sort but already is much more accurate and much faster than current way of doing the tests. Eventually approval by a physician may still be needed to accept the result of an algorithm, but even then the gains could be significant. Mostly in terms of time needed for tests results and that can lead to more lifes saved.</p>

<p align="justify">Each new technologies can be used for bad or good thing. This definitelly is an example of the later.</p>

<p align="justify">I wonder if similar research is done at any European hospitals or Laboratory centers. If you know about any, please let us know!</p>

<hr>

<h3>Real-Time Anomaly Detection Using LSTM Auto-Encoders with DeepLearning4J on Apache Spark</h3>

<p align="justify">Session was held by Romeo Kienzler of IBM. Topic is very on time, the panel was about Machine Learning, well it's subclass in fact - Deep Learning, it was about IoT too, which is the next big thing in IT. I know, we have heard that for many years now... The thing is, technology seems to be now at the level that actually allows for this to grow to its real potential.</p>

<p align="justify">Romeo explained Deep Learning concepts, so we had a quick recap of Neural Networks, how they work and how they are used in Deep Learning.</p>

<p align="justify">Deep Learning is good at solving mathematical problems, not so much at recognizing sequences, and that is big thing of IoT, where Time based sequences are rather very common.</p> 

<p align="justify">This is where LSTM comes handy.<a href="https://en.wikipedia.org/wiki/Long_short-term_memory">So Long Short Term Memory</a> adds memory, long term memory in fact to neural networks. Thanks to that you can recognize and process sequences.</p>

<p align="justify">One example shown was where algorithm was teached using Shakespir literature and then it could write poems ;). Or when algorithm was teached to write C code like text ^^.</p>

<p align="justify">The main topic was Anomaly Detection though. If you're into it, watch the video! One example I can think of using this would be for instance for power grids. Normally, power consumption is something we can predict. There are very simillar trends based on what day of a week it is, what time and what season. I can think of using Deep Learning and LSTM in particular to build very good anomaly detection model that can alert the maintenance teams of something unexpected happening.</p>

<p align="justify">Other example, if you manage Data Center systems, storage for instance, there would be some trends there too. Would be interesting to see if we can use this to detect anomalies which could help finding out something happens to the infrastructure. This can be also used for forecasting and in storage area - as an example - it could be a real help for all of you trying so hard to determine what is the best oversubscription policy and when you should buy additional disks. You can watch the recording of the session <a href="https://www.youtube.com/watch?v=qqL2pVzV5FQ">here</a>.</p>

<hr>

<h3>Hops Hadoop and its HSFS (Hops FS) performance</h3>

<p align="justify">One of the thoughts I have had after the conference was that USA is really ahead of Europe in Data world. It really looks like it. I supose we will catch up sooner or later hopefully, nevertheless for now we are lagging behind.</p>

<p align="justify">Hops Hadoop is one example where an European project found a spot for itself. Hops is the only European Hadoop distribution apparently.</p>

<p align="justify">Jim Dowling of KTH Royal Institute of Technology in Stockholm shows new approach for Namenodes architecture. If you're into Hadoop world you must have thought about it before and things are kind of tricky with Namenode in HDFS. You can read more about it <a href="http://blog.cloudera.com/blog/2014/03/a-guide-to-checkpointing-in-hadoop/">here</a>.</p>

<p align="justify">So HopsFS reengineered NameNode from scratch while maintaining almost 100% compatibility with standard HDFS clients. Instead of keeping all metadata in memory, checkpoints in fsimage and recent changes in edit log they keep all that data in MySQL in memory Database Cluster that is build with a distributed approach. That means HSFS clients can write to HSFS in pararell. This is not the case with standard HDFS architecture, where each write operation triggers system wide lock that prevents more than one write operation to happen at a time.</p>

<p align="justify">This seems to have quite significant impact on performance in large clusters. Please watch the <a href="https://www.youtube.com/watch?v=mTRsrjH5WLI">video</a> for benchmark data and examples, but if you use large cluster and HDFS performance is a problem for you, this might be something you want to try as Spotify did aparently. I wonder thugh if they still use it, from what I know they have moved to Google Cloud (or are being in the process of tranistion).</p>

<p align="justify">One last comment, apart from performance, amount of medatada you can store with HSFS is much higher. In HDFS there is upper limit due to the fact all that data needs to be keept in JVM memory.</p>

<hr>

<h3>Summary</h3>

<p align="justify">I have seen more sessions, plan to watch even more on Youtube. And you will see dedicated posts about some of the concepts and tools which are not described in this article.</p>

<p align="justify">A good summary for this year DataWorks Summit may be the fact that a lot of use cases, real life examples and development seem to go toward streaming and IoT technologies. Batch processing will be taken over by streaming quite soon Laregely due to IoT and there, automotive seem to be the main actor.</p>

<p align="justify">BMW and their Big Data Team lead held a session about they're journey, where they are and what still needs to be done. Especially given the fact they are part of big international organization where processes makes some things happen slower than at a startup for instance. Anyway, the message was clear. BMW sells almost 2 millions cars each year. Each of them is now "connected". This is huge amount of data to tranfer, store and anlyze. Cars soon will not only send data to central, they will communicate with each other and with the surroundings. Their sensor will (and some already are) use advanced AI algorithms to drive the cars by themselves. This all will be possible thanks to development in Big Data technologies.</p>

<p align="center">
  <img src="../images/DWS2017/bmw.jpg">
</p>

<p align="justify">Tobias Buerger who gave that speach shared also experience he and his team had and what are their lessons learned. I can only recommend to watch his pannel so much to every team leads, managers and CTOs who have something to do with new technologies, Big Data in particular. Some of the most important experience they have (that's something so obvious it's hard to imagine someone would not know it, and yet...) were:</p>

<ul>
	<li>Make sure you have a great team! From my own experience too, yes, this is important, so much, really.</li>
	<li>Be prepared for immaturity. In so dynamic environment as anything related to Big Data - yes. Don't expect enterpise grade, production ready everything. Sometimes you may need to choose between environment tested for years that will need a month to analyze your data and environment which may not have that much maturity, but will perform the analysis in 5 minutes. The choice is yours.</li>
	<li>Be prepated for pitfalls, it happens.</li>
</ul>