
## Adding Modules


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

## Adding Datasets


```python
matches = pd.read_csv('WorldCupMatches.csv')
cups = pd.read_csv('WorldCups.csv')
```


```python
#matches.dropna()
```


```python
final_matches = matches[matches['Stage'] == 'Final']
```


```python
#final_matches
```

## Home Field Adventage (Top Four)
Here I look at if being the host country increases or decreases the likelyhood of getting to the top four. I also look at if being the home team increases your chances of winning a match. Finally, I find out how the host country changes over time and how being a host country changes. 

First, I create a variable that has the columns I will need:

country: which country is the host country

winner - fourth: which country got that place in that world cup


```python
finalCompared = cups[['Country','Winner','Runners-Up','Third','Fourth']]
```

Here I create a boolean column that will say true if the host country is in the final four and false if not. 


```python
finalCompared['homeShowUp'] = ((finalCompared['Country'] == finalCompared['Winner']) | (finalCompared['Country'] == finalCompared['Runners-Up'])  | (finalCompared['Country'] == finalCompared['Third']) | (finalCompared['Country'] == finalCompared['Fourth']) )
```

    /usr/local/lib/python3.5/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.



```python
finalCompared
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Winner</th>
      <th>Runners-Up</th>
      <th>Third</th>
      <th>Fourth</th>
      <th>homeShowUp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Uruguay</td>
      <td>Uruguay</td>
      <td>Argentina</td>
      <td>USA</td>
      <td>Yugoslavia</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Italy</td>
      <td>Italy</td>
      <td>Czechoslovakia</td>
      <td>Germany</td>
      <td>Austria</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>France</td>
      <td>Italy</td>
      <td>Hungary</td>
      <td>Brazil</td>
      <td>Sweden</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Brazil</td>
      <td>Uruguay</td>
      <td>Brazil</td>
      <td>Sweden</td>
      <td>Spain</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Switzerland</td>
      <td>Germany FR</td>
      <td>Hungary</td>
      <td>Austria</td>
      <td>Uruguay</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Sweden</td>
      <td>Brazil</td>
      <td>Sweden</td>
      <td>France</td>
      <td>Germany FR</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chile</td>
      <td>Brazil</td>
      <td>Czechoslovakia</td>
      <td>Chile</td>
      <td>Yugoslavia</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>England</td>
      <td>England</td>
      <td>Germany FR</td>
      <td>Portugal</td>
      <td>Soviet Union</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Mexico</td>
      <td>Brazil</td>
      <td>Italy</td>
      <td>Germany FR</td>
      <td>Uruguay</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Germany</td>
      <td>Germany FR</td>
      <td>Netherlands</td>
      <td>Poland</td>
      <td>Brazil</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Argentina</td>
      <td>Argentina</td>
      <td>Netherlands</td>
      <td>Brazil</td>
      <td>Italy</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Spain</td>
      <td>Italy</td>
      <td>Germany FR</td>
      <td>Poland</td>
      <td>France</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Mexico</td>
      <td>Argentina</td>
      <td>Germany FR</td>
      <td>France</td>
      <td>Belgium</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Italy</td>
      <td>Germany FR</td>
      <td>Argentina</td>
      <td>Italy</td>
      <td>England</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>USA</td>
      <td>Brazil</td>
      <td>Italy</td>
      <td>Sweden</td>
      <td>Bulgaria</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>France</td>
      <td>France</td>
      <td>Brazil</td>
      <td>Croatia</td>
      <td>Netherlands</td>
      <td>True</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Korea/Japan</td>
      <td>Brazil</td>
      <td>Germany</td>
      <td>Turkey</td>
      <td>Korea Republic</td>
      <td>False</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Germany</td>
      <td>Italy</td>
      <td>France</td>
      <td>Germany</td>
      <td>Portugal</td>
      <td>True</td>
    </tr>
    <tr>
      <th>18</th>
      <td>South Africa</td>
      <td>Spain</td>
      <td>Netherlands</td>
      <td>Germany</td>
      <td>Uruguay</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Brazil</td>
      <td>Germany</td>
      <td>Argentina</td>
      <td>Netherlands</td>
      <td>Brazil</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



Next, I create a histogram of the boolean values.


```python
plt.hist(finalCompared.homeShowUp,align='mid',bins=[0,0.33,0.5,0.66,1])
plt.ylabel('count')
plt.xlabel('Whether they made it to the top 4 (0 = False, 1 = True)')
plt.title('Whether or not the Home Country\'s team made it into the top four' )
plt.show()
```


![png](output_13_0.png)


### Analysis of Home field vs top four finish
From just this graph, it doesn't seem like there is much evidence to conclude that meaning the host country means you will be in the semi-finals. While the true bar is slightly higher, it's not enough to conclude any difference. What this graph is used for a start into some more interesting graphs comparing all matches to host country, which starts to get more interesting. 

## Home Field Adventage (Host Country)
While it seems like there isn't a greater chance of you winning the entire cup if you are the host country, but what about each match? This next section looks at how the host country has done in each match over time, and how host field adventage has decreased as time went on. 

Matchesjoin is a dataframe of two datasets, a dataset of each match, and a dataset of each world cup as a whole. So the last few columns repeat for each match that was in that specific world cup. 


```python
matchesJoin = matches.set_index(['Year']).join(cups.drop(['Attendance'],axis = 1).set_index(['Year']))
```


```python
#matchesJoin.head()
```

I then decided to say this dataframe as a csv just so that I share it with my partner. 


```python
f = open('test.csv','w')
f.write(matchesJoin.to_csv())
```




    326412




```python
matchesJoin = pd.read_csv('test.csv')
```


```python
matchesJoin = matchesJoin.dropna()
```


```python
#matchesJoin
```

This section is my attempt to create a column that has whither or not a team's name was in the "Win Condition" column with no luck. In the interest of time and sanity, I did decided to use excel to create this column and created a new file called tabdata.txt. I'm fairly certain that there is a way to do this in pandas, in fact I know ther is,  I just can't find it at the moment. If that changes or I decided to ask Kent about it, I'll put the pandas code here. But for now, I'm using tabdata.txt


```python

#matchesJoin['specialHomeWin'] = any(x in str(matchesJoin['Home Team Name']) for x in str('Win conditions').split())
#matchesJoin = matchesJoin.drop(['SpecialHomeWin'],axis=1)
#matchesJoin['homeWin'] = matchesJoin['Home Team Goals'] > matchesJoin['Away Team Goals']
```


```python
matchesJoin = pd.read_csv('tabdata.txt', sep="\t")
#matchesJoin
```

Once I've got a column that says whither the team won with a special condition or not. The next step was to create a column called home win. This boolean column would be true if the hom team won, and false if the home team lost. 


```python
matchesJoin['Home Win'] = (matchesJoin['Home Team Goals'] > matchesJoin['Away Team Goals']) | (matchesJoin['Special Win Home'] == True)
```

I added a column called "isHome" which is another boolean column but this time says true if the host team was in that match, and false if they weren't. 


```python
matchesJoin['isHome'] = (matchesJoin['Home Team Name'] == matchesJoin['Country']) | (matchesJoin['Away Team Name'] == matchesJoin['Country'])
matchesJoin[['Home Team Goals', 'Away Team Goals','Special Win Home','Special Win Away','Home Win']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Home Team Goals</th>
      <th>Away Team Goals</th>
      <th>Special Win Home</th>
      <th>Special Win Away</th>
      <th>Home Win</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
      <td>3</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>4</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>3</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>15</th>
      <td>6</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>16</th>
      <td>6</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>17</th>
      <td>4</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>18</th>
      <td>3</td>
      <td>2</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>19</th>
      <td>4</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>20</th>
      <td>3</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>22</th>
      <td>5</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>23</th>
      <td>3</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>24</th>
      <td>7</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>822</th>
      <td>2</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>823</th>
      <td>2</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>824</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>825</th>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>826</th>
      <td>1</td>
      <td>7</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>827</th>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>828</th>
      <td>1</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>829</th>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>830</th>
      <td>0</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>831</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>832</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>833</th>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>834</th>
      <td>1</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>835</th>
      <td>2</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>836</th>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>837</th>
      <td>2</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>838</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>839</th>
      <td>1</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>840</th>
      <td>2</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>841</th>
      <td>2</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>842</th>
      <td>1</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>843</th>
      <td>2</td>
      <td>1</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>844</th>
      <td>0</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>845</th>
      <td>2</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>846</th>
      <td>1</td>
      <td>0</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>847</th>
      <td>0</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>848</th>
      <td>1</td>
      <td>7</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>849</th>
      <td>0</td>
      <td>0</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>850</th>
      <td>0</td>
      <td>3</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>851</th>
      <td>1</td>
      <td>0</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>852 rows × 5 columns</p>
</div>



Next I created a new dataframe that had all time the host team was in a match. This dataframe will come in handy for the next part. But for now, all I need is the matches the host country played. So the dataframe hostMatch dataframe has all games that the host country participanted in.  


```python
home = matchesJoin[(matchesJoin['isHome'] == True)]
hostMatch = home[((home['Home Team Name'] == home['Country']) & (home['Home Win'] == True))|((home['Away Team Name'] == home['Country']) & (home['Home Win'] == False))]
hostMatch[['Home Team Name','Home Team Goals','Away Team Goals','Away Team Name','Home Win','Country']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Home Team Name</th>
      <th>Home Team Goals</th>
      <th>Away Team Goals</th>
      <th>Away Team Name</th>
      <th>Home Win</th>
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>Uruguay</td>
      <td>1</td>
      <td>0</td>
      <td>Peru</td>
      <td>True</td>
      <td>Uruguay</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Uruguay</td>
      <td>4</td>
      <td>0</td>
      <td>Romania</td>
      <td>True</td>
      <td>Uruguay</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Uruguay</td>
      <td>6</td>
      <td>1</td>
      <td>Yugoslavia</td>
      <td>True</td>
      <td>Uruguay</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Uruguay</td>
      <td>4</td>
      <td>2</td>
      <td>Argentina</td>
      <td>True</td>
      <td>Uruguay</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Italy</td>
      <td>7</td>
      <td>1</td>
      <td>USA</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Italy</td>
      <td>1</td>
      <td>0</td>
      <td>Spain</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Italy</td>
      <td>1</td>
      <td>0</td>
      <td>Austria</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Italy</td>
      <td>2</td>
      <td>1</td>
      <td>Czechoslovakia</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>37</th>
      <td>France</td>
      <td>3</td>
      <td>1</td>
      <td>Belgium</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Brazil</td>
      <td>4</td>
      <td>0</td>
      <td>Mexico</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Brazil</td>
      <td>2</td>
      <td>0</td>
      <td>Yugoslavia</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Brazil</td>
      <td>7</td>
      <td>1</td>
      <td>Sweden</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Brazil</td>
      <td>6</td>
      <td>1</td>
      <td>Spain</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Switzerland</td>
      <td>2</td>
      <td>1</td>
      <td>Italy</td>
      <td>True</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>92</th>
      <td>Switzerland</td>
      <td>4</td>
      <td>1</td>
      <td>Italy</td>
      <td>True</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sweden</td>
      <td>3</td>
      <td>0</td>
      <td>Mexico</td>
      <td>True</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Sweden</td>
      <td>2</td>
      <td>1</td>
      <td>Hungary</td>
      <td>True</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Sweden</td>
      <td>2</td>
      <td>0</td>
      <td>Soviet Union</td>
      <td>True</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>132</th>
      <td>Sweden</td>
      <td>3</td>
      <td>1</td>
      <td>Germany FR</td>
      <td>True</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>139</th>
      <td>Chile</td>
      <td>3</td>
      <td>1</td>
      <td>Switzerland</td>
      <td>True</td>
      <td>Chile</td>
    </tr>
    <tr>
      <th>147</th>
      <td>Chile</td>
      <td>2</td>
      <td>0</td>
      <td>Italy</td>
      <td>True</td>
      <td>Chile</td>
    </tr>
    <tr>
      <th>160</th>
      <td>Chile</td>
      <td>2</td>
      <td>1</td>
      <td>Soviet Union</td>
      <td>True</td>
      <td>Chile</td>
    </tr>
    <tr>
      <th>166</th>
      <td>Chile</td>
      <td>1</td>
      <td>0</td>
      <td>Yugoslavia</td>
      <td>True</td>
      <td>Chile</td>
    </tr>
    <tr>
      <th>183</th>
      <td>England</td>
      <td>2</td>
      <td>0</td>
      <td>Mexico</td>
      <td>True</td>
      <td>England</td>
    </tr>
    <tr>
      <th>188</th>
      <td>England</td>
      <td>2</td>
      <td>0</td>
      <td>France</td>
      <td>True</td>
      <td>England</td>
    </tr>
    <tr>
      <th>192</th>
      <td>England</td>
      <td>1</td>
      <td>0</td>
      <td>Argentina</td>
      <td>True</td>
      <td>England</td>
    </tr>
    <tr>
      <th>197</th>
      <td>England</td>
      <td>2</td>
      <td>1</td>
      <td>Portugal</td>
      <td>True</td>
      <td>England</td>
    </tr>
    <tr>
      <th>199</th>
      <td>England</td>
      <td>4</td>
      <td>2</td>
      <td>Germany FR</td>
      <td>True</td>
      <td>England</td>
    </tr>
    <tr>
      <th>215</th>
      <td>Mexico</td>
      <td>4</td>
      <td>0</td>
      <td>El Salvador</td>
      <td>True</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Mexico</td>
      <td>1</td>
      <td>0</td>
      <td>Belgium</td>
      <td>True</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>367</th>
      <td>Belgium</td>
      <td>1</td>
      <td>2</td>
      <td>Mexico</td>
      <td>False</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>389</th>
      <td>Iraq</td>
      <td>0</td>
      <td>1</td>
      <td>Mexico</td>
      <td>False</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>397</th>
      <td>Mexico</td>
      <td>2</td>
      <td>0</td>
      <td>Bulgaria</td>
      <td>True</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>415</th>
      <td>Italy</td>
      <td>1</td>
      <td>0</td>
      <td>Austria</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>427</th>
      <td>Italy</td>
      <td>1</td>
      <td>0</td>
      <td>USA</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>440</th>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>Czechoslovakia</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>453</th>
      <td>Italy</td>
      <td>2</td>
      <td>0</td>
      <td>Uruguay</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>457</th>
      <td>Italy</td>
      <td>1</td>
      <td>0</td>
      <td>rn"&gt;Republic of Ireland</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>462</th>
      <td>Italy</td>
      <td>2</td>
      <td>1</td>
      <td>England</td>
      <td>True</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>478</th>
      <td>USA</td>
      <td>2</td>
      <td>1</td>
      <td>Colombia</td>
      <td>True</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>522</th>
      <td>France</td>
      <td>3</td>
      <td>0</td>
      <td>South Africa</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>537</th>
      <td>France</td>
      <td>4</td>
      <td>0</td>
      <td>Saudi Arabia</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>552</th>
      <td>France</td>
      <td>2</td>
      <td>1</td>
      <td>Denmark</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>566</th>
      <td>France</td>
      <td>1</td>
      <td>0</td>
      <td>Paraguay</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>572</th>
      <td>Italy</td>
      <td>0</td>
      <td>0</td>
      <td>France</td>
      <td>False</td>
      <td>France</td>
    </tr>
    <tr>
      <th>577</th>
      <td>France</td>
      <td>2</td>
      <td>1</td>
      <td>Croatia</td>
      <td>True</td>
      <td>France</td>
    </tr>
    <tr>
      <th>579</th>
      <td>Brazil</td>
      <td>0</td>
      <td>3</td>
      <td>France</td>
      <td>False</td>
      <td>France</td>
    </tr>
    <tr>
      <th>644</th>
      <td>Germany</td>
      <td>4</td>
      <td>2</td>
      <td>Costa Rica</td>
      <td>True</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>660</th>
      <td>Germany</td>
      <td>1</td>
      <td>0</td>
      <td>Poland</td>
      <td>True</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>676</th>
      <td>Ecuador</td>
      <td>0</td>
      <td>3</td>
      <td>Germany</td>
      <td>False</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>692</th>
      <td>Germany</td>
      <td>2</td>
      <td>0</td>
      <td>Sweden</td>
      <td>True</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>700</th>
      <td>Germany</td>
      <td>1</td>
      <td>1</td>
      <td>Argentina</td>
      <td>True</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>706</th>
      <td>Germany</td>
      <td>3</td>
      <td>1</td>
      <td>Portugal</td>
      <td>True</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>741</th>
      <td>France</td>
      <td>1</td>
      <td>2</td>
      <td>South Africa</td>
      <td>False</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>772</th>
      <td>Brazil</td>
      <td>3</td>
      <td>1</td>
      <td>Croatia</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>806</th>
      <td>Cameroon</td>
      <td>1</td>
      <td>4</td>
      <td>Brazil</td>
      <td>False</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>820</th>
      <td>Brazil</td>
      <td>1</td>
      <td>1</td>
      <td>Chile</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>824</th>
      <td>Brazil</td>
      <td>2</td>
      <td>1</td>
      <td>Colombia</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>836</th>
      <td>Brazil</td>
      <td>1</td>
      <td>1</td>
      <td>Chile</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>845</th>
      <td>Brazil</td>
      <td>2</td>
      <td>1</td>
      <td>Colombia</td>
      <td>True</td>
      <td>Brazil</td>
    </tr>
  </tbody>
</table>
<p>66 rows × 6 columns</p>
</div>



Here we have the first "new" dataframe that was created. what I mean is, this is the first dataframe that doesn't just get a subset of the orginal dataframe. homeWinGroup is a groupby dataframe that counts the amount of times the host country won by Year, that way we can visuilze the change in host country wins over time. the next three columns added "total","lost",and "ratio" are pretty self-explanitory, but I'm going to explain them anyway.

Total is the number of games the host country played

lost is the number they lost

ratio is the ratio of total wins over total games. 


```python
homeWinGroup= hostMatch[['Home Win','Year']].groupby('Year').count()
homeWinGroup['Total']= matchesJoin[(matchesJoin['isHome'] == True)][['isHome','Year']].groupby('Year').count()
homeWinGroup['Lost'] = homeWinGroup['Total'] - homeWinGroup['Home Win']
homeWinGroup['Ratio'] = homeWinGroup['Home Win']/homeWinGroup['Total']
homeWinGroup
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Home Win</th>
      <th>Total</th>
      <th>Lost</th>
      <th>Ratio</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1930</th>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>1934</th>
      <td>4</td>
      <td>5</td>
      <td>1</td>
      <td>0.800000</td>
    </tr>
    <tr>
      <th>1938</th>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>1950</th>
      <td>4</td>
      <td>6</td>
      <td>2</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>1954</th>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>1958</th>
      <td>4</td>
      <td>6</td>
      <td>2</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>1962</th>
      <td>4</td>
      <td>6</td>
      <td>2</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>1966</th>
      <td>5</td>
      <td>6</td>
      <td>1</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>1970</th>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>5</td>
      <td>7</td>
      <td>2</td>
      <td>0.714286</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>3</td>
      <td>5</td>
      <td>2</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>6</td>
      <td>7</td>
      <td>1</td>
      <td>0.857143</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>1</td>
      <td>4</td>
      <td>3</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>7</td>
      <td>7</td>
      <td>0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>6</td>
      <td>7</td>
      <td>1</td>
      <td>0.857143</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>6</td>
      <td>11</td>
      <td>5</td>
      <td>0.545455</td>
    </tr>
  </tbody>
</table>
</div>



Finally, I create three graphs. the first one show the total number of wins by a host country over time. The second shows the percent of wins of a host country over time. And finally, the last graph shows how often a host country will get a certain percet of won matches. 


```python
homeWinGroup.reset_index(inplace=True)
plt.figure(figsize=(20,5))
plt.subplot('131')
plt.scatter('Year','Home Win',data=homeWinGroup)
plt.ylabel('Number of Host Wins')
plt.xlabel('Year')
plt.title('Number of Total Host Wins each Year')
plt.subplot('132')
plt.scatter('Year','Ratio',data=homeWinGroup)
plt.ylabel('Percent of Games Won')
plt.xlabel('Year')
plt.title('The Percent of Games that a Host team won each Year' )
plt.subplot('133')
plt.hist('Ratio',data=homeWinGroup,bins=[0.5, 0.55,0.6, 0.65,0.7, 0.75,0.8, 0.85, 0.9,0.95,1])
plt.ylabel('Number Of Percents')
plt.xlabel('Percent of Games Won')
plt.title('How Often does a host team get a specific Percent of wins' )
plt.text(0.78, 2.5, r'Mean = 0.6', fontsize=15)
plt.show()
```


![png](output_36_0.png)



```python
homeWinGroup.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Home Win</th>
      <th>Total</th>
      <th>Lost</th>
      <th>Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>18.000000</td>
      <td>18.000000</td>
      <td>18.000000</td>
      <td>18.000000</td>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1973.333333</td>
      <td>3.666667</td>
      <td>5.500000</td>
      <td>1.833333</td>
      <td>0.638372</td>
    </tr>
    <tr>
      <th>std</th>
      <td>26.184863</td>
      <td>1.970369</td>
      <td>2.007339</td>
      <td>1.248529</td>
      <td>0.234291</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1930.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1955.000000</td>
      <td>2.000000</td>
      <td>4.000000</td>
      <td>1.000000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1974.000000</td>
      <td>4.000000</td>
      <td>5.500000</td>
      <td>2.000000</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1993.000000</td>
      <td>5.000000</td>
      <td>6.750000</td>
      <td>2.000000</td>
      <td>0.825000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2014.000000</td>
      <td>7.000000</td>
      <td>11.000000</td>
      <td>5.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



### Analysis of Host Team Advantage
from these three graphs, it's clear that there isn't much of an increase of whither or not a time will win a match if they are the host country, over time and in general. We can see this from the fact that there is no clear linear pattern or any pattern with either of the two scatter graphs. However, while the mean ratio of wins for a host country is over 50% say that on average, the host team has a greater then 50% chance of winning. I would agrue that this increase isn't enough for there to be any significant evidence that being the host country makes you more likely to win a match. More then likely, the match would have been won regardless of there host status. One thing to note, however, is the slight inversion of the total vs year compared to ratio vs year. This will be shown off in more detail in the next graphs. 

## Home Field Advantage (General)
Now that we have graphs on whither or not a host time has won a match, it's clear that the next step should be to answer the question, does being the "home team" in a match increase your chances of winning? does this change over time? 

So here I create a new groupby dataframe called homeTeamWin. I then create a few columns which are similar to homeWinGroupbut instead have all matches played each world cup rather then just the host countries games. 


```python
homeTeamWin= matchesJoin[['Home Win','Year']].groupby('Year').count()

homeTeamWin['Total'] = matchesJoin[['Home Win','Year']].groupby('Year').count()
homeTeamWin.drop(['Home Win'],axis=1,inplace=True)
homeTeamWin['Won'] = matchesJoin[matchesJoin['Home Win'] == True][['Home Win','Year']].groupby('Year').count()
homeTeamWin['Lost'] = homeTeamWin['Total'] - homeTeamWin['Won']
homeTeamWin['Ratio'] = homeTeamWin['Won']/homeTeamWin['Total']
homeTeamWin.reset_index(inplace=True)
homeTeamWin
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Total</th>
      <th>Won</th>
      <th>Lost</th>
      <th>Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1930</td>
      <td>18</td>
      <td>18</td>
      <td>0</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1934</td>
      <td>17</td>
      <td>16</td>
      <td>1</td>
      <td>0.941176</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1938</td>
      <td>18</td>
      <td>15</td>
      <td>3</td>
      <td>0.833333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1950</td>
      <td>22</td>
      <td>19</td>
      <td>3</td>
      <td>0.863636</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1954</td>
      <td>26</td>
      <td>24</td>
      <td>2</td>
      <td>0.923077</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1958</td>
      <td>35</td>
      <td>24</td>
      <td>11</td>
      <td>0.685714</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1962</td>
      <td>32</td>
      <td>27</td>
      <td>5</td>
      <td>0.843750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1966</td>
      <td>32</td>
      <td>27</td>
      <td>5</td>
      <td>0.843750</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1970</td>
      <td>32</td>
      <td>27</td>
      <td>5</td>
      <td>0.843750</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1974</td>
      <td>38</td>
      <td>15</td>
      <td>23</td>
      <td>0.394737</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1978</td>
      <td>38</td>
      <td>29</td>
      <td>9</td>
      <td>0.763158</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1982</td>
      <td>52</td>
      <td>26</td>
      <td>26</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1986</td>
      <td>52</td>
      <td>22</td>
      <td>30</td>
      <td>0.423077</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1990</td>
      <td>52</td>
      <td>27</td>
      <td>25</td>
      <td>0.519231</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1994</td>
      <td>52</td>
      <td>27</td>
      <td>25</td>
      <td>0.519231</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1998</td>
      <td>64</td>
      <td>30</td>
      <td>34</td>
      <td>0.468750</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2002</td>
      <td>64</td>
      <td>28</td>
      <td>36</td>
      <td>0.437500</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2006</td>
      <td>64</td>
      <td>34</td>
      <td>30</td>
      <td>0.531250</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2010</td>
      <td>64</td>
      <td>25</td>
      <td>39</td>
      <td>0.390625</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2014</td>
      <td>80</td>
      <td>43</td>
      <td>37</td>
      <td>0.537500</td>
    </tr>
  </tbody>
</table>
</div>



I then create three graphs which are the same as before


```python

plt.figure(figsize=(15,5))
plt.subplot('131')
plt.scatter('Year','Won',data=homeTeamWin)
plt.ylabel('Number of Home Wins')
plt.xlabel('Year')
plt.title('Number of Total Home Wins each Year')
plt.subplot('132')
plt.scatter('Year','Ratio',data=homeTeamWin)
plt.ylabel('Percent of Home Wins')
plt.xlabel('Year')
plt.title('Percent of Home Wins each Year')
plt.text(1960, .9, r'Mean = 0.864 SD = 0.088 before 1970', fontsize=8)
plt.text(1930, .55, r'Mean = 0.498 SD = 0.103 after 1970', fontsize=8)
plt.annotate("1970",xy=(1970,.84),xytext=(1970, .6),arrowprops=dict(facecolor='black', shrink=0.05),)
plt.subplot('133')
plt.hist('Ratio',data=homeTeamWin,rwidth=0.5,bins=[0.4, 0.45,0.5, 0.55,0.6, 0.65,0.7, 0.75,0.8, 0.85, 0.9,0.95,1])
plt.ylabel('Number of Percent of Home Wins')
plt.xlabel('Percent of Home Wins')
plt.title('Histogram of Percents')
plt.text(0.575, 3, r'Mean = 0.66', fontsize=13)
plt.show()
```


![png](output_42_0.png)



```python
print(homeTeamWin[homeTeamWin['Year'] <= 1970].describe())
print(homeTeamWin.describe())
homeTeamWin[homeTeamWin['Year'] > 1970].describe()
```

                  Year      Total        Won       Lost     Ratio
    count     9.000000   9.000000   9.000000   9.000000  9.000000
    mean   1951.333333  25.777778  21.888889   3.888889  0.864243
    std      14.422205   7.189885   4.910307   3.218868  0.087962
    min    1930.000000  17.000000  15.000000   0.000000  0.685714
    25%    1938.000000  18.000000  18.000000   2.000000  0.843750
    50%    1954.000000  26.000000  24.000000   3.000000  0.843750
    75%    1962.000000  32.000000  27.000000   5.000000  0.923077
    max    1970.000000  35.000000  27.000000  11.000000  1.000000
                  Year      Total        Won       Lost      Ratio
    count    20.000000  20.000000  20.000000  20.000000  20.000000
    mean   1974.800000  42.600000  25.150000  17.450000   0.663162
    std      25.582889  18.619175   6.698586  14.155062   0.208974
    min    1930.000000  17.000000  15.000000   0.000000   0.390625
    25%    1957.000000  30.500000  21.250000   4.500000   0.492188
    50%    1976.000000  38.000000  26.500000  17.000000   0.611607
    75%    1995.000000  55.000000  27.250000  30.000000   0.843750
    max    2014.000000  80.000000  43.000000  39.000000   1.000000





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Total</th>
      <th>Won</th>
      <th>Lost</th>
      <th>Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1994.000000</td>
      <td>56.363636</td>
      <td>27.818182</td>
      <td>28.545455</td>
      <td>0.498642</td>
    </tr>
    <tr>
      <th>std</th>
      <td>13.266499</td>
      <td>12.419925</td>
      <td>6.968761</td>
      <td>8.454154</td>
      <td>0.103052</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1974.000000</td>
      <td>38.000000</td>
      <td>15.000000</td>
      <td>9.000000</td>
      <td>0.390625</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1984.000000</td>
      <td>52.000000</td>
      <td>25.500000</td>
      <td>25.000000</td>
      <td>0.430288</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1994.000000</td>
      <td>52.000000</td>
      <td>27.000000</td>
      <td>30.000000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2004.000000</td>
      <td>64.000000</td>
      <td>29.500000</td>
      <td>35.000000</td>
      <td>0.525240</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2014.000000</td>
      <td>80.000000</td>
      <td>43.000000</td>
      <td>39.000000</td>
      <td>0.763158</td>
    </tr>
  </tbody>
</table>
</div>



### Analysis of Home Team Advantage (General)
From the three graphs, it's clear that there was a one point a very signficant home field advantage. It seems that before 1970, if you were the home team, you were almost certain to win. And with a standerd deveation of 0.087, 50% is clearly not close to the mean. However, after 1970, the mean ratio of wins is closer to 50% being within one standerd deviation, making it clearly close to 50%. So this means that at one point, there was a significant chance of winning if you were the home team. But now a days, it is more random. Also from the first graph, you can see a postive linear slope that shows that as time went on, more matches were played. 


```python
totalWins = finalCompared[['Winner','Country']].groupby('Winner').count()
totalWins.loc['Germany'] = 4
totalWins.drop('Germany FR', axis=0 ,inplace=True)
totalWins.reset_index(inplace=True)
```


```python
plt.bar('Winner','Country',data=totalWins)
plt.xticks(rotation=90)
plt.ylabel('Number of First Places')
plt.xlabel('Country')
plt.title('Bar Graph of Total Winners')
plt.show()
```


![png](output_46_0.png)



```python

matchesJoin.loc[matchesJoin['Home Win'] == True, 'Winner Country'] = matchesJoin['Home Team Name']
matchesJoin.loc[matchesJoin['Home Win'] == False, 'Winner Country'] = matchesJoin['Away Team Name']
matchesJoin['Winner Country']
```




    0              France
    1                 USA
    2          Yugoslavia
    3             Romania
    4           Argentina
    5               Chile
    6          Yugoslavia
    7                 USA
    8             Uruguay
    9               Chile
    10          Argentina
    11             Brazil
    12           Paraguay
    13            Uruguay
    14          Argentina
    15          Argentina
    16            Uruguay
    17            Uruguay
    18            Austria
    19            Hungary
    20        Switzerland
    21             Sweden
    22            Germany
    23              Spain
    24              Italy
    25     Czechoslovakia
    26     Czechoslovakia
    27            Germany
    28              Spain
    29            Austria
                ...      
    822            France
    823           Germany
    824            Brazil
    825           Germany
    826           Germany
    827       Netherlands
    828           Germany
    829         Argentina
    830       Netherlands
    831         Argentina
    832       Netherlands
    833        Costa Rica
    834         Argentina
    835           Belgium
    836            Brazil
    837          Colombia
    838       Netherlands
    839        Costa Rica
    840            France
    841           Germany
    842         Argentina
    843           Belgium
    844           Germany
    845            Brazil
    846         Argentina
    847       Netherlands
    848           Germany
    849         Argentina
    850       Netherlands
    851           Germany
    Name: Winner Country, Length: 852, dtype: object




```python
totalMatchWins = matchesJoin[['Winner Country','Country']].groupby('Winner Country').count()
totalMatchWins.reset_index(inplace=True)
totalMatchWins
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Winner Country</th>
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Algeria</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Argentina</td>
      <td>54</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Australia</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Austria</td>
      <td>15</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Belgium</td>
      <td>21</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bolivia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brazil</td>
      <td>79</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Bulgaria</td>
      <td>8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Cameroon</td>
      <td>9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chile</td>
      <td>14</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Colombia</td>
      <td>10</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Costa Rica</td>
      <td>7</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Croatia</td>
      <td>8</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Cuba</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Czech Republic</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Czechoslovakia</td>
      <td>15</td>
    </tr>
    <tr>
      <th>17</th>
      <td>C�te d'Ivoire</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Denmark</td>
      <td>9</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Ecuador</td>
      <td>4</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Egypt</td>
      <td>2</td>
    </tr>
    <tr>
      <th>21</th>
      <td>England</td>
      <td>34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>France</td>
      <td>34</td>
    </tr>
    <tr>
      <th>23</th>
      <td>German DR</td>
      <td>4</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Germany</td>
      <td>36</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Germany FR</td>
      <td>38</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Ghana</td>
      <td>5</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Greece</td>
      <td>3</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Honduras</td>
      <td>2</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Hungary</td>
      <td>16</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>42</th>
      <td>New Zealand</td>
      <td>2</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Nigeria</td>
      <td>6</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Northern Ireland</td>
      <td>8</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Norway</td>
      <td>5</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Paraguay</td>
      <td>12</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Peru</td>
      <td>6</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Poland</td>
      <td>18</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Portugal</td>
      <td>16</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Romania</td>
      <td>11</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Russia</td>
      <td>3</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Saudi Arabia</td>
      <td>4</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Scotland</td>
      <td>6</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Senegal</td>
      <td>3</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Serbia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Slovakia</td>
      <td>2</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Slovenia</td>
      <td>1</td>
    </tr>
    <tr>
      <th>58</th>
      <td>South Africa</td>
      <td>3</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Soviet Union</td>
      <td>18</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Spain</td>
      <td>35</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Sweden</td>
      <td>22</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Switzerland</td>
      <td>14</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Tunisia</td>
      <td>3</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Turkey</td>
      <td>6</td>
    </tr>
    <tr>
      <th>65</th>
      <td>USA</td>
      <td>12</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Ukraine</td>
      <td>3</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Uruguay</td>
      <td>26</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Wales</td>
      <td>4</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Yugoslavia</td>
      <td>21</td>
    </tr>
    <tr>
      <th>70</th>
      <td>rn"&gt;Bosnia and Herzegovina</td>
      <td>1</td>
    </tr>
    <tr>
      <th>71</th>
      <td>rn"&gt;Republic of Ireland</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
<p>72 rows × 2 columns</p>
</div>




```python
plt.figure(figsize = (25,10))
plt.bar('Winner Country','Country',data=totalMatchWins)
plt.xticks(rotation=90)
plt.ylabel('Number of matches won')
plt.xlabel('Country')
plt.title('Matches a Country has Won')
plt.show()
```


![png](output_49_0.png)



```python
from ipywidgets import interact #interactive, fixed, interact_manual
import ipywidgets as widgets
totalMatchesWonByYear = matchesJoin[['Winner Country','Country','Year']].groupby(['Year','Winner Country']).count()
totalMatchesWonByYear.reset_index(inplace=True)
def f(x):
    currentBar = plt.bar('Winner Country','Country',data=totalMatchesWonByYear[totalMatchesWonByYear['Year'] == x])
    plt.ylim(0,10)
    plt.xticks(rotation=90)
    plt.ylabel('Number of Matches Won')
    plt.xlabel('Country')
    plt.title('Number of Matches Won in ' + str(x))
interact(f,x=(1930,2015,4))

```


<p>Failed to display Jupyter Widget of type <code>interactive</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>






    <function __main__.f(x)>




```python
matchesJoin.columns
```




    Index(['Year', 'Datetime', 'Stage', 'Stadium', 'City', 'Home Team Name',
           'Home Team Goals', 'Away Team Goals', 'Away Team Name',
           'Win conditions', 'Attendance', 'Half-time Home Goals',
           'Half-time Away Goals', 'Referee', 'Assistant 1', 'Assistant 2',
           'RoundID', 'MatchID', 'Home Team Initials', 'Away Team Initials',
           'Country', 'Winner', 'Runners-Up', 'Third', 'Fourth', 'GoalsScored',
           'QualifiedTeams', 'MatchesPlayed', 'isHome', 'Special Win Home',
           'Special Win Away', 'Home Win', 'Winner Country'],
          dtype='object')




```python
matchesJoin['TotalScore'] = matchesJoin['Away Team Goals'] + matchesJoin['Home Team Goals']
groupByScore = matchesJoin[['TotalScore','Year']].groupby(['Year']).sum()
groupByScore['TotalGames'] = matchesJoin[['Year','Winner Country']].groupby(['Year']).count()
groupByScore['ScoresPerGame'] = groupByScore['TotalScore']/groupByScore['TotalGames']
groupByScore['AverageAttendence'] = matchesJoin[['Year','Attendance']].groupby(['Year']).sum()
groupByScore['AverageAttendence'] = groupByScore['AverageAttendence']/groupByScore['TotalGames']
groupByScore.reset_index(inplace=True)
groupByScore
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>TotalScore</th>
      <th>TotalGames</th>
      <th>ScoresPerGame</th>
      <th>AverageAttendence</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1930</td>
      <td>70</td>
      <td>18</td>
      <td>3.888889</td>
      <td>32808.277778</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1934</td>
      <td>70</td>
      <td>17</td>
      <td>4.117647</td>
      <td>21352.941176</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1938</td>
      <td>84</td>
      <td>18</td>
      <td>4.666667</td>
      <td>20872.222222</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1950</td>
      <td>88</td>
      <td>22</td>
      <td>4.000000</td>
      <td>47511.181818</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1954</td>
      <td>140</td>
      <td>26</td>
      <td>5.384615</td>
      <td>29561.807692</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1958</td>
      <td>126</td>
      <td>35</td>
      <td>3.600000</td>
      <td>23423.142857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1962</td>
      <td>89</td>
      <td>32</td>
      <td>2.781250</td>
      <td>27911.625000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1966</td>
      <td>89</td>
      <td>32</td>
      <td>2.781250</td>
      <td>48847.968750</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1970</td>
      <td>95</td>
      <td>32</td>
      <td>2.968750</td>
      <td>50124.218750</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1974</td>
      <td>97</td>
      <td>38</td>
      <td>2.552632</td>
      <td>49098.763158</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1978</td>
      <td>102</td>
      <td>38</td>
      <td>2.684211</td>
      <td>40678.710526</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1982</td>
      <td>146</td>
      <td>52</td>
      <td>2.807692</td>
      <td>40571.596154</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1986</td>
      <td>132</td>
      <td>52</td>
      <td>2.538462</td>
      <td>46039.057692</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1990</td>
      <td>115</td>
      <td>52</td>
      <td>2.211538</td>
      <td>48388.750000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1994</td>
      <td>141</td>
      <td>52</td>
      <td>2.711538</td>
      <td>68991.115385</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1998</td>
      <td>171</td>
      <td>64</td>
      <td>2.671875</td>
      <td>43517.187500</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2002</td>
      <td>161</td>
      <td>64</td>
      <td>2.515625</td>
      <td>42268.703125</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2006</td>
      <td>147</td>
      <td>64</td>
      <td>2.296875</td>
      <td>52491.234375</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2010</td>
      <td>145</td>
      <td>64</td>
      <td>2.265625</td>
      <td>49669.625000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2014</td>
      <td>206</td>
      <td>80</td>
      <td>2.575000</td>
      <td>53990.537500</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.linear_model import LinearRegression
from sklearn.cross_validation import train_test_split
from numpy.polynomial.polynomial import polyfit
#test = train_test_split(groupByScore['Year'],groupByScore['TotalScore'])
#test
linreg = LinearRegression()
linreg.fit(groupByScore['Year'].reshape(-1,1),groupByScore['TotalScore'])
print(linreg.intercept_)
print(linreg.coef_)
x = np.arange(10)
y = 5 * x + 10

# Fit with polyfit
b, m = polyfit(x, y, 1)

```

    -2209.447117858981
    [1.17994081]


    /usr/local/lib/python3.5/site-packages/ipykernel_launcher.py:7: FutureWarning: reshape is deprecated and will raise in a subsequent release. Please use .values.reshape(...) instead
      import sys



```python

plt.figure(figsize=(15,5))
plt.subplot('121')
plt.scatter('Year','TotalScore',data=groupByScore)
plt.annotate('1954', xy = (1954,140), xytext = (1960,160),arrowprops=dict(facecolor='black',shrink=0.05))
plt.ylabel('Number of Scores')
plt.xlabel('Year')
plt.title('Number of Scores vs. Year')
plt.subplot('122')
plt.scatter('Year','ScoresPerGame',data=groupByScore)
plt.annotate('1954', xy = (1954,5.38), xytext = (1960,5),arrowprops=dict(facecolor='black',shrink=0.05))
plt.ylabel('Number of Scores per Game')
plt.xlabel('Year')
plt.title('Number of Scores per Game vs. Year')
plt.show()
```


![png](output_54_0.png)



```python
plt.figure(figsize=(20,5))
plt.subplot('131')
plt.scatter('Year','AverageAttendence',data=groupByScore)
plt.annotate('1994', xy = (1994,68990), xytext = (1980,69000),arrowprops=dict(facecolor='black',shrink=0.05))
plt.ylabel('Average Attendence per Game')
plt.xlabel('Year')
plt.title('Average Attendence per Game vs. Year')
plt.subplot('132')
plt.scatter('TotalScore','AverageAttendence',data=groupByScore)
plt.annotate('1994', xy = (141,68990), xytext = (110,69000),arrowprops=dict(facecolor='black',shrink=0.05))
plt.ylabel('Average Attendence per Game')
plt.xlabel('Total Scores')
plt.title('Average Attendence per Game vs. Total Scores that Year')
plt.subplot('133')
plt.scatter('ScoresPerGame','AverageAttendence',data=groupByScore)
plt.annotate('1994', xy = (2.7,68990), xytext = (3.5,69000),arrowprops=dict(facecolor='black',shrink=0.05))
plt.ylabel('Average Attendence per Game')
plt.xlabel('Average Score per Game')
plt.title('Average Attendence vs. Average Scores per Game')
plt.show()
```


![png](output_55_0.png)



```python
matchesJoin.columns
```




    Index(['Year', 'Datetime', 'Stage', 'Stadium', 'City', 'Home Team Name',
           'Home Team Goals', 'Away Team Goals', 'Away Team Name',
           'Win conditions', 'Attendance', 'Half-time Home Goals',
           'Half-time Away Goals', 'Referee', 'Assistant 1', 'Assistant 2',
           'RoundID', 'MatchID', 'Home Team Initials', 'Away Team Initials',
           'Country', 'Winner', 'Runners-Up', 'Third', 'Fourth', 'GoalsScored',
           'QualifiedTeams', 'MatchesPlayed', 'isHome', 'Special Win Home',
           'Special Win Away', 'Home Win', 'Winner Country', 'TotalScore'],
          dtype='object')




```python
masterGroupbyFinalFour = pd.DataFrame()


groupByWinner = cups[['Winner','Year']].groupby('Winner').count()
groupByWinner.reset_index(inplace=True)
groupByWinner.columns = ['Country','WinnerCount']
#groupByWinner.set_index('Country',inplace=True)


groupByRunnersUp = cups[['Runners-Up','Year']].groupby('Runners-Up').count()
groupByRunnersUp.reset_index(inplace=True)
groupByRunnersUp.columns = ['Country','Runners-UpCount']
#groupByRunnersUp.set_index('Country',inplace=True)


groupByThird = cups[['Third','Year']].groupby('Third').count()
groupByThird.reset_index(inplace=True)
groupByThird.columns = ['Country','ThirdCount']
#groupByThird.set_index('Country',inplace=True)


groupByFourth = cups[['Fourth','Year']].groupby('Fourth').count()
groupByFourth.reset_index(inplace=True)
groupByFourth.columns = ['Country','FourthCount']
#groupByFourth.set_index('Country',inplace=True)

masterGroupbyFinalFour = pd.merge(groupByWinner,groupByRunnersUp,on='Country',how='outer')
masterGroupbyFinalFour = pd.merge(masterGroupbyFinalFour,groupByThird,on='Country',how='outer')
masterGroupbyFinalFour = pd.merge(masterGroupbyFinalFour,groupByFourth,on='Country',how='outer')
masterGroupbyFinalFour.set_index('Country',inplace=True)
masterGroupbyFinalFour.fillna(0,inplace=True)
masterGroupbyFinalFour

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>WinnerCount</th>
      <th>Runners-UpCount</th>
      <th>ThirdCount</th>
      <th>FourthCount</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Argentina</th>
      <td>2.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>5.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>England</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>France</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Germany FR</th>
      <td>3.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>4.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>Czechoslovakia</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Hungary</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Netherlands</th>
      <td>0.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Austria</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Croatia</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Poland</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Portugal</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Bulgaria</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Korea Republic</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Soviet Union</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Yugoslavia</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
masterGroupbyFinalFour.columns
```




    Index(['WinnerCount', 'Runners-UpCount', 'ThirdCount', 'FourthCount'], dtype='object')




```python
masterGroupbyFinalFour.plot.bar(stacked=True, figsize=(10,7))
#.loc[:,['WinnerCount', 'Runners-UpCount', 'ThirdCount', 'FourthCount']].plot.bar(stacked=True, figsize=(10,7))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f96c3cb0390>




![png](output_59_1.png)



```python
def f (x):
    masterGroupbyFinalFour = pd.DataFrame()

    groupByWinner = cups[cups['Year'] <= x][['Winner','Year']].groupby('Winner').count()
    groupByWinner.reset_index(inplace=True)
    groupByWinner.columns = ['Country','WinnerCount']
    #groupByWinner.set_index('Country',inplace=True)


    groupByRunnersUp = cups[cups['Year'] <= x][['Runners-Up','Year']].groupby('Runners-Up').count()
    groupByRunnersUp.reset_index(inplace=True)
    groupByRunnersUp.columns = ['Country','Runners-UpCount']
    #groupByRunnersUp.set_index('Country',inplace=True)


    groupByThird = cups[cups['Year'] <= x][['Third','Year']].groupby('Third').count()
    groupByThird.reset_index(inplace=True)
    groupByThird.columns = ['Country','ThirdCount']
    #groupByThird.set_index('Country',inplace=True)


    groupByFourth = cups[cups['Year'] <= x][['Fourth','Year']].groupby('Fourth').count()
    groupByFourth.reset_index(inplace=True)
    groupByFourth.columns = ['Country','FourthCount']
    #groupByFourth.set_index('Country',inplace=True)

    masterGroupbyFinalFour = pd.merge(groupByWinner,groupByRunnersUp,on='Country',how='outer')
    masterGroupbyFinalFour = pd.merge(masterGroupbyFinalFour,groupByThird,on='Country',how='outer')
    masterGroupbyFinalFour = pd.merge(masterGroupbyFinalFour,groupByFourth,on='Country',how='outer')
    masterGroupbyFinalFour.set_index('Country',inplace=True)
    masterGroupbyFinalFour.fillna(0,inplace=True)
    masterGroupbyFinalFour.plot.bar(stacked=True, figsize=(10,7))
    #.loc[:,['WinnerCount', 'Runners-UpCount', 'ThirdCount', 'FourthCount']]
    plt.title('Total Semi-Final Apperances Since ' + str(x))
interact(f,x=(1930,2015,4))
```


<p>Failed to display Jupyter Widget of type <code>interactive</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>






    <function __main__.f(x)>




```python
df = open('finalData.csv','w')
df.write(matchesJoin.to_csv())
```




    237492




```python
plt.figure(figsize=(10, 10))
plt.barh(cups.Year,cups.QualifiedTeams,alpha=0.5) 
plt.ylabel('Year')
plt.xlabel('QualifiedTeams')
plt.yticks(cups.Year, rotation=30)
plt.xticks(cups.QualifiedTeams)
plt.title('No of teams qualifying per year')
plt.show()
```


![png](output_62_0.png)

