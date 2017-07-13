---
layout: post
comments: true
title: Is Beyoncé better than Queen? - Part 1.
---
#### Also: What is sentiment analysis? How to create a wordcloud? What is wrong with Beyoncé? Step by step analysis.


Hey guys! I was recently scrolling through some memes and came across this:
<p align="center">
  <img src="/images/bey_vs_queen/beyonce-vs-mercury.jpg">
</p>

<p align="justify">You have surely seen this before, haven't you? I like Beyoncé. Like, a lot. But I'm also aware that nowadays popular music is not so sophisticated. Is it? What a great question we can answer right now with a little analytic skills! Let's go and check, if Freddie Mercury's texts are FAR better than those of Beyoncé (what my boyfriend is constantly pointing out to me, so yes, I will be doing this analysis only to throw it at his face saying "AHHHAAAAAA!". Back to the post now.)</p>

What should we do:
 - collect and explore the data
 - clear the data
 - analyze the data
 - present the results
 
 What will we need?
- Lyrics of Freddie Mercury's songs
- Lyrics of Beyoncé's songs
- RStudio and some special libraries
 
 ## Part 1 - Clearing the data.

##### Let's go!
<p align="justify">For lyrics, you can go to <a href="https://www.kaggle.com/gyani95/380000-lyrics-from-metrolyrics">this</a> Kaggle site and download the 99Mb dataset that contains Beyoncé's songs, and then to <a href="https://www.kaggle.com/mousehead/songlyrics">this</a> Kaggle site that contains dataset with Queen's songs.</p>

<p align="justify">Then, we have to launch RStudio, load the data, inspect it, clear it, and prepare the subsets that will be analysed.</a>

1. Load the data:

```
setwd("C:/computor/directory_with_your_downloaded_data/")
songdata <- read.csv(file="songdata.csv")
lyrics <- read.csv(file="lyrics.csv")
```

2. Inspect it:

```
str(songdata)
'data.frame':  57650 obs. of  4 variables:
 $ artist: Factor w/ 643 levels "'n Sync","ABBA",..: 2 2 2 2 2 2 2 2 2 2 ...
 $ song  : Factor w/ 44824 levels "'39","'59 Crunch",..: 1364 2345 2896 3677 3678 6022 6771 7219 8410 8598 ...
 $ link  : Factor w/ 57650 levels "/a/abba/ahesmykindofgirl_20598417.html",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ text  : Factor w/ 57494 levels "'AD 'AKHSHYAV LO NISH'AR DAVAR  \nTEN LI SIMAN  \nHAKE'EV SHEHAYAH NISH'AR  \nKEN KOL HAZMAN  \nATAH MITRACHEK, K'MU GAL NE'ELA"| __truncated__,..: 31695 43057 17616 32559 32560 51085 11108 8594 25646 18976 ...

 str(lyrics)
'data.frame':  339277 obs. of  6 variables:
 $ index : int  0 1 2 3 4 5 6 7 8 9 ...
 $ song  : Factor w/ 236867 levels "0-0","0-0-0",..: 56272 205225 85347 233083 23435 8810 146916 219754 178029 228598 ...
 $ year  : int  2009 2009 2009 2009 2009 2009 2009 2009 2009 2009 ...
 $ artist: Factor w/ 17088 levels "009-sound-system",..: 4499 4499 4499 4499 4499 4499 4499 4499 4499 4499 ...
 $ genre : Factor w/ 12 levels "Country","Electronic",..: 10 10 10 10 10 10 10 10 10 10 ...
 $ lyrics: Factor w/ 229599 levels "","\003Its what youre afraid of.\nAll of my fears,\nAll of my Faults.\nAll that came first,\nAll will be lost.",..: 141437 150816 108358 142333 149557 92449 187210 196953 16818 136101 ...

head(songdata)
  artist                  song                                       link
1   ABBA Ahe's My Kind Of Girl /a/abba/ahesmykindofgirl_20598417.html
2   ABBA      Andante, Andante      /a/abba/andanteandante_20002708.html

 ... <truncated>
1 Look at her face, it's a wonderful face  \nAnd ... <truncated>
2 Take it easy with me, please  ... <truncated>
(...)

head(lyrics)
  index                   song year          artist genre
1     0              ego-remix 2009 beyonce-knowles   Pop
2     1           then-tell-me 2009 beyonce-knowles   Pop
                                                                                              ... <truncated>
1 Oh baby, how you doing? ... <truncated>
2  ... <truncated>
(...)

colnames(songdata)
[1] "artist" "song"   "link"   "text"  
colnames(lyrics)
[1] "index"  "song"   "year"   "artist" "genre"  "lyrics"
```

<p align="justify">From the above we know that first dataset is composed from 4 columns, "artist" "song", "link" and  "text", all of them are factor type. Second dataset has 6 columns, "index"  "song"   "year"   "artist" "genre" and "lyrics", also factors apart from index, which is an integer. we won't need index and link columns, so we will delete them from the subsets. Also, we would like to change factor type  to string in the "artist" columns in subsets, you will see why.</p>

3. Look for Beyoncé and Queen and substract them:

<p align="justify">Both datasets contain the "artist" column, but we don't know how the names are stored - capital letters? Hyphen, spaces? E in BEYONCE has an accent, is it considered? Instead of looking for the value equal to "Beyonce" or "Queen" we will grep the column searching for string that matches. Then, we will copy found rows into new datasets and clear them.</p>

```
nrow(songdata[grep("queen", songdata$artist, ignore.case = TRUE),])
[1] 413
nrow(lyrics[grep("queen", lyrics$artist, ignore.case = TRUE),])
[1] 41
nrow(lyrics[grep("beyonc", lyrics$artist, ignore.case = TRUE),])
[1] 371
nrow(songdata[grep("beyonc", songdata$artist, ignore.case = TRUE),])
[1] 0
queen <- songdata[grep("queen", songdata$artist, ignore.case = TRUE),]
beyonce <- lyrics[grep("beyonc", lyrics$artist, ignore.case = TRUE),]
```

4. Clear data subsets:

Let's check what artists did we found using `grep`:

```
table(queen$artist)

                                     'n Sync                                         ABBA 
                                           0                                            0 
                                 Ace Of Base                                 Adam Sandler 
                                           0                                            0 
                                       Adele                                    Aerosmith 
                                           0                                            0 
                                  Air Supply                                Aiza Seguerra 
                                           0                                            0 
                                     Alabama                         Alan Parsons Project 
                                           0                                            0 
(...)
                                       
```

<p align="justify">What the hell? This is not what we wanted! Why does it look like that? Remember when we check the types of columns? Artists are stored as factor with levels, it means that we get the whole lists of them, even if the count is 0 (if you wanna read about factors, you can visit <a href="https://www.stat.berkeley.edu/classes/s133/factors.html">this page</a>). As I mentioned before, we wanna change factor to string.</p>

```
queen <- data.frame(lapply(queen, as.character), stringsAsFactors=FALSE)
table(queen$artist)

                  Queen           Queen Adreena           Queen Latifah Queens Of The Stone Age             Queensryche 
                    163                      41                      50                      68                      91 

```

<p align="justify">See? Much better. Now we clearly see we have to get rid of Queen Adreena, Queen Latifah, Queens Of The Stone Age and Queensryche rows.</p>

```
queen <- queen[queen$artist=="Queen",]
unique(queen$artist)
[1] "Queen"
nrow(queen)
[1] 162
```

How about Beyoncé?

```
beyonce <- data.frame(lapply(beyonce, as.character), stringsAsFactors=FALSE)
unique(beyonce$artist)
[1] "beyonce-knowles"  "beyoncas-shakira" "beyonce"         
beyonce <- beyonce[beyonce$artist=="beyonce",]
unique(beyonce$artist)
[1] "beyonce"
nrow(beyonce)
[1] 118
```

<p align="justify">For the final touch, let's get rid of columns we won't use and change the name of the columns so they will be identical in both subsets.</p>

```
colnames(beyonce)[colnames(beyonce)=="lyrics"] <- "text"
beyonce$index <- NULL
beyonce$genre <- NULL
queen$link <- NULL
```

Now our subsets are ready to be analysed!
