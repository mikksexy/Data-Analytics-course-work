# Data Analytics course work
This is a showcase of a course work I did for TJTS4901 Database Systems and Data Analytics course in JYU in 2022.

The aim of the course was researching a topic of interest with data analysis methods. The course work started with finding an interesting dataset and coming up with research questions or hypotheses based on it. Next, a database was set up and the data was transformed and loaded into the system. In order to answer the research questions, SQL queries and visualizations were implemented in a BI analytics tool. The queries were later indexed for better performance. A dashboard was created out of the visualizations. Finally, the dashboard and the findings were reported in a video format.

## Stack used
Ubuntu VirtualBox  
PostgreSQL  
pgAdmin  
Metabase  
## Business area

I used to be an avid CS:GO player having competed in it at national level. Therefore, I wanted to find new insights from competition data by comparing what made the top teams stand out from their competition. 

From a business perspective, 

## About dataset
The dataset was based in an esports title CS:GO and data from its professional matches from hltv.org between 11/2015 and 3/2020.

https://www.kaggle.com/datasets/mateusdmachado/csgo-professional-matches

It comprised of four tables: results.csv, picks.csv, economy.csv, and players.csv. I built the following SQL schema based on it:  
<img width="951" height="731" alt="TJTS4901_rak" src="https://github.com/user-attachments/assets/dc61276c-70d6-4b26-9f0e-d5b351284af0" />

<details>
<summary>Click to see the queries used for creating the tables</summary>

```
code
```
</details>

## Results

### RQ1. The game received updates to its in-game economy on 10.10.2018 and 13.3.2019. Have the updates balanced out the matches?
The game consists of two opposing sides, terrorists and counter-terrorists. Terrorists' objective is to either eliminate their opponents or detonate a bomb. The counter-terrorists want to defend bombsites by either eliminating their opponents or defusing a planted bomb. During the match both teams play as both sides. A half consists of 15 rounds after which the sides are switched. The first team to get 16 rounds is the winner. Therefore, starting on the "easier" side is important, as there won't be enough rounds to play on the easier side if the first half didn't go well. Before the economic changes the matches were most likely heavily counter-terrorist (CT) favoured. Thus, starting the match on the CT side was seen advantageous. 

The updates tried to make the CT side economy more expensive. Thus, getting the necessary defensive gear would be more difficult. Therefore, the T side would have an advantage, hopefully balancing the sides. The balance could be observed from the CT side round win percentage or match length. The latter was observed and this led to the following findings:

<details>
<summary>Click to see the queries used for creating the tables</summary>

```
code
```
</details>

### RQ2.

### RQ3. 
