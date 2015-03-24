# Problem
We want to use the [Echo Nest Artist API] in order to visualize different
attributes of an artist compared to similiar artists. Also, we would like
to see if there is a way of plotting a timeline for the *hotttesss* artist.

# Questions
1. How do the similar artists related to the input artist differ
   as far as their [familiarity] goes?
2. Can we get the *hotttesss* artists of all time?
3. Can we use a Histogram to visualize all this collected data?

# Resources
1. [Echo Nest Artist API]
2. [plotTimeline]

### 1. Mini-abstract and relevance of [Echo Nest Artist API]:
We want to input three artists to see what other artists are similiar
to them.

```python
from pyechonest import artist

artists = [artist.Artist('Kanye West'), artist.Artist('Lupe Fiasco'), artist.Artist('Common Sense')]
simArt = artist.similar(ids=[art.id for art in artists], results = 8) 
```
When you ```print simArt``` the following output will appear on the console:

```[<artist - Common>, <artist - Nas>, <artist - Talib Kweli>, <artist - The Roots>, <artist - Rhymefest>, <artist - Mos Def>, <artist - J. Cole>, <artist - Wale>]```

In my opinion, Echo Nest did a very good job by comparing artists. This is an almost
an exact replica of the list I was expecting; however, they have the artist *Common*
and *Common Sense*. *Common Sense* changed his name to *Common* in the early 2000s.
I think Echo Nest should delete duplicate artist that appear in their database for
artists. There are some other duplicate artist I have ran into in the past, as well.

The comparisons for their [familiarity]:
```
>>> nas = artist.Artist('Nas')
>>> nas.get_familiarity()
0.826423
>>> talib = artist.Artist('Talib Kweli')
>>> talib.get_familiarity()
0.72596
>>> inputKanye = artist.Artist('Kanye West')
>>> kanye.get_familiarity()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'kanye' is not defined
>>> inputKanye = artist.Artist('Kanye West')
>>> inputKanye.get_familiarity()
0.871675
>>> inputCommon = artist.Artist('Common')
>>> inputCommon.get_familiarity()
0.798834
>>> inputCommon.get_familiarity()
0.798834
>>> inputCommon = artist.Artist('Common Sense')
>>> inputCommon.get_familiarity()
0.453981
```
We can conclude, that all of the artist have around the same [familiarity]
rate. Although, we see that *Common Sense* (the redundant duplicate of 
*Common*) has a much lower [familiarity] rate against "his duplicate".
If someone knew *Common* only by *Common Sense*, they would have data from
Echo Nest that is not completely accurate. In this case, *Common* is the 
"correct" artist representation.

The ```top_hottt()``` attribute returns a list of *hottt* Artist objects.
Let us see who are the ```top_hott()``` artists currently. This attribute
only works for their current status. I wanted an attribute that calculated
their *overall_hotttnesss*, if there was such an attribute. I will have to
implement this attritube in the future. The top artists currently are:

```python
hotttArtist = artist.top_hottt(results=20)
print hotttArtist
```
The output of the code above:
```
[<artist - Taylor Swift>, <artist - Sam Smith>, <artist - Ed Sheeran>, <artist - Maroon 5>, <artist - Calvin Harris>, <artist - Sia>, <artist - David Guetta>, <artist - Meghan Trainor>
, <artist - Avicii>, <artist - Ellie Goulding>, <artist - Ariana Grande>, <artist - Madonna>, <artist - Hozier>, <artist - Rihanna>, <artist - The Weeknd>, <artist - Mark Ronson>,
<artist - Modest Mouse>, <artist - Imagine Dragons>, <artist - Pitbull>, <artist - Kendrick Lamar>]
```
This list is pretty accurate as far as I know. There are some artists I do
not know on here so I trust Echo Nest's algorithm for their ```top_hottt()```
function. Unfortunately, there is no function or attribute that provides us
with the overall *hotttnesss* of an artist. As stated earlier, I will try
to implement my own mediocre function for overall *hotttnesss*. We want
attributes that are not just for current status.

*This answers questions 1 and 2*

### 2. Mini-abstract and relevance of [plotTimeline]:
I am going to use the dates from the ```get_years_active()``` function and
figure out a way to create the list into an int so I can plot similiar artists
next to each other comparing their attributes in a histogram. The different 
 ```plot()``` functions require an int for their x-axis; hence, the difficult
in plotting the *actual* years they were active, instead of the *number* of 
years they were active. We can color the different bars on the histogram to 
represent each artist in a key. We can ```import matplotlib.dates as mdates``` 
in order to get the correct format for the years and days. Also, we can plot 
different attributes, depending on the user's input call for either *hotttnesss*, 
[familiarity], or *strength* for the ```top_hottt()``` artists that [Echo Nest Artist API]
provides. We can visualize the ```top_hottt()``` artists' attributes compared 
to your favorite artists to see why your favorites are not or in the ```top_hottt()``` 
artists for Echo Nest.

*This answers question 3*

[familiarity]: http://developer.echonest.com/forums/thread/839
[Echo Nest Artist API]: https://github.com/echonest/pyechonest/blob/master/pyechonest/artist.py 
[plotTimeline]: http://blog.mafr.de/2012/03/11/time-series-data-with-matplotlib/
[familiarity.py]: https://github.com/JoePaxton/familiarity/blob/master/familiarity.py
