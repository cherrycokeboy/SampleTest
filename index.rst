.. Football Visualization documentation master file, created by
   sphinx-quickstart on Tue Nov 13 11:28:29 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Austin H and Gavin's Football Visualization Website!
====================================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

Abstract
====================

This website was created by Gavin Schaeferle and Austin Hansen. The purpose of this website is to analysis data about the Football World Cup. To do this, we set about answering one big question: **How has the world cup changed over time?** To answer this question, we focused on multiple aspects of our data, these subsections are 

#. "Does being the host country increase your chances of winning?" 
#. "Does being the home team in a match increase your chances of winning?"
#. "Which country has won the most World Cups? And Which team won the most matches within the World Cup?"
#. "Which country has gotten to the most semi-finals?"
#. "Which World Cup has had the most scoring?"
#. "Which World Cup had the most attendance?"


In the end, we found that the world cup has been increasing in popularity and increasing in the number of teams participating. However, the most interesting thing to notice, is how the world cup not only grow on it's own, but also grew along side the world as a whole. 

Data Acquisition and Manipulation
======================================
The first step to any data science project, is to acquire some data. In our project, this was done be vigorously scrolling through the internet, trying to find any data on the World Cup. Our first stop was kaggle.com, because it has some really good data on a lot of different subjects, exceptionally sports. And after looking around for a while, we did in fact find the data we were looking for `here <...>`_. On that website's page, we found three datasets. The first had information on the general world cups from 1930 to 2014. The second had information on each match that happened at each world cup. The last on had information each people and couch of each team in each world cup. From this data, we had to do a little data maneuvering to get them all together and working. This was done by doing a quick join in pandas like this: 

.. code-block:: python

	matchesJoin = matches.set_index(['Year']).join(cups.drop(['Attendance'],axis = 1).set_index(['Year']))

the dataframe *matches* is the dataframe with every match in each world cup. next, the set_index(['Year']) is used to make sure the two dataframes have the same index. Next, within the join function, the *cups* dataframe contains the general information on each world cup. Notice the .drop function being called on the *cups* dataframe. This was done because both *matches* and *cups* have a column called "Attendance" so to make the join work, one of them had to go. We choose to drop the *cups* column because there are more match attendances then cups so later on the *matches* attendance column will be used along with the other info in *matches* and *cups* so having that column is more important. Finally, we set the index of the *cups* dataframe to be the same as the *matches* dataframe and we got ourselves a good joined dataframe. This is just the beginning of all the data manipulations that are done to this dataframe to create the graphs later on in this website. 

The other big change to the data was adding a column for which team won each match. This may not at first seem like such a challenge, because there are columns of which how many times a team scored in the match. However, the score doesn't take into account if the match was a tie at the end of regulation time. So one of the harder things to add within the data was a column that could tell into another column "win condition" and if that row's cell had that countries name in it, then say true. Otherwise (if they did lose) then say False. More information on how this was done in the notebook


Host Country Data
==========================================
To start answer the big question **How has the world cup changed over time?** we started by looking at how the host country did over time, and how has being the "home" country changed over time. `Here <notebooks/Worldcupdata/Worldcupdata.md>`_ is the analysis of that data

From this analysis we created two graphs. The first one shows the number of times a host country made it into the final four. 

.. figure:: image/hosttopfour.png

From just this graph, it doesn't seem like there is much evidence to conclude that meaning the host country means you will be in the semi-finals. While the true bar is slightly higher, it's not enough to conclude any difference. What this graph is used for a start into some more interesting graphs comparing all matches to host country, which starts to get more interesting.

The second one, we created three graphs that show three different things. The first shows the total host country wins over each world cup. The second shows the percent of wins by the host country each world cup. And finally the last one is a bit hard to put into words. Mainly, each block's height is the the number of times a percent of wins by the host country was between 0.2-0.25; 0.25-0.30; ... 

.. figure:: image/hostratio.png

from these three graphs, it's clear that there isn't much of an increase of whither or not they will win a match if they are the host country, over time and in general. We can see this from the fact that there is no clear linear pattern or any pattern with either of the two scatter graphs. However, while the mean percent of wins for a host country is over 50%, meaning the host team has a greater then 50% chance of winning. I would argue that this increase isn't enough for there to be any significant evidence that being the host country makes you more likely to win a match. More then likely, the match would have been won regardless of there host status. One thing to note, however, is the slight inversion of the total vs year compared to ratio vs year. This will be shown off in more detail in the next graphs.


Home Team Data
===============================
Going along with the host country data, the home team data looks at how often the home team won over the year. With this data, we created one figure with three graphs

The three graphs are very similar to the host country's three graph figure. The first one looks at how many times the home team won their match over each world cup. The second looks at the percent of times the home country won. And the final graph creates a histogram of percent of wins. 

.. figure:: image/homeratio.png

From the three graphs, it's clear that there was at one point a very significant home field advantage. It seems that before 1970, if you were the home team, you were almost certain to win. And with a standard deviation of 0.088, 50% is clearly not close to the mean. However, after 1970, the mean ratio of wins is closer to 50% being within one standard deviation. So this means that at one point, there was a significant chance of winning if you were the home team. But now a days, it is more random. Also from the first graph, you can see a positive linear slope that shows that as time went on, more matches were played. Yet contrasting to what was said before, as time went on, the percent of times the home team won has gone down over time. So, what we can gather from this data, is that the world cup has both gotten more random in it's selection of who is the home team, and, more importantly, that as time went on, more teams were more evenly matched. 


Country Wins
=====================
Let's take a broader view of the world cup and look at each countries win rate. The first graph looks at the number of times a country has won a world cup

.. figure:: image/numberofcountrywin.png

Notice how few countries there are! out of 20 different world cups, only eight countries have every won the whole thing. Really shows how dominating some countries are at football! This doesn't really answer the overall question **How had the world cup changed over time** but it does give us some background into the next few graphs that will answer this question

The next graph we created was how many times a country has won a match in the world cup. 

.. figure:: image/numberofcountrymatcheswin.png

This time, there are a lot more countries. Although a lot of them only won one game, plus this doesn't look at any teams that haven't won any games, just teams that won them. So again, this graph doesn't really answer the overall question, but does give some context into answering it later on

The final one we did was create an interactive graph that shows a different graph for each year. Each graph shows how many wins a country had for a specific world cup

.. figure:: image/matcheswinovertime.png 

this figure doesn't have the interactive parts to it but the notebook does here. What this interactive graph shows us this the change in development in countries over time. starting in 1930, only nine countries even won a game. but by 2014, 27 teams had won a match in the world cup. This bigger increase in teams shows how football's popularity has increased over time, and how countries have developed over time. One more interesting thing about the graphs is that you can see when the world cup team selection committees increased their selection of countries. this increase happened right around the 80's where in 1978, 13 teams won a match from 1982 where 21 teams won a match. The team increase then doesn't occur again until 1998 where 28 teams win a match. This again shows the development of the world cup as a popular sporting event across the world and the development of more and more countries, as more countries are eligible to partake in a heavily European/Brazilian game. This fact can actually be seen in the data here:

.. figure:: image/qual.png

Semi-Finals
==================
The next graph answers the question: "Which country has gotten to the most semi-finals?"
This section only has one graph but it is an interaction graph. Again, you won't be able to view on the website so instead, view it `here <notebooks/Worldcupdata.ipynb>`_. This graph shows the amount of semi-final finishes per country over time. The picture below shows the total number of semi-final finishes between 1930 and 2014. 

.. figure:: image/semi-finals.png

The first interesting thing to note is that the first two world cups didn't have a single repeat in semi-finalists. Showing that back then, no country was yet a dominate force to be reckoned with just yet. Also another thing about the first few world cups, Brazil (the soon to be number one football team) was not in the first two semi-finals. However, after that time, there semi-final placements would skyrocket at a fast pace. Another interesting thing about the graph is the creation of Germany FR after WWII, being very strong after a few rough no shows after the war. Actually beating Germany in number of semi-final place, just showing how long Germany was split up. Finally, looking at the world cup semi-finalist over time, there is defiantly an increase in the number of teams that have gotten to the semi-finals. With a steady increase from the beginning, only stopping during WWII. Also fun fact, the U.S has only been in the semi-finals once, and it was the first world cup. You can actually see how the USA has stayed constant over all this time. 



Scoring Over Time
============================
The next question we set out to answer, was whither the number of scoring has increased over time. And also, how has scoring effected the attendance of a match.

This figure shows the number of scores per year. The second shows the average number of scores per game over time. 

.. figure:: image/scores.png

What the first plot shows, is that as time yet on, more and more matches were played. This meant more points, and an increase of scores over time. This graph highlights the increase popularity of the world cup. The other graph shows how dominate the world cup teams were over time. in the first few cups, the games were averaging about 4 scores a game, which in football is quite high on average. This shows that the few teams that were playing, the scoring was very high and possible one sided. If it wasn't one sided, then at the very least it was a lot of scoring on both teams. Continuing to later years, the amount of scores per game goes lower and lower. This contrasted with the first few world cups show that, over time, the teams got so good at predicting the other teams moves, that most games were a stand still going to the end with an average of one point per time over and average 2 points. So from both of these graphs, it can be shown that as time went on, more games were played, and the teams were more competitive. 

Also related to this section is the attendance per game vs. scoring. The attendance data will be seen in more detail later on, but for now, let's look at how the attendance vs. scoring has changed. This figure has three plots, the first looks at attendance per game over time, the second looks at attendance per game vs total scores, and finally a plot on attendance per game vs scores per game. 

.. figure:: image/attscore.png

The first graph we'll look at later in the website. as for the other two, there does seem to be the ever so common positive slope for total and the negative slope for average/ratio. To further clarify this, the second graph has a negative slope as there are more scores. This happened because as the world cup got more popular, more people showed up at a game. Yet at the same time, more matches were played. So this increase comes from more popularity in the world cup along with more matches per world cup. The third graph shows how as the average score per game goes up, the average attendance of said game goes down. This can be explained like the other figure above. As the world cup got popular (an increase in attendance) the teams started getting more competitive and scoring less per game. So this would create a negative correlation between average attendance per game and average scores per game. The one point we'd like to mention is the 1994 point at the top. This point is significantly higher than any other point. After some investigation, it became clear that 1994 was the most attended world cup ever! This would explain the high average attendance per match as well as the weirdly high average attended per game vs total scores and vs average scores per game. More about that later.

Attendance
================
The attendance graph shows the total attendance per year at the FIFA World Cup, also the code to create this graph in located `Here <attendence.ipynb>`_

.. figure:: image/attend.png

There is a gap after 1938 and before 1950 because of World War II. As you can see the total attendance per year keeps growing until hitting its peak in 1994, then dips down a bit and returns to a positive slope. We believe that the peak in attendance during that year is determined by a couple factors. First, is that because of the Soviet Union collapsing in 1991, many new countries were born and new teams came into the world. Secondly, is that the World Cup that year was held in the United States which at the time had a lot of high capacity stadiums. Third, it was the first year the new country Russia had been in the World Cup as well as the newly reformed Germany. Lastly, the final was between Italy and Brazil, where Italy had been a powerhouse in the past decade and Brazil was beginning their stretch of dominance for the next several World Cups. The match ended 0-0 and went to penalties where Brazil won 3-2.



Conclusion
===================

#. Being the Host country does not increase your chance of winning. Even as time went on, the host country never really had any advantage, even though the average percent of wins were above 50%
#. Being the home team did at one point increase your chance of winning. But now the home and away teams a much more evenly spaced. 
#. As the world cup got more popular, more teams starting showing up and winning matches. 
#. Over time, the world cup has gotten more matches while scoring less per game.
#. Attendance has gone up as the world cup got more popular


The world cup has change drastically seen the 1930's! It has gotten increasingly popular every four years, it has continued to increase the amount of games per cup, it has continued to increase the level of games played and yet also increase the amount of countries allowed in also increasing competition. Attendance has also steady increased over time. Yet the coolest thing to note about this data is how it highlights the development of the world and how different countries started to improve enough to be a part of a global event such as the world cup. All in all, the world cup has continued to grow every year, being more and more people together to enjoy a wonderful sport.
 
