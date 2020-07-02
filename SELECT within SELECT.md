# Tables

## world
|name|continent|area|population|gdp|
|-|-|-|-|-|

---
# Questions
1. Show countries with a population larger than 'Russia'
```sql
SELECT name FROM world
	WHERE population > (SELECT population FROM world WHERE name = 'Russia')
```
2. Show countries in 'Europe' with a per capita greater than the UK
```sql
SELECT name FROM world
	WHERE gdp/population > (SELECT gdp/population FROM world WHERE name = 'United Kingdom') AND continent = 'Europe'
```
3. List name and continet of contries in the contnents containing either 'Argentina' or 'Australia'
```sql
SELECT name, continent FROM world
	WHERE continet IN (SELECT continent FROM world WHERE name IN ('Argentina','Australia'))
```
4. Country that has a population greater than Canada but less then Poland
```sql
SELECT name, continent FROM world WHERE
	population > (SELECT population FROM world WHERE name = 'Canada') AND
	population < (SELECT population FROM world WHERE name = 'Poland')
```
5. Show european contries population as a % of Germanys population
```sql
SELECT
	name, 
	CONCAT(
		ROUND(
			(population / (SELECT population FROM world WHERE name = 'Germany')) * 100,
			0),
		'%')
		AS 'percentage'
FROM world 
WHERE contient = 'EUROPE'
```
6. Contries that have a GDP greater than all European GDP's
```sql
SELECT name FROM world
	WHERE gdp > ALL (SELECT gdp FROM world WHERE contient = 'Europe')
```
or
```sql
SELECT name FROM world
	WHERE gdp > (SELECT MAX(gdp) FROM world WHERE contient = 'Europe')
```
7. Find the larget country in each continent by area showing the continent, name, and area
```sql
SELECT continent, name, area FROM wrold
	WHERE (continent, area) IN 
		(SELECT continent, MAX(area) FROM world GROUP BY continent)
```
or
```sql
SELECT continent, name, area FROM world x
	WHERE area >= 
		(SELECT area FROM world y WHERE y.continent = x.continent)
```
8. First country of each continent alphabetically
```sql
SELECT continet, name FROM world x
	WHERE name <= ALL (SELECT name FROM world y WHERE x.continent AND y.continent)
```

---
## Harder Questions
9. Find continents where all countries with a population <= 25000000. Then the names so the countries associated with that continent
```sql
SELECT name, continent, population FROM world x
	WHERE 25000000 >= ALL (SELECT population FROM world y WHERE x.continent = y.continent)
```
10. Show contries with more than 3 times that of any other contry in the continent
```sql
SELECT name, continent FROM world x
	WHERE population > ALL (SELECT 3 * poulation FROM world y WHERE x.continent = y.continent AND x.name <> y.name)
```

---
Previous: [[SELECT from Nobel]]
Next: [[SUM and COUNT]]