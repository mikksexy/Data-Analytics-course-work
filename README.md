# Data Analytics course work
This is a showcase of a course work I did for TJTS4901 Database Systems and Data Analytics course in JYU in 2022.

The aim of the course was researching a topic of interest with data analysis methods. The course work started with finding an interesting dataset and coming up with research questions or hypotheses based on it. Next, a database was set up and the data was transformed and loaded into the system. In order to answer the research questions, SQL queries and visualizations were implemented in a BI analytics tool. The queries were later indexed for better performance. A dashboard was created out of the visualizations. Finally, the dashboard and the findings were reported in a video format.

## Skills portrayed
+ Advanced SQL queries  
+ Reporting  
+ ETL  
+ Query optimization  

Things to improve on:
- Better suggestions for business improvements
- Visualizations
- Further transforming the data

## Tools used
Ubuntu in VirtualBox  
PostgreSQL  
pgAdmin  
Metabase  

## About dataset
The dataset was based in an esports title CS:GO and data from its professional matches from hltv.org between 11/2015 and 3/2020. It was downloaded from the following source:

https://www.kaggle.com/datasets/mateusdmachado/csgo-professional-matches

The aforementioned site has a sufficient explanation of the game. Anyhow, the game is played 5vs5 and it consists of two opposing sides, terrorists (T) and counter-terrorists (CT). Ts' objective is to either eliminate their opponents or detonate a bomb. The CTs want to defend bombsites by either eliminating their opponents or defusing the planted bomb. During the match both teams play as both sides. A half consists of 15 rounds after which the sides are switched. The first team to get to 16 rounds is the winner of the map. Each of the 7 maps are a different playing ground. Often a professional match consists of multiple maps played. Therefore, the matches are either best of 1, 3, or 5 maps. A veto process is also important as not every team can master all of the maps. 

The game has an in-game economy where every player gets an income after each round. Weapons and equipment can be purchased with the income that is based on round loss streak, kills, and objectives.

The dataset comprises of four tables: results.csv, picks.csv, economy.csv, and players.csv. I built the following SQL schema based on it:  
![Looginen_rakenne](https://github.com/user-attachments/assets/c02511a9-38d4-4cbc-a29f-8379ea65afb5)


<details>
<summary>Click to see the queries used for creating the tables</summary>

```
/*
 * Author: Sami Mikkola
 * Steps for loading the data
 *  - Download and install Postgres on your machine (see www.postgres.org)
 *  - Download data files and script
 *  - Start Postgres and create a database called htcs
 *  - Replace all instances of $LOADDIR$ with the correct path
 *  - Run this script from inside Postgres
 */
 


CREATE TABLE Results (
	date date NOT NULL,
	team_1 varchar(50) NOT NULL,
	team_2 varchar(50) NOT NULL,
	_map varchar(50) NOT NULL,
	result_1 smallint NOT NULL,
	result_2 smallint NOT NULL,
	map_winner char(1) NOT NULL,
	starting_ct char(1) NOT NULL,
	ct_1 smallint NOT NULL,
	t_2 smallint NOT NULL,
	t_1 smallint NOT NULL,
	ct_2 smallint NOT NULL,
	event_id int NOT NULL,
	match_id int NOT NULL,
	rank_1 smallint NOT NULL,
	rank_2 smallint NOT NULL,
	map_wins_1 smallint NOT NULL,
	map_wins_2 smallint NOT NULL,
	match_winner char(1) NOT NULL,
	PRIMARY KEY (match_id, _map)
) ;


COPY Results FROM '/home/sami/database/data/results.csv'
    DELIMITER ','
	CSV HEADER;


CREATE TABLE Picks (
	date date NOT NULL,
	team_1 varchar(50) NOT NULL,
	team_2 varchar(50) NOT NULL,
	inverted_teams char(1) NOT NULL,
	match_id int NOT NULL PRIMARY KEY,
	event_id int NOT NULL,
	best_of varchar(20) NOT NULL,
	system varchar(50) NOT NULL,
	t1_removed_1 varchar(50) NOT NULL,
	t1_removed_2 varchar(50) NOT NULL,
	t1_removed_3 varchar(50) NOT NULL,
	t2_removed_1 varchar(50) NOT NULL,
	t2_removed_2 varchar(50) NOT NULL,
	t2_removed_3 varchar(50) NOT NULL,
	t1_picked_1 varchar(50) NOT NULL,
	t2_picked_1 varchar(50) NOT NULL,
	left_over varchar(50) NOT NULL
) ;

COPY Picks FROM '/home/sami/database/data/picks.csv'
    DELIMITER ','
	CSV HEADER;


CREATE TABLE Economy (
	date date NOT NULL,
	match_id int NOT NULL,
	event_id int NOT NULL,
	team_1 varchar(50) NOT NULL,
	team_2 varchar(50) NOT NULL,
	best_of varchar(20) NOT NULL,
	_map varchar(50) NOT NULL,
	t1_start varchar(2) NOT NULL,
	t2_start varchar(2) NOT NULL,
	"1_t1" decimal(19,4),
	"2_t1" decimal(19,4),
	"3_t1" decimal(19,4),
	"4_t1" decimal(19,4),
	"5_t1" decimal(19,4),
	"6_t1" decimal(19,4),
	"7_t1" decimal(19,4),
	"8_t1" decimal(19,4),
	"9_t1" decimal(19,4),
	"10_t1" decimal(19,4),
	"11_t1" decimal(19,4),
	"12_t1" decimal(19,4),
	"13_t1" decimal(19,4),
	"14_t1" decimal(19,4),
	"15_t1" decimal(19,4),
	"16_t1" decimal(19,4),
	"17_t1" decimal(19,4),
	"18_t1" decimal(19,4),
	"19_t1" decimal(19,4),
	"20_t1" decimal(19,4),
	"21_t1" decimal(19,4),
	"22_t1" decimal(19,4),
	"23_t1" decimal(19,4),
	"24_t1" decimal(19,4),
	"25_t1" decimal(19,4),
	"26_t1" decimal(19,4),
	"27_t1" decimal(19,4),
	"28_t1" decimal(19,4),
	"29_t1" decimal(19,4),
	"30_t1" decimal(19,4),
	"1_t2" decimal(19,4),
	"2_t2" decimal(19,4),
	"3_t2" decimal(19,4),
	"4_t2" decimal(19,4),
	"5_t2" decimal(19,4),
	"6_t2" decimal(19,4),
	"7_t2" decimal(19,4),
	"8_t2" decimal(19,4),
	"9_t2" decimal(19,4),
	"10_t2" decimal(19,4),
	"11_t2" decimal(19,4),
	"12_t2" decimal(19,4),
	"13_t2" decimal(19,4),
	"14_t2" decimal(19,4),
	"15_t2" decimal(19,4),
	"16_t2" decimal(19,4),
	"17_t2" decimal(19,4),
	"18_t2" decimal(19,4),
	"19_t2" decimal(19,4),
	"20_t2" decimal(19,4),
	"21_t2" decimal(19,4),
	"22_t2" decimal(19,4),
	"23_t2" decimal(19,4),
	"24_t2" decimal(19,4),
	"25_t2" decimal(19,4),
	"26_t2" decimal(19,4),
	"27_t2" decimal(19,4),
	"28_t2" decimal(19,4),
	"29_t2" decimal(19,4),
	"30_t2" decimal(19,4),
	"1_winner" decimal(19,4),
	"2_winner" decimal(19,4),
	"3_winner" decimal(19,4),
	"4_winner" decimal(19,4),
	"5_winner" decimal(19,4),
	"6_winner" decimal(19,4),
	"7_winner" decimal(19,4),
	"8_winner" decimal(19,4),
	"9_winner" decimal(19,4),
	"10_winner" decimal(19,4),
	"11_winner" decimal(19,4),
	"12_winner" decimal(19,4),
	"13_winner" decimal(19,4),
	"14_winner" decimal(19,4),
	"15_winner" decimal(19,4),
	"16_winner" decimal(19,4),
	"17_winner" decimal(19,4),
	"18_winner" decimal(19,4),
	"19_winner" decimal(19,4),
	"20_winner" decimal(19,4),
	"21_winner" decimal(19,4),
	"22_winner" decimal(19,4),
	"23_winner" decimal(19,4),
	"24_winner" decimal(19,4),
	"25_winner" decimal(19,4),
	"26_winner" decimal(19,4),
	"27_winner" decimal(19,4),
	"28_winner" decimal(19,4),
	"29_winner" decimal(19,4),
	"30_winner" decimal(19,4),
	PRIMARY KEY (match_id, _map)
) ;


COPY Economy FROM '/home/sami/database/data/economy.csv'
    DELIMITER ','
	CSV HEADER;


CREATE TABLE Players (
	date date NOT NULL,
	player_name varchar(50),
	team varchar(50) NOT NULL,
	opponent varchar(50) NOT NULL,
	country varchar(50) NOT NULL,
	player_id int NOT NULL,
	match_id int NOT NULL,
	event_id int NOT NULL,
	event_name varchar(100) NOT NULL,
	best_of varchar(20) NOT NULL,
	map_1 varchar(50) NOT NULL,
	map_2 varchar(50),
	map_3 varchar(50),
	kills decimal(19, 4),
	assists decimal(19, 4),
	deaths decimal(19, 4),
	hs decimal(19, 4),
	flash_assists decimal(19, 4),
	kast decimal(19,4),
	kddiff decimal(19, 4),
	adr decimal(19, 4),
	fkdiff decimal(19, 4),
	rating decimal(19, 4),
	m1_kills decimal(19, 4),
	m1_assists decimal(19, 4),
	m1_deaths decimal(19, 4),
	m1_hs decimal(19, 4),
	m1_flash_assists decimal(19, 4),
	m1_kast decimal(19,4),
	m1_kddiff decimal(19, 4),
	m1_adr decimal(19, 4),
	m1_fkdiff decimal(19, 4),
	m1_rating decimal(19, 4),
	m2_kills decimal(19, 4),
	m2_assists decimal(19, 4),
	m2_deaths decimal(19, 4),
	m2_hs decimal(19, 4),
	m2_flash_assists decimal(19, 4),
	m2_kast decimal(19,4),
	m2_kddiff decimal(19, 4),
	m2_adr decimal(19, 4),
	m2_fkdiff decimal(19, 4),
	m2_rating decimal(19, 4),
	m3_kills decimal(19, 4),
	m3_assists decimal(19, 4),
	m3_deaths decimal(19, 4),
	m3_hs decimal(19, 4),
	m3_flash_assists decimal(19, 4),
	m3_kast decimal(19, 4),
	m3_kddiff decimal(19, 4),
	m3_adr decimal(19, 4),
	m3_fkdiff decimal(19, 4),
	m3_rating decimal(19, 4),
	kills_ct decimal(19, 4),
	deaths_ct decimal(19, 4),
	kddiff_ct decimal(19, 4),
	adr_ct decimal(19, 4),
	kast_ct decimal(19, 4),
	rating_ct decimal(19, 4),
	kills_t decimal(19, 4),
	deaths_t decimal(19, 4),
	kddiff_t decimal(19, 4),
	adr_t decimal(19, 4),
	kast_t decimal(19, 4),
	rating_t decimal(19, 4),
	m1_kills_ct decimal(19, 4),
	m1_deaths_ct decimal(19, 4),
	m1_kddiff_ct decimal(19, 4),
	m1_adr_ct decimal(19, 4),
	m1_kast_ct decimal(19, 4),
	m1_rating_ct decimal(19, 4),
	m1_kills_t decimal(19, 4),
	m1_deaths_t decimal(19, 4),
	m1_kddiff_t decimal(19, 4),
	m1_adr_t decimal(19, 4),
	m1_kast_t decimal(19, 4),
	m1_rating_t decimal(19, 4),
	m2_kills_ct decimal(19, 4),
	m2_deaths_ct decimal(19, 4),
	m2_kddiff_ct decimal(19, 4),
	m2_adr_ct decimal(19, 4),
	m2_kast_ct decimal(19, 4),
	m2_rating_ct decimal(19, 4),
	m2_kills_t decimal(19, 4),
	m2_deaths_t decimal(19, 4),
	m2_kddiff_t decimal(19, 4),
	m2_adr_t decimal(19, 4),
	m2_kast_t decimal(19, 4),
	m2_rating_t decimal(19, 4),
	m3_kills_ct decimal(19, 4),
	m3_deaths_ct decimal(19, 4),
	m3_kddiff_ct decimal(19, 4),
	m3_adr_ct decimal(19, 4),
	m3_kast_ct decimal(19, 4),
	m3_rating_ct decimal(19, 4),
	m3_kills_t decimal(19, 4),
	m3_deaths_t decimal(19, 4),
	m3_kddiff_t decimal(19, 4),
	m3_adr_t decimal(19, 4),
	m3_kast_t decimal(19, 4),
	m3_rating_t decimal(19, 4),
	PRIMARY KEY (match_id, player_id)
) ;


COPY Players FROM '/home/sami/database/data/players.csv'
    DELIMITER ','
	CSV HEADER;

```
</details>

## Business use

From a business perspective, analyzing CS:GO match data is mostly beneficial for professional coaching staff, game developers, and the gambling industry. The dataset could also come in handy for talent acquisition and player management. 

Some of the findings could have business impact by offering the professional teams statistics about key in-game focus areas to improve in. 

## Operative SQL queries
With the aforementioned business use in mind, I made 5 different operative queries that could be useful for the stakeholders. I later indexed them to make them more optimized.

### 1. A team's played maps with their win rates
<details>
<summary>Click to see the query</summary>

```
SELECT _map                       AS "map"
      , SUM(CASE WHEN map_winner = '1'
            AND team_1 = 'fnatic'
            OR team_2 = 'fnatic'
            AND map_winner = '2'
          THEN 1
          ELSE 0
        END)                      AS "won"
      , COUNT(*) AS "total"
      , SUM(CASE WHEN map_winner = '1'
            AND team_1 = 'fnatic'
            OR team_2 = 'fnatic'
            AND map_winner = '2'
          THEN 1
          ELSE 0
        END) * 100 / COUNT(*)     AS "winrate"
FROM results
WHERE team_1 = 'fnatic' OR team_2 = 'fnatic'
GROUP BY 1
ORDER BY total;
```
</details>

<details>

<summary>Click to see the indexing and its result</summary>

```
Before - Soft parse: (6,633 + 6.817 + 6,611 + 6,514 + 6,480) / 5 = _6,611_
CREATE INDEX team1_idx ON results (team_1);
CREATE INDEX team2_idx ON results (team_2);
After - Soft parse: (0,780 + 0,795 + 0,778 + 0,788 + 0,781) / 5 = _0,7824_
```
</details>


### 2. A team's ct and t sided win rates for each map
<details>
<summary>Click to see the query</summary>

```
WITH a AS (SELECT _map                        AS map
    , SUM(CASE WHEN team_1 = 'fnatic'
        THEN ct_1
        ELSE ct_2
      END)                                    AS ct_rounds
    , SUM(CASE WHEN team_1 = 'fnatic'
        THEN ct_1 + t_2
        ELSE ct_2 + t_1
      END)                                    AS ct_rounds_total
    , SUM(CASE WHEN team_1 = 'fnatic'
        THEN t_1
        ELSE t_2
      END)                                    AS t_rounds
    , SUM(CASE WHEN team_1 = 'fnatic'
        THEN t_1 + ct_2
        ELSE t_2 + ct_1
      END)                                    AS t_rounds_total
    , COUNT(*)                                AS total
FROM results
WHERE team_1 = 'fnatic' OR team_2 = 'fnatic'
GROUP BY 1
    ORDER BY total
)
SELECT a.map
    , (a.ct_rounds * 100 / a.ct_rounds_total) AS ct_winrate
    , (a.t_rounds * 100 / a.t_rounds_total)   AS t_winrate
FROM a;
```
</details>

<details>

<summary>Click to see the indexing and its result</summary>

```
Before - Soft parse: (6,703 + 6,749 + 6,732 + 6,737 + 6,710) / 5 = _6,7262_
Same indexing as above
After - Soft parse: (0,890 + 0,895 + 0,9 + 0,901 + 0,893) / 5 = _0,8958_
```
</details>

### 3. A player's match statistics from last 3 months
<details>
<summary>Click to see the query</summary>

```
WITH p AS (
    SELECT player_name                      AS "name"
    , match_id
    , AVG(kills)                            AS "total_kills"
    , AVG(deaths)                           AS "total_deaths"
    , AVG(rating)                           AS "total_rating"
    , AVG(kast)                             AS "total_kast"
    , AVG(hs)                               AS "total_hs"
  FROM players
  WHERE team ILIKE 'ENCE'
  AND date >= '2019-02-01'::timestamp
  AND date <= '2019-02-01'::timestamp + 90 * INTERVAL '1 day' -- or date >= MAX(date) - 90 * INTERVAL '1 day' etc.
  GROUP BY 1, 2
)
, r AS (
    SELECT match_id
    , SUM(result_1 + result_2)              AS "total_rounds"
    , COUNT(*)                              AS "total_maps"
  FROM results
  GROUP BY 1
)
SELECT p.name
    , AVG(p.total_rating)                   AS "Rating"
    , AVG(p.total_kills / r.total_rounds)   AS "Kills per round"
    , AVG(p.total_hs * 100 / total_kills )  AS "Headshots"
    , SUM(r.total_maps)                     AS "Maps played"
    , AVG(p.total_deaths / r.total_rounds)  AS "Deaths per round"
    , AVG(p.total_kast)                     AS "Rounds contributed"
FROM r
JOIN p
  ON (p.match_id = r.match_id)
GROUP BY 1;
```
</details>

<details>

<summary>Click to see the indexing and its result</summary>

```
Before - Soft parse: (386,179 + 390,769 + 392,125 + 403,185 + 396,865) / 5 = _393,8246_
CREATE INDEX date_idx ON players (date);
After - Soft parse: (37,231 + 37,829 + 37,233 + 37,321 + 37,764) / 5 = _37,4756_
```
</details>

### 4. A player's map based statistics from last 3 months
<details>
<summary>Click to see the query</summary>

```
WITH p AS (
    SELECT player_name                      AS "name"
    , match_id
    , CASE WHEN map_3 ILIKE 'nuke'
          THEN m3_kills
        WHEN map_2 ILIKE 'nuke'
          THEN m2_kills
        ELSE m1_kills
      END                                   AS "total_kills"
    , CASE WHEN map_3 ILIKE 'nuke'
          THEN m3_deaths
        WHEN map_2 ILIKE 'nuke'
          THEN m2_deaths
        ELSE m1_deaths
      END                                   AS "total_deaths"
    , CASE WHEN map_3 ILIKE 'nuke'
          THEN m3_rating
        WHEN map_2 ILIKE 'nuke'
          THEN m2_rating
        ELSE m1_rating
      END                                   AS "total_rating"
    , CASE WHEN map_3 ILIKE 'nuke'
          THEN m3_kast
        WHEN map_2 ILIKE 'nuke'
          THEN m2_kast
        ELSE m1_kast
      END                                   AS "total_kast"
    , CASE WHEN map_3 ILIKE 'nuke'
          THEN m3_hs
        WHEN map_2 ILIKE 'nuke'
          THEN m2_hs
        ELSE m1_hs
      END                                   AS "total_hs"
  FROM players
  WHERE team ILIKE 'ENCE'
  AND date >= '2019-02-01'::timestamp
  AND date <= '2019-02-01'::timestamp + 90 * INTERVAL '1 day'
  GROUP BY 1, 2, 3, 4, 5, 6, 7
)
, r AS (
    SELECT match_id
      , SUM(result_1 + result_2)            AS "total_rounds"
      , COUNT(*)                            AS "total_maps"
  FROM results
  WHERE _map ILIKE 'nuke'
  GROUP BY 1
)
SELECT p.name
    , AVG(p.total_rating)                   AS "Rating"
    , AVG(p.total_kills / r.total_rounds)   AS "Kills per round"
    , AVG(p.total_hs * 100 / total_kills )  AS "Headshots"
    , SUM(r.total_maps)                     AS "Maps played"
    , AVG(p.total_deaths / r.total_rounds)  AS "Deaths per round"
    , AVG(p.total_kast)                     AS "Rounds contributed"
FROM r
JOIN p
  ON (p.match_id = r.match_id)
GROUP BY 1;
```
</details>

<details>

<summary>Click to see the indexing and its result</summary>

```
Before - Soft parse: (279,967 + 279,682 + 280,040 + 280,472 + 281,579) / 5 = _280,348_
Players.date indexed as above
After - Soft parse: (41,74 + 41,745 + 42,198 + 41,758 + 41,745) / 5 = _41,8372_
```
</details>

### 5. A team's map based pistol round win rate
<details>
<summary>Click to see the query</summary>

```
WITH a AS (SELECT _map                                 AS map
    , SUM(CASE WHEN team_1 = 'fnatic' AND t1_start = 'ct' AND "1_winner" = 1
          THEN 1
        WHEN team_2 = 'fnatic' AND t2_start = 't' AND "16_winner" = 2
          THEN 1
        WHEN team_1 = 'fnatic' AND t1_start = 't' AND "16_winner" = 1
          THEN 1
        WHEN team_2 = 'fnatic' AND t2_start = 'ct' AND "1_winner" = 2
          THEN 1
        ELSE 0
      END)                                             AS ct_wins
    , SUM(CASE WHEN team_1 = 'fnatic' AND t1_start = 't' AND "1_winner" = 1
          THEN 1
        WHEN team_2 = 'fnatic' AND t2_start = 'ct' AND "16_winner" = 2
          THEN 1
        WHEN team_1 = 'fnatic' AND t1_start = 'ct' AND "16_winner" = 1
          THEN 1
        WHEN team_2 = 'fnatic' AND t2_start = 't' AND "1_winner" = 2
          THEN 1
        ELSE 0
      END)                                             AS t_wins
    , COUNT(*)                                         AS total
  FROM economy
  WHERE team_1 = 'fnatic' OR team_2 = 'fnatic'
  GROUP BY 1
      ORDER BY total DESC
)
SELECT a.map
    , (a.ct_wins * 100 / a.total)                      AS ct_winrate
    , (a.t_wins * 100 / a.total)                       AS t_winrate
    , ((a.t_wins + a.ct_wins) * 100 / (a.total * 2))   AS map_winrate
    , a.total
FROM a;
```
</details>

<details>

<summary>Click to see the indexing and its result</summary>

```
Before - Soft parse: (11,712 + 11,836 + 11,729 + 12,167 + 11,925) / 5 = _11,8738_
CREATE INDEX team12_idx ON economy (team_1);
CREATE INDEX team21_idx ON economy (team_2);
After - Soft parse: (1,097 + 1,1 + 1,105 + 1,103 + 1,095) / 5 = _1,1_
```
</details>

## "Interesting" research questions

### RQ1. The game received updates to its in-game economy on 10.10.2018 and 13.3.2019. Have the updates made the matches more even?

The longer the match, the more entertaining it likely is. This balance could be observed either from the CT side round win percentage or the match length. The latter was observed and this led to the following findings:
![tk1](https://github.com/user-attachments/assets/32a75c4b-5eb2-470e-bf57-3722f2c910b4)

<details>

<summary>Click to see the query</summary>

```
WITH a AS (SELECT AVG(result_1 + result_2)           AS rounds1
        , STDDEV(result_1 + result_2)                AS sd1
        , COUNT(*)                                   AS cnt1
  FROM results
  WHERE date < '2018-10-09'::timestamp
), b AS (SELECT AVG(result_1 + result_2)             AS rounds2
        , STDDEV(result_1 + result_2)                AS sd2
        , COUNT(*)                                   AS cnt2
  FROM results
  WHERE date >= '2018-10-10'::timestamp
  AND date < '2019-03-13'::timestamp
), c AS (SELECT AVG(result_1 + result_2)             AS rounds3
        , STDDEV(result_1 + result_2)                AS sd3
        , COUNT(*)                                   AS cnt3
  FROM results
  WHERE date >= '2019-03-13'::timestamp
), d AS (SELECT AVG(result_1 + result_2)             AS rounds4
        , STDDEV(result_1 + result_2)                AS sd4
        , COUNT(*)                                   AS cnt4
  FROM results
)
, e AS (SELECT rounds1                               AS "map_length_before"
        , sd1                                        AS "sd_before"
        , cnt1                                       AS "cnt_before"
        , rounds2                                    AS "map_length_between"
        , sd2                                        AS "sd_between"
        , cnt2                                       AS "cnt_between"
        , rounds3                                    AS "map_length_after"
        , sd3                                        AS "sd_after"
        , cnt3                                       AS "cnt_after"
        , rounds4                                    AS "map_length_avg"
        , sd4                                        AS "sd_total"
        , cnt4                                       AS "cnt_total"
        , ((rounds2 - rounds1) / (sd2 / SQRT(cnt2))) AS "t2"
        , ((rounds3 - rounds2) / (sd3 / SQRT(cnt3))) AS "t3" -- Notable difference to confidence 0.0005 < 3.291 on infinite degree of freedom
  FROM a, b, c, d
)
SELECT map_length_before
    , map_length_between
    , map_length_after
    , t2
    , t3
FROM e;
```
</details>

Based on these results, the first update did not have a notable effect on the average match length. However, the second update had a more noticeable impact on rounds played. The matches were 0.5 rounds longer on average after the latter update. 

Conducting a t-test was also attempted. The first result, _t2_, comparing _map_length_before_ and _map_length_between_ was not notable. Instead, _t3_ with a value of 10.36 is remarkable when compared to a 99.95 % confidence with infinite degree of freedom, 3.291.

The annual averages of match lengths were also visualized:

![tk12](https://github.com/user-attachments/assets/43796993-0c46-4bf8-84b2-3bcdc54fb096)



<details>

<summary>Click to see the query</summary>

```
SELECT EXTRACT(YEAR FROM date) AS year
    , AVG(result_1 + result_2) AS rounds_map
    , stddev(result_1 + result_2) AS standard_deviation
    , COUNT(*) AS count
FROM results
GROUP BY 1
ORDER BY 1;
```
</details>

The graph shows that the trend of rounds played has been growing since 2016. The most remarkable difference was between 2018 and 2019 which could be explained by the update on 13.3.2019. However, a more interesting fact is that the value of _map_length_between_ was noticeable lower than the annual averages of both 2018 and 2019. Thus, the first update made the matches somewhat shorter. 

Something noteworthy is that the data from 2015 and 2020 is only partial. Therefore, at least the data from 2015 could be unreliable.

### RQ2. Do more flash assists or entry kills lead to a more likely win?

Flash assist (FA) means that that a kill was achieved while the opponent was blinded by utility, a flashbang grenade. A blinded enemy is way easier to eliminate and this can be achieved with coordinated teamwork. Thus, a higher number of FAs could indicate better teamwork. 

Entry kills or first kills (FK) lead to an advantageous position as the situation turns into a 5vs4. After an FK the team with the advantage can overpower their opponents. 

![tk2](https://github.com/user-attachments/assets/fd83a814-346f-4a6c-abc4-6a46d07dd002)

<details>

<summary>Click to see the query</summary>

```
WITH a AS (SELECT team
         , match_id
         , SUM(flash_assists)               AS "avg_fa"
         , SUM(fkdiff)                      AS "avg_fkdiff"
    FROM players
    GROUP BY 1, 2
), b AS (SELECT match_id
        , team_1
        , team_2
        , map_winner
        , rank_1
        , rank_2
    FROM results
    GROUP BY 1, 2, 3, 4, 5, 6
), c AS (SELECT team
        , COUNT(team)                       AS "played"
    FROM players
    GROUP BY 1
)
, d AS (SELECT a.team
        , c.played
        , AVG(a.avg_fa)                     AS "flash_assists"
        , AVG(a.avg_fkdiff)                 AS "fkdiff"
        , AVG(CASE WHEN b.team_1 = a.team AND b.map_winner = '1'
                    THEN 1
                WHEN b.team_1 = a.team AND b.map_winner = '2'
                    THEN 0
                WHEN b.team_2 = a.team AND b.map_winner = '2'
                    THEN 1
                ELSE 0
              END)                         AS "win_pct"
        , (AVG(a.avg_fa) - 7.76 ) * (AVG(CASE WHEN b.team_1 = a.team AND b.map_winner = '1'
                    THEN 1
                WHEN b.team_1 = a.team AND b.map_winner = '2'
                    THEN 0
                WHEN b.team_2 = a.team AND b.map_winner = '2'
                    THEN 1
                ELSE 0
              END) - 0.46)                 AS "fa_cov"
        , (AVG(a.avg_fkdiff) + 0.55 ) * (AVG(CASE WHEN b.team_1 = a.team AND b.map_winner = '1'
                    THEN 1
                WHEN b.team_1 = a.team AND b.map_winner = '2'
                    THEN 0
                WHEN b.team_2 = a.team AND b.map_winner = '2'
                    THEN 1
                ELSE 0
              END) - 0.46)                 AS "fk_cov"
    FROM b
    JOIN a
        ON (a.match_id = b.match_id)
    JOIN c
        ON (c.team = a.team)
    WHERE c.played > 1000 AND b.rank_1 < 50 AND b.rank_2 < 50
    GROUP BY 1, 2
    ORDER BY 3 ASC
)
, e AS (SELECT AVG(d.flash_assists)         AS "fa"
        , STDDEV(d.flash_assists)           AS "fa_sd"
        , AVG(d.fkdiff)                     AS "fk"
        , STDDEV(d.fkdiff)                  AS "fk_sd"
        , AVG(d.win_pct)                    AS "win"
        , STDDEV(d.win_pct)                 AS "win_sd"
        , AVG(d.fa_cov)                     AS "fa_cov"
        , AVG(d.fk_cov)                     AS "fk_cov"
    FROM d
)
SELECT e.fa_cov / (e.fa_sd * e.win_sd)      AS "fa_correlation"
    , e.fk_cov / (e.fk_sd * e.win_sd)       AS "fk_correlation"
FROM e;
```
</details>

Comparing these two values' correlation to map wins shows that FKs are noticeably more important. However, they both significantly correlate with map wins. 

These results were also visualized. The data was limited to matches where both of the teams were top 50. Additionally, each team had a minimum of 200 maps played. The following graph shows each team fulfilling the aforementioned limitations based on the average of FAs and its relation to map win percentage.

![tk21](https://github.com/user-attachments/assets/2297e6bc-0e7a-4a1c-b778-53d61aae3282)

There is no clear, significant correlation visible. The next graph shows similarly FKs correlation to map win percentage:

![tk22](https://github.com/user-attachments/assets/6188766a-530c-4b14-9766-b5ca73431905)

Here, the correlation is more visible. Thus, FKs are more important than FAs. However, FAs are an area that can lead to higher FKs. 

<details>

<summary>Click to see the query for the previous graphs</summary>

```
WITH a AS (SELECT team
        , match_id
        , SUM(flash_assists)  AS "avg_fa"
        , SUM(fkdiff)         AS "avg_fkdiff"
    FROM players
    GROUP BY 1, 2
), b AS (SELECT match_id
        , team_1
        , team_2
        , map_winner
        , rank_1
        , rank_2
    FROM results
    GROUP BY 1, 2, 3, 4, 5, 6
), c AS (SELECT team
            , COUNT(team)     AS "played"
    FROM players
    GROUP BY 1
)
SELECT a.team
    , c.played
    , AVG(a.avg_fa)           AS "flash_assists"
    , AVG(a.avg_fkdiff)       AS "fkdiff"
    , AVG(CASE WHEN b.team_1 = a.team AND b.map_winner = '1'
            THEN 1
        WHEN b.team_1 = a.team AND b.map_winner = '2'
            THEN 0
        WHEN b.team_2 = a.team AND b.map_winner = '2'
            THEN 1
        ELSE 0
        END)                  AS "win_pct"
FROM b
JOIN a
    ON (a.match_id = b.match_id)
JOIN c
    ON (c.team = a.team)
WHERE c.played > 1000 AND b.rank_1 < 50 AND b.rank_2 < 50
GROUP BY 1, 2;
```
</details>

### RQ3. Do top teams win more eco rounds than lesser teams?

Eco rounds mean rounds where little to no money is spent. Thus, a team taking an eco round only plays with pistols while their opposition is likely playing with stronger weapons and better utility. Winning these rounds is quite rare and is definitely a swing in both teams' economies. 

![tk3](https://github.com/user-attachments/assets/dbd1552d-5e35-4b1a-b42b-57894eb1d9a6)

<details>

<summary>Click to see the query</summary>

```
WITH a AS (SELECT team_1
    , SUM(CASE WHEN "2_t1" < 5000
            THEN 1
        WHEN "3_t1" < 5000
            THEN 1
        WHEN "4_t1" < 5000
            THEN 1
        WHEN "5_t1" < 5000
            THEN 1
        WHEN "6_t1" < 5000
            THEN 1
        WHEN "7_t1" < 5000
            THEN 1
        WHEN "8_t1" < 5000
            THEN 1
        WHEN "9_t1" < 5000
            THEN 1
        WHEN "10_t1" < 5000
            THEN 1
        WHEN "11_t1" < 5000
            THEN 1
        WHEN "12_t1" < 5000
            THEN 1
        WHEN "13_t1" < 5000
            THEN 1
        WHEN "14_t1" < 5000
            THEN 1
        WHEN "15_t1" < 5000
            THEN 1
        WHEN "17_t1" < 5000
            THEN 1
        WHEN "18_t1" < 5000
            THEN 1
        WHEN "19_t1" < 5000
            THEN 1
        WHEN "20_t1" < 5000
            THEN 1
        WHEN "21_t1" < 5000
            THEN 1
        WHEN "22_t1" < 5000
            THEN 1
        WHEN "23_t1" < 5000
            THEN 1
        WHEN "24_t1" < 5000
            THEN 1
        WHEN "25_t1" < 5000
            THEN 1
        WHEN "26_t1" < 5000
            THEN 1
        WHEN "27_t1" < 5000
            THEN 1
        WHEN "28_t1" < 5000
            THEN 1
        WHEN "29_t1" < 5000
            THEN 1
        WHEN "30_t1" < 5000
            THEN 1
        ELSE 0 END)                                                             AS "t1_ecos"
    , team_2
    , SUM(CASE WHEN "2_t2" < 5000
            THEN 1
        WHEN "3_t2" < 5000
            THEN 1
        WHEN "4_t2" < 5000
            THEN 1
        WHEN "5_t2" < 5000
            THEN 1
        WHEN "6_t2" < 5000
            THEN 1
        WHEN "7_t2" < 5000
            THEN 1
        WHEN "8_t2" < 5000
            THEN 1
        WHEN "9_t2" < 5000
            THEN 1
        WHEN "10_t2" < 5000
            THEN 1
        WHEN "11_t2" < 5000
            THEN 1
        WHEN "12_t2" < 5000
            THEN 1
        WHEN "13_t2" < 5000
            THEN 1
        WHEN "14_t2" < 5000
            THEN 1
        WHEN "15_t2" < 5000
            THEN 1
        WHEN "17_t2" < 5000
            THEN 1
        WHEN "18_t2" < 5000
            THEN 1
        WHEN "19_t2" < 5000
            THEN 1
        WHEN "20_t2" < 5000
            THEN 1
        WHEN "21_t2" < 5000
            THEN 1
        WHEN "22_t2" < 5000
            THEN 1
        WHEN "23_t2" < 5000
            THEN 1
        WHEN "24_t2" < 5000
            THEN 1
        WHEN "25_t2" < 5000
            THEN 1
        WHEN "26_t2" < 5000
            THEN 1
        WHEN "27_t2" < 5000
            THEN 1
        WHEN "28_t2" < 5000
            THEN 1
        WHEN "29_t2" < 5000
            THEN 1
        WHEN "30_t2" < 5000
            THEN 1
        ELSE 0 END)                                                             AS "t2_ecos"
    FROM economy
    GROUP BY 1, 3
), d AS (SELECT team_1
    , SUM(CASE WHEN "2_t1" < 5000 AND "2_winner" = 1
            THEN 1
        WHEN "3_t1" < 5000 AND "3_winner" = 1
            THEN 1
        WHEN "4_t1" < 5000 AND "4_winner" = 1
            THEN 1
        WHEN "5_t1" < 5000 AND "5_winner" = 1
            THEN 1
        WHEN "6_t1" < 5000 AND "6_winner" = 1
            THEN 1
        WHEN "7_t1" < 5000 AND "7_winner" = 1
            THEN 1
        WHEN "8_t1" < 5000 AND "8_winner" = 1
            THEN 1
        WHEN "9_t1" < 5000 AND "9_winner" = 1
            THEN 1
        WHEN "10_t1" < 5000 AND "10_winner" = 1
            THEN 1
        WHEN "11_t1" < 5000 AND "11_winner" = 1
            THEN 1
        WHEN "12_t1" < 5000 AND "12_winner" = 1
            THEN 1
        WHEN "13_t1" < 5000 AND "13_winner" = 1
            THEN 1
        WHEN "14_t1" < 5000 AND "14_winner" = 1
            THEN 1
        WHEN "15_t1" < 5000 AND "15_winner" = 1
            THEN 1
        WHEN "17_t1" < 5000 AND "17_winner" = 1
            THEN 1
        WHEN "18_t1" < 5000 AND "18_winner" = 1
            THEN 1
        WHEN "19_t1" < 5000 AND "19_winner" = 1
            THEN 1
        WHEN "20_t1" < 5000 AND "20_winner" = 1
            THEN 1
        WHEN "21_t1" < 5000 AND "21_winner" = 1
            THEN 1
        WHEN "22_t1" < 5000 AND "22_winner" = 1
            THEN 1
        WHEN "23_t1" < 5000 AND "23_winner" = 1
            THEN 1
        WHEN "24_t1" < 5000 AND "24_winner" = 1
            THEN 1
        WHEN "25_t1" < 5000 AND "25_winner" = 1
            THEN 1
        WHEN "26_t1" < 5000 AND "26_winner" = 1
            THEN 1
        WHEN "27_t1" < 5000 AND "27_winner" = 1
            THEN 1
        WHEN "28_t1" < 5000 AND "28_winner" = 1
            THEN 1
        WHEN "29_t1" < 5000 AND "29_winner" = 1
            THEN 1
        WHEN "30_t1" < 5000 AND "30_winner" = 1
            THEN 1
        ELSE 0 END)                                                             AS "t1_ecos_won"
    , team_2
    , SUM(CASE WHEN "2_t2" < 5000 AND "2_winner" = 2
            THEN 1
        WHEN "3_t2" < 5000 AND "3_winner" = 2
            THEN 1
        WHEN "4_t2" < 5000 AND "4_winner" = 2
            THEN 1
        WHEN "5_t2" < 5000 AND "5_winner" = 2
            THEN 1
        WHEN "6_t2" < 5000 AND "6_winner" = 2
            THEN 1
        WHEN "7_t2" < 5000 AND "7_winner" = 2
            THEN 1
        WHEN "8_t2" < 5000 AND "8_winner" = 2
            THEN 1
        WHEN "9_t2" < 5000 AND "9_winner" = 2
            THEN 1
        WHEN "10_t2" < 5000 AND "10_winner" = 2
            THEN 1
        WHEN "11_t2" < 5000 AND "11_winner" = 2
            THEN 1
        WHEN "12_t2" < 5000 AND "12_winner" = 2
            THEN 1
        WHEN "13_t2" < 5000 AND "13_winner" = 2
            THEN 1
        WHEN "14_t2" < 5000 AND "14_winner" = 2
            THEN 1
        WHEN "15_t2" < 5000 AND "15_winner" = 2
            THEN 1
        WHEN "17_t2" < 5000 AND "17_winner" = 2
            THEN 1
        WHEN "18_t2" < 5000 AND "18_winner" = 2
            THEN 1
        WHEN "19_t2" < 5000 AND "19_winner" = 2
            THEN 1
        WHEN "20_t2" < 5000 AND "20_winner" = 2
            THEN 1
        WHEN "21_t2" < 5000 AND "21_winner" = 2
            THEN 1
        WHEN "22_t2" < 5000 AND "22_winner" = 2
            THEN 1
        WHEN "23_t2" < 5000 AND "23_winner" = 2
            THEN 1
        WHEN "24_t2" < 5000 AND "24_winner" = 2
            THEN 1
        WHEN "25_t2" < 5000 AND "25_winner" = 2
            THEN 1
        WHEN "26_t2" < 5000 AND "26_winner" = 2
            THEN 1
        WHEN "27_t2" < 5000 AND "27_winner" = 2
            THEN 1
        WHEN "28_t2" < 5000 AND "28_winner" = 2
            THEN 1
        WHEN "29_t2" < 5000 AND "29_winner" = 2
            THEN 1
        WHEN "30_t2" < 5000 AND "30_winner" = 2
            THEN 1
        ELSE 0 END)                                                             AS "t2_ecos_won"
    FROM economy
    GROUP BY 1, 3
), b AS (SELECT a.team_1
        , SUM(t1_ecos)                                                          AS "t1_ecos"
        , SUM(t1_ecos_won)                                                      AS "t1_ecos_won"
        , a.team_2
        , SUM(t2_ecos)                                                          AS "t2_ecos"
        , SUM(t2_ecos_won)                                                      AS "t2_ecos_won"
    FROM a
    JOIN d
        ON (d.team_1 = a.team_1 AND d.team_2 = a.team_2)
    GROUP BY 1, 4
), c AS (SELECT b.team_1                                                        AS "team"
        , SUM(CASE WHEN b.team_1 = b.team_2
            THEN b.t1_ecos + b.t2_ecos
            ELSE b.t1_ecos END)                                                 AS "ecos"
        , SUM(CASE WHEN b.team_1 = b.team_2
            THEN b.t1_ecos_won + b.t2_ecos_won
            ELSE b.t1_ecos_won END)                                             AS "ecos_won"
    FROM b
    GROUP BY 1
), ranking1 AS (SELECT team_1
        , rank_1
        , team_2
        , rank_2
    FROM results
), ranking2 AS (SELECT team_1
        , AVG(CASE WHEN team_1 = team_2
                THEN rank_2
            ELSE rank_1
            END)                                                                AS "rank_avg"
        , COUNT(team_1)                                                         AS "played"
    FROM ranking1
    GROUP BY 1
), ranking3 AS (SELECT team_1                                                   AS "team"
        , rank_avg
        , played
        , c.ecos                                                                AS "ecos"
        , c.ecos_won                                                            AS "ecos_won"
        , (c.ecos_won * 100 / c.ecos)                                           AS "eco_winrate"
    FROM ranking2
    JOIN c
        ON (c.team = team_1)
    WHERE rank_avg < 10 AND played > 100
    GROUP BY 1, 2, 3, 4, 5, 6
    ORDER BY 2
)
, ranking4 AS (SELECT team_1                                                    AS "team"
        , rank_avg
        , played
        , c.ecos                                                                AS "ecos"
        , c.ecos_won                                                            AS "ecos_won"
        , (c.ecos_won * 100 / c.ecos)                                           AS "eco_winrate"
    FROM ranking2
    JOIN c
        ON (c.team = team_1)
    WHERE (rank_avg BETWEEN 10 AND 30) AND played > 100
    GROUP BY 1, 2, 3, 4, 5, 6
    ORDER BY 2
)
, ranking5 AS (SELECT team_1                                                    AS "team"
        , rank_avg
        , played
        , c.ecos                                                                AS "ecos"
        , c.ecos_won                                                            AS "ecos_won"
        , (c.ecos_won * 100 / c.ecos)                                           AS "eco_winrate"
    FROM ranking2
    JOIN c
        ON (c.team = team_1)
    WHERE (rank_avg BETWEEN 30 AND 100) AND played > 100
    GROUP BY 1, 2, 3, 4, 5, 6
    ORDER BY 2
)
SELECT
    AVG(ranking3.eco_winrate)                                                   AS "eco_winrate_top10"
    , AVG(ranking4.eco_winrate)                                                 AS "eco_winrate_top30"
    , AVG(ranking5.eco_winrate)                                                 AS "eco_winrate_top100"
    , SUM(b.t1_ecos_won + b.t2_ecos_won) * 100 / SUM(b.t1_ecos + b.t2_ecos)     AS "avg_eco_winrate"
FROM b, ranking3, ranking4, ranking5
ORDER BY 2 ASC;
```
</details>

Based on these numbers the better the team, the more of these eco rounds they win. However, the sample size is something to be wary of. For example, the _eco_winrate_top30_ excludes the top 10, thus only consisting of teams that have their ranking average between 10 and 30 during their existence. Therefore, the sample sizes are not the same between the groups.

The eco win rates were also visualized per team:

![tk31](https://github.com/user-attachments/assets/fea4b4b1-2fd1-4e2a-b068-42a33c2cbb9f)

<details>

<summary>Click to see the query</summary>

```
WITH a AS (SELECT team_1
    , SUM(CASE WHEN "2_t1" < 5000
            THEN 1
        WHEN "3_t1" < 5000
            THEN 1
        WHEN "4_t1" < 5000
            THEN 1
        WHEN "5_t1" < 5000
            THEN 1
        WHEN "6_t1" < 5000
            THEN 1
        WHEN "7_t1" < 5000
            THEN 1
        WHEN "8_t1" < 5000
            THEN 1
        WHEN "9_t1" < 5000
            THEN 1
        WHEN "10_t1" < 5000
            THEN 1
        WHEN "11_t1" < 5000
            THEN 1
        WHEN "12_t1" < 5000
            THEN 1
        WHEN "13_t1" < 5000
            THEN 1
        WHEN "14_t1" < 5000
            THEN 1
        WHEN "15_t1" < 5000
            THEN 1
        WHEN "17_t1" < 5000
            THEN 1
        WHEN "18_t1" < 5000
            THEN 1
        WHEN "19_t1" < 5000
            THEN 1
        WHEN "20_t1" < 5000
            THEN 1
        WHEN "21_t1" < 5000
            THEN 1
        WHEN "22_t1" < 5000
            THEN 1
        WHEN "23_t1" < 5000
            THEN 1
        WHEN "24_t1" < 5000
            THEN 1
        WHEN "25_t1" < 5000
            THEN 1
        WHEN "26_t1" < 5000
            THEN 1
        WHEN "27_t1" < 5000
            THEN 1
        WHEN "28_t1" < 5000
            THEN 1
        WHEN "29_t1" < 5000
            THEN 1
        WHEN "30_t1" < 5000
            THEN 1
        ELSE 0 END)                             AS "t1_ecos"
    , team_2
    , SUM(CASE WHEN "2_t2" < 5000
            THEN 1
        WHEN "3_t2" < 5000
            THEN 1
        WHEN "4_t2" < 5000
            THEN 1
        WHEN "5_t2" < 5000
            THEN 1
        WHEN "6_t2" < 5000
            THEN 1
        WHEN "7_t2" < 5000
            THEN 1
        WHEN "8_t2" < 5000
            THEN 1
        WHEN "9_t2" < 5000
            THEN 1
        WHEN "10_t2" < 5000
            THEN 1
        WHEN "11_t2" < 5000
            THEN 1
        WHEN "12_t2" < 5000
            THEN 1
        WHEN "13_t2" < 5000
            THEN 1
        WHEN "14_t2" < 5000
            THEN 1
        WHEN "15_t2" < 5000
            THEN 1
        WHEN "17_t2" < 5000
            THEN 1
        WHEN "18_t2" < 5000
            THEN 1
        WHEN "19_t2" < 5000
            THEN 1
        WHEN "20_t2" < 5000
            THEN 1
        WHEN "21_t2" < 5000
            THEN 1
        WHEN "22_t2" < 5000
            THEN 1
        WHEN "23_t2" < 5000
            THEN 1
        WHEN "24_t2" < 5000
            THEN 1
        WHEN "25_t2" < 5000
            THEN 1
        WHEN "26_t2" < 5000
            THEN 1
        WHEN "27_t2" < 5000
            THEN 1
        WHEN "28_t2" < 5000
            THEN 1
        WHEN "29_t2" < 5000
            THEN 1
        WHEN "30_t2" < 5000
            THEN 1
        ELSE 0 END)                             AS "t2_ecos"
    FROM economy
    GROUP BY 1, 3
), d AS (SELECT team_1
    , SUM(CASE WHEN "2_t1" < 5000 AND "2_winner" = 1
            THEN 1
        WHEN "3_t1" < 5000 AND "3_winner" = 1
            THEN 1
        WHEN "4_t1" < 5000 AND "4_winner" = 1
            THEN 1
        WHEN "5_t1" < 5000 AND "5_winner" = 1
            THEN 1
        WHEN "6_t1" < 5000 AND "6_winner" = 1
            THEN 1
        WHEN "7_t1" < 5000 AND "7_winner" = 1
            THEN 1
        WHEN "8_t1" < 5000 AND "8_winner" = 1
            THEN 1
        WHEN "9_t1" < 5000 AND "9_winner" = 1
            THEN 1
        WHEN "10_t1" < 5000 AND "10_winner" = 1
            THEN 1
        WHEN "11_t1" < 5000 AND "11_winner" = 1
            THEN 1
        WHEN "12_t1" < 5000 AND "12_winner" = 1
            THEN 1
        WHEN "13_t1" < 5000 AND "13_winner" = 1
            THEN 1
        WHEN "14_t1" < 5000 AND "14_winner" = 1
            THEN 1
        WHEN "15_t1" < 5000 AND "15_winner" = 1
            THEN 1
        WHEN "17_t1" < 5000 AND "17_winner" = 1
            THEN 1
        WHEN "18_t1" < 5000 AND "18_winner" = 1
            THEN 1
        WHEN "19_t1" < 5000 AND "19_winner" = 1
            THEN 1
        WHEN "20_t1" < 5000 AND "20_winner" = 1
            THEN 1
        WHEN "21_t1" < 5000 AND "21_winner" = 1
            THEN 1
        WHEN "22_t1" < 5000 AND "22_winner" = 1
            THEN 1
        WHEN "23_t1" < 5000 AND "23_winner" = 1
            THEN 1
        WHEN "24_t1" < 5000 AND "24_winner" = 1
            THEN 1
        WHEN "25_t1" < 5000 AND "25_winner" = 1
            THEN 1
        WHEN "26_t1" < 5000 AND "26_winner" = 1
            THEN 1
        WHEN "27_t1" < 5000 AND "27_winner" = 1
            THEN 1
        WHEN "28_t1" < 5000 AND "28_winner" = 1
            THEN 1
        WHEN "29_t1" < 5000 AND "29_winner" = 1
            THEN 1
        WHEN "30_t1" < 5000 AND "30_winner" = 1
            THEN 1
        ELSE 0 END)                             AS "t1_ecos_won"
    , team_2
    , SUM(CASE WHEN "2_t2" < 5000 AND "2_winner" = 2
            THEN 1
        WHEN "3_t2" < 5000 AND "3_winner" = 2
            THEN 1
        WHEN "4_t2" < 5000 AND "4_winner" = 2
            THEN 1
        WHEN "5_t2" < 5000 AND "5_winner" = 2
            THEN 1
        WHEN "6_t2" < 5000 AND "6_winner" = 2
            THEN 1
        WHEN "7_t2" < 5000 AND "7_winner" = 2
            THEN 1
        WHEN "8_t2" < 5000 AND "8_winner" = 2
            THEN 1
        WHEN "9_t2" < 5000 AND "9_winner" = 2
            THEN 1
        WHEN "10_t2" < 5000 AND "10_winner" = 2
            THEN 1
        WHEN "11_t2" < 5000 AND "11_winner" = 2
            THEN 1
        WHEN "12_t2" < 5000 AND "12_winner" = 2
            THEN 1
        WHEN "13_t2" < 5000 AND "13_winner" = 2
            THEN 1
        WHEN "14_t2" < 5000 AND "14_winner" = 2
            THEN 1
        WHEN "15_t2" < 5000 AND "15_winner" = 2
            THEN 1
        WHEN "17_t2" < 5000 AND "17_winner" = 2
            THEN 1
        WHEN "18_t2" < 5000 AND "18_winner" = 2
            THEN 1
        WHEN "19_t2" < 5000 AND "19_winner" = 2
            THEN 1
        WHEN "20_t2" < 5000 AND "20_winner" = 2
            THEN 1
        WHEN "21_t2" < 5000 AND "21_winner" = 2
            THEN 1
        WHEN "22_t2" < 5000 AND "22_winner" = 2
            THEN 1
        WHEN "23_t2" < 5000 AND "23_winner" = 2
            THEN 1
        WHEN "24_t2" < 5000 AND "24_winner" = 2
            THEN 1
        WHEN "25_t2" < 5000 AND "25_winner" = 2
            THEN 1
        WHEN "26_t2" < 5000 AND "26_winner" = 2
            THEN 1
        WHEN "27_t2" < 5000 AND "27_winner" = 2
            THEN 1
        WHEN "28_t2" < 5000 AND "28_winner" = 2
            THEN 1
        WHEN "29_t2" < 5000 AND "29_winner" = 2
            THEN 1
        WHEN "30_t2" < 5000 AND "30_winner" = 2
            THEN 1
        ELSE 0 END)                             AS "t2_ecos_won"
    FROM economy
    GROUP BY 1, 3
), b AS (SELECT a.team_1
        , SUM(t1_ecos)                          AS "t1_ecos"
        , SUM(t1_ecos_won)                      AS "t1_ecos_won"
        , a.team_2
        , SUM(t2_ecos)                          AS "t2_ecos"
        , SUM(t2_ecos_won)                      AS "t2_ecos_won"
    FROM a
    JOIN d
        ON (d.team_1 = a.team_1 AND d.team_2 = a.team_2)
    GROUP BY 1, 4
), c AS (SELECT b.team_1                        AS "team"
        , SUM(CASE WHEN b.team_1 = b.team_2
                THEN b.t1_ecos + b.t2_ecos
            ELSE b.t1_ecos END)                 AS "ecos"
        , SUM(CASE WHEN b.team_1 = b.team_2
                THEN b.t1_ecos_won + b.t2_ecos_won
            ELSE b.t1_ecos_won END)             AS "ecos_won"
    FROM b
    GROUP BY 1
), ranking1 AS (SELECT team_1
        , rank_1
        , team_2
        , rank_2
    FROM results
), ranking2 AS (SELECT team_1
        , AVG(CASE WHEN team_1 = team_2
                THEN rank_2
            ELSE rank_1
            END)                               AS "rank_avg"
        , COUNT(team_1)                        AS "played"
    FROM ranking1
    GROUP BY 1
), ranking3 AS (SELECT team_1                  AS "team"
        , rank_avg
        , played
        , c.ecos                               AS "ecos"
        , c.ecos_won                           AS "ecos_won"
        , (c.ecos_won * 100 / c.ecos)          AS "eco_winrate"
    FROM ranking2
    JOIN c
        ON (c.team = team_1)
    WHERE rank_avg < 100 AND played > 100
    GROUP BY 1, 2, 3, 4, 5, 6
    ORDER BY 2
)
SELECT ranking3.team                           AS "team"
    , ranking3.rank_avg                        AS "rank"
    , ranking3.eco_winrate                     AS "eco_winrate"
FROM b, ranking3
GROUP BY 1, 2, 3
ORDER BY 2 ASC;
```
</details>

According to the graph there is a dip between top 10 and top 20 teams. Therefore, with different grouping (e.g. top 10 vs top 20 vs top 30) the results would differ. However, the top 20 teams still seem to have less variation between them than worse ranked teams.

Based on this, from a business perspective, it might be reasonable to try to put more thought into these eco rounds which are often deemed as an instant loss. An interesting further research question would be to find out how an eco round win impacts the course of the match.

## Summary

So, I set up a database on Ubuntu in VirtualBox. I found an interesting dataset and loaded it into the DB. I tried to think of potential stakeholders that could benefit from the dataset. Then, I constructed 5 different operative SQL queries for these stakeholders. I also practiced optimizing these queries by indexing. Lastly, I explored 3 "interesting" research questions. The task for the course work was to showcase complex SQL queries and so they are quite complex. After reviewing them, there are quite a few points to improve on. I could've looked more into WHILE statements and their viability to potentially shorten the queries. Anyhow, a lot was learned during this course work. 
