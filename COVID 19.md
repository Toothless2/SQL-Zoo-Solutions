# Tables
## covid
|name|whn|confirmed|deaths|recovered|
|-|-|-|-|-|

whn: is a date so `DAY`, `MONTH`, `YEAR`, etc can be used
Also covers use of `LAG`, `LEAD`, `RANK`, and `NTILE`

## world
|name|continent|area|population|gdp|
|-|-|-|-|-|

---
# Questions
1. Show the march data for 'Spain'
```sql
SELECT name, DAY(whn), confirmed, deaths, recovered
FROM covid
WHERE name = 'Spain' AND MONTH(whn) = 3
ORDER BY whn
```
2. Show the confirmed cases for the current day and the previous day for 'Italy' in March
```sql
SELECT name, confirmed, LAG(whn, 1) OVER (PARTITION BY name ORDER BY whn)
FROM covid WHERE name = 'Italy' AND MONTH(whn) = 3 ORDER BY whn
```
3. Show the number of new confirmed cases each day in 'Italy' for March
```sql
SELECT name, DAY(whn), confirmed - (LAG(whn, 1) OVER (PARTITION BY name ORDER BY whn))
FROM covid WHERE name = 'Italy' AND MONTH(whn) = 3 ORDER BY whn
```
4. Show the number of new cases in 'Italy' each week, showing Monday only
```sql
SELECT name, WEEK(whn), confirmed - (LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn))
FROM covid WHERE WEKDAY(whn) = 0 ORDER BY whn
```
> `LAG` is operating over the table projected from `WHEN` thus 1 week prior is the previous row
5. Show the number of new cases each week in 'Italy' showing Monday only, using `JOIN`
```sql
SELECT tw.name, DATE_FORMAT(tw.whn, '%Y-%m-%d'), tw.confirmed - lw.confirmed
FROM covid tw JOIN covid lw
	ON DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn AND tw.name = lw.name
WHERE tw.name = 'Italy' AND WEEKDAY(tw.whn) = 0 ORDER BY tw.whn
```
6. Show the rannkings of confirmed and death rates for each country
```sql
SELECT name,
	confirmed, RANK() OVER (ORDER BY confirmed DESC) rc,
	deaths, RANK() OVER (ORDER BY deaths DESC) rd
FROM covid WHERE whn = '2020-04-20' ORDER BY confrirmed DESC
```
7. The the infection rate ranking for each county. Only include conuntries with a population of at least 10 million
```sql
SELECT
	world.name,
	ROUND(100000 * confirmed / population, 0),
	RANK() OVER (ORDER BY confirmed / population)
FROM covid JOIN world ON covid.name = world.name
WHERE whn = '2020-04-20' AND population > 10000000 ORDER BY population DESC
```
8. For each country that has had at least 1000 new cases in a single day, show the date and peak number of new cases
```sql
SELECT name, date, peakNewCases
FROM 
	(SELECT *, RANK() OVER (PARTITION BY name ORDER BY peakNewCases DESC) AS rank 
	 FROM 
	 	(SELECT name, DATE_FORMAT(whn, '%Y-%m-%d') AS date,
			confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) as peakNewCases
		 FROM covid) temp
	 WHERE peakNewCases >= 1000 ORDER BY date, peakNewCases DESC) temp2
WHERE rank = 1
```

---
Previous: [[Window Functions]]
Next: [[Self Join]]