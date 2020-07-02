# Tables

## game
|id|mdate|stadium|team1|team2|
|-|-|-|-|-|

## goal
|matchid|teamid|player|gtime|
|-|-|-|-|

## eteam
|id|teamname|coach|
|-|-|-|

## Relations
game -> goal : relates by `game.id` = `goal.matchid`
game -> eteam : relates by `game.team1` = `eteam.id` OR `game.team2` = `eteam.id`
goal -> eteam : relates by `goal.teamid` = `eteam.id`

---
# Questions
1. Show the matchid and play name for all goans scored by Germany ('GER')
```sql
SELECT matchid, name FROM goal WHERE teamid = 'GER'
```
2. Show id, stadium, team1, and team2 for just game 1012
```sql
SELECT id, stadium, team1, team2 FROM game WHERE id = 1012
```
3. Show player, teamid, stadium, and mdate for every German goal
```sql
SELECT player, teamid, stadium, mdate FROM gate 
	JOIN goal ON (id = matchid)
	WHERE teamid = 'GER'
```
4. Show team1, team2, and player for every goal scored by Mario
```sql
SELECT team1, team2, plyer FROM game
	JOIN goal ON (id = matchid)
	WHERE name LIKE 'Mario%'
```
5. Show player, teamid, coach, and gtime for all goals scored in the first 10mins (`gtime <= 10`)
```sql
SELECT player, teamid, coach, gtime FROM goal
	JOIN eteam ON id = teamid
	WHERE gtime <= 10
```
6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach
```sql
SELECT mdate, teamname FROM game
	JOIN eteam ON team1 = eteam.id
	WHERE coach = 'Fernando Santos'
```
7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sql
SELECT player FROM goal
	JOIN game ON id = matchid
	WHERE stadium = 'National Stadium, Warsaw'
```

---

## Harder Questions
8. Show the names of the players who scored a goal against Germany
```sql
SELECT player FROM goal
	JOIN game ON matchid = id
	WHERE teamid <> 'GER' AND 'GER' IN (team1, team2)
```
9. Show teamname and the total number of goals scored
```sql
SELECT teamname, COUNT(teamid) AS 'scored' FROM eteam
	JOIN goal ON teamid = id
	GROUP BY teamname
```
10. Show the stadium and the number of goals scored in each stadium
```sql
SELECT stadium, COUNT(matchid) AS 'totalscored' FROM game
	JOIN goal ON id = matchid
	GROUP BY stadium
```
11. For every match involving 'POL', show the matchid, date, and number of goals
```sql
SELECT matchid, mdate, COUNT(matchid) FROM game
	JOIN goal ON matchid = id
	WHERE 'POL' IN (team1, team2)
	GROUP BY matchid
```
12. For every match where 'GER' scores, show matchid, mdate, and the number of goals scored by 'GER'
```sql
SELECT matchid, mdate, COUNT(matchid) FROM goal
	JOIN game ON id = matchid
	WHERE teamid = 'GER'
	GROUP BY matchid
```
13. List every match with the goals scored by each team as shown and sort by mdate, matchid, team1, team2

|mdate|team1|score1|team2|score2|
|-|-|-|-|-|

```sql
SELECT
	mdate,
	team1,
	SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) as score1,
	team2,
	SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) as score2
FROM game LEFT JOIN goal ON matchid = id
GROUP BY matchid, team1, team2
ORDER BY mdate, matchid, team1, team2
```

---
Previous: [[SUM and COUNT]]
Next: [[More JOIN Operations]]