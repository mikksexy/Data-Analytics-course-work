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

From a business perspective, analyzing CS:GO match data is mostly beneficial for professional coaching staff, game developers, and the gambling industry.

## About dataset
The dataset was based in an esports title CS:GO and data from its professional matches from hltv.org between 11/2015 and 3/2020. It was downloaded from the following source:

https://www.kaggle.com/datasets/mateusdmachado/csgo-professional-matches

The aforementioned site has a sufficient explanation of the game. Anyhow, the game is played 5vs5 and it consists of two opposing sides, terrorists (T) and counter-terrorists (CT). Ts' objective is to either eliminate their opponents or detonate a bomb. The CTs want to defend bombsites by either eliminating their opponents or defusing the planted bomb. During the match both teams play as both sides. A half consists of 15 rounds after which the sides are switched. The first team to get to 16 rounds is the winner of the map. Each of the 7 maps are a different playing ground. Often a professional match consists of multiple maps played. Therefore, the matches are either best of 1, 3, or 5 maps. A veto process is also important as not every team can master all of the maps. 

The game has an in-game economy where every player gets an income after each round. Weapons and equipment can be purchased with the income that is based on round loss streak, kills, and objectives.

The dataset comprises of four tables: results.csv, picks.csv, economy.csv, and players.csv. I built the following SQL schema based on it:  
<img width="951" height="731" alt="TJTS4901_rak" src="https://github.com/user-attachments/assets/dc61276c-70d6-4b26-9f0e-d5b351284af0" />

<details>
<summary>Click to see the queries used for creating the tables</summary>

```
code
```
</details>

## Results

### RQ1. The game received updates to its in-game economy on 10.10.2018 and 13.3.2019. Have the updates made the matches more even?

The longer the match, the more entertaining it likely is. This balance could be observed either from the CT side round win percentage or the match length. The latter was observed and this led to the following findings:
![tk1](https://github.com/user-attachments/assets/32a75c4b-5eb2-470e-bf57-3722f2c910b4)

<details>

<summary>Click to see the queries used</summary>

```
code
```
</details>

Based on these results, the first update did not have a notable effect on the average match length. However, the second update had a more noticeable impact on rounds played. The matches were 0.5 rounds longer on average after the latter update. 

Conducting a t-test was also attempted. The first result, _t2_, comparing _map_length_before_ and _map_length_between_ was not notable. Instead, _t3_ with a value of 10.36 is remarkable when compared to a 99.95 % confidence with infinite degree of freedom, 3.291.

The annual averages of match lengths were also visualized:

![tk12](https://github.com/user-attachments/assets/43796993-0c46-4bf8-84b2-3bcdc54fb096)



<details>

<summary>Click to see the queries used</summary>

```
code
```
</details>

The graph shows that the trend of rounds played has been growing since 2016. The most remarkable difference was between 2018 and 2019 which could be explained by the update on 13.3.2019. However, a more interesting fact is that the value of _map_length_between_ was noticeable lower than the annual averages of both 2018 and 2019. Thus, the first update made the matches somewhat shorter. 

Something to note is that the data from 2015 and 2020 is only partial.

### RQ2.

### RQ3. 
