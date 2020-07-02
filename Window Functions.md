# Tables

## ge
|yr|firstName|lastName|constituency|party|votes|
|-|-|-|-|-|-|

---
# Questions
1. Show the lastName, party, and votes for the constituency 'S14000024' in 2017
```sql
SELECT lastName, party, votes FROM ge
	WHERE constituency = 'S14000024' AND yr = 2017
```
2. Show the party and rank or constituency 'S14000024' in 2017. List by the output party
```sql
SELECT
	party,
	votes,
	RANK() OVER (ORDER BY votes DESC) as posn
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party 
```
3. Use Partition to show the ranking of each party in 'S14000024' in each year. Include yr, party, votes, and ranking
```sql
SELECT yr, party, votes,
	RANK() OVER (PARTITION BY yr ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party, yr
```
4. Use `PARTITION BY` constituency to show the ranking of each party in Edinbugh in 2017. Order your results so the winners are shown first, then by constituency
```sql
SELECT constituency, party, votes, RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency BETWEEN 'S14000024' TO 'S14000026' AND yr = 2017
ORDER BY posn, constituency
```
5. Show the parties the won for each Edinbugh constituency in 2017
```sql
SELECT constituency, party
FROM
	(SELECT
		constituency,
		party,
		votes,
		RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
	 FROM ge 
	 WHERE constituency BETWEEN 'S14000024' TO 'S14000026' AND yr = 2017
	) g
WHERE posn = 1
```
6. How many seats for each party in scotland in 2017
```sql
SELECT party, COUNT(1)
FROM
	(SELECT constituency, party,
		RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
	 FROM ge
	 WHERE constituency LIKE 'S%' AND yr = 2017
	) i
WHERE posn = 1
```

---
Previous: [[Numeric Examples]]
Next: [[COVID 19]]