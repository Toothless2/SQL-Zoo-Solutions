# Tables
## world
|name|continent|area|population|gdp|
|-|-|-|-|-|

# Questions
1. Show the name, continent, area, and population of all countries
```SQL
SELECT name, continent, area FROM world
```
2. Display countries with at least 200 million (200,000,000) population
```SQL
SELECT name FROM wolrd WHERE population >= 200000000
```
3. Give the name and per capita GDP for the countries in [[SELECT from World#Questions#2 | Question 2]]
```sql
SELECT name, (gdp/population) AS 'pre Capita GDP' FROM wolrd WHERE population >= 200000000
```
4. Show the name and population of South American countries in millions
```sql
SELECT name, (population / 1000000) AS 'pop in millions' FROM world WHERE continent = 'South America'
```
5. Show the name an popultion for France, Germany, and Italy
```sql
SELECT name, popultion FROM world WHERE name IN ('France', 'Germany', 'Italy')
```
6. Show countries that have name that includes 'United'
```sql
SELECT name FROM world WHERE name LIKE '%United%'
```
7. Show countries that have an area of more than 3 million km$^{\text{2}}$ or a population of 250 million
```sql
SELECT name FROM world WHERE area >= 3000000 OR population >= 250000000
```
8. Show [[SELECT from World#Questions#7 | Question 7]] as `XOR`
```sql
SELECT name FROM world WHERE area >= 3000000 XOR population >= 250000000
```
9. Show the population for countries in South America in millions and GDP in bilions to 2DP
```sql
SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2) FROM world WHERE continent = 'South America'
```
10. Show the per-capita GDP for the trillion dollar countries to the nearest $1000
```sql
SELESE name, ROUND(gdp/population, -3) FROM word WHERE gdp >= 1000000000000
```
11. Show where name and capital are the same length
```sql
SELECT name, capital FROM world WHERE LENGTH(name) = LENGTH(capital)
```
12. Show the name and the capital where the first letters of each match, excluding where they are the same word
```sql
SELESE name, capital FROM world WHERE name <> capital AND LEFT(name, 1) = LEFT(capital, 1)
```
13. Fins countries what contall all vowels in their name with no spaces
```sql
SELECT name FROM world
WHERE
	LOWER(name) LIKE '%a%' AND
	LOWER(name) LIKE '%e%' AND
	LOWER(name) LIKE '%i%' AND
	LOWER(name) LIKE '%o%' AND
	LOWER(name) LIKE '%u%' AND
	LOWER(name) NOT LIKE '% %'
```

---

Previous: [[SELECT Name]]
Next: [[SELECT from Nobel]]